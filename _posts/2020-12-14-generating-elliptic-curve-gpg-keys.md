---
layout: post
title: "Generating Elliptic Curve GPG Keys"
date: 2020-12-14
tags: [gpg, ecc, cryptography]
---

#### Table of Contents
* [Generate Master Key](#generate-master-key)
* [Generate Sub Keys](#generate-sub-keys)

#### Generate Master Key

```
gpg --expert --full-generate-key
```

<br />

```
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
   (9) ECC and ECC
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (13) Existing key
Your selection? 11
```

<br />

```
Possible actions for a ECDSA/EdDSA key: Sign Certify Authenticate 
Current allowed actions: Sign Certify 

   (S) Toggle the sign capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? s
```

<br />

```
Possible actions for a ECDSA/EdDSA key: Sign Certify Authenticate 
Current allowed actions: Certify 

   (S) Toggle the sign capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? q
```

<br />

```
Please select which elliptic curve you want:
   (1) Curve 25519
   (3) NIST P-256
   (4) NIST P-384
   (5) NIST P-521
   (6) Brainpool P-256
   (7) Brainpool P-384
   (8) Brainpool P-512
   (9) secp256k1
Your selection? 1
```

<br />

```
Please specify how long the key should be valid.
 0 = key does not expire
  <n>  = key expires in n days
  <n>w = key expires in n weeks
  <n>m = key expires in n months
  <n>y = key expires in n years
Key is valid for? (0) 0
```

<br />

```
Key does not expire at all
Is this correct? (y/N) y
```

<br />

```
GnuPG needs to construct a user ID to identify your key.

Real name: John Doe
Email address: [john@example.com](mailto:john@example.com)
```

<br />

```
Comment: 
You selected this USER-ID:
"John Doe <[john@example.com](mailto:john@example.com)>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
```

<br />

```
┌──────────────────────────────────────────────────────┐
│ Please enter the passphrase to                       │
│ protect your new key                                 │
│                                                      │
│ Passphrase: ________________________________________ |
│                                                      │
│       <OK>                <Cancel>                   │
└──────────────────────────────────────────────────────┘
```

<br />

```
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: key 0xCFD0817C3ED641EC marked as ultimately trusted
gpg: revocation certificate stored as '/home/user/.gnupg/openpgp-revocs.d/7A6991F497C82D0D92F57D26CFD0817C3ED641EC.rev'
public and secret key created and signed.

pub   ed25519/0xCFD0817C3ED641EC 2020-12-16 [C]
  Key fingerprint = 7A69 91F4 97C8 2D0D 92F5  7D26 CFD0 817C 3ED6 41EC
uid                              John Doe <[john@example.com](mailto:john@example.com)>
```

<br />

#### Generate Sub Keys

```
gpg --expert --edit-key CFD0817C3ED641EC
```

<br />

```
gpg (GnuPG) 2.2.12; Copyright (C) 2018 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Secret key is available.

gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
sec  ed25519/0xCFD0817C3ED641EC
 created: 2020-12-16  expires: never       usage: C   
 trust: ultimate      validity: ultimate
[ultimate] (1). John Doe <[john@example.com](mailto:john@example.com)>

gpg> addkey
```

<br />

```
Please select what kind of key you want:
   (3) DSA (sign only)
   (4) RSA (sign only)
   (5) Elgamal (encrypt only)
   (6) RSA (encrypt only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (12) ECC (encrypt only)
  (13) Existing key
Your selection? 11
```

<br />

```
Possible actions for a ECDSA/EdDSA key: Sign Authenticate 
Current allowed actions: Sign 

   (S) Toggle the sign capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? q
```

<br />

```
Please select which elliptic curve you want:
   (1) Curve 25519
   (3) NIST P-256
   (4) NIST P-384
   (5) NIST P-521
   (6) Brainpool P-256
   (7) Brainpool P-384
   (8) Brainpool P-512
   (9) secp256k1
Your selection? 1
```

<br />

```
Please specify how long the key should be valid.
 0 = key does not expire
  <n>  = key expires in n days
  <n>w = key expires in n weeks
  <n>m = key expires in n months
  <n>y = key expires in n years
Key is valid for? (0) 0
```

<br />

```
Is this correct? (y/N) y
Really create? (y/N) y
```

<br />

```
┌──────────────────────────────────────────────────────┐
│ Please enter the passphrase to                       │
│ protect your new key                                 │
│                                                      │
│ Passphrase: ________________________________________ |
│                                                      │
│       <OK>                <Cancel>                   │
└──────────────────────────────────────────────────────┘
```

<br />

```
sec  ed25519/0xCFD0817C3ED641EC
 created: 2020-12-16  expires: never       usage: C   
 trust: ultimate      validity: ultimate
ssb  ed25519/0x7C076343DDCFF935
 created: 2020-12-16  expires: never       usage: S   
[ultimate] (1). John Doe <[john@example.com](mailto:john@example.com)>

gpg> addkey
```

<br />

```
Please select what kind of key you want:
   (3) DSA (sign only)
   (4) RSA (sign only)
   (5) Elgamal (encrypt only)
   (6) RSA (encrypt only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (12) ECC (encrypt only)
  (13) Existing key
Your selection? 11
```

<br />

```
Possible actions for a ECDSA/EdDSA key: Sign Authenticate 
Current allowed actions: 

   (S) Toggle the sign capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? a
```

<br />

```
Possible actions for a ECDSA/EdDSA key: Sign Authenticate 
Current allowed actions: Authenticate 

   (S) Toggle the sign capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? q
```

<br />

```
Please select which elliptic curve you want:
   (1) Curve 25519
   (3) NIST P-256
   (4) NIST P-384
   (5) NIST P-521
   (6) Brainpool P-256
   (7) Brainpool P-384
   (8) Brainpool P-512
   (9) secp256k1
Your selection? 1
```

<br />

```
Please specify how long the key should be valid.
 0 = key does not expire
  <n>  = key expires in n days
  <n>w = key expires in n weeks
  <n>m = key expires in n months
  <n>y = key expires in n years
Key is valid for? (0) 0
```

<br />

```
Is this correct? (y/N) y
Really create? (y/N) y
```

<br />

```
┌──────────────────────────────────────────────────────┐
│ Please enter the passphrase to                       │
│ protect your new key                                 │
│                                                      │
│ Passphrase: ________________________________________ |
│                                                      │
│       <OK>                <Cancel>                   │
└──────────────────────────────────────────────────────┘
```

<br />

```
sec  ed25519/0xCFD0817C3ED641EC
 created: 2020-12-16  expires: never       usage: C   
 trust: ultimate      validity: ultimate
ssb  ed25519/0x7C076343DDCFF935
 created: 2020-12-16  expires: never       usage: S   
ssb  ed25519/0xF68C485481EE8237
 created: 2020-12-16  expires: never       usage: A   
[ultimate] (1). John Doe <[john@example.com](mailto:john@example.com)>

gpg> addkey
```

<br />

```
Please select what kind of key you want:
   (3) DSA (sign only)
   (4) RSA (sign only)
   (5) Elgamal (encrypt only)
   (6) RSA (encrypt only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (12) ECC (encrypt only)
  (13) Existing key
Your selection? 12
```

<br />

```
Please select which elliptic curve you want:
   (1) Curve 25519
   (3) NIST P-256
   (4) NIST P-384
   (5) NIST P-521
   (6) Brainpool P-256
   (7) Brainpool P-384
   (8) Brainpool P-512
   (9) secp256k1
Your selection? 1
```

<br />

```
Please specify how long the key should be valid.
 0 = key does not expire
  <n>  = key expires in n days
  <n>w = key expires in n weeks
  <n>m = key expires in n months
  <n>y = key expires in n years
Key is valid for? (0) 0
```

<br />

```
Is this correct? (y/N) y
Really create? (y/N) y
```

<br />

```
┌──────────────────────────────────────────────────────┐
│ Please enter the passphrase to                       │
│ protect your new key                                 │
│                                                      │
│ Passphrase: ________________________________________ |
│                                                      │
│       <OK>                <Cancel>                   │
└──────────────────────────────────────────────────────┘
```

<br />

```
sec  ed25519/0xCFD0817C3ED641EC
 created: 2020-12-16  expires: never       usage: C   
 trust: ultimate      validity: ultimate
ssb  ed25519/0x7C076343DDCFF935
 created: 2020-12-16  expires: never       usage: S   
ssb  ed25519/0xF68C485481EE8237
 created: 2020-12-16  expires: never       usage: A   
ssb  cv25519/0xAA1E1A86CE6A0068
 created: 2020-12-16  expires: never       usage: E   
[ultimate] (1). John Doe <[john@example.com](mailto:john@example.com)>

gpg> save
```

<br />

```
gpg -k
```

<br />

```
/home/user/.gnupg/pubring.kbx

*****

pub   ed25519/0xCFD0817C3ED641EC 2020-12-16 [C]
  Key fingerprint = 7A69 91F4 97C8 2D0D 92F5  7D26 CFD0 817C 3ED6 41EC
uid                   [ultimate] John Doe <[john@example.com](mailto:john@example.com)>
sub   ed25519/0x7C076343DDCFF935 2020-12-16 [S]
sub   ed25519/0xF68C485481EE8237 2020-12-16 [A]
sub   cv25519/0xAA1E1A86CE6A0068 2020-12-16 [E]
```
