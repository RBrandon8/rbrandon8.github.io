---
layout: post
title: PowerShell Commands
nav_order: 2
parent: Exchange
published: true
permalink: /_docs/Exchange/Powershell
---
## Remote Connections
{: .fs-5}

---
Connect to On Prem Exchange

{% capture code %}$UserCredential = Get-Credential
$Server = <exch_server_name>
$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "$server/PowerShell/" -Authentication Kerberos
Import-PSSession $Session -DisableNameChecking{% endcapture %}
{% include code.html code=code lang="powershell" %}

<br>
