---
layout: post
title: "Transmission-Daemon Notifications"
date: 2020-12-13
tags: [transmissionbt, bittorrent]
---

### Tables of Contents
* [Configure Notifications Script](#configure-notifications-script)
* [Configure Transmission](#configure-transmission)


### Configure Notifications Script
```
mkdir scripts
cd scripts
```

<br />

```
$EDITOR transmission.sh
```

<br />

```
#!/bin/sh
curl -s \
  -F "token=API-Token" \
  -F "user=UserKey" \
  -F "message=Transmission completed downloading $TR_TORRENT_NAME" \
  -F "title=$TR_TORRENT_NAME" \
  https://api.pushover.net/1/messages.json
```

### Configure Transmission 
```
systemctl stop transmission-daemon
```

<br />

```
$EDITOR /etc/transmission-daemon/settings.json
```

<br />

```
{
    "alt-speed-down": 0,
    "alt-speed-enabled": false,
    "alt-speed-time-begin": 0000,
    "alt-speed-time-day": 127,
    "alt-speed-time-enabled": false,
    "alt-speed-time-end": 0000,
    "alt-speed-up": 0,
    "bind-address-ipv4": "0.0.0.0",
    "bind-address-ipv6": "::",
    "blocklist-enabled": true,
    "blocklist-url": "http://john.bitsurge.net/public/biglist.p2p.gz",
    "cache-size-mb": 4,
    "dht-enabled": false,
    "download-dir": "/mnt/diska/t/complete",
    "download-limit": 0,
    "download-limit-enabled": 0,
    "download-queue-enabled": true,
    "download-queue-size": 0,
    "encryption": 2,
    "idle-seeding-limit": 0,
    "idle-seeding-limit-enabled": true,
    "incomplete-dir": "/mnt/diskb/t/incomplete",
    "incomplete-dir-enabled": true,
    "lpd-enabled": false,
    "max-peers-global": 0,
    "message-level": 1,
    "peer-congestion-algorithm": "",
    "peer-id-ttl-hours": 1,
    "peer-limit-global": 0,
    "peer-limit-per-torrent": 50,
    "peer-port": 51413,
    "peer-port-random-high": 65535,
    "peer-port-random-low": 49152,
    "peer-port-random-on-start": true,
    "peer-socket-tos": "default",
    "pex-enabled": false,
    "port-forwarding-enabled": false,
    "preallocation": 1,
    "prefetch-enabled": true,
    "queue-stalled-enabled": true,
    "queue-stalled-minutes": 30,
    "ratio-limit": 0,
    "ratio-limit-enabled": true,
    "rename-partial-files": true,
    "rpc-authentication-required": false,
    "rpc-bind-address": "0.0.0.0",
    "rpc-enabled": true,
    "rpc-host-whitelist": "*",
    "rpc-host-whitelist-enabled": true,
    "rpc-password": "",
    "rpc-port": 9091,
    "rpc-url": "/transmission/",
    "rpc-username": "transmission",
    "rpc-whitelist": "127.0.0.1",
    "rpc-whitelist-enabled": true,
    "scrape-paused-torrents-enabled": true,
    "script-torrent-done-enabled": true,
    "script-torrent-done-filename": "/home/user/transmission.sh",
    "seed-queue-enabled": false,
    "seed-queue-size": 10,
    "speed-limit-down": 100,
    "speed-limit-down-enabled": false,
    "speed-limit-up": 0,
    "speed-limit-up-enabled": true,
    "start-added-torrents": true,
    "trash-original-torrent-files": false,
    "umask": 0,
    "upload-limit": 0,
    "upload-limit-enabled": 0,
    "upload-slots-per-torrent": 0,
    "utp-enabled": false
}
```

<br />

```
systemctl start transmission-daemon
```

