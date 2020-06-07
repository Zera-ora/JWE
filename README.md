<!--<div style="margin: 10px 0; padding: 6px; border: 2px solid #7777ff; border-radius: 10px; background: #eeeeff">
  <div style="margin: -3px 10px -3px -3px; padding: 5px 20px; background: #7777ff; border-radius: 7px; color: #ffffff; display: inline-block; font-weight: bold;">✔ Tip</div>Placeholder text
</div>
<div style="margin: 10px 0; padding: 6px; border: 2px solid #ff7777; border-radius: 10px; background: #ffeeee">
  <div style="margin: -3px 10px -3px -3px; padding: 5px 20px; background: #ff7777; border-radius: 7px; color: #ffffff; display: inline-block; font-weight: bold;">💀 Danger</div>Placeholder text
</div>
<div style="margin: 10px 0; padding: 6px; border: 2px solid #dfdf77; border-radius: 10px; background: #ffffee">
  <div style="margin: -3px 10px -3px -3px; padding: 5px 20px; background: #dfdf77; border-radius: 7px; color: #ffffff; display: inline-block; font-weight: bold;">⚠ Warning</div>Placeholder text
</div>-->

# JWE specification

> This specification is an adaptation of the formal standard [RFC 7516: JSON Web Encryption (JWE)](https://tools.ietf.org/html/rfc7516).


## Table of Contents

 1. [Introduction](#introduction)
 2. [Notational Conventions](#notational-conventions)
 3. [Terminology](#terminology)
 4. [Overview](#overview)
 5. [JWE Compact Serialization Overview](#jwe-compact-serialization-overview)
 6. [JWE JSON Serialization Overview](#jwe-json-serialization-overview)



### Introduction

JSON Web Encryption represents content using JSON<sup>[[RFC 7159]](https://tools.ietf.org/html/rfc7159)</sup> and provides encryption and integrity protection.

### Notational Conventions

Key words<sup>[[RFC 2119]](https://tools.ietf.org/html/rfc2119)</sup> appear fully capitalized. An explanation of each key word is given below:

 - **MUST** - Is an absolute requirement.
 - **MUST NOT** - Is an absolute prohibition.
 - **SHOULD** - Recommended but not required.
 - **SHOULD NOT** - Not recommended but is allowed.
 - **MAY** - optional.
 - **`BASE64URL(OCTETS)`** - The base64url encoding of a series of octets.
 - **`UTF8(STRING)`** - The octets of a UTF-8<sup>[[RFC 3629]](https://tools.ietf.org/html/rfc3629)</sup> encoded string consisting of unicode characters.
 - **`ASCII(STRING)`** - The octets of an ASCII<sup>[[RFC 20]](https://tools.ietf.org/html/rfc20)</sup> encoded string consisting of ASCII characters.

The concatenation of two values is denoted by `||`.

### Terminology

For a full list of terms, please read [Section 2 of RFC 7516](https://tools.ietf.org/html/rfc7516#section-2).

<!--
 - **JSON Web Signature (JWS)** - A data structure representing a digitally signed or MACed message.
 - **Base64url encoding** - Base64 encoding using the URL safe character set<sup>[[Section 5 of RFC 4648]](https://tools.ietf.org/html/rfc4648#section-5)</sup>.
 - **Collision-resistant name** - A name in a namespace that allows names to be allocated in a manner such that they are highly unlikely to collide with other names.
 - **Header parameter** - A name/value pair in the JOSE header.
 - **JOSE header** - JSON object containing the parameters describing the cryptographic options and parameters used.
 - **StringOrURI** - A JSON string value with any characters. Any value containing a `:` must be a URI.
 - **Ciphertext** - 
 - **Digital signature** - 
 - **Initialization Vector (IV)** - 
 - **Message Authentication Code (MAC)** - 
 - **Plaintext** - 
 - **JSON Web Encryption** - A data structure representing an encrypted and integrity-protected message.
 - **
-->

### Overview

A JWE represents encrypted content using base64url encoded JSON. A JWE is composed of the following:

 - JOSE header.
 - JWE encrypted key.
 - JWE initialization vector.
 - JWE AAD.
 - JWE ciphertext.
 - JWE authentication tag.

A JOSE header is composed of the following:

 - JWE protected header.
 - JWE shared unprotected header.
 - JWE per-recipient unprotected header.

There are two serializations fo JWEs: JWE Compact Serialization and JWE JSON Serialization.

### JWE Compact Serialization Overview

No JWE shared unprotected header or JWE per-recipient unprotected header is used. The JOSE header is the JWE protected header.

The JWE is represented as the following concatenation (line breaks for display purposes):

```
BASE64URL(UTF8(JWE protected header)) || . ||
BASE64URL(JWE encrypted key) || . ||
BASE64URL(JWE initialization vector) || . ||
BASE64URL(JWE ciphertext) || . ||
BASE64URL(JWE authentication tag)
```

<!-- add link to later part -->

### JWE JSON Serialization Overview

One or more of the possible JOSE header parameters **MUST** be present. The JOSE header is the union of these parameters.

The JWE includes some or all of the following parameters:

```
"protected": BASE64URL(UTF8(JWE protected header)),
"unprotected": JWE shared unprotected header,
"header": JWE per-recipient unprotected header,
"encrypted_key": BASE64URL(JWE encrypted key),
"iv": BASE64URL(JWE initialization vector),
"ciphertext": BASE64URL(JWE ciphertext),
"tag": BASE64URL(JWE authentication tag),
"aad": BASE64URL(JWE AAD)
```

The JWE JSON Serialization can encrypt the plaintext to multiple recipients.

<!-- add link to later part -->