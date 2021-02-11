---
layout: post
title: "Autoconnect OpenVPN on Boot"
date: 2021-02-10
tags: [openvpn]
---

```
nano /etc/openvpn/login.txt
```

<br />

```
user
pass
```

<br />

```
chmod 700 /etc/openvpn/login.txt
nano /etc/init.d/openvpnauto
```

<br />

<script src="https://gist.github.com/robert-marshall/5fc9f60251e200dbc272a753c49989c8.js"></script>

<br />

```
chmod +x /etc/init.d/openvpnauto
update-rc.d openvpnauto defaults 98

```
<br />

```
service openvpnauto start
reboot
```