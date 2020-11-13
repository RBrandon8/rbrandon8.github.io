---
layout: post
title: Management Powershell Commands
nav_order: 1
parent: Exchange
published: false
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
  $Server = <exch_server_name>
$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "$server/PowerShell/" -Authentication Kerberos
Import-PSSession $Session -DisableNameChecking{% endcapture %}
  {% include code.html code=code lang="" %}
  
  Remove OWA Profile Picture User Access
{% capture code %}Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -SetPhotoEnabled $False
Get-CASMailbox -ResultSize Unlimited | Set-CASMailbox -OWAMailboxPolicy Default{% endcapture %}
{% include code.html code=code lang="" %}

Delete Profile Photo
{% capture code %}Remove-UserPhoto -Identity <user>{% endcapture %}
{% include code.html code=code lang="" %}
