---
layout: post
title: Conversion Cheat Sheet
nav_order: 1
parent: OpenSSL
date: 11/09/2020
permalink: /_docs/OpenSSL/Conversions
---
### PFX to PEM

#### Combined CACerts

  Export Certificate
  ```
  openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
  ```
  Export Key
  ```
  openssl pkcs12 -in cert.pfx -nocerts -out cert.key -nodes
  ```
  
### Seperate CACerts, Certificate, and Key files

#### Remove Password from Key

```
openssl rsa -in cert.key -out certnopw.key 
```

#### Validate Certificates
