---
layout: post
title: Management Powershell Commands
nav_order: 1
parent: Exchange
published: true
date: 13/11/2020
permalink: /_docs/Exchange/Powershell.md
---

<br>
{: .fs-6}

## Remote Connections
{: .fs-5}
<br>
  Connect to On Prem Exchange
  {% capture code %}$UserCredential = Get-Credential
$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://stp-exch1.stpetes.org/PowerShell/ -Authentication Kerberos
Import-PSSession $Session -DisableNameChecking{% endcapture %}
  {% include code.html code=code lang="powershell" %}
