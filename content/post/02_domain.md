---
title: "Things to do After Purchasing a Domain"
date: 2019-03-02T00:22:40+08:00
draft: true
---

## Setup HTTPS

```
sudo certbot --nginx -d siwei.dev -d www.siwei.dev
```

if you see `Error getting validation data`, means the domain connection is not ready.

```
server {
    listen 80;
    server_name domain_name.com www.domain_name.com;
    return 301 https://domain_name.com$request_uri;
}

server {
    listen 443 ssl;

    ssl_certificate /etc/letsencrypt/live/domain_name.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/domain_name.com/privkey.pem;

    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';

    root /var/www/home;

    error_page 404 =404 /404.html;

    # Add index.php to the list if you are using PHP
    index index.php index.html index.htm index.nginx-debian.html;

    server_name domain_name.com;

    location /file {
        try_files $uri =404;
    }

    location / {
        try_files $uri $uri/ /index.html /index$uri /index$uri/ =404;
    }

}
```