---
layout: post
title: "Install Matrix Synapse"
date: 2021-02-13
tags: [matrix, nginx, debian]
---

### Table of Contents
* [matrix](#matrix)
* [nginx](#nginx)

### Matrix
```
sudo apt install -y lsb-release wget apt-transport-https
```

<br />

```
sudo wget -O /usr/share/keyrings/matrix-org-archive-keyring.gpg https://packages.matrix.org/debian/matrix-org-archive-keyring.gpg
```

<br />

```
echo "deb [signed-by=/usr/share/keyrings/matrix-org-archive-keyring.gpg] https://packages.matrix.org/debian/ $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/matrix-org.list
```

<br />

```
sudo apt update
```

<br />

```
sudo apt install matrix-synapse-py3
```

<br />

```
$EDITOR /etc/matrix-synapse/homeserver.yaml
    enable_registration: true
```

<br />

```
systemctl restart matrix-synapse
```

### Nginx

```
$EDITOR /etc/nginx/sites-available/matrix
```

<br />

```
server {
    listen 443 ssl;
    server_name matrix.myawesomesite.com;

    ssl on;
    ssl_certificate     /etc/nginx/ssl/cert.pem;
    ssl_certificate_key    /etc/nginx/ssl/key.pem;
    ssl_client_certificate /etc/nginx/ssl/client.crt;
    ssl_verify_client on;

    location / {
        proxy_pass http://localhost:8008;
        proxy_set_header X-Forwarded-For $remote_addr;
    }
}
```

<br />

```
ln -s /etc/nginx/sites-available/matrix /etc/nginx/sites-enabled/matrix
nginx -t
```

<br />

```
systemctl restart nginx
```




