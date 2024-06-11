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

#. Log in to the Analysis Cockpit via SSH.
#. Stop the Analysis Cockpit Service temporarily:

    .. code-block:: console

        nextron@cockpit:~$ sudo systemctl stop asgard-analysis-cockpit.service

    This will stop the Analysis Cockpit service. You can start
    the service again after you have extended the disk space.

#. Run the following command to check the current disk space:

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

#. Run the following command to identify your attached disks:

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

#. Run the following command to check all the physical volumes:

    .. code-block:: console

        nextron@cockpit:~$ sudo pvs
          PV         VG        Fmt  Attr PSize   PFree
          /dev/sda5  debian-vg lvm2 a--  <24.52g    0

    The output will show all the physical volumes. Please note the name
    of the volume group (VG), in our case **debian-vg**.

#. Run the following command to create a new physical volume for the new disk:

    .. code-block:: console

        nextron@cockpit:~$ sudo pvcreate /dev/sdb
          Physical volume "/dev/sdb" successfully created.

#. Check your physical volumes again:

    .. code-block:: console

        nextron@cockpit:~$ sudo pvs
          PV         VG        Fmt  Attr PSize   PFree 
          /dev/sda5  debian-vg lvm2 a--  <24.52g     0 
          /dev/sdb             lvm2 ---   20.00g 20.00g

    You can see that the new physical volume **/dev/sdb** has been created.
    It is not yet part of the volume group (VG).

#. Run the following command to identify your volume groups:

    .. code-block:: console

        nextron@cockpit:~$ sudo vgs
          VG        #PV #LV #SN Attr   VSize   VFree
          debian-vg   1   2   0 wz--n- <24.52g    0

    The output will show all the volume groups. In this case, the only volume
    group is **debian-vg**.

#.  Extend the volume group with our new physical volume:

    .. code-block:: console

        nextron@cockpit:~$ sudo vgextend debian-vg /dev/sdb
          Volume group "debian-vg" successfully extended

#. Looking at the volume groups again, you will see that the volume group **debian-vg** has been extended:

    .. code-block:: console

        nextron@cockpit:~$ sudo vgs
          VG        #PV #LV #SN Attr   VSize   VFree  
          debian-vg   2   2   0 wz--n- <44.52g <20.00g

    The volume group has more space (VSize) and free space (VFree).

#. We now need to extend the logical volume (using the free space):

    .. code-block:: console

        nextron@cockpit:~$ sudo lvextend -l +100%FREE /dev/debian-vg/root
          Size of logical volume debian-vg/root changed from 23.56 GiB (6032 extents) to <43.56 GiB (11151 extents).
          Logical volume debian-vg/root successfully resized.

    Explanation: **/dev/debian-vg/root** is the logical volume that we want to extend.
    The "-l +100%FREE" option tells the lvextend command to use all the free space
    available in the volume group. The device **/dev/debian-vg** is our volume group.
    The logical volume **root** is what we extended (output of "sudo lvs").

#. Run the following command to resize the file system:

    .. code-block:: console

        nextron@cockpit:~$ sudo resize2fs /dev/debian-vg/root
        resize2fs 1.47.0 (5-Feb-2023)
        Filesystem at /dev/debian-vg/root is mounted on /; on-line resizing required
        old_desc_blocks = 3, new_desc_blocks = 6
        The filesystem on /dev/debian-vg/root is now 11418624 (4k) blocks long.

#. Run the following command to check the disk space again:

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

#. You successfully extended your disk space. Reboot your Analysis Cockpit
   to make sure everything is working as expected.

   .. code-block:: console

        nextron@cockpit:~$ sudo reboot

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

#. Log in to the Analysis Cockpit via SSH.
#. Stop the Analysis Cockpit Service temporarily:

    .. code-block:: console

        nextron@cockpit:~$ sudo systemctl stop asgard-analysis-cockpit.service

    This will stop the Analysis Cockpit service. You can start
    the service again after you have extended the disk space.

