---
template: post
title: Asymmetric encryption in Nodejs
slug: how-to-asymmetric-encryption-in-nodejs
draft: true
date: 2020-04-29T08:37:49.057Z
description: >-
  How to generate public and private key, and how to encrypt e decrypt using
  this keys
category: NodeJs
tags:
  - encryption
---
## How asymmetric encryption works?

In an asymmetric key encryption scheme, anyone can encrypt messages using the public key, but only the holder of the paired private key can decrypt. Security depends on the secrecy of the private key.

![](/media/asymmetric-encryption.png)

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
* To encrypt and decrypt in **nodejs**:

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

  const enc = encrypt('hello', `public.pem`)
  console.log('enc', enc)

  const dec = decrypt(enc, `private.pem`)
  console.log('dec', dec)
  ```
* To encrypt public key in **javascript**

  ```javascript
  var crypt = new JSEncrypt();
  //You can also use setPrivateKey and setPublicKey, they are both alias to setKey
  crypt.setKey(__YOUR_OPENSSL_PRIVATE_OR_PUBLIC_KEY__); 

  var text = 'test';
  var enc = crypt.encrypt(text);
  ```
* Alternative: to **generate** private and public key in nodejs:

  ```javascript
  const { writeFileSync } = require('fs')
  const { generateKeyPairSync } = require('crypto')

  function generateKeys() {
    const { privateKey, publicKey } = generateKeyPairSync('rsa', {
      modulusLength: 4096,
      publicKeyEncoding: {
        type: 'pkcs1',
        format: 'pem',
      },
      privateKeyEncoding: {
        type: 'pkcs1',
        format: 'pem',
        cipher: 'aes-256-cbc',
        passphrase: '',
      },
    })

    writeFileSync('private.pem', privateKey)
    writeFileSync('public.pem', publicKey)}
  ```
* references::

  * [Asymmetric Encryption using Nodejs Crypto module](https://stackoverflow.com/questions/54087514/asymmetric-encryption-using-nodejs-crypto-module)
  * [https://github.com/travist/jsencrypt](https://github.com/travist/jsencrypt "https\://github.com/travist/jsencrypt")