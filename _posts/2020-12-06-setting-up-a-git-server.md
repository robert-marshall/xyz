---
layout: post
title: "Setting Up A Git Server"
date: 2020-12-06
tags: [ssh, git]
---

##### table of contents
- [computer](#computer)
- [server](#server)
- [push](#push)
- [clone](#clone)

# [computer](#computer)

```
scp ~/.ssh/id_ed25519.pub root@myawesomesite.com/tmp/
```

# [server](#server)

```
adduser git
su - git
mkdir .ssh && chmod 700 .ssh
touch .ssh/authorized_keys && chmod 600 .ssh/authorized_keys
exit
```

<br />

```
cat /tmp/id_ed25519.pub >> /home/git/.ssh/authorized_keys
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

# [push](#push)

```
cd myawesomeproject
git init
git add .
git commit -sm 'descriptive commit message'
git remote add origin git@myawesomesite.com:/srv/git/myawesomeproject
git push origin master
```

# [clone](#clone)

```
git clone git@myawesomesite.com:/srv/git/myawesomeproject
cd project
$EDITOR file
git commit -sam 'descriptive commit message'
git push origin master
```

##### Resources
- [Generating ed25519 SSH Key](https://robertmarshall.xyz/generating-ed25519-ssh-key)


