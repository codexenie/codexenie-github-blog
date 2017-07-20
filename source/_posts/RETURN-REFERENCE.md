---
title: RETURN REFERENCE
date:
tags: 
    - Effective C++ item 14
    - don't try to return a reference when you must return an object.
---
## don't try to return a reference when you must return an object.
----
Never return a pointer or reference in function. 
### Description
Never return a pointer or reference to a local stack object, a reference to a heap-allocated object, or a pointer or reference to a local static object. If return heap-based objects it is possible to occur memory leak. And local static object are destroyed ath the exit of function. It is not valid on out of function scope. 

#### __example 1__
```cpp
const char& func1()
{
	char* ch = new char();
	
	return *ch; /* not compiant */
}

const char& func2()
{
	char* ch = 0;
	if (ch != 0)
	{
		return *ch;
	}
	return *ch; /* not compiant */
}
```

#### __alternative 1__
```cpp
const char func1()
{
	char* ch = new char();
	
	return ch; /* compiant */
}

const char func2()
{
	char ch = 0;
	if (ch != 0)
	{
		return ch;
	}
	return *ch; /* compiant */
}
```


### Related Link
+ ["Effective C++" Third Edition by Scott Meyers.] (http://aristeia.com/books.html) 
+ [CWE-562: Return of Stack Variable Address](https://cwe.mitre.org/data/definitions/562.html)

----
