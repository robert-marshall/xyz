---
layout: post
title: "Setting Up A Git Server"
date: 2020-12-07
tags: [ssh, git]
---

### Table of Contents
* [On The Server](#on-the-server)
* [On The Computer](#on-the-computer)
   * [Pushing to the Server](#pushing)
   * [Cloning the Repository](#cloning)


### On The Server
```
adduser git
su - git
mkdir .ssh && chmod 700 .ssh
touch .ssh/authorized_keys && chmod 600 .ssh/authorized_keys
exit
```

<br />

```
$EDITOR /usr/share/git-core/templates/description
```

<br />

```
cd /srv/
mkdir git
chown git:git -R git/
cd git
```

<br />

```
su git
mkdir myawesomeproject
cd myawesomeproject
git init --bare
```

### On The Computer
```
gpg --export-ssh-key john | ssh root@myawesomesite.com "cat >>  ~/.ssh/authorized_keys"
```

#### Pushing to the Servers
```
cd myawesomeproject
git init
git add .
git commit -sm 'descriptive commit message'
git remote add origin git@myawesomesite.com:/srv/git/myawesomeproject
git push origin master
```

### Cloning the Repository
```
git clone git@myawesomesite.com:/srv/git/myawesomeproject
cd project
$EDITOR file
git add .
git commit -sm 'descriptive commit message'
git push origin master
```


