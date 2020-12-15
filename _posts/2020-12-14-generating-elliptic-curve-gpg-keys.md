---
layout: post
title: "Generating Elliptic Curve GPG Keys"
date: 2020-12-14
tags: [gpg, ecc, cryptography]
---

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
Is this correct? (y/N) y
```

<br />

```
Real name: John Doe
Email address: john@myawesomesite.com
```

<br />

```
Comment: 
You selected this USER-ID:
    "John Doe <john@myawesomesite.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
```

<br />

```
gpg -k
```

<br />

```
pub   ed25519/0xA29718477DE222AD 2020-12-10 [C]
      Key fingerprint = 1CC9 CF3C 56EA B2DA 22D0  8A95 A297 1847 7DE2 22AD
uid                   [ultimate] John Doe <john@myawesomesite.com>
```

<br />

```
gpg --expert --edit-key 0xA29718477DE222AD
```

<br />

```
sec  ed25519/0xA29718477DE222AD
     created: 2020-12-10  expires: never       usage: C   
     trust: ultimate      validity: ultimate
[ultimate] (1). John Doe <john@myawesomesite.com>

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
```

<br />

```
Really create? (y/N) 
```

<br />

```
sec  ed25519/0xA29718477DE222AD
     created: 2020-12-10  expires: never       usage: C   
     trust: ultimate      validity: ultimate
ssb  ed25519/0x83C57359B2D47835
     created: 2020-12-10  expires: never       usage: S   
[ultimate] (1). John Doe <john@myawesomesite.com>

gpg> 
```

<br />

```
gpg> addkey
```

<br />

```
Possible actions for a ECDSA/EdDSA key: Sign Authenticate 
Current allowed actions: Sign 

   (S) Toggle the sign capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? s
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
```

<br />

```
Really create? (y/N) y
```

<br />

```
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
```

<br />

```
Really create? (y/N) y
```

<br />

```
sec  ed25519/0xA29718477DE222AD
     created: 2020-12-10  expires: never       usage: C   
     trust: ultimate      validity: ultimate
ssb  ed25519/0x83C57359B2D47835
     created: 2020-12-10  expires: never       usage: S   
ssb  ed25519/0x68569F3EE4FC00AC
     created: 2020-12-10  expires: never       usage: A   
ssb  cv25519/0xBF2CEE6E46FA86DA
     created: 2020-12-10  expires: never       usage: E   
[ultimate] (1). John Doe <john@myawesomesite.com>

gpg> save
```

<br />

```
gpg -k
```

<br />

```
pub   ed25519/0xA29718477DE222AD 2020-12-10 [C]
      Key fingerprint = 1CC9 CF3C 56EA B2DA 22D0  8A95 A297 1847 7DE2 22AD
uid                   [ultimate] John Doe <john@myawesomesite.com>
sub   ed25519/0x83C57359B2D47835 2020-12-10 [S]
sub   ed25519/0x68569F3EE4FC00AC 2020-12-10 [A]
sub   cv25519/0xBF2CEE6E46FA86DA 2020-12-10 [E]
```

