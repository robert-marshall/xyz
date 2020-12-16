---
layout: post
title: "Push To Multiple Git Remotes Simultaneously"
date: 2020-12-09
tags: [git]
---

### Table of Contents
* [On The Server](#on-the-server)
* [On The Computer](#on-the-computer)

### On The Server
```
su - git
```

<br />

```
cd /srv/git/
mkdir myawesomeproject
cd myawesomeproject
git init --bare
```

### On The Computer
```
mkdir myawesomeproject
cd myawesomeproject
git init
```

<br />

```
git remote -v
git remote add origin git@myawesomesite.com:/srv/git/myawesomeproject
git remote set-url --add --push origin git@myawesomesite.com:/srv/git/myawesomeproject
git remote set-url --add --push origin git@github.com:username/myawesomeproject
git remote set-url --add --push origin git@gitlab.com:username/myawesomeproject
```