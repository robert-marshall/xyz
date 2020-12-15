---
layout: post
title: "Generating ed25519 SSH Key"
date: 2020-12-07
tags: [ssh, ecc, ed25519]
---

##### table of contents
- [generating](#generating)
- [adding](#adding)
- [specifying](#specifying)

# [generating](#generating)

```
ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C "user@myawesomesite.com"
```

# [adding](#adding)

```
eval "$(ssh-agent -s)"

ssh-add ~/.ssh/id_ed25519

ssh-add
```

# [specifying](#specifying)

```
$EDITOR ~/.ssh/config
```

<br />

```
Host awesomesite
  HostName awesomesite.com
  User user
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
```
