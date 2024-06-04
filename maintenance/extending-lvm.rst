.. Index:: Extending Disk Space

Extending Disk Space
--------------------

.. warning::
    This chapter assumes you already attached a second disk or
    increased the disk space of your existing disk via your
    hypervisor. If you have not done so, please refer to the
    documentation of your hypervisor on how to attach a second
    disk or increase the disk space of your existing disk.

    Please make sure that you create a snapshot of your Analysis
    Cockpit before proceeding with the following steps. This will
    allow you to revert to the previous state in case something
    goes wrong! This is very important since you are actively
    changing the disk space of your Analysis Cockpit. You could
    lose data if something goes wrong!

The Debian system running your Analysis Cockpit is configured
with LVM (Logical Volume Manager), which allows you to extend
the disk space of the Analysis Cockpit. This is useful if you
have a lot of data to analyze and the disk space is not
sufficient. The following steps describe how to extend the disk
space:

.. hint::
    If you are struggling or uncomfortable with the following
    steps, please contact our support team for assistance.

Scenario 1: Second Disk
^^^^^^^^^^^^^^^^^^^^^^^

This section focuses on extending the disk space by attaching a
second disk to the Analysis Cockpit. We will add the second disk
to our existing volume group and extend the logical volume.

1. Log in to the Analysis Cockpit via SSH.
2. Stop the Analysis Cockpit Service temporarily:

    .. code-block:: console

        nextron@cockpit:~$ sudo systemctl stop asgard-analysis-cockpit.service

    This will stop the Analysis Cockpit service. You can start
    the service again after you have extended the disk space.

3. Run the following command to check the current disk space:

    .. code-block:: console
        :emphasize-lines: 5

        nextron@cockpit:~$ df -h
        Filesystem                   Size  Used Avail Use% Mounted on
        udev                         1.9G     0  1.9G   0% /dev
        tmpfs                        392M  524K  392M   1% /run
        /dev/mapper/debian--vg-root   24G  3.4G   19G  16% /
        tmpfs                        2.0G     0  2.0G   0% /dev/shm
        tmpfs                        5.0M     0  5.0M   0% /run/lock
        /dev/sda1                    455M   51M  380M  12% /boot
        tmpfs                        392M     0  392M   0% /run/user/1000
   
   The output will show the current disk space usage.

4. Run the following command to identify your attached disks:

    .. code-block:: console
        :emphasize-lines: 3, 9
        :linenos:

        nextron@cockpit:~$ lsblk
        NAME                  MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
        sda                     8:0    0   25G  0 disk 
        ├─sda1                  8:1    0  487M  0 part /boot
        ├─sda2                  8:2    0    1K  0 part 
        └─sda5                  8:5    0 24.5G  0 part 
          ├─debian--vg-root   254:0    0 23.6G  0 lvm  /
          └─debian--vg-swap_1 254:1    0  980M  0 lvm  [SWAP]
        sdb                     8:16   0   20G  0 disk 
        sr0                    11:0    1 1024M  0 rom

    The output will show the attached disks. In this example, the
    newly attached disk is **sdb**, whereas the existing disk is **sda**.

5. Run the following command to check all the physical volumes:

    .. code-block:: console

        nextron@cockpit:~$ sudo pvs
          PV         VG        Fmt  Attr PSize   PFree
          /dev/sda5  debian-vg lvm2 a--  <24.52g    0

    The output will show all the physical volumes. Please note the name
    of the volume group (VG), in our case **debian-vg**.

6. Run the following command to create a new physical volume for the new disk:

    .. code-block:: console

        nextron@cockpit:~$ sudo pvcreate /dev/sdb
          Physical volume "/dev/sdb" successfully created.

7. Check your physical volumes again:

    .. code-block:: console

        nextron@cockpit:~$ sudo pvs
          PV         VG        Fmt  Attr PSize   PFree 
          /dev/sda5  debian-vg lvm2 a--  <24.52g     0 
          /dev/sdb             lvm2 ---   20.00g 20.00g

    You can see that the new physical volume **/dev/sdb** has been created.
    It is not yet part of the volume group (VG).

8. Run the following command to identify your volume groups:

    .. code-block:: console

        nextron@cockpit:~$ sudo vgs
          VG        #PV #LV #SN Attr   VSize   VFree
          debian-vg   1   2   0 wz--n- <24.52g    0

    The output will show all the volume groups. In this case, the only volume
    group is **debian-vg**.

