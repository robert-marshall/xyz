---
layout: post
title: "Install And Configure Transmission Daemon"
date: 2020-12-11
tags: [transmission, daemon, bit-torrent, debian]
---

##### table of contents
- [install](#install)
- [configure](#configure)

# [install](#install)

```
apt install transmission-daemon
```

<br />

```
systemctl stop transmission-daemon
```

# [configure](#configure)

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
    "bind-address-ipv4": "127.0.0.1",
    "bind-address-ipv6": "::",
    "blocklist-enabled": true,
    "blocklist-url": "http://john.bitsurge.net/public/biglist.p2p.gz",
    "cache-size-mb": 4,
    "dht-enabled": false,
    "download-dir": "/mnt/drivename/torrents/complete",
    "download-limit": 0,
    "download-limit-enabled": 0,
    "download-queue-enabled": true,
    "download-queue-size": 0,
    "encryption": 2,
    "idle-seeding-limit": 0,
    "idle-seeding-limit-enabled": true,
    "incomplete-dir": "/mnt/drivename/torrents/incomplete",
    "incomplete-dir-enabled": true,
    "lpd-enabled": false,
    "max-peers-global": 0,
    "message-level": 0,
    "peer-congestion-algorithm": "lp",
    "peer-id-ttl-hours": 1,
    "peer-limit-global": 0,
    "peer-limit-per-torrent": 0,
    "peer-port": 49739,
    "peer-port-random-high": 65535,
    "peer-port-random-low": 49152,
    "peer-port-random-on-start": true,
    "peer-socket-tos": "reliability",
    "pex-enabled": false,
    "port-forwarding-enabled": false,
    "preallocation": 0,
    "prefetch-enabled": false,
    "queue-stalled-enabled": true,
    "queue-stalled-minutes": 0,
    "ratio-limit": 0,
    "ratio-limit-enabled": true,
    "rename-partial-files": false,
    "rpc-authentication-required": true,
    "rpc-bind-address": "0.0.0.0",
    "rpc-enabled": true,
    "rpc-host-whitelist": "",
    "rpc-host-whitelist-enabled": false,
    "rpc-password": "CHANGE_PASSWORD",
    "rpc-port": CHANGE_PORT_NUMBER,
    "rpc-url": "/transmission/",
    "rpc-username": "CHANGE_USERNAME",
    "rpc-whitelist": "127.0.0.1",
    "rpc-whitelist-enabled": false,
    "scrape-paused-torrents-enabled": false,
    "script-torrent-done-enabled": false,
    "script-torrent-done-filename": "",
    "seed-queue-enabled": false,
    "seed-queue-size": 0,
    "speed-limit-down": 0,
    "speed-limit-down-enabled": true,
    "speed-limit-up": 0,
    "speed-limit-up-enabled": true,
    "start-added-torrents": true,
    "trash-original-torrent-files": true,
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
