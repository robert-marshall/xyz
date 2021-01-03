---
layout: post
title: "Install PeerTube On Debian"
date: 2021-01-04
tags: [peertube, debian]
---

### table of contents
*  [Dependencies](#dependencies)
* [User](#user)
* [Database](#basedase)
* [PeerTube](#peertube)
* [Nginx](#nginx)
* [Tuning](#tuning)
* [systemd](#systemd)
* [Administrator](#administrator)

### Dependencies

```
apt install -y curl sudo unzip vim

curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt-get install -y nodejs

curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

apt update && apt install yarn

apt install nginx ffmpeg postgresql postgresql-contrib openssl g++ make redis-server git python-dev

systemctl start redis postgresql
```

### User

```
useradd -m -d /var/www/peertube -s /bin/bash -p peertube peertube
passwd peertube
```

### Database

```
sudo -u postgres createuser -P db_username
sudo -u postgres createdb -O db_name -E UTF8 -T template0 peertube_prod

sudo -u postgres psql -c "CREATE EXTENSION pg_trgm;" peertube_prod
sudo -u postgres psql -c "CREATE EXTENSION unaccent;" peertube_prod
```

### Peertube

```
VERSION=$(curl -s https://api.github.com/repos/chocobozzz/peertube/releases/latest | grep tag_name | cut -d '"' -f 4) && echo "Latest Peertube version is $VERSION"

cd /var/www/peertube && sudo -u peertube mkdir config storage versions && cd versions

sudo -u peertube wget -q "https://github.com/Chocobozzz/PeerTube/releases/download/${VERSION}/peertube-${VERSION}.zip"
sudo -u peertube unzip peertube-${VERSION}.zip && sudo -u peertube rm peertube-${VERSION}.zip

cd ../ && sudo -u peertube ln -s versions/peertube-${VERSION} ./peertube-latest
cd ./peertube-latest && sudo -H -u peertube yarn install --production --pure-lockfile

cd /var/www/peertube && sudo -u peertube cp peertube-latest/config/production.yaml.example config/production.yaml

$EDITOR config/production.yaml
```

### Nginx

```
sudo cp /var/www/peertube/peertube-latest/support/nginx/peertube /etc/nginx/sites-available/peertube

sudo sed -i 's/${WEBSERVER_HOST}/[peertube-domain]/g' /etc/nginx/sites-available/peertube
sudo sed -i 's/${PEERTUBE_HOST}/localhost:9000/g' /etc/nginx/sites-available/peertube

sudo $EDITOR /etc/nginx/sites-available/peertube

sudo ln -s /etc/nginx/sites-available/peertube /etc/nginx/sites-enabled/peertube
sudo nginx -t

sudo systemctl restart nginx
```

### Tuning

```
sudo cp /var/www/peertube/peertube-latest/support/sysctl.d/30-peertube-tcp.conf /etc/sysctl.d/
sudo sysctl -p /etc/sysctl.d/30-peertube-tcp.conf
```

### systemd

```
sudo cp /var/www/peertube/peertube-latest/support/systemd/peertube.service /etc/systemd/system/

sudo systemctl daemon-reload
sudo systemctl enable peertube

sudo systemctl start peertube
sudo journalctl -feu peertube

sudo service peertube start
```

### Administrator

```
cd /var/www/peertube/peertube-latest && NODE_CONFIG_DIR=/var/www/peertube/config NODE_ENV=production npm run reset-password -- -u root
```
