---
layout: post
author: Brandon Ricketts
title: Expressions Cheat Sheet
nav_order: 1
parent: SSRS
permalink: /_docs/SSRS/Setup/Expression Cheat Sheet
---

## Date Expressions
---
  First day of last month: 
```
=dateadd("m",-1,dateserial(year(Today),month(Today),1))  
```
  First day of this month: 
```
=dateadd("m",0,dateserial(year(Today),month(Today),1))  
```
  First day of next month: 
```
=dateadd("m",1,dateserial(year(Today),month(Today),1))  
```
  Last day of last month: 
```
=dateadd("m",0,dateserial(year(Today),month(Today),0)) 
```
  Last day of this month: 
```
=dateadd("m",1,dateserial(year(Today),month(Today),0)) 
```
  Last day of next month: 
```
=dateadd("m",2,dateserial(year(Today),month(Today),0)) 
```

## Alternating Row Highlighting
---
  Alternating Row
```
=IIF(ROWNUMBER(NOTHING) MOD 2, "White", "LightGrey") 
```
  Alternating Row with groups
```
=IIF(RunningValue(Fields!Location.Value, CountDistinct, Nothing) MOD 2 = 1,  "White", "LightGrey") 
```
 