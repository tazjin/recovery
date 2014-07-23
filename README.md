-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA512

# Recovery outline

This project is my recovery plan for access to my online identities in case something unexpected happens. The idea is to cover all unexpected events from something as little as a disk failure to as big as an accident causing complete memory loss.

I don't believe in security by obscurity, rather the cryptography and physical safety used for the elements of this plan needs to be trustworthy.

The rough idea is that I can recover access to my online identities from my email account. To guarantee access to my email account, I need a secure way for me to access my account password and two-factor token basically from scratch.

My password management is done with simple GPG encryption to my own key. The idea is to store a GPG key in a physically safe location so that I can use it in combination with public data to access my stuff. The chain is as follows:

Physical token with GPG private key passphrase (on a Yubikey, in a deposit box)
- -> protected GPG private key (printed / on USB in a (separate) deposit box)
- -> public repository (this) with GPG encrypted instructions
- -> instructions lead to SSH private key recovery
- -> instructions have two-factor emergency tokens
- -> SSH private key allows retrieval of password store
- -> password store (dependent on GPG key) contains Google credentials (and in best case even still valid ones for all other stuff)

## Technologies and tools

This plan is based partially on technology and partially on physical objects as well. The involved components are (for N = backup factor):

* my GPG private key
* my SSH private key
* N Yubikeys
* N safety deposit boxes
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
* Access to my email allows access recovery to other services

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

**USB memory**:
The USB memory **must** contain a file with the filenames and SHA-512 digests of all files contained on it. This file **must** be signed with my key.

## Implementation status
Just this document and the repository at [Github](https://github.com/tazjin/recovery/)

## Known problems & Open questions

* This makes me theoretically vulnerable to identity takeovers by somebody who can access my deposit boxes. How do I add a safety factor outside of those? How many levels deep can it go?
* Is it possible to make the boxes tamper-proof, i.e. have it be obvious that somebody opened them and looked at the content? Is read-once USB memory a thing? How do you make sure there is enough redundancy for a person not to go and tamper with all your copies just to make you lose access?
* Can there be a reliable secret known to me with not much explanation (and assuming the explanation is public) even after a memory loss event?

## Random notes

* The contents of the USB key must be as permanent as possible, replacing all USB keys should (optimally) be an expensive thing to do
* Do **not** rely on humans

## Future paranoia options

Things I can do to improve the security of this:

* Split up physical tokens into several deposit boxes, figure out a way to remind myself of where they are (symmetrically encrypted public note about this, with me carrying the symmetric key in some form)

-----BEGIN PGP SIGNATURE-----
Version: GnuPG v2

iQIcBAEBCgAGBQJT0D9FAAoJEGb1BWgduPQ7phgP/1oxvSh67vApzrvUllk3hbqQ
cNm5tAwD5RzODRYlHurbuWxjYyhiGpaYd4ghy5z9uE6hGgR1UNy7xIRK3ovnpMDT
1m2mfyDxJE00vLwUWvpprkj2sDoR9qb1vNhguI8rMvm6EC1bnfd1tVeyJLIlFAm6
RNNquhBb37pi8gZWpSyBI07aef9enIf+Nr4ZHe1I3SQCeJIdV8hcUN8fZ757CtKv
kPeKeCUzrKAERxAkj6L4ColrjKn7/kgEXhnGXi/6pIImLfFz/OBZXxxuzzmCM9J0
JU9n3b9eKjAG1u9pfRVAvGBFivrHtYf2BRYNrWb94kH68fEzIu6nSf/M8VcDDLnH
3RwEMCLwxzZsUKaLFbUBLnU+ZAuKdqQH0ZOVgJHUdFiL5whw/fZB+kReg2KoNzIl
Ilj63tiGzpfOk0/GV32brrC1bK76y0oX1c+RnDS6qAQmVqglKvAA53+JVo5gWfho
cZ28ZM8k9QRtFvAiIhnlHJj8+rC71G3S8udNywbP2T89W9EtXoZ8Uvr4CAGYfOos
gTmphi7lWch/eM7xhBIxcwwFNsKYZdQOugcy7C+Vk/z8dl83cIpKTUVHhFIRmPXy
QJzRDdn99VKdQaxMPGobLdA5uNmoLzejyBmWzQakOVpj/Rc3Yd63BTy2xudHA5Lj
BxymU6xs3llyDmeJhKoe
=Xwj1
-----END PGP SIGNATURE-----
