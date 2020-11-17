---
layout: post
title: Management Powershell Commands
nav_order: 1
parent: F5
published: true
date: 11/11/2020
permalink: /_docs/F5/Powershell.md
---

<br>
{: .fs-6}

## Remote Connections
{: .fs-5}
<br>

Connect to On Prem Exchange

{% capture code %}{% raw %}$UserCredential = Get-Credential
$Server = <exch_server_name>
$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "$server/PowerShell/" -Authentication Kerberos
Import-PSSession $Session -DisableNameChecking{% endraw %}{% endcapture %}
{% include code.html code=code lang="powershell" %}