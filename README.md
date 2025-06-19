# Nginx web server <!-- omit in toc -->

## Overview

This project is a basic DDEV nginx webserver setup.

## Service status

1. Ensure `stub_status` module is enabled.

    ```shell
    nginx -V 2>&1 | grep -o with-http_stub_status_module
    ```

2. Configure endpoint.

    ```conf
    server {
        listen 8080 default_server;

        location /stub_status {
            stub_status;
            allow 127.0.0.1;   # allow localhost
            allow 172.0.0.0/8; # allow other Docker containers
            allow ::1;         # allow IPv6 localhost
            deny all;          # deny everyone else
        }
    }
    ````

3. Access endpoint.

    ```shell
    $ ddev exec curl web:8080/stub_status
    Active connections: 1
    server accepts handled requests
    2 2 2
    Reading: 0 Writing: 1 Waiting: 0
    ```

4. Access `:8080/stub_status` to view in browser.
