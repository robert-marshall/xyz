---
layout: post
title: "Jekyll Automated Deployment"
date: 2020-12-10
tags: [jekyll, ruby, git, nginx, debian]
---

##### table of contents
- [server](#server)
- [nginx](#nginx)
- [computer](#computer)

# [server](#server)

```
apt install ruby-full build-essential git nginx
```

<br />

```
su - git
```

<br />

```
$EDITOR .bashrc
```

<br />

```
# Install Ruby Gems to ~/.gems
export GEM_HOME=$HOME/.gems
export PATH=$GEM_HOME/bin:$PATH
```

<br />

```
source .bashrc
gem install jekyll bundler
```

<br />

```
cd /srv/git/
mkdir myawesomeblog
cd myawesomeblog
git init --bare
```

<br />

```
$EDITOR hooks/post-receive
```

<br />

```
#!/bin/bash -l

# Install Ruby Gems to ~/.gems
export GEM_HOME=$HOME/.gems
export PATH=$GEM_HOME/bin:$PATH

TMP_GIT_CLONE=$HOME/tmp/myawesomeblog
GEMFILE=$TMP_GIT_CLONE/Gemfile
PUBLIC_WWW=/var/www/myawesomeblog

git clone $GIT_DIR $TMP_GIT_CLONE
BUNDLE_GEMFILE=$GEMFILE bundle install
BUNDLE_GEMFILE=$GEMFILE bundle exec jekyll build -s $TMP_GIT_CLONE -d $PUBLIC_WWW
rm -Rf $TMP_GIT_CLONE
exit
```

<br />

```
chmod +x hooks/post-receive
```

<br />

```
exit
```

<br />

```
mkdir /var/www/myawesomeblog
chown git:git -R /var/www/myawesomeblog/
```

# [nginx](#nginx)

```
cd /etc/nginx/sites-available/
$EDITOR myawesomeblog
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

    root /var/www/myawesomeblog;
    location / { }
}
```

<br />

```
ln -s /etc/nginx/sites-available/myawesomeblog /etc/nginx/sites-enabled/myawesomeblog
nginx -t
```

<br />

```
systemctl restart nginx
```

# [computer](#computer)

```
apt install ruby-full build-essential
```

<br />

```
$EDITOR .bashrc
```

<br />

```
# Install Ruby Gems to ~/.gems
export GEM_HOME=$HOME/.gems
export PATH=$GEM_HOME/bin:$PATH
```

<br />

```
source .bashrc
gem install jekyll bundler
```

<br />

```
jekyll new myawesomeblog
```

<br />

```
cd myawesomeblog
```

<br />

```
git init
git remote add deploy git@myawesomesite.com:/srv/git/myawesomeblog
git add .
git commit -m 'descriptive commit message'
git push deploy master
```

##### Resources
- [Setting Up A Git Server](https://robertmarshall.xyz/setting-up-a-git-server/)
- [Push To Multiple Git Remotes Simultaneously](https://robertmarshall.xyz/push-to-multiple-git-remotes-simultaneously/)
