---
layout: post
title: "Change Host Default SSH Key"
date: 2020-12-13
tags: [ssh]
---

```
cd /etc/ssh/
mkdir default_keys
mv ssh_host_* default_keys/
```

```
dpkg-reconfigure openssh-server
```

```
md5sum ssh_host_*
```

```
cd default_keys
md5sum ssh_host_*
```

```
cd /etc/ssh/
rm -rfv default_keys
rm ssh_host_ecdsa_key* ssh_host_rsa_key*
```

```
$EDITOR /etc/ssh/sshd_config
```

```
HostKey /etc/ssh/ssh_host_ed25519_key
KexAlgorithms curve25519-sha256@libssh.org
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com
MACs hmac-sha2-512-etm@openssh.com
```