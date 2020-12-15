---
layout: post
title: "Install Searx On Debian"
date: 2020-12-05
tags: [searx, uwsgi, nginx, debian]
---

##### table of contents
- [searx](#searx)
  - [install packages](#installpackages)
  - [create user](#createuser)
  - [install searx & dependencie](#installsearx&dependencie)
  - [configuration](#configuration)
- [uwsgi](#uwsgi)
- [nginx](#nginx)

# [searx](#searx)
- [install packages](#installpackages)

```
sudo -H apt-get install -y \
    virtualenv python3-dev python3-babel python3-venv \
    uwsgi uwsgi-plugin-python3 \
    git build-essential libxslt-dev zlib1g-dev libffi-dev libssl-dev \
    shellcheck
```

- [create user](#createuser)

```
sudo -H useradd --shell /bin/bash --system \
    --home-dir "/usr/local/searx" \
    --comment 'Privacy-respecting metasearch engine' searx

sudo -H mkdir "/usr/local/searx"

sudo -H chown -R "searx:searx" "/usr/local/searx"
```

- [install searx & dependencie](#installsearx&dependencie)

```
sudo -H -u searx -i

git clone "https://github.com/searx/searx.git" "/usr/local/searx/searx-src"

python3 -m venv "/usr/local/searx/searx-pyenv"

echo ". /usr/local/searx/searx-pyenv/bin/activate" >>  "/usr/local/searx/.profile"
```

<br />

```
sudo -H -u searx -i

command -v python && python --version
/usr/local/searx/searx-pyenv/bin/python
Python 3.8.1

pip install -U pip
pip install -U setuptools
pip install -U wheel

cd "/usr/local/searx/searx-src"

pip install -e .
```

- [configuration](#configuration)

```
sudo -H mkdir -p "/etc/searx"

sudo -H cp "/usr/local/searx/searx-src/searx/settings.yml" "/etc/searx/settings.yml"

sudo -H sed -i -e "s/ultrasecretkey/$(openssl rand -hex 16)/g" "/etc/searx/settings.yml"

sudo -H sed -i -e "s/{instance_name}/searx@$(uname -n)/g" "/etc/searx/settings.yml"
```

# [uwsgi](#uwsgi)

```
$EDITOR /etc/uwsgi/apps-available/searx.ini
```

<br />

```
[uwsgi]

# uWSGI core
# ----------
#
# https://uwsgi-docs.readthedocs.io/en/latest/Options.html#uwsgi-core

# Who will run the code
uid = searx
gid = searx

# set (python) default encoding UTF-8
env = LANG=C.UTF-8
env = LANGUAGE=C.UTF-8
env = LC_ALL=C.UTF-8

# chdir to specified directory before apps loading
chdir = /usr/local/searx/searx-src/searx

# searx configuration (settings.yml)
env = SEARX_SETTINGS_PATH=/etc/searx/settings.yml

# disable logging for privacy
disable-logging = true

# The right granted on the created socket
chmod-socket = 666

# Plugin to use and interpretor config
single-interpreter = true

# enable master process
master = true

# load apps in each worker instead of the master
lazy-apps = true

# load uWSGI plugins
plugin = python3,http

# By default the Python plugin does not initialize the GIL.  This means your
# app-generated threads will not run.  If you need threads, remember to enable
# them with enable-threads.  Running uWSGI in multithreading mode (with the
# threads options) will automatically enable threading support. This *strange*
# default behaviour is for performance reasons.
enable-threads = true


# plugin: python
# --------------
#
# https://uwsgi-docs.readthedocs.io/en/latest/Options.html#plugin-python

# load a WSGI module
module = searx.webapp

# set PYTHONHOME/virtualenv
virtualenv = /usr/local/searx/searx-pyenv

# add directory (or glob) to pythonpath
pythonpath = /usr/local/searx/searx-src


# speak to upstream
# -----------------
#
# Activate the 'http' configuration for filtron or activate the 'socket'
# configuration if you setup your HTTP server to use uWSGI protocol via sockets.

# using IP:
#
# https://uwsgi-docs.readthedocs.io/en/latest/Options.html#plugin-http
# Native HTTP support: https://uwsgi-docs.readthedocs.io/en/latest/HTTP.html

http = 127.0.0.1:8888

# using unix-sockets:
#
# On some distributions you need to create the app folder for the sockets::
#
#   mkdir -p /run/uwsgi/app/searx
#   chown -R searx:searx  /run/uwsgi/app/searx
#
# socket = /run/uwsgi/app/searx/socket
```

<br />

```
sudo -H ln -s /etc/uwsgi/apps-available/searx.ini /etc/uwsgi/apps-enabled/

sudo -H service uwsgi start   searx

sudo -H service uwsgi restart searx

sudo -H service uwsgi stop    searx
```

# [nginx](#nginx)

```
$EDITOR /etc/nginx/sites-available/searx
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

    server_name searx.myawesomesite.com;

    error_page 404 /404.html;
        location = /404.html {
        internal;
    }

    location / {
        include uwsgi_params;
        uwsgi_pass unix:/run/uwsgi/app/searx/socket;
    }

    root /usr/local/searx/searx-src/searx;
    location /static { }
}
```

<br />

```
nginx -t

sudo -H ln -s /etc/nginx/sites-available/searx /etc/nginx/sites-enabled/searx

sudo -H systemctl restart nginx
sudo -H service uwsgi restart searx
```


