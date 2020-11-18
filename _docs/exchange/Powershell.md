---
layout: post
title: PowerShell Commands
nav_order: 2
parent: Exchange
published: true
date: 17/11/2020
permalink: /_docs/Exchange/Powershell
---
## Remote Connections
{: .fs-5}

---
#### Connect to On Prem Exchange
{: .fs-4}

{% capture code %}$UserCredential = Get-Credential
$Server = <exch_server_name>
$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "$server/PowerShell/" -Authentication Kerberos
Import-PSSession $Session -DisableNameChecking{% endcapture %}
{% include code.html code=code lang="powershell" %}

<br>
#### Prerequisites for O365 if not already installed
- Install [Microsoft Online Services Sign-in Assistant](https://go.microsoft.com/fwlink/p/?LinkId=286152) if not on Windows 10.
- Install MSOnline module
{% capture code %}Install-Module MSOnline{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

#### Exchange Onlne w/ Modern Auth
Connect-MsolService
<br>

#### Teams\Skype Online w/ Modern AUth
<br>

## Performance & Maintenance

---
Mailbox Count Per DB
{% capture code %}Get-Mailbox -ResultSize unlimited | Group-Object -Property:Database | Select-Object Name,Count | Sort-Object Name | Format-Table -Auto {% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

Server Version
{% capture code %}Get-ExchangeServer | Format-List Name,Edition,AdminDisplayVersion {% endcapture %}
{% include code.html code=code lang="powershell" %}
Run command and compare build number to the Microsoft [documentation](https://docs.microsoft.com/en-us/exchange/new-features/build-numbers-and-release-dates?view=exchserver-2016)
<br>

Exchange Backpressure Values
{% capture code %}[xml]$bp=Get-ExchangeDiagnosticInfo [-Server <ServerIdentity> ] -Process EdgeTransport -Component ResourceThrottling; $bp.Diagnostics.Components.ResourceThrottling.ResourceTracker.ResourceMeter {% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

{% capture code %}{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>
