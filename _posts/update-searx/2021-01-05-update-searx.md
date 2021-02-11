---
layout: post
title: "Update Searx"
date: 2021-01-05
tags: [searx, git]
---

```
sudo -H -u searx -i
```

<br />

```
cd searx-src
```

<br>

```
git stash
git pull origin master
git stash apply
./manage.sh update_packages
```

<br />

```
exit
```

<br />

```
systemctl restart uwsgi
```
