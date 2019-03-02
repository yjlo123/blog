---
title: "Things to do After Purchasing a Domain"
date: 2019-03-02T00:22:40+08:00
draft: false
tags: ["domain","nginx","web"]
---

Yesterday, I purchased a new domain from Namecheap and realized there were a bunch of things to do to make the new webpage live. Here I listed some notes for future reference.

## Setup HTTPS
For certain domain suffixes, HTTPS is compulsory. For instance, `.dev` is a secure namespace and the website requires HTTPS to work in browser.


### - Generate a new cert using certbot
{{< highlight shell "linenos=table" >}}
# for example, your domain is domain.com
sudo certbot --nginx -d domain.com -d www.doamin.com
{{< / highlight >}}

If you see `Error getting validation data`, means the DNS settings have not take effect.
It says it may take up to 48 hours to finish the propagation, but in my case, it only delayed about 3 minutes.

### - Add domains to an existing cert

{{< highlight shell "linenos=table" >}}
nginx -s stop
certbot certonly --standalone -d domain.com -d www.domain.com -d abc.domain.com --expand
nginx
{{< / highlight >}}
Remember to stop Nginx, otherwise, the following message will be shown.
```
Problem binding to port 80: Could not bind to IPv4 or IPv6.
```

The genenrated cert files will be put at `/etc/letsencrypt/live/domain.com/`

## Configure Nginx
Redirect `http` to `https`, and `www` to `non-www`:
{{< highlight nginx "linenos=table" >}}
server {
    listen 80;
    server_name domain.com www.domain.com;
    return 301 https://domain.com$request_uri;
}

server {
    listen 443 ssl;
    server_name www.domain.com;
    ssl_certificate /etc/letsencrypt/live/domain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/domain.com/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    return 301 https://domain.com$request_uri;
}
{{< / highlight >}}
Then the main server block:
{{< highlight nginx "linenos=table" >}}
server {
    listen 443 ssl;
    server_name domain.com;

    ssl_certificate /etc/letsencrypt/live/domain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/domain.com/privkey.pem;

    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';

    root /var/www/home;

    error_page 404 =404 /404.html;

    # Add index.php to the list if you are using PHP
    index index.html index.htm index.nginx-debian.html;

    location / {
        try_files $uri $uri/ /index.html /index$uri /index$uri/ =404;
    }
}
{{< / highlight >}}

## Check Redirection
The following Python programs checks if the https and subdomain redirections are correct.
{{< highlight python "linenos=table" >}}
import requests

hosts = [
    #(host_name, subdomains)
    ('yjlo.xyz', ['page']),
    ('runtime.xyz', []),
]

def check_url(domain, sub=None):
    sub_domains = ['', 'www.']
    if sub:
        for s in sub:
            sub_domains.append(s + '.')
    failed_urls = []
    for schema in ['http', 'https']:
        for sub_domain in sub_domains:
            url = '{}://{}{}'.format(schema, sub_domain, domain)
            try:
                r = requests.get(url)
                status = r.status_code
                label = ' ' if status == 200 else '*'
                print('{}[{}] {}'.format(label, status, url))
            except Exception as e:
                print('*[err] {} {}'.format(url, e))
                failed_urls.append(url)
    return failed_urls

if __name__ == '__main__':
    error_urls = []
    for d, s in hosts:
        error_urls.extend(check_url(d, s))

    if error_urls:
        print('\n===== [Failed URLs] =====')
        for eus in error_urls:
            print(eus)

{{< / highlight >}}
