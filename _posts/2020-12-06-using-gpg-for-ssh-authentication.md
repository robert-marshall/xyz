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
/home/user/.gnupg/pubring.kbx
-------------------------------
pub   ed25519/0xCFD0817C3ED641EC 2020-12-16 [C]
  Key fingerprint = 7A69 91F4 97C8 2D0D 92F5  7D26 CFD0 817C 3ED6 41EC
  Keygrip = E6C27E4747CF2AE23FD8B920801A566B82D7BAD4
uid                   [ultimate] John Doe <john@example.com>
sub   ed25519/0x7C076343DDCFF935 2020-12-16 [S]
  Keygrip = B22E4EBEF3CA1BFCF4C5D4D3D1691C20EC0E58C4
sub   ed25519/0xF68C485481EE8237 2020-12-16 [A]
  Keygrip = B9766D225F73842BC74BF2F8D7E2DCBBA8AD238E
sub   cv25519/0xAA1E1A86CE6A0068 2020-12-16 [E]
  Keygrip = 2C28BB45418BBFF293720EFDECE360816379192A
```

<br />

```
echo B9766D225F73842BC74BF2F8D7E2DCBBA8AD238E >> ~/.gnupg/sshcontrol
```

<br />

```
ssh-add -l
256 SHA256:LVaJ4xWkeC/VD+gw5aZpFA1XQXTTISrI1G2sm0xNTss (none) (ED25519)
```

<br />

```
gpg --export-ssh-key john
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINiLnlkHWQQ6CdQmOGiKtrKbXiQWnH3/GhglC5qKhdv2 openpgp:0x81EE8237
```