9.  Extend the volume group with our new physical volume:

    .. code-block:: console

        nextron@cockpit:~$ sudo vgextend debian-vg /dev/sdb
          Volume group "debian-vg" successfully extended

10. Looking at the volume groups again, you will see that the volume group **debian-vg** has been extended:

    .. code-block:: console

        nextron@cockpit:~$ sudo vgs
          VG        #PV #LV #SN Attr   VSize   VFree  
          debian-vg   2   2   0 wz--n- <44.52g <20.00g

    The volume group has more space (VSize) and free space (VFree).

11. We now need to extend the logical volume (using the free space):

    .. code-block:: console

        nextron@cockpit:~$ sudo lvextend -l +100%FREE /dev/debian-vg/root
          Size of logical volume debian-vg/root changed from 23.56 GiB (6032 extents) to <43.56 GiB (11151 extents).
          Logical volume debian-vg/root successfully resized.

    Explanation: **/dev/debian-vg/root** is the logical volume that we want to extend.
    The "-l +100%FREE" option tells the lvextend command to use all the free space
    available in the volume group. The device **/dev/debian-vg** is our volume group.
    The logical volume **root** is what we extended (output of "sudo lvs").

12. Run the following command to resize the file system:

    .. code-block:: console

        nextron@cockpit:~$ sudo resize2fs /dev/debian-vg/root
        resize2fs 1.47.0 (5-Feb-2023)
        Filesystem at /dev/debian-vg/root is mounted on /; on-line resizing required
        old_desc_blocks = 3, new_desc_blocks = 6
        The filesystem on /dev/debian-vg/root is now 11418624 (4k) blocks long.

13. Run the following command to check the disk space again:

    .. code-block:: console
        :emphasize-lines: 5

        nextron@cockpit:~$ df -h
        Filesystem                   Size  Used Avail Use% Mounted on
        udev                         1.9G     0  1.9G   0% /dev
        tmpfs                        392M  532K  392M   1% /run
        /dev/mapper/debian--vg-root   43G  3.5G   38G   9% /
        tmpfs                        2.0G     0  2.0G   0% /dev/shm
        tmpfs                        5.0M     0  5.0M   0% /run/lock
        /dev/sda1                    455M   51M  380M  12% /boot
        tmpfs                        392M     0  392M   0% /run/user/1000

14. You successfully extended your disk space. Reboot your Analysis Cockpit
    to make sure everything is working as expected.

Scenario 2: Increased Disk Size
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. danger::
    This section is only relevant if you increased the disk size of your
    existing disk. If you attached a second disk, please refer to the
    previous section. This method is more advanced and should only be
    used if you are comfortable with the steps.

This section focuses on extending the disk space in case you increased the disk
size of your existing/attached disk. We will extend the disk space by extending
the partition and resizing the file system.

1. Log in to the Analysis Cockpit via SSH.
2. Stop the Analysis Cockpit Service temporarily:

    .. code-block:: console

        nextron@cockpit:~$ sudo systemctl stop asgard-analysis-cockpit.service

    This will stop the Analysis Cockpit service. You can start
    the service again after you have extended the disk space.

3. Run the following command to check the current disk space:

    .. code-block:: console
        :emphasize-lines: 5

        nextron@cockpit:~$ df -h
        Filesystem                   Size  Used Avail Use% Mounted on
        udev                         1.9G     0  1.9G   0% /dev
        tmpfs                        392M  524K  392M   1% /run
        /dev/mapper/debian--vg-root   24G  3.4G   19G  16% /
        tmpfs                        2.0G     0  2.0G   0% /dev/shm
        tmpfs                        5.0M     0  5.0M   0% /run/lock
        /dev/sda1                    455M   51M  380M  12% /boot
        tmpfs                        392M     0  392M   0% /run/user/1000
   
   The output will show the current disk space usage.

4. Run the following command to identify your attached disks:

    .. code-block:: console
        :emphasize-lines: 3, 9

        nextron@cockpit:~$ lsblk
        NAME                  MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
        sda                     8:0    0   40G  0 disk 
        ├─sda1                  8:1    0  487M  0 part /boot
        ├─sda2                  8:2    0    1K  0 part 
        └─sda5                  8:5    0 24.5G  0 part 
          ├─debian--vg-root   254:0    0 23.6G  0 lvm  /
          └─debian--vg-swap_1 254:1    0  980M  0 lvm  [SWAP]
        sr0                    11:0    1 1024M  0 rom


    The output will show the attached disks. In this example, our
    disk is **sda**.

