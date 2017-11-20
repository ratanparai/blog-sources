---
layout: single
title: SSL certificate for Intranet network
excerpt: SSL (read HTTPS) encrypted internal website for security is must for banking solution. This is how I solved the problem. 
date: 2017-08-18 12:44:00 +0600
tags: 
    - https
    - intranet-ssl
    - ssl
    - openssl
toc: true
---
## Setup OpenSSL
1. Download and install OpenSSL from [here](https://slproweb.com/products/Win32OpenSSL.html). For our current task **light** version is more than enough. I have downloaded [this](https://slproweb.com/download/Win64OpenSSL_Light-1_1_0f.exe) one
2. Add `C:\OpenSSL-Win64\bin` to your environment variable `PATH`
3. If you face **no configuration error** when running OpenSSL, then you need to add a new **Environment variable**: _**Variable Name**_ - `OPENSSL_CONF` and _**Variable Value**_ - `C:\OpenSSL-Win64\bin\openssl.cfg`

# Generate self signed root CA 
### Generate Root CA Key
Open `cmd` and `cd` to the directory you want to save the certificates _**or**_ from the **folder** `SHITF`+`RMB` and select `Open Powershell Windows here`. then type - 

```bash
openssl genrsa -des3 -out myrootca.key 2048
``` 
and press `ENTER`. Type a new **Password** to protect the key file

### Request for certificate
Then create a certificate request using the root CA key file
```bash
openssl req -new -key myrootca.key -out myrootca.req
```
When asked enter the **Certificate Authority** information that will be shown as **Authority** that verified the issued certificate.

### Self signed the requested certificate
To self sign the request certificate run -
```bash
openssl x509 -req -days 7305 -extensions v3_ca -signkey myrootca.key -in myrootca.req -out myrootca.crt
```
you need to install the `.crt` file to all of the **computer** that you want to use varify your issued certificates. When importing `.crt` certificate make sure you select `Place all certificates in the following store` and browse to `Trusted root certification authorities`

## Issue Certificate as a CA
We have created our own Certificate Authority in the previous step. Now its time to issue certificate. 

### Generate Server Key
At first we need to create server key.
```bash
openssl genrsa -out myhost.key 2048
```
### Request for certificate
Fill the information for the Server. When asked for `CA`, give your web server's `IP address` or `domain` name 
```bash
openssl req -new -key myhost.key -out myhost.req
```
### Issue the Certificate
Create a new file and name it `v3.ext` in the working directory with the contents. Change the `[alt_names]` portion as needed.
```ext
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = localhost
IP.2 = 192.168.10.240
```
after making required changes to the `v3.ext` file run the command bellow in `cmd`

```bash
openssl x509 -req -days 3650 -CA myrootca.crt -CAkey myrootca.key -CAcreateserial -sha256 -extfile v3.ext -out myhost.crt -in myhost.req
```

## Generate `.pfx` file for `IIS` Server
To use the server certificate with `IIS` server we need `.pfx` file. To generate `.pfx` file we need to run-
```
openssl pkcs12 -export -out myhost.pfx -inkey myhost.key -in myhost.crt
```



### *Verify Certificate Chain
You can verify certificate chain in `Windows` for debugging purpose by running
```
certutil -f -urlfetch -verify myhost.crt
```
Where `myhost.crt` is the server certificate
