---
layout: post
title: Conversion Cheat Sheet
nav_order: 1
parent: OpenSSL
published: true
date: 12/11/2020
permalink: /_docs/OpenSSL/Conversions
---
<br>
PFX to PEM
{: .fs-6}

## Combined CACerts
{: .fs-5}
<br>
  Export Certificate    
  {% capture code %}openssl pkcs12 -in certname.pfx -nokeys -out cert.pem{% endcapture %}
  {% include code.html code=code lang="" %}

  Export Key
  {% capture code %}openssl pkcs12 -in cert.pfx -nocerts -out cert.key -nodes{% endcapture %}
  {% include code.html code=code lang="" %}
<br>

## Seperate CACerts, Certificate, and Key files  
{: .fs-5}
<br>
Export CA
{% capture code %}openssl pkcs12 -in cert.pfx -cacerts -nokeys -chain -out CACerts.pem{% endcapture %}
{% include code.html code=code lang="" %}

Export Certificate
{% capture code %}openssl pkcs12 -in certname.pfx -nokeys -out cert.pem{% endcapture %}
{% include code.html code=code lang="" %}

Export Key
{% capture code %}openssl pkcs12 -in cert.pfx -nocerts -out cert.key -nodes{% endcapture %}
{% include code.html code=code lang="" %}
<br>

## Remove Password from Key  
{: .fs-5}
<br>
{% capture code %}openssl rsa -in cert.key -out certnopw.key{% endcapture %}
{% include code.html code=code lang="" %}
<br>