5. We now have to increase the partition size. Please follow the next steps carefully:

    .. code-block:: console

        nextron@cockpit:~$ sudo fdisk -u /dev/sda

6. press "p" to print the current partitions of the disk:

    .. code-block:: none
        :emphasize-lines: 1, 13

        Command (m for help): p

        Disk /dev/sda: 40 GiB, 42949672960 bytes, 83886080 sectors
        Disk model: HARDDISK        
        Units: sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disklabel type: dos
        Disk identifier: 0x82b90d84

        Device     Boot   Start      End  Sectors  Size Id Type
        /dev/sda1  *       2048   999423   997376  487M 83 Linux
        /dev/sda2       1001470 52426751 51425282 24.5G  5 Extended
        /dev/sda5       1001472 52426751 51425280 24.5G 8e Linux LVM

        You can see that **/dev/sda2** is our extended partition. We
        will delete this partition now, and in the process the **/dev/sda5**
        partition will also be deleted. The partition number is the number
        in the Device (i.e. /dev/sda2 is partition number 2).

7. Delete the partition:

    .. code-block:: none
        :emphasize-lines: 1, 2, 6

        Command (m for help): d
        Partition number (1,2,5, default 5): 2

        Partition 2 has been deleted.

        Command (m for help): p
        Disk /dev/sda: 40 GiB, 42949672960 bytes, 83886080 sectors
        Disk model: HARDDISK        
        Units: sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disklabel type: dos
        Disk identifier: 0x82b90d84

        Device     Boot Start    End Sectors  Size Id Type
        /dev/sda1  *     2048 999423  997376  487M 83 Linux

8. Create a new partition. Choose "extended" when asked for the partition type, the rest can stay default:

    .. code-block:: none
        :emphasize-lines: 1, 5-8, 12, 23

        Command (m for help): n
        Partition type
           p   primary (1 primary, 0 extended, 3 free)
           e   extended (container for logical partitions)
        Select (default p): e
        Partition number (2-4, default 2): 
        First sector (999424-83886079, default 999424): 
        Last sector, +/-sectors or +/-size{K,M,G,T,P} (999424-83886079, default 83886079): 

        Created a new partition 2 of type 'Extended' and of size 39.5 GiB.

        Command (m for help): p
        Disk /dev/sda: 40 GiB, 42949672960 bytes, 83886080 sectors
        Disk model: HARDDISK        
        Units: sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disklabel type: dos
        Disk identifier: 0x82b90d84

        Device     Boot  Start      End  Sectors  Size Id Type
        /dev/sda1  *      2048   999423   997376  487M 83 Linux
        /dev/sda2       999424 83886079 82886656 39.5G  5 Extended

9. Now we need to create the logical partition. Use the default values for first and last sector. If asked to remove the LVM signature, type "n":

    .. code-block:: none
        :emphasize-lines: 1, 10, 12, 25

        Command (m for help): n
        All space for primary partitions is in use.
        Adding logical partition 5
        First sector (1001472-83886079, default 1001472): 
        Last sector, +/-sectors or +/-size{K,M,G,T,P} (1001472-83886079, default 83886079): 

        Created a new partition 5 of type 'Linux' and of size 39.5 GiB.
        Partition #5 contains a LVM2_member signature.

        Do you want to remove the signature? [Y]es/[N]o: n

        Command (m for help): p

        Disk /dev/sda: 40 GiB, 42949672960 bytes, 83886080 sectors
        Disk model: HARDDISK
        Units: sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disklabel type: dos
        Disk identifier: 0x82b90d84

        Device     Boot   Start      End  Sectors  Size Id Type
        /dev/sda1  *       2048   999423   997376  487M 83 Linux
        /dev/sda2        999424 83886079 82886656 39.5G  5 Extended
        /dev/sda5       1001472 83886079 82884608 39.5G 83 Linux

10. Adjust the beginning of the partition to the value it was before (see Step 5. - Start value of **/dev/sda5**):

    .. code-block:: none

        Command (m for help): x

        Expert command (m for help): b
        Partition number (1,2,5, default 5): 5
        New beginning of data (999425-83886079, default 1001472): 1001472

        Expert command (m for help): r

