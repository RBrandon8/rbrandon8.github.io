---
layout: post
title: Building an F5 APM Policy with Radius MFA authentication
nav_order: 1
parent: F5
permalink: /_docs/F5/CombineRadiusWithNTLM
---

I recently was trying to add DUO MFA to an F5 APM policy.  After installing the proxy app in our environment using DUO's [documentation](https://duo.com/docs/f5bigip) the last step was to add the Radius Auth item to my F5 APM policy.  I added the item to the APM policy and when testing noticed that the RADIUS Auth was interferring with NTLM applications after a user logged in.  Intially I had set up the authentication directly after the credential check like below.

![](/assets/images/f5_Radius_Not_Working.JPG)

Thinking that the order of authentication may have been the issue, I moved the SSO mapping before the Radius Auth hoping that it would cache the credentials before it "broke" NTLM.

![](/assets/images/f5_Radius_Working.JPG)

This broke the Radius Auth item. Reviewing the Radius Auth and SSO Mapping items led me to the final piece of the solution.  I needed to change the variables on the Radius Auth to use the cached credentials, rather then use the form variables which were being invalidated after being passed to Radius Auth. 

Default values
![](/assets/images/f5_Radius_Properties_NW.JPG)

Updated working values.
![](/assets/images/f5_Radius_Properties.JPG)



