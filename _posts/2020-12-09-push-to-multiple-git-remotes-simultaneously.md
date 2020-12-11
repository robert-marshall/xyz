---
layout: post
title: "Push To Multiple Git Remotes Simultaneously"
date: 2020-12-09
tags: [git, ssh]
---

##### table of contents
- [server](#server)
- [computer](#computer)

# [server](#server)

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

# [computer](#computer)

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

##### Resources
- [Setting Up A Git Server](https://robertmarshall.xyz/setting-up-a-git-server)
- [Generating ed25519 SSH Key](https://robertmarshall.xyz/generating-ed25519-ssh-key)