11. Now we need to change the partition type to LVM:

    .. code-block:: none
        :emphasize-lines: 1, 2, 3, 7, 19

        Command (m for help): t
        Partition number (1,2,5, default 5): 5
        Hex code or alias (type L to list all): 8e

        Changed type of partition 'Linux' to 'Linux LVM'.

        Command (m for help): p
        Disk /dev/sda: 40 GiB, 42949672960 bytes, 83886080 sectors
        Disk model: HARDDISK        
        Units: sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disklabel type: dos
        Disk identifier: 0x82b90d84

        Device     Boot   Start      End  Sectors  Size Id Type
        /dev/sda1  *       2048   999423   997376  487M 83 Linux
        /dev/sda2        999424 83886079 82886656 39.5G  5 Extended
        /dev/sda5       1001472 83886079 82884608 39.5G 8e Linux LVM

12. We can save the new partition table. This will exit the tool:

    .. code-block:: console

        Command (m for help): w
        The partition table has been altered.
        Syncing disks.

        nextron@cockpit:~$

13. Running "lsblk" we can see that the disk space increased:

    .. code-block:: console
        :emphasize-lines: 6

        nextron@cockpit:~$ lsblk
        NAME                  MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
        sda                     8:0    0   40G  0 disk 
        ├─sda1                  8:1    0  487M  0 part /boot
        ├─sda2                  8:2    0    1K  0 part 
        └─sda5                  8:5    0 39.5G  0 part 
          ├─debian--vg-root   254:0    0 23.6G  0 lvm  /
          └─debian--vg-swap_1 254:1    0  980M  0 lvm  [SWAP]
        sr0                    11:0    1 1024M  0 rom

14. Resize your phyiscal volumes:

    .. code-block:: console
        :emphasize-lines: 1, 4, 7
        :linenos:

        nextron@cockpit:~$ sudo pvresize /dev/sda5
          Physical volume "/dev/sda5" changed
          1 physical volume(s) resized or updated / 0 physical volume(s) not resized
        nextron@cockpit:~$ sudo pvs
          PV         VG        Fmt  Attr PSize   PFree 
          /dev/sda5  debian-vg lvm2 a--  <39.52g 15.00g
        nextron@cockpit:~$ sudo lvs
          LV     VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
          root   debian-vg -wi-ao----  38.56g                                                    
          swap_1 debian-vg -wi-ao---- 980.00m

    We can see that the physical volume **/dev/sda5** has been resized (PFree).
    The output will also show all the physical volumes (line 6) and logical
    volumes (line 9). Please note the name of the volume group (VG) and logical
    volume, in our case **debian-vg** and **root** respectively.

15. Resize the logical volume:

    .. code-block:: console

        nextron@cockpit:~$ sudo lvextend -l +100%FREE /dev/debian-vg/root
          Size of logical volume debian-vg/root changed from 23.56 GiB (6032 extents) to 38.56 GiB (9872 extents).
          Logical volume debian-vg/root successfully resized.

    Explanation: **/dev/debian-vg/root** is the logical volume that we want to extend.
    The "-l +100%FREE" option tells the lvextend command to use all the free space
    available in the volume group. The device **/dev/debian-vg** is our volume group.
    The logical volume **root** is what we extended (output of "sudo lvs").

16. Resize the file system:

    .. code-block:: console

        nextron@cockpit:~$ sudo resize2fs /dev/debian-vg/root
        resize2fs 1.47.0 (5-Feb-2023)
        Filesystem at /dev/debian-vg/root is mounted on /; on-line resizing required
        old_desc_blocks = 3, new_desc_blocks = 5
        The filesystem on /dev/debian-vg/root is now 10108928 (4k) blocks long.

17. Run the following command to verify the disk size:

    .. code-block:: console
        :emphasize-lines: 5

        nextron@cockpit:~$ df -h
        Filesystem                   Size  Used Avail Use% Mounted on
        udev                         1.9G     0  1.9G   0% /dev
        tmpfs                        392M  500K  392M   1% /run
        /dev/mapper/debian--vg-root   38G  928M   36G   3% /
        tmpfs                        2.0G     0  2.0G   0% /dev/shm
        tmpfs                        5.0M     0  5.0M   0% /run/lock
        /dev/sda1                    455M   51M  380M  12% /boot
        tmpfs                        392M     0  392M   0% /run/user/1000

18. If everything looks correct, you can reboot your system to make sure everything is working as expected.