Part 1: Sending and receiving encrypted messages
================================================

IRCrypt only affects private messages and notices as defined by section 4.4 of
[rfc1459]. All other messages shall be passed unchanged by plug-ins
implementing IRCrypt.  Furthermore, only the `<text>` part of these messages may
be modified. 


1.1 Symmetric Ciphers
---------------------

The `<text>` part of an encyrpted message has the form:

    >CRY-<PART-ID> <CRYPT-MSG>


### `<PART-ID>`

`<PART-ID>` specifies the identifier of the message part. This is intended for
multipart messages and is a continuous descending integer value with a value of
“0” indicating the last part of a message.

This means that for short messages, you can simply ignore this identifier and
just start the message with “>CRY-0 ” which tells your communication partner
that he can directly decrypt and display the message.

It may however be, that an already long message grows to large to send at once
via IRC after encryption, as one message may not exceed 512 characters
(including IRC protocol command identifier, trailing \CR\LF, etc.) as specified
in [rfc1459, sec.2.3]. In such a case it is necessary to split the encrypted
messages in multiple parts, sending them as separate messages. Given that the
message has to be split in N parts the `<PART-ID>` of the first part to send is
N, the second is N-1, … until the last part is send with `<PART-ID>` set to 0.

The descending order of the part ID ensures that:

 - The client knows how many parts will be send, making it possible to
   effectively allocate memory or, if the number of parts is to high for the
   client to handle, to refuse the messages.

 - The client can indicate and may throw away “old” message parts which were
   never completely transmitted, i.e. due to a failing connection. If, for
   example, a client receives messages preceded by “>CRY-2” and “>CRY-1” but
   the next message is again preceded by “>CRY-1”, the client knows that
   something is not right, may throw away the old message parts and try
   decoding the current message only.


### `<CRYPT-MSG>`

`<CRYPT-MSG>` is a message encrypted according to the OpenPGP standard, Base64
encoded and cut into multiple parts (see `<PART-ID>`) if necessary. The used
cipher may be everything allowed by OpenPGP, nevertheless, it is strongly
suggested to use modern and secure ciphers like AES256 or TWOFISH.

Using GPG and the Unix base64 tool such a message can be generated using the
following command:

    echo 'Message' | gpg --symmetric --cipher-algo TWOFISH | base64 -w 0


### TIMEOUT

As using `<PART-ID>` greater than 0 should make a client keep these message
parts in memory while waiting for subsequent parts, this could be used as a
possible attack on clients: Sending such messages would cause a client to
constantly allocate new memory. However, subsequent message parts should be
send one after another over a short period of time. Thus is is not only valid
but recommended to discard old message parts after some time, if no subsequent
parts are being received.

Given the nature of IRC as “instant” chat protocol, consecutive messages should
not be delayed very long and it should be reasonable to assume a message to
time out after five minutes.


### Example message

The following line contains a valid IRC mMessage from Angel to Wiz. It is
encrypted using the TWOFISH cipher with 256bits key size and “secret” as
passphrase. The decrypted contents of this message is “Hello are you receiving
this message ?”:

    :Angel PRIVMSG Wiz :>CRY-0 jA0ECgMCpf88FdB5AdFg0lwB03DpHgpQAqoGSR2QTIynudCXM178TN2Y06ahv+I1i/mLwDMt+s021cb14YdVWJXUVqBKTbpQ3B3aIthsxsb0qrQoUTdZTKHjGYXeYPCFoRaetkOiEPUcAWK9RA==

Assuming that this message would be to long, the following two IRC messages
should produce the same output in Wizs IRC client:

    :Angel PRIVMSG Wiz :>CRY-1 jA0ECgMCpf88FdB5AdFg0lwB03DpHgpQAqoGSR2QTIynudCXM178TN2Y06ahv+I1i/mLwDMt+s02
    :Angel PRIVMSG Wiz :>CRY-0 1cb14YdVWJXUVqBKTbpQ3B3aIthsxsb0qrQoUTdZTKHjGYXeYPCFoRaetkOiEPUcAWK9RA==
