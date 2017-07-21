---
title: REDUNDANT_COND
---

## Redundant_Condition Prohibit using a conditional expression having the same result at all times
----
There are conditional expressions which the result is always a true or false in the program.
### Description
In the program, the conditional expression having always true or false results can be a logic error. This error leads to an unachievable code.
#### __example 1__
```cpp
uint16_t  bad_1307_var1;
int8_t    bad_1307_var2;

/* Always false */
if ( bad_1307_var1 < 0U )      /* Not compliant */   
...

/* Always true */
if ( bad_1307_var1 <= 0xffffU )   /* Not compliant */
...
     
/* Always true */
if ( bad_1307_var2 < 130 )   /* Not compliant */ 
...
```
The example is the conditional expression having always true of false results.

#### __alternative 1__
```cpp
uint16_t  good_1307_var1;
int8_t    good_1307_var2;

if ( good_1307_var1 > 0U )        /* Compliant */
...

if ( good_1307_var1 < 0xffffU )    /* Compliant */
...
     
if ( good_1307_var2 < 120 )       /* Compliant */ 
...
```
If the correct conditional expression is used, the logic error can be removed.

### Related Link
+ [CWE-570: Expression is Always False](https://cwe.mitre.org/data/definitions/570.html)
+ [CWE-571: Expression is Always True](https://cwe.mitre.org/data/definitions/571.html)

