---
template: post
slug: how-to-encrypt-strings-in-nodejs
draft: false
socialImage: /media/image-2.jpg
title: How to encrypt strings in nodejs
date: '2019-06-03T23:46:37.121Z'
description: Two ways to encrypt strings in nodeJs
category: Encryption
tags:
  - encryption
  - security
---

In my projects I essentially find useful two ways to encrypt strings: **hash functions** one-way and one-way and **encryption-decryption** two-way :

## 1. Hash functions with Bcrypt

Hash functions are essentials for store encrypted password, and the best library for nodejs is **Bcrypt**. You can find more information in this article: [why use Bcrypt?](https://codahale.com/how-to-safely-store-a-password/).

Install:

    npm install bcrypt

To hash a password:

    const bcrypt = require('bcrypt');
    const saltRounds = 10;
    const myPlaintextPassword = 'myPassword';
    
    bcrypt.hash(myPlaintextPassword, saltRounds).then(function(hash) {
    	// Store hash in your password DB.
    });

At user login to compare password with the one stored in the db you can use:

    bcrypt.compare(plaintextPassToCheck, hashStoredInDB).then(function(res) {
      // res == true/false
    });

More info: [github.com/kelektiv/node.bcrypt.js](https://github.com/kelektiv/node.bcrypt.js)

## 2. Simple Encryption and Decryption

In other scenarios I needed to crypt strings in order to hide texts  to users but in a way that allows me to decrypt and retrieve the original content. In this case a fast tool is **Crypto**.

Install:

    npm install crypto

To encrypt and decrypt a string:

    var crypto = require('crypto');
    
    var cypherKey = "mySecretKey";
    
    function encrypt(text){
      var cipher = crypto.createCipher('aes-256-cbc', cypherKey)
      var crypted = cipher.update(text,'utf8','hex')
      crypted += cipher.final('hex');
      return crypted; //94grt976c099df25794bf9ccb85bea72
    }
    
    function decrypt(text){
      var decipher = crypto.createDecipher('aes-256-cbc',cypherKey)
      var dec = decipher.update(text,'hex','utf8')
      dec += decipher.final('utf8');
      return dec; //myPlainText
    }

More info: [nodejs.org/api/crypto](https://nodejs.org/api/crypto.html)
