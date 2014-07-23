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

## Implementation status
Just this document and the repository at [Github](https://github.com/tazjin/recovery/)

## Known problems & Open questions

* This makes me theoretically vulnerable to identity takeovers by somebody who can access my deposit boxes. How do I add a safety factor outside of those? How many levels deep can it go?
* Can there be a reliable secret known to me with not much explanation (and assuming the explanation is public) even after a memory loss event?

## Future paranoia options

Things I can do to improve the security of this:

* Split up physical tokens into several deposit boxes, figure out a way to remind myself of where they are (symmetrically encrypted public note about this, with me carrying the symmetric key in some form)

-----BEGIN PGP SIGNATURE-----
Version: GnuPG v2

iQIcBAEBCgAGBQJT0CTuAAoJEGb1BWgduPQ7eMcQAL7jSNu4tkb3nuwZSLAsooT8
zBKB+C44ZhIN8p2dPq+wxP0zqRSMzOV4uh2vInX5z4+yASnnYTuAGsBlnlGzGfGm
+17Ct1OZQYc1iORaKlej7HTYWXandnXCM8ue6HZNZNgcjTo4jkafvS6aQG+c20RR
3HEzsnwI+Qe8myfVRQG34/FEtPe9QFgQNi6oD/hpiVQ9pN3RWDYFnAfgTmO6mgMM
gY5Z/RNzvNbUBTAA+bxhiQPS++L8iutHtYK9WXdoFP+zY0flUbjsjRDhBDWowIO2
Xy6RoIUeOjivDYbG8MtB/ibQ6pxiEaiDibxKrZ95082e7wxaf5lWTF+dAOvCqRVD
bqdAFVI0xWDGQkmrzjjevCtZd5KN2u1zTGYBXyuZ+z2RSRE1mTk5CjQT2x3xebvS
L8Ee8ixTfzAHqK4z17YM/3uvOvFjL5tFQja0AnHsORGuk6gYB7Y8I3Mkf0CEoFna
rEFPE7wJvqX7V69F+F8o5ragXVpDoj6D0CfPHFBqrB+QiiGK0pQYt4CXLK8bNgO6
qQc1I6LxQ+p1XTC9Us53XguAbtLTSIBr0ko5NIj4+GWLVFoDYkEpZfLHN3DolTXW
GK2ZsRMwP6gef1hPf/4IhyMgdIrL+FakAIBkUJ3OdroVbShHePUvePr4JZQIO0A+
T1n8ezZ9Pi+SGvC/tDZG
=0mQY
-----END PGP SIGNATURE-----
