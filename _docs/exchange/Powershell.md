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
{: .fs-6}

---
 Connect to On Prem Exchange
{: .fs-5}

{% capture code %}$UserCredential = Get-Credential
$Server = <exch_server_name>
$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "$server/PowerShell/" -Authentication Kerberos
Import-PSSession $Session -DisableNameChecking{% endcapture %}
{% include code.html code=code lang="powershell" %}

<br>
Prerequisites for O365\Azure if not already installed
{: .fs-5}

- Install [Microsoft Online Services Sign-in Assistant](https://go.microsoft.com/fwlink/p/?LinkId=286152) if not on Windows 10.
- Install MSOnline module
{% capture code %}Install-Module MSOnline{% endcapture %}
{% include code.html code=code lang="powershell" %}
- Allow local and remote signed scripts
{% capture code %}set-executionpolicy remotesigned{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

AzureAD w/ Modern Auth
{: .fs-5}

- Install Module
{% capture code %}Install-Module -Name AzureAD{% endcapture %}
{% include code.html code=code lang="powershell" %}
- Connect
{% capture code %}Connect-AzureAD{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

Exchange Online w/ Modern Auth
{: .fs-5}

- Install Module
{% capture code %}Install-Module -Name ExchangeOnlineManagement{% endcapture %}
{% include code.html code=code lang="powershell" %}
- Connect
{% capture code %}Connect-ExchangeOnline{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

Sharepoint Online w/ Modern Auth
{: .fs-5}

- Install Module
{% capture code %}Install-Module -Name Microsoft.Online.SharePoint.PowerShell{% endcapture %}
{% include code.html code=code lang="powershell" %}
- Connect
{% capture code %}$orgName="org" <org.onmicrosoft.com>
Connect-SPOService -Url https://$orgName-admin.sharepoint.com{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

Teams\Skype Online w/ Modern Auth
{: .fs-5}

- Install Module
{% capture code %}Install-Module MicrosoftTeams{% endcapture %}
{% include code.html code=code lang="powershell" %}
- Connect
*Not working with Powershell 7 currently
{% capture code %}Import-Module MicrosoftTeams
$sfbSession = New-CsOnlineSession
Import-PSSession $sfbSession{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

Security & Compliance Center
{: .fs-5}

- Install Module
{% capture code %}Import-Module ExchangeOnlineManagement{% endcapture %}
{% include code.html code=code lang="powershell" %}
- Connect
{% capture code %}Connect-IPPSSession -UserPrincipalName user@domain.com{% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>
## Performance & Maintenance
{: .fs-6}

---
Mailbox Count Per DB
{: .fs-5}

{% capture code %}Get-Mailbox -ResultSize unlimited | Group-Object -Property:Database | Select-Object Name,Count | Sort-Object Name | Format-Table -Auto {% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>

Server Version
{: .fs-5}

{% capture code %}Get-ExchangeServer | Format-List Name,Edition,AdminDisplayVersion {% endcapture %}
{% include code.html code=code lang="powershell" %}
Run command and compare build number to the Microsoft [documentation](https://docs.microsoft.com/en-us/exchange/new-features/build-numbers-and-release-dates?view=exchserver-2016)
<br>
<br>

Exchange Backpressure Values
{: .fs-5}

{% capture code %}[xml]$bp=Get-ExchangeDiagnosticInfo [-Server <ServerIdentity> ] -Process EdgeTransport -Component ResourceThrottling; $bp.Diagnostics.Components.ResourceThrottling.ResourceTracker.ResourceMeter {% endcapture %}
{% include code.html code=code lang="powershell" %}
<br>
