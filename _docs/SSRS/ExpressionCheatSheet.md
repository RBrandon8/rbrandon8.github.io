---
layout: post
author: Brandon Ricketts
title: Expressions Cheat Sheet
nav_order: 1
parent: SSRS
published: true
date: 08/11/2020
permalink: /_docs/SSRS/Setup/Expression Cheat Sheet
---

## Date Expressions
---
  First day of last month: 
  {% capture code %}=dateadd("m",-1,dateserial(year(Today),month(Today),1)){% endcapture %}
  {% include code.html code=code lang="" %}

  First day of this month: 
  {% capture code %}=dateadd("m",0,dateserial(year(Today),month(Today),1)){% endcapture %}
  {% include code.html code=code lang="" %}

  First day of next month: 
  {% capture code %}=dateadd("m",1,dateserial(year(Today),month(Today),1)){% endcapture %}
  {% include code.html code=code lang="" %}

  Last day of last month: 
{% capture code %}=dateadd("m",0,dateserial(year(Today),month(Today),0)){% endcapture %}
{% include code.html code=code lang="" %}

  Last day of this month: 
{% capture code %}=dateadd("m",1,dateserial(year(Today),month(Today),0)){% endcapture %}
{% include code.html code=code lang="" %}

  Last day of next month: 
{% capture code %}=dateadd("m",2,dateserial(year(Today),month(Today),0)){% endcapture %}
{% include code.html code=code lang="" %}

## Alternating Row Highlighting
---
  Alternating Row
{% capture code %}=IIF(ROWNUMBER(NOTHING) MOD 2, "White", "LightGrey"){% endcapture %}
{% include code.html code=code lang="" %}

  Alternating Row with groups
{% capture code %}=IIF(RunningValue(Fields!Location.Value, CountDistinct, Nothing) MOD 2 = 1,  "White", "LightGrey"){% endcapture %}
{% include code.html code=code lang="" %}
 
