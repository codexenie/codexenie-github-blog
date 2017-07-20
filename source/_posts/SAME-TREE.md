---
title: SAME TREE
date:
tags: 
    - Effective C++ item 36
    - Never redefine an inherited non-virtual function.
---
## Never redefine an inherited non-virtual function.
----
Non-virtual functions are statically bound.
### Description
Non-virtual functions are statically bound. It should have the same behavior no matter whether you call the derived function from a pointer to base class or from a pointer to derived class. Otherwise it is not is-a inheritance. 

#### __example 1__
```cpp
class A{
	public:
	void call();
};

class B : public A{
	public:
	void call(); /* not compliant */
};

void func()
{
	A* x = new B();
	x->call(); 
}
```

#### __alternative 1__
```cpp
class A{
	public:
	virtual void call();
};

class B : public A{
	public:
	void call(); /* compliant */
};

void func()
{
	A* x = new B();
	x->call(); 
}

```



### Related Link
+ ["Effective C++" Third Edition by Scott Meyers.] (http://aristeia.com/books.html) 
+ [CERT C++  OOP02-CPP. Do not hide inherited non-virtual member functions](https://www.securecoding.cert.org/confluence/display/cplusplus/OOP02-CPP.+Do+not+hide+inherited+non-virtual+member+functions)

----
