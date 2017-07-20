---
title: SAME TREE
date:
tags: 
    - CWE-483
    - Incorrect Block Delimitation.
---
## Missed Brace
----
The code does not explicitly delimit a block that is intended to contain 2 or more statements, creating a logic error.
### Description
In C++, braces  are optional for blocks. When the delimiter is omitted, it is possible to insert a logic error in which a statement is thought to be in a block but is not. 

#### __example 1__
```cpp
void func(int a)
{
	if(a > 1)
		a++;
		a++; /* not compliant */
}
```

#### __alternative 1__
```cpp
void func(int a)
{
	if(a > 1)
	{
		a++;
		a++; /* compliant */
	}
}
```



### Related Link
+ [CWE-483: Incorrect Block Delimitation](https://cwe.mitre.org/data/definitions/483.html)

----
