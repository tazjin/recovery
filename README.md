-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA512

# Recovery outline

This project is my recovery plan for access to my online identities in case something unexpected happens. The idea is to cover all unexpected events from something as little as a disk failure to as big as an accident causing complete memory loss.

I don't believe in security by obscurity, rather the cryptography and physical safety used for the elements of this plan needs to be trustworthy.

## Technologies and tools

This plan is based partially on technology and partially on physical objects as well. The involved components are:

* my GPG private key
* my SSH private key
* (Yubikey) * backup factor
* (safety deposit box) * backup factor
* several publically accessible and mirrored git repositories with strong content encryption.
** this repository, existing on Github, BitBucket and possibly at other places as well. It should contain instructions that I could follow even if I had no recollection of creating this recovery plan
** a single file encrypted to my own public key 
** my [pass](http://www.passwordstore.org/)-store (TODO: directory structure leak fix)
* a physical reminder of the existence of this that I can, for example, carry in my wallet. Really cool would be something in card-format containing RFID as well. (TODO: investigate)

## Baseline assumptions

These are the minimum available things I assume for being able to recover using this plan.

* I can think, use computers and understand English
* I can physically move to places to retrieve things or send someone to retrieve them for me
* I know and can prove my real-life identity

## The plan

### Online

**password store**:
A repository somewhere on the internet containing my pass-store. This repository *should* require my SSH private key to access.

**README.md**:
This document, containing information about how the plan works. The current version of this document must always be signed with my private key and preferably exist in a git repository with the `HEAD` signed by my private key as well.

**hello.md**:
A symmetrically encrypted document for my future self in case I have forgotten about this for some reason. I carry the encryption key with the physical reminder token mentioned above. The document must be signed with my private key and contain instructions on how to verify it's authenticity.
This document *must* not be considered secret, just a bit harder to get to. They can contain information about the location of my deposit box(en).

**secrets.gpg**:
Encrypted secrets needed for recovery, this includes:
* SSH private key
* Instructions
** How do I retrieve and open the password store with the things I have at this very moment?
** How do I verify that these instructions were written by me?
* 2-factor recovery tokens where applicable (GMail is of highest importance)

### Offline

**Yubikeys**:

Yubikeys have a [second slot](http://www.yubico.com/products/services-software/personalization-tools/) that you can customize.

* First slot: GPG private key passphrase
* Second slot: SSH private key passphrase

**Private keys**:
All copies of these private keys must be protected by a passphrase.

* Printed copies of both private keys in unambigous & OCR-compatible font (TODO: investigate). Laminated if possible.
* USB memory with private keys

**Safety deposit boxes**:
For starters one box containing everything will have to do (especially because they're really hard to get in Stockholm). Ideally I would have them spread out around different places (that'll probably get me on some lists).

Contents of the safety deposit [boxen](http://en.wiktionary.org/wiki/boxen):
* One Yubikey containing what is mentioned above
* One USB memory containing private keys
* Physical copies of private keys.

It is important to separate the private keys from the passphrases because until then the passphrases are essentially useless. Need more deposit boxes!

## Implementation status
Nothing yet

## Known problems & Open questions

* This makes me theoretically vulnerable to identity takeovers by somebody who can access my deposit boxes. How do I add a safety factor outside of those? How many levels deep can it go?
* Can there be a reliable secret known to me with not much explanation (and assuming the explanation is public) even after a memory loss event?

## Future paranoia options

Things I can do to improve the security of this:

* Split up physical tokens into several deposit boxes, figure out a way to remind myself of where they are (symmetrically encrypted public note about this, with me carrying the symmetric key in some form)
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v2

iQIcBAEBCgAGBQJT0BmlAAoJEGb1BWgduPQ7mCsP/0X5PJMNpGtBCiXlOwPQ2stE
IcVS+A/nx1q7FAPs7nyPDiI0WVTVWyN/YXfVag1KTPtMUG+Wn1aJqqs4of3QygNt
ZnUGCN2RMCCSpNTuqv16X71XmptklV/O1nDPH5cFSq/yeWKFjTjWA0rK5o9XCqfF
E0/ebbmNmu20YURKp5qOPLjDzEJMuxeeSKxkc4/INI4gH6CMRYg3R9Xc+0EH3/0V
shE6TqIx+Xf7nf9LHUw5Ouwj84O3X25zLLJazYf4Vx4X0zk2IkP+s2njEcn5qk3a
3iFDbSSmUC2f3br5YWM39EHygUlfDLD939/cefKJ59l6LYonCRv4jB9BVuE/K6hw
x5n0At9Ea5rG4Jn42g8Vag93cJ+LNvDNmbXeP12rhfhWEp5mI7vjJHEkQuFm6VCN
65dzyArI9XPIj1V0+B+qPqZh3SYG/xWint4VGHs3XEdIWVqe01RJTgAB3zLGecdd
e97ajwtXtn06EiuT9wF5DeXkBEslZqo1ijxCgM5sWpPHg5MsySKAFU/mfdV5sitG
l3K6FE1qbaQ0YAKd8FHvFWt3Ic3jsdv7CeyW1s1hAz08ltxDymg9H40TgoWg06ou
dvG+EzAnKwOo7q2FqSEX2Col7W1hhlsfW1FsZV/Ou/xY05fQlEHF7kIUzykdAyeJ
TsUU0utHI9GNNGW8Jx5e
=IXnU
-----END PGP SIGNATURE-----