---
title: VIRTUAL_DESTRUCTOR
date:
tags: 
    - Effective C++ item 7
    - Declare destructors virtual in polymorphic base classes.
---
## Declare destructors virtual in polymorphic base classess.
----
If base class with a non-virtual destructor, it occured undefined behavior.
### Description
If delete base class pointer with non-virtual destructor, it happens at runtime is that the derived part of the object is never destroyed. So polymorphic base classes should declare virtual desturctors. If a class has any virtual functions, it should have a virtual destructor. Classes not designed to be base classes or not designed to be used polymorphically should not declare virtual destructors.

#### __example 1__
```cpp
class A
{
public:
	A();
	~A(); /* not compliant; destructor is not virtual */
};

class B : public A
{
	~B()
	{
		mem = 0;
	}
private:
	int mem;
};

void func()
{
	A* a = new B();
	delete a;
}
```
If delete A class pointer, it happens at runtime is that destructor of B didn't called.

#### __alternative 1__
```cpp
class A
{
public:
	A();
	virtual ~A(); /* compliant; */
};

class B : public A
{
	~B()
	{
		mem = 0;
	}
private:
	int mem;
};

void func()
{
	A* a = new B();
	delete a;
}
```
Destructor of A must be virtual.


### Related Link
+ ["Effective C++" Third Edition by Scott Meyers.] (http://aristeia.com/books.html) 
+ [CERT C++  OOP52-CPP. Do not delete a polymorphic object without a virtual destructor](https://www.securecoding.cert.org/confluence/display/cplusplus/OOP52-CPP.+Do+not+delete+a+polymorphic+object+without+a+virtual+destructor)

----
