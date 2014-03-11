IRCrypt – Encryption Layer for IRC
==================================

*IMPORTANT: This is a working draft and not intended for usage yet!*

IRCrypt is intended to define an encryption layer for the IRC protocol defined
in [rfc1459]. The projects primary goals are:

1. Not to interfere with regular IRC. IRC is used as transport protocol, thus
   stays completely intact. IRCrypt should not cause any problems for regular
   clients.
2. To be easily adoptable, so that it can be adapted for and integrated into a
   wide range of clients quickly.
3. To be flexible in such a way that it supports a wide range of strong
   cryptographic ciphers.
4. To enable encryption and key exchange based on a web of trust.


OpenPGP
-------

IRCrypt neither defines custom cryptographic ciphers, nor a way how to use or
implement those ciphers. Instead it relies on the OpenPGP standard defined in
[rfc4880].

OpenPGP is implemented among other projects by the GNU privacy Guard [gnupg]
which can be used for message de- and encryption as well as managing the
web-of-trust. The first plug-ins to implement IRCrypt are based on GPG and it
is our recommendation to do the same if you want to build a plug-in for your
client.


IRCrypt Protocol Definition
---------------------------

To help IRCrypt grow a little bit faster, there exists a **basic version** of
IRCrypt and some **optional extensions**. So some parts of the protocol are
divided into the definition of the basic version and the **optional
extensions**. The structure of the protocol is as following:

1. **General protocol information**
2. **Symmetric Cipher**
3. **Asymmetric Cipher**
	1. Basic Version
	2. Optional Extensions
4. **Key Exchange**
	1. Basic Version
	2. Optional Extensions

References
----------

 - [rfc1459] http://tools.ietf.org/html/rfc1459
 - [rfc4880] http://tools.ietf.org/html/rfc4880
 - [gnupg]   http://www.gnupg.de
