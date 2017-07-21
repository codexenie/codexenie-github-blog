---
title: LACK INIT OBJ

---
## Copy all parts of an object.
----
You must copy all parts of an object when define copy constructor and copy assignment operator.
### Description
Copying functions should be sure to copy all of an object's data members and all of its base class parts. Most compiler say nothing about partial copy when define copy constructor and copy assignment operator. 

#### __example 1__
```cpp
class C
{
public:
	C(const C& c);
	C& operator=(const C& rhs);
private:
	int mem1;
	int mem2;
};

C::C(const C& c):mem1(c.mem1) /* not compiant; mem2 is not copyed */
{

}

C& C::operator=(const C& rhs) /* not compiant; mem2 is not copyed */
{
	mem1 = rhs.mem1;
	return *this;
}

class D : C
{
public:
	D(const D& d);
	D& operator=(const D& rhs);
private:
	char mem;
};

D::D(const D& d) : C(d), mem(d.mem)
{

}

D& D::operator=(const D& rhs)
{
	C::operator=(rhs);
	mem = rhs.mem;
	return *this;
}

```
Copy constructor and copy assignment operator of class C copy partially member of class C.

#### __alternative 1__
```cpp
class C
{
public:
	C(const C& c);
	C& operator=(const C& rhs);
private:
	int mem1;
	int mem2;
};

C::C(const C& c):mem1(c.mem1), mem2(c.mem2) /* compiant; */
{

}

C& C::operator=(const C& rhs) /* compiant */
{
	mem1 = rhs.mem1;
	mem2 = rhs.mem2;
	return *this;
}

class D : C
{
public:
	D(const D& d);
	D& operator=(const D& rhs);
private:
	char mem;
};

D::D(const D& d) : C(d), mem(d.mem)
{

}

D& D::operator=(const D& rhs)
{
	C::operator=(rhs);
	mem = rhs.mem;
	return *this;
}

```
Copy constructor and copy assignment operator of class C must copy whole member of class C.

### Related Link
+ ["Effective C++" Third Edition by Scott Meyers.](http://aristeia.com/books.html)
----
