---
title: Self-signed certificate with SAN during COVID-19
date: 2020-04-29 11:12:34
tags : [Apache, Server, Client]
categories:
 - [SSL, HTTPs]
cover: https://surleboutdesdoigts.me/img/https_SSL_cover.png
---

Recently, I have been working with Angular 9. I implemented an app shell for a project of mine. And, well, I needed my app to be secured in order to use Push notifications with service workers.

So, I created a self signed certificate, using a simple command. I answered the questions the system asked me.
And my certificate got generated. But, it was not working on chrome because of the Common Name is not used anymore. I tried on firefox and it was.

So after some little research on the internet, I found some answers and decided to put everything here for anyone who would be needed to do this.

This article as been written for any kind of people, so if you have never did this before do no worry. Stay right here!
Everything is explained in the article.

# Pre-requisite

First things, first! Make sure you have **OpenSSL installed** on your machine. If you are on a unix machine (MACOSX, Linux), it is already installed on you machine. If you are on Windows 7 or 10, you can use Cmdlet [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate?redirectedfrom=MSDN&view=win10-ps) on powershell. You can also use **OpenSSL** with git-bash command line by installing git.

# Create a self-signed certificate with SAN

Ok, so. We are going to create a configuration file to be used for the private key and the CSR.

```
[ req ]
default_bits         = 2048
distinguished_name   = req_distinguished_name
req_extensions       = req_ext
[ req_distinguished_name ]
countryName          = Country Name (2 letter code)
stateOrProvinceName  = State or Province Name (full name)
localityName         = Locality Name (eg, city)
organizationName     = Organization Name (eg, company)
commonName           = Common Name (e.g. server FQDN or YOUR name)
[ req_ext ]
subjectAltName = @alt_names
[alt_names]
DNS.1   = <PUT YOUR DOMAIN HERE>
DNS.2   = <PUT YOUR DOMAIN HERE>
DNS.3   = <PUT YOUR DOMAIN HERE>
```

Replace the domain where it is needed. If there is more than 3 domains, you can add them following the same pattern. Of course you can remove them if there is too much.

Note: Theorically, there is no limit to the number of alternative domains you can put in this configuration file. But added more domain will increase the size of the certificate, hence once sending to a website's visitor's session will end up with some performance issues.

Save the file under whatever name you want. I will save mine under the name `SSL_SAN.config`.

Now, we can generate the CSR and the private key with this command line.
```
openssl req -out sslcert.csr -newkey rsa:2048 -nodes -keyout private.key -config SSL_SAN.cnf
```

This will create 2 files:
 - `sslcert.csr` which is your Certificate Signing Request
 - `private.key` which is your private key ( do not share this key)

Finally to create your public certificate, the one you have to share with everybody. Execute this command :
```
openssl x509 -signkey private.key -in sslcert.csr -req -days 365 -out cert.crt
```

This will create 1 file:
 - `cert.crt` which is the certificate
 - It will be valid for 365 days

Done! You have your certificate ready to use.

# Knowledge


## What is a Certificate Signing Request?

In order to obtain an SSL certificate from a certificate authority (CA), you must generate a certificate signing request (CSR). A CSR consists mainly of the public key of a key pair, and some additional information. Both of these components are inserted into the certificate when it is signed.

## NET::ERR_CERT_COMMON_NAME_INVALID on Google Chrome

From [Google Chrome Entreprise Help](https://support.google.com/chrome/a/answer/9813310?hl=en&visit_id=637237802054649601-806617213&rd=1)
```
Known issue
During Transport Layer Security (TLS) connections, Chrome browser checks to make sure the connection to the site is using a valid, trusted server certificate.

For Chrome 58 and later, only the subjectAlternativeName extension, not commonName, is used to match the domain name and site certificate. The certificate subject alternative name can be a domain name or IP address. If the certificate doesn’t have the correct subjectAlternativeName extension, users get a NET::ERR_CERT_COMMON_NAME_INVALID error letting them know that the connection isn’t private. If the certificate is missing a subjectAlternativeName extension, users see a warning in the Security panel in Chrome DevTools that lets them know the subject alternative name is missing.

Workaround
Some public key infrastructures (PKIs), legacy systems, and older versions of network monitoring software use certificates without subjectAlternativeName extensions. If you’re having issues with any of these, contact the software vendor or administrator and ask them to generate a new certificate.

For Microsoft® Windows®, you can use the PowerShell Cmdlet New-SelfSignedCertificate and specify the DnsName parameter.

For OpenSSL, you can use the subjectAltName extension to specify the subject alternative name.

If needed, until Chrome 65, you can set the EnableCommonNameFallbackForLocalAnchors policy. This lets Chrome use the commonName of a certificate to match a hostname if the certificate is missing a subjectAlternativeName extension.
```



Thank you for reading. I hope it helped you.
For more information on OpenSSL, you can go on [OpenSSL Essentials: Working with SSL Certificates, Private Keys and CSRs](https://www.digitalocean.com/community/tutorials/openssl-essentials-working-with-ssl-certificates-private-keys-and-csrs) which a really good article written by Mitchell Anicas.
This is my preferred reference when I need to refresh my memory on some useful commands.
