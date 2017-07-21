---
title: MIS_MATCH_MEM_MAN

---
## Mismatched_Memory_Management Prohibit allocating and deallocating dynamic memory not consistent with each other
----
A dynamic memory shall be allocated and deallocated by checking it more clearly than the other component of C/C++ language.
### Description
When deallocating a memory allocated dynamically, using inappropriate deallocation function is an undefined behavior. If the memory is not deallocated correctly, the memory can be damaged or the program can be ended.
The memory allocation and deallocation shall be executed in pair as the following table.

| allocation | deallocation |
|---|---|
| allocator<T>::allocate()  |  allocator<T>::deallocate() |
|  operator new()/new |  operator delete()/delete |
|  operator new[]()/new[] |  operator delete[]()/delete[] |
|  std::malloc(), std::calloc(), std::realloc() |  std::free() |

#### __example 1__
```cpp
void foo(){
  BarObj *ptr = new BarObj()
  /* do some work with ptr here */
  ...

  free(ptr);
}
...
free(ptr);
```
The pointer allocated as a new shall not be deallocated by a free().

#### __alternative 1__
```cpp
void foo(){
  BarObj *ptr = new BarObj()
  /* do some work with ptr here */
  ...

delete ptr;
}
```
It shall be deallocated correctly by a delete.

#### __example 2__
```cpp
void f() {
  int *array = new int[10];
  // ...
  delete array;
}
```
The pointer allocated as a new[] shall not be deallocated by a delete.

#### __alternative 2__
```cpp
void f() {
  int *array = new int[10];
  // ...
  delete array;
}
```
The pointer allocated as a new[] shall be deallocated surely by delete [].


### Related Link
+ [CWE-762: Mismatched Memory Management Routines](http://cwe.mitre.org/data/definitions/762.html)
+ [CERT C++  MEM31-CPP. Properly deallocate dynamically allocated resources](https://www.securecoding.cert.org/confluence/display/cplusplus/MEM31-CPP.+Properly+deallocate+dynamically+allocated+resources)

----
