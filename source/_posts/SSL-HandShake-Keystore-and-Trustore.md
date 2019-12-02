---
title: SSL HandShake & Keystore and Trustore
date: 2019-11-30 23:20:06
tags: [SSL,Server,Client]
categories:
- [SSL,HTTPs]
date: 2019-10-24 22:45:42
cover: https://surleboutdesdoigts.me/img/https_SSL_cover.png
---

Have you ever hear two developers arguing about the difference between a Java keystore and a Trustore ? Do you know how both are used in a during an communication over SSL/TLS. Maybe SSL handshake rings a bell ?

In this article, I will explain first the differences between a Java Keystore and a Trustore. Then I will describe the SSL Handshake and tell you how the keystore and the truststore are used.

# Basic knowledge

A *private* key can *sign or decrypt data*.

A *public* key can *verify or encrypt data*.

A *certifcate* holds a *public key* and information about the owner 
of the public key.

A *Certifcate Authority* is an entity that issues digital certificates.
It verifies the identity of another entity and encrypts it with its 
private key.

# Java Keystore and a TrustStore definitions.

## Java KeyStore

A java keystore stores private keys, certificates with public keys or just secret keys. Those may be used for cryptographic purposes, server identity authentication, etc .
In a Java keystore, the entries are referenced by an alias for ease lookup.
If your java Keystore is from a server and you want to communicate over SSL/TLS (HTTPS) then a keystore containing the private key of the server will be used during an SSL Handshake.
By convention, your Java keystore must contain what identifies you. 

## TrustStore

A trustStore holds onto certicates that identify others. It will contains certicates of trusted servers we would communicate with. This ensure that we communicate with the correct server.

Example, a client would use his trustStore to found if there is a match between the server's public key and the Certificate chain from the the server. If there is no match then an SSLHandShakeException will happen and the connection will not be set up.

By default, Java comes with a trustore called cacerts which resides at $JAVA_HOME/jre/lib/security directory. It contains default trusted Certificate Authorities.
This default truststore can be overriden.

# SSL HandShake explained

SSL Handshake's purpose is to provide privacy and data integrity for communication between a server and a client. During the handshake, a client and a server will exchange everything that is necessary to ensure a secured connection takes place.

Notice on your browser the small lock on the left side of the url address bar and also notice that the url starts with *https*.
When you opened a tab to browse this website the server hosting it created an HTTPS connection using one-way SSL Handshake.

Another example would be for two servers using what is called a two-way way SSL Handshake to establish a secure HTTP connection.

Next sections will describe these handshakes.

## One-way SSL HandShake

![My Handshake SSL Diagram](https://surleboutdesdoigts.me/img/SSL Handshake diagram.png "My SSL Handshake diagram")

> T ( green in the circle ) represents the TrustStore
> K ( blue in the circle ) represents the KeyStore

This diagram is not completely true. The exchange of the public key is done via a trusted third party. The trusted third-party (CA) will incorporate it into a digital certificate.This third party is called a Certificate Authority (CA).

## Two-way SSL HandShake

The two-way SSL HandShake is very similar to the one-way SSL HandShake, only one step is missing. The server request for client authentication. It will use the client certificate chain and compare it to the certificate it holds in its Truststore to authenticate the client.