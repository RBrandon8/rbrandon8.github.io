---
layout: post
title: Validating Certificates
nav_order: 2
parent: OpenSSL
published: true
date: 11/11/2020
permalink: /_docs/OpenSSL/Validation
---
<br>

## Verify a Self Signed Certificate
{: .fs-5}
{% capture code %}openssl verify -CAfile CACert.pem -untrusted intermediare.pem cert.pem{% endcapture %}
{% include code.html code=code lang="bash" %}
<br>

## Verify Key and Certificate Match
{: .fs-5}
{% capture code %}openssl x509 -noout -modulus -in cert.pem | openssl md5
openssl rsa -noout -modulus -in cert.key | openssl md5{% endcapture %}
{% include code.html code=code lang="bash" %}


<br>

## Verify Certificate Expiration Date
{: .fs-5}
{% capture code %}openssl x509 -startdate -enddate -noout -in cert.pem{% endcapture %}
{% include code.html code=code lang="bash" %}
<br>