+++
categories = ["self-hosting"]
comments = false
date = "2017-01-08T15:11:25-06:00"
draft = false
showpagemeta = true
slug = ""
tags = ["development", "self-hosting", "privacy", "tutorial"]
title = "Self-hosting Adventures Part 2"
description = "Web server configuration"

+++

In order to run all the different services from a single server, I used a number of virtual hosts pointing to different applications/ports on the server. I used nginx and server blocks to get this done. I also wanted to make sure that I used HTTPS/TLS for all kinds of web traffic. That leads us into the first part of the configuration.

Obtaining a self-signed certificate
-----------------------------------
First of all, big shoutout to the team at [Let's Encrypt](https://letsencrypt.com/) for their incredible work. For anyone wondering how their service works to provide trusted self-signed certificates, I highly recommend reading [how it works](https://letsencrypt.org/how-it-works/). Now let's dive into the process.

I followed [this guide from Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-14-04) to generate my certificate. Instead of just the two domains (as with the example in that guide), I specified all of my *planned* host names, and it was quite a big list. I also had to make sure that the A records of all those host names existed with my domain registrar. Once I had my self-signed certificate, I was having a little trouble setting up my singular certificate with all of my different server blocks. After some [ducking](https://duckduckgo.com), however, I finally figured it out and now my `/etc/nginx/sites-available/default` file kind of looks like this:
```
server {
    listen 443 tls;
    server_name sadmansk.com;

    # certificate directives (from the guide linked above)
    .
    .
    # location and other directives
    .
    .
}
# other services had blocks similar to this
server {
    listen 443 tls;
    server_name *host*.sadmansk.com;
    
    location \ {
        
```

Redirecting Traffic
-------------------

I added the following blocks, one for redirecting HTTP traffic to HTTPS and the other for removing `www` as a hostname:
```
# HTTP redirects to HTTPS
server {
    listen 80;
    server_name *.sadmansk.com;
    return 301 https://$host$request_uri;
}
# redirect WWW
server {
    listen 443;
    server_name www.sadmansk.com;
    return 301 $scheme://sadmansk.com$request_uri;
}
```

Virtual Hosts
-------------
For applications that ran on various ports on the machines, I setup reverse proxies inside their respective server blocks:

```
    location /  {
        proxy_set_header        Host $host;
        proxy_set_header        X-Real-IP $remote_addr;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header        X-Forwarded-Proto $scheme;

        proxy_pass              http://localhost:PORT/;
    }
```

Setting up the virtual host for [Gitlab](https://git.sadmansk.com/) was a little trickier. I followed the instructions on this [section](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/nginx.md#using-a-non-bundled-web-server) of the documentation to make it work properly.

And that's pretty much it for the webserver! Next up, I'll focus on how my Gitlab instance is setup, and how I take advantage of Gitlab CI for deploying my website and blog.
