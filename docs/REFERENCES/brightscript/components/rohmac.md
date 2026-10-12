---
title: "roHMAC"
excerpt: 'Interface to HMAC functions for generating a Message Authentication Code'
deprecated: false
hidden: false
metadata:
  title: 'roHMAC'
  description: 'The roHMAC component provides an interface to HMAC functions, generating a Message Authentication Code based on a key using a digest algorithm.'
  robots: index
next:
  description: ''
---


The HMAC component provides an interface to HMAC functions. These functions generate a Message Authentication Code (MAC) based on a key, in such a way that no one without the key could plausibly generate the MAC. HMAC uses a digest (hash) algorithm to generate the MAC.

**Supported Digest Algorithms**

The supported digest algorithms are the same as those supported by [roEVPDigest](doc:roevpdigest).

**Example**

```brightscript
hmac = CreateObject("roHMAC")
signature_key = CreateObject("roByteArray")
signature_key.fromAsciiString(getKey())
if hmac.setup("sha1", signature_key) = 0
    message = CreateObject("roByteArray")
    message.fromAsciiString(getMessage())
    result = hmac.process(message)
    print result.toBase64String()
end if


hmac = CreateObject("roHMAC")
signature_key = CreateObject("roByteArray")
signature_key.fromAsciiString(getKey())
if hmac.setup("sha1", signature_key) = 0
    message1 = CreateObject("roByteArray")
    message1.fromAsciiString(getMessage1())
    hmac.update(message1)
    message2 = CreateObject("roByteArray")
    message2.fromAsciiString(getMessage2())
    hmac.update(message2)
    result = hmac.final()
    print result.toBase64String()
end if
```


## Supported interfaces

- [ifHMAC](doc:ifhmac)