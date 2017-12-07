# Hybrid Crypto JS

## Introduction
<a name="introduction" />

*Hybrid Crypto JS* is a hybrid (RSA+AES) encryption and decryption toolkit for JavaScript, including automatic and persistent key management on React Native. *Hybrid Crypto JS* combines RSA and AES encryption algorithms making it possible to efficiently encrypt and decrypt large messages.

## Documentation
<a name="documentation" />

**Getting started**
- [Introduction](#introduction)
- [Documentation](#documentation)
- [Installation](#installation)

**Features**
- [Encryption](#encryption)
- [Decryption](#decryption)
- [Signatures](#signatures)
- [Verifying](#verifying)
- [RSA keypairs](#rsa-keypairs)
- [React Native key management](#rn-key-management)

### Installation
<a name="installation" />

*Hybrid Crypto JS* isn't released yet, stay tuned!

## Features

### Encryption
<a name="encryption" />

*Hybrid Crypto JS* provides basic encryption function which supports also multiple RSA keys, with or without [signature](#signatures). Encrypted message is outputted as a JSON string.
```js
var message = 'Hello world!';

// Encryption with one public RSA key
var encrypted = crypto.encrypt(publicKey, message);

// Function also supports encryption with multiple RSA public keys
var encrypted = crypto.encrypt([publicKey1, publicKey2, publicKey3], message);

// Encryption with signature
var encrypted = crypto.encrypt(publicKey, message, signature);
```

**Pretty-printed sample output**
```js
{
    "v": "hybrid-crypto-js_0.1.0",        // Current package version
    "iv": "CmtyaZTyzoAp1mTNUTztic0v1...", // Initialization vector
    "keys": {                             // Encrypted AES keys by RSA fingerprints
        "85:3d:10:e1:56...": "bHaTF9...",
        "d3:48:6a:e9:13...": "t9eds3..."
    },
    "cipher": "+iwVFsC2dECBQvwcm9DND..."  // Actual encrypted message
    "signature": "sdL93kfdm12feds3C2..."  // Signature (optional)
}

```

### Decryption
<a name="decryption" />

Decrypting message with *Hybrid Crypto JS* is as easy as encrypting. Decryption function can decrypt any message which has been encrypted with keypair's public key. Decrypted message is outputted as a JSON object.
```js

var encrypted = '{"v":"hybrid-crypto-js_0.1.0","iv":"CmtyaZTyzoAp1mTN...';

// Decrypt encryped message with private RSA key
var decrypted = crypto.decrypt(privateKey, encrypted);

// Get decrypted message
var message = decrypted.message;
```
**Sample output**
```js
{
    message: "Hello world!",            // Actual decrypted message
    signature: "sdL93kfdm12feds3C2..."  // Signature (optional)
}
```

### Signatures
<a name="signatures" />

*Hybrid Crypto JS* provides simple message signing. When issuer signs a message, message receiver can be sure of the message issuer.

```js
var message = 'Hello world!';

// Create a signature with ISSUER's private RSA key
var signature = crypto.signature(issuerPrivateKey, message);

// Encrypt message with RECEIVERS public RSA key and attach the signature
var encrypted = crypto.encrypt(receiverPublicKey, message, signature);
```

### Verifying
<a name="verifying" />

Message receiver needs to have message issuer's public RSA key in order to verify message issuer.

```js
// Encrypted message with signature
var encrypted = '{"v":"hybri... ..."signature":"sdL93kfd...';

// Decrypt message with own (RECEIVER) private key
var decrypted = crypto.decrypt(receiverPrivateKey, encrypted);

// Verify message with ISSUER's public key
var verified = crypto.verify(issuerPublicKey, decrypted);
```
Verification function return *true* or *false* depending on whether the verification was successfull.

### RSA keypairs
<a name="rsa-keypairs" />

*In progress*

### React Native key management
<a name="rn-key-management" />

*In progress*
