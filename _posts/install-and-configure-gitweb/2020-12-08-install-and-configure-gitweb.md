---
layout: post
title: "Install and Configure GitWeb"
date: 2020-12-08
tags: [gitweb, git]
---

#### Table of Contents
* [Install Dependencies ](#install-dependencies)
* [Configure Nginx](#configure-nginx)
* [Configure GitWeb](#configure-gitweb)
* [Set a Custom Theme](#set-a-custom-theme)

<br />

### Install Dependencies 

```
apt install nginx git gitweb fcgiwrap highlight -y
```

### Configure Nginx

```
$EDITOR /etc/nginx/sites-available/gitweb
```

<br />

```
server {
  listen 443 ssl http2;

  ssl on;
  ssl_certificate     /etc/nginx/ssl/cert.pem;
  ssl_certificate_key    /etc/nginx/ssl/key.pem;
  ssl_client_certificate /etc/nginx/ssl/client.crt;
  ssl_verify_client on;

  server_name myawesomesite.com;

  location /index.cgi {
    root /usr/share/gitweb/;
    include fastcgi_params;
    gzip off;
    fastcgi_param SCRIPT_NAME $uri;
    fastcgi_param GITWEB_CONFIG /etc/gitweb.conf;
    fastcgi_pass  unix:/var/run/fcgiwrap.socket;
    fastcgi_hide_header X-Powered-By;
  }

  location / {
    root /usr/share/gitweb/;
    index index.cgi;
  }
}
```

<br />

```
ln -s /etc/nginx/sites-available/gitweb /etc/nginx/sites-enabled/gitweb
```

<br />

```
nginx -t
service nginx restart
```

### Configure GitWeb

```
$EDITOR /etc/gitweb.conf
```

<br />

```
$GIT = "/bin/git";

# git folder
$projectroot = "/srv/git";
$project_maxdepth = 2009;

# dont display owner
our $omit_owner = 1;

# highlight
$feature{'highlight'}{'default'} = [1];
$projects_list = $projectroot;
@stylesheets = ("static/gitweb.css");
$javascript = "static/gitweb.js";

# catagories
$projects_list_group_categories = 1;
```

<br />

```
systemctl stop nginx 
systemctl restart fcgiwrap 
systemctl start nginx
```

### Set a Custom Theme

```
cd  -
```

<br />

```
git clone https://github.com/kogakure/gitweb-theme /usr/share/gitweb/gitweb-theme
cd /usr/share/gitweb/gitweb-theme/
./setup -vi --install
```
