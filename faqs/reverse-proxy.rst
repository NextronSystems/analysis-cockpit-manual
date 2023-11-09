.. Index:: Reverse Proxy to access the Analysis Cockpit

Reverse Proxy to access the Analysis Cockpit
--------------------------------------------

**Q: I am using a Reverse Proxy to access the Analysis Cockpit. What do I have to take care of?**

The Analysis Cockpit partially uses large URLs to communicate with its backend.
Proxy server usually do not allow arbitrary large URLs.

In case of nginx the default header size is 8k (see http://nginx.org/en/docs/http/ngx_http_core_module.html#large_client_header_buffers).
If you want to use the Analyst Cockpit behind a nginx reverse proxy, you need to increase the *large_client_header_buffer*.
A size of 100k should be sufficient. Also the HTTP2 protocol has to be disabled.

A minimal example configuration for nginx looks as follows:

.. code-block:: nginx

    server {
       listen 443 ssl; # !! no http2 !!
       ssl_certificate /path/to/your/certificate.crt;
       ssl_certificate_key /path/to/your/private.key;
       location / {
          proxy_pass https://analysis-cockpit.your.org;
          proxy_set_header Host $http_host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       }
       large_client_header_buffers 4 100k; # increase maximal allowed URL length
    }
