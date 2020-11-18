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
Connect to On Prem Exchange

{% capture code %}$UserCredential = Get-Credential
$Server = <exch_server_name>
$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "$server/PowerShell/" -Authentication Kerberos
Import-PSSession $Session -DisableNameChecking{% endcapture %}
{% include code.html code=code lang="powershell" %}

<br>
Prerequisites for O365 if not already installed
- Install [Microsoft Online Services Sign-in Assistant](https://go.microsoft.com/fwlink/p/?LinkId=286152) if not on Windows 10.
- Install MSOnline module
{% capture code %}Install-Module MSOnline{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

AzureAD
- Install Module
{% capture code %}Install-Module -Name AzureAD{% endcapture %}
{% include code.html code=code lang="powershell" %}
{% capture code %}Connect-AzureAD{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

Exchange Online
{% capture code %}$credential = Get-Credential
Import-Module ExchangeOnlineManagement
Connect-ExchangeOnline -Credential $credential -ShowProgress $true{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

Sharepoint Online
{% capture code %}$credential = Get-Credential
$orgName= "myorg" <myorg.microsoft.com>
Connect-SPOService -Url https://$orgName-admin.sharepoint.com -Credential $Credential{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

Teams\Skype Online
{% capture code %}$credential = Get-Credential
Import-Module MicrosoftTeams
$sfboSession = New-CsOnlineSession -Credential $credential
Import-PSSession $sfboSession{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

##Performance & Maintenance

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
