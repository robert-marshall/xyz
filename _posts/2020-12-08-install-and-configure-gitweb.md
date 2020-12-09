---
layout: post
title: "Install And Configure GitWeb"
date: 2020-12-08
tags: [git, gitweb, fcgi, nginx, debian] 
---

##### table of contents
- [install](#install)
- [nginx](#nginx)
- [gitweb](#gitweb)
- [theme](#theme)

<br />

# [install](#install)

```
apt install nginx nginx-common git gitweb fcgiwrap highlight -y
```

# [nginx](#nginx)

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

  server_name git.myawesomesite.com;

  location /index.cgi {
    root /usr/share/gitweb/;
    include fastcgi_params;
    gzip off;
    fastcgi_param SCRIPT_NAME $uri;
    fastcgi_param GITWEB_CONFIG /etc/gitweb.conf;
    fastcgi_pass  unix:/var/run/fcgiwrap.socket;
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

# [gitweb](#gitweb)

```
$EDITOR /etc/gitweb.conf
```

<br />

```
# git folder
$projectroot = "/srv/git";

# display owner
our $omit_owner = 1; 

# highlight
$feature{'highlight'}{'default'} = [1];
$projects_list = $projectroot;
@stylesheets = ("static/gitweb.css");
$javascript = "static/gitweb.js";
```

<br />

```
systemctl stop nginx 
systemctl restart fcgiwrap 
systemctl start nginx
```

# [theme](#theme)

```
cd  -
```

<br />

```
git clone https://github.com/kogakure/gitweb-theme /usr/share/gitweb/gitweb-theme
cd /usr/share/gitweb/gitweb-theme/
./setup -vi --install
```

##### Resources
- [Generating ed25519 SSH Key](https://robertmarshall.xyz/generating-ed25519-ssh-key)
- [Setting Up A Git Server](https://robertmarshall.xyz/setting-up-a-git-server)

