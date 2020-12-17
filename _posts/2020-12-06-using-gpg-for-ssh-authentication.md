---
layout: post
title: "Using GPG For SSH Authentication"
date: 2020-12-06
tags: [gpg, ssh]
---

```
echo enable-ssh-support >> $HOME/.gnupg/gpg-agent.conf
```

<br />

```
$EDITOR ~/.bashrc
```

<br />

```
unset SSH_AGENT_PID
if [ "${gnupg_SSH_AUTH_SOCK_by:-0}" -ne $$ ]; then
  export SSH_AUTH_SOCK="$(gpgconf --list-dirs agent-ssh-socket)"
fi
export GPG_TTY=$(tty)
gpg-connect-agent updatestartuptty /bye >/dev/null
```

<br />

```
gpg --list-keys --with-keygrip
```

<br />

```
/home/john/.gnupg/pubring.kbx
-------------------------------
pub   ed25519/0xDDC02A3277446075 2020-12-17 [C]
      Key fingerprint = 9E14 10EB BDF4 FF2E 38A5  E791 DDC0 2A32 7744 6075
      Keygrip = 40652CFE7B26B9D1BED00A4B611FDFBC29C90278
uid                   [ultimate] John Doe <john@myawesomesite.com>
sub   ed25519/0x747A8AE5E0D62442 2020-12-17 [S]
      Keygrip = 1E41CB5D0A0609A7CC294F30B57D1845B5CA1FF8
sub   ed25519/0x0E37E18B7E50FABE 2020-12-17 [A]
      Keygrip = B407DBA27867FA9FDF1590C02C0CD7A53B11265D
sub   cv25519/0x554E03ABE05B8D80 2020-12-17 [E]
      Keygrip = 4021E10E5BF9236A576146CDB9E6946805F11483
```

<br />

```
echo B407DBA27867FA9FDF1590C02C0CD7A53B11265D >> ~/.gnupg/sshcontrol
```

<br />

```
ssh-add -l
256 SHA256:/DPdoURGWR51XtoRmLukat3dxWeFQkOwrUY3rO1dJtw (none) (ED25519)
```

<br />

```
gpg --export-ssh-key john
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIPCpHG3iKBszyJ2NJ0P5dVZbNGpzYdSNt8f6OAO3RKAa openpgp:0x7E50FABE
```