#. Run the following command to check the current disk space:

    .. code-block:: console
        :emphasize-lines: 5

        nextron@cockpit:~$ df -h
        Filesystem                   Size  Used Avail Use% Mounted on
        udev                         2.0G     0  2.0G   0% /dev
        tmpfs                        395M  5.4M  390M   2% /run
        /dev/mapper/asgard--vg-root   24G  4.1G   18G  19% /
        tmpfs                        2.0G     0  2.0G   0% /dev/shm
        tmpfs                        5.0M     0  5.0M   0% /run/lock
        tmpfs                        2.0G     0  2.0G   0% /sys/fs/cgroup
        /dev/sda1                    470M   83M  363M  19% /boot
        tmpfs                        395M     0  395M   0% /run/user/1000
   
   The output will show the current disk space usage.

#. Run the following command to identify your attached disk:

    .. code-block:: console
        :emphasize-lines: 3

        nextron@cockpit:~$ lsblk              
        NAME                  MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT          
        sda                     8:0    0   35G  0 disk                                                                                                             
        ├─sda1                  8:1    0  487M  0 part /boot                                                                                                       
        ├─sda2                  8:2    0    1K  0 part                                                                                                             
        └─sda5                  8:5    0 24.5G  0 part            
          ├─asgard--vg-root   254:0    0 23.6G  0 lvm  /                                                                                                           
          └─asgard--vg-swap_1 254:1    0  980M  0 lvm  [SWAP]                                                                                                      
        sr0                    11:0    1 1024M  0 rom

    The output will show the attached disks. In this example, our
    disk is **sda**.

#. We now have to increase the partition size. Please follow the next steps carefully:

    .. code-block:: console

        nextron@cockpit:~$ sudo fdisk -u /dev/sda

#. press "p" to print the current partitions of the disk:

    .. code-block:: none
        :emphasize-lines: 1, 12

        Command (m for help): p
        Disk /dev/sda: 35 GiB, 37580963840 bytes, 73400320 sectors
        Disk model: HARDDISK        
        Units: sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disklabel type: dos
        Disk identifier: 0x492a1933

        Device     Boot   Start      End  Sectors  Size Id Type
        /dev/sda1  *       2048   999423   997376  487M 83 Linux
        /dev/sda2       1001470 52426751 51425282 24.5G  5 Extended
        /dev/sda5       1001472 52426751 51425280 24.5G 8e Linux LVM

        You can see that **/dev/sda2** is our extended partition. Please note
        the ``End`` value of the ``Extended`` partition (52426751 in this case).

#. Create a new partition:

    Please note that the **First sector** value should be the **End** value + 1
    of the **Extended** partition from the previous step. The **Last sector**
    value can be left empty to use the remaining disk space. Please use the
    default value for the partition type (primary), partition number, and Last sector.

    .. code-block:: none
        :emphasize-lines: 1, 5-8, 24

        Command (m for help): n
        Partition type
           p   primary (1 primary, 1 extended, 2 free)
           l   logical (numbered from 5)
        Select (default p): p
        Partition number (3,4, default 3):  
        First sector (999424-73400319, default 999424): 52426752
        Last sector, +/-sectors or +/-size{K,M,G,T,P} (52426752-73400319, default 73400319): 

        Created a new partition 3 of type 'Linux' and of size 10 GiB.

        Command (m for help): p
        Disk /dev/sda: 35 GiB, 37580963840 bytes, 73400320 sectors
        Disk model: HARDDISK     
        Units: sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disklabel type: dos
        Disk identifier: 0x492a1933
        
        Device     Boot    Start      End  Sectors  Size Id Type
        /dev/sda1  *        2048   999423   997376  487M 83 Linux
        /dev/sda2        1001470 52426751 51425282 24.5G  5 Extended
        /dev/sda3       52426752 73400319 20973568   10G 83 Linux
        /dev/sda5        1001472 52426751 51425280 24.5G 8e Linux LVM
        
        Partition table entries are not in disk order.

#. Change the partition type to Linux LVM:

    .. code-block:: none
        :emphasize-lines: 1-3, 7, 19

        Command (m for help): t
        Partition number (1-3,5, default 5): 3
        Hex code (type L to list all codes): 8e

        Changed type of partition 'Linux' to 'Linux LVM'.

        Command (m for help): p
        Disk /dev/sda: 35 GiB, 37580963840 bytes, 73400320 sectors
        Disk model: HARDDISK
        Units: sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disklabel type: dos
        Disk identifier: 0x492a1933

        Device     Boot    Start      End  Sectors  Size Id Type
        /dev/sda1  *        2048   999423   997376  487M 83 Linux
        /dev/sda2        1001470 52426751 51425282 24.5G  5 Extended
        /dev/sda3       52426752 73400319 20973568   10G 8e Linux LVM
        /dev/sda5        1001472 52426751 51425280 24.5G 8e Linux LVM

        Partition table entries are not in disk order.

