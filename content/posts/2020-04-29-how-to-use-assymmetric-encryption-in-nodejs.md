---
template: post
title: Asymmetric encryption in Nodejs
slug: how-to-asymmetric-encryption-in-nodejs
draft: false
date: 2020-05-04T18:00:00.000Z
description: >-
  How to generate public and private key, and how to encrypt e decrypt using
  this keys
category: NodeJs
tags:
  - encryption
---
## How asymmetric encryption works?

In an asymmetric key encryption scheme, anyone can encrypt messages using the public key, but only the holder of the paired private key can decrypt. Security depends on the secrecy of the private key.

![asymmetric key cryptography](/media/asymmetric-encryption.png "asymmetric key cryptography")

## Generate private and public key

To **generate** private and public key we will use **openssl**:

* Within your terminal (Unix based OS) type the following to generate a **private key**:

  ```shell
  openssl genrsa -out rsa_4096_priv.pem 4096
  ```
* You can see it:

  ```shell
  cat rsa_4096_priv.pem
  ```
* Next, you can generate the **public key** by executing the following command:

  ```shell
  openssl rsa -pubout -in rsa_4096_priv.pem -out rsa_4096_pub.pem
  ```
* You can see it:

  ```shell
  cat rsa_4096_pub.pem
  ```

## How to use the keys in nodejs e javascript

To encrypt and decrypt in **nodejs** we can use [crypto](https://www.npmjs.com/package/crypto-js):

* Run: `npm install crypto-js` to install it, and you can use these following functions to encrypt and decrypt:

  ```javascript
  const crypto = require('crypto')
  const path = require('path')
  const fs = require('fs')

  function encrypt(toEncrypt, relativeOrAbsolutePathToPublicKey) {
    const absolutePath = path.resolve(relativeOrAbsolutePathToPublicKey)
    const publicKey = fs.readFileSync(absolutePath, 'utf8')
    const buffer = Buffer.from(toEncrypt, 'utf8')
    const encrypted = crypto.publicEncrypt(publicKey, buffer)
    return encrypted.toString('base64')}

  function decrypt(toDecrypt, relativeOrAbsolutePathtoPrivateKey) {
    const absolutePath = path.resolve(relativeOrAbsolutePathtoPrivateKey)
    const privateKey = fs.readFileSync(absolutePath, 'utf8')
    const buffer = Buffer.from(toDecrypt, 'base64')
    const decrypted = crypto.privateDecrypt(
      {
        key: privateKey.toString(),
        passphrase: '',
      },
      buffer,
    )
    return decrypted.toString('utf8')}

  const enc = encrypt('hello', `<public.pem>`)
  console.log('enc', enc)

  const dec = decrypt(enc, `<private.pem>`)
  console.log('dec', dec)
  ```
* Now you can distribute the public key and use it also in client side. 

  In **javascript** you can use [**JSEncrypt** ](https://www.npmjs.com/package/jsencrypt)library:

  ```javascript
  var crypt = new JSEncrypt();
  //You can also use setPrivateKey and setPublicKey, they are both alias to setKey
  crypt.setKey(__YOUR_OPENSSL_PRIVATE_OR_PUBLIC_KEY__); 

  var text = 'test';
  var enc = crypt.encrypt(text);
  ```
* references:

  * [Asymmetric Encryption using Nodejs Crypto module](https://stackoverflow.com/questions/54087514/asymmetric-encryption-using-nodejs-crypto-module)