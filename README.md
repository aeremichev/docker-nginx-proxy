# docker-nginx-proxy

Example config

```
server {
    listen 80;
    server_name mydomen.ru;

    #access_log /var/log/nginx/mydomen.ru_access.log;
    #error_log /var/log/nginx/mydomen.ru_error.log;
    access_log off;
    error_log off;

    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  300;
    client_max_body_size 100m;

    location / {
        proxy_pass       http://127.0.0.1:8100;
        proxy_set_header Host      $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

server {
    listen       80;
    server_name  www.mydomen.ru;
    return       301 $scheme://mydomen.ru$request_uri;
}

```
