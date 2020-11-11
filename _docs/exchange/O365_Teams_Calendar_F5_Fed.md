---
layout: post
author: Brandon Ricketts
title: Integrating Teams Calendar with Exchange OnPrem and F5 Federation
nav_order: 1
parent: exchange
date: 09/11/2020
permalink: /_docs/exchange/O365_Teams_Calendar_F5_Fed
published: true
---

### Requirements

- [x] Exchange 2016 CU3 or later
- [x] Funcition Hybrid Services with OAuth setup
- [x] Functioning F5 APM Federation with Exchange On Prem
- [x] Understanding that this information is provided as is and is an attempt to help the reader make an informed decision on what is best for their environment.

The default F5 iapp template for Exchange does include an option for integrating with hybrid services.  The default settings allow for basic service communicaton, however the template does not seem to be keeping pace with changes in O365 authentication methods.  A great example of this is Teams Calendars.  In order for Teams Calendars to work with APM authentication for autodiscover services you must update the iRule to include the xml and all json uri's.



Default iRule
```
priority 1
when HTTP_REQUEST {
	 set is_disabled 0
	 switch -glob [string tolower [HTTP::path]] {
		 "/ews/mrsproxy.svc" -
		 "/ews/exchange.asmx/wssecurity" {
			 set is_disabled 1
			 set path [HTTP::path]
			 ACCESS::disable
			 HTTP::path _disable-$path
			 <EWS_POOL><EDGE_POOL>
		 }
		 "/autodiscover/autodiscover.svc/wssecurity" -
		 "/autodiscover/autodiscover.svc" {
			 set is_disabled 1
			 set path [HTTP::path]
			 ACCESS::disable
			 HTTP::path _disable-$path
			 <AD_POOL><EDGE_POOL>
		 }
	 }

```


Updated Rule
```
priority 1
when HTTP_REQUEST {
	 set is_disabled 0
	 switch -glob [string tolower [HTTP::path]] {
		 "/ews/mrsproxy.svc" -
		 "/ews/exchange.asmx/wssecurity" {
			 set is_disabled 1
			 set path [HTTP::path]
			 ACCESS::disable
			 HTTP::path _disable-$path
			 pool <EWS_POOL><EDGE_POOL>
		 }
		 "/autodiscover/autodiscover.svc/wssecurity" -
		 "/autodiscover/autodiscover.svc" - 
		 "/autodiscover/autodiscover.xml" -
		 "/autodiscover/autodiscover.json*" {
			 set is_disabled 1
			 set path [HTTP::path]
			 ACCESS::disable
			 HTTP::path _disable-$path
			 pool <AD_POOL><EDGE_POOL>
		 }
	 }
}
when HTTP_REQUEST_RELEASE {
	if { [info exists is_disabled] && $is_disabled == 0 } { return }
		if { [info exists path] } {
			HTTP::path $path
			unset is_disabled
			unset path
	}
}
```
