---
layout: post
title: Conversion Cheat Sheet
nav_order: 1
parent: OpenSSL
published: true
date: 11/11/2020
permalink: /_docs/OpenSSL/Conversions
---
<br>
PFX to PEM
{: .fs-6}

## Combined CACerts
{: .fs-5}
<br>
  Export Certificate  
  
  ```
  openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
  ```

  Export Key
  
  ```
  openssl pkcs12 -in cert.pfx -nocerts -out cert.key -nodes
  ```
<br>

## Seperate CACerts, Certificate, and Key files  
{: .fs-5}
<br>
Export CA
```
openssl pkcs12 -in cert.pfx -cacerts -nokeys -chain -out CACerts.pem
```

Export Certificate
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```  

Export Key

```
openssl pkcs12 -in cert.pfx -nocerts -out cert.key -nodes
```
<br>

## Remove Password from Key  
{: .fs-5}
<br>
```
openssl rsa -in cert.key -out certnopw.key
```
<br>