#. We can save the new partition table. This will exit the tool:

    .. code-block:: console

        Command (m for help): w
        The partition table has been altered.
        Syncing disks.

        nextron@cockpit:~$

#. Running "lsblk" we can see a new partition:

    .. code-block:: console
        :emphasize-lines: 6

        nextron@cockpit:~$ lsblk
        NAME                  MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
        sda                     8:0    0   35G  0 disk 
        ├─sda1                  8:1    0  487M  0 part /boot
        ├─sda2                  8:2    0    1K  0 part 
        ├─sda3                  8:3    0   10G  0 part 
        └─sda5                  8:5    0 24.5G  0 part 
          ├─asgard--vg-root   254:0    0 23.6G  0 lvm  /
          └─asgard--vg-swap_1 254:1    0  980M  0 lvm  [SWAP]
        sr0                    11:0    1 1024M  0 rom 

#. Create a new physical volume for the new partition:

    .. code-block:: console
        :emphasize-lines: 1, 3, 5

        nextron@cockpit:~$ sudo pvcreate /dev/sda3
          Physical volume "/dev/sda3" successfully created.
        nextron@cockpit:~$ sudo pvs
          PV         VG        Fmt  Attr PSize   PFree 
          /dev/sda3            lvm2 ---   10.00g 10.00g
          /dev/sda5  asgard-vg lvm2 a--  <24.52g     0

    Running ``sudo pvs`` we can see all the physical volumes. The new physical
    volume **/dev/sda3** has been created and is not yet part of the volume group (VG).

#. Extend the volume group with our new physical volume:

    .. code-block:: console
        :emphasize-lines: 1, 3, 5

        nextron@cockpit:~$ sudo vgextend asgard-vg /dev/sda3
          Volume group "asgard-vg" successfully extended
        nextron@cockpit:~$ sudo vgs
          VG        #PV #LV #SN Attr   VSize   VFree 
          asgard-vg   2   2   0 wz--n- <34.52g 10.00g

    Running ``sudo vgs`` we can see that the volume group **asgard-vg** has been extended (VFree).

#. Add the physical volume to the volume group:

    .. code-block:: console

        nextron@cockpit:~$ sudo lvextend -l +100%FREE /dev/asgard-vg/root
          Size of logical volume asgard-vg/root changed from 23.56 GiB (6032 extents) to 33.56 GiB (8592 extents).
          Logical volume asgard-vg/root successfully resized.

    Explanation: **/dev/asgard-vg/root** is the logical volume that we want to extend.
    The "-l +100%FREE" option tells the lvextend command to use all the free space
    available in the volume group. The device **/dev/asgard-vg** is our volume group.
    The logical volume **root** is what we extended (output of "sudo lvs").

#. Resize the file system:

    .. code-block:: console

        nextron@cockpit:~$ sudo resize2fs /dev/asgard-vg/root
        resize2fs 1.44.5 (15-Dec-2018)
        Filesystem at /dev/asgard-vg/root is mounted on /; on-line resizing required
        old_desc_blocks = 3, new_desc_blocks = 5
        The filesystem on /dev/asgard-vg/root is now 8798208 (4k) blocks long.

#. Run the following command to verify the disk size:

    .. code-block:: console
        :emphasize-lines: 5

        nextron@cockpit:~$ df -h
        Filesystem                   Size  Used Avail Use% Mounted on
        udev                         2.0G     0  2.0G   0% /dev
        tmpfs                        395M  5.4M  390M   2% /run
        /dev/mapper/asgard--vg-root   33G  4.2G   28G  14% /
        tmpfs                        2.0G     0  2.0G   0% /dev/shm
        tmpfs                        5.0M     0  5.0M   0% /run/lock
        tmpfs                        2.0G     0  2.0G   0% /sys/fs/cgroup
        /dev/sda1                    470M   83M  363M  19% /boot
        tmpfs                        395M     0  395M   0% /run/user/1000

#. If everything looks correct, you can reboot your system to make sure everything is working as expected.

    .. code-block:: console

        nextron@cockpit:~$ sudo reboot