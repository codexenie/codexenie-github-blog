---
title: MIS_MATCH_MEM_MAN
date:
tags: 
    - CWE-762
    - Mismatched Memory Management Rosutines
---
## Mismatched_Memory_Management 서로 맞지 않는 동적 메모리 할당과 해제 금지
----
동적 메모리는 C/C++ 언어의 다른 구성요소보다 더 확실하게 확인하여 할당하거나 해제해야 한다. 
### 설명
동적으로 할당한 메모리를 해제할 때 알맞지 않은 해제 함수를 사용하는 것은 정의하지 않은 행동이다. 메모리 해제 올바르게 하지 않으면 메모리를 손상시키거나 프로그램이 종료될 수 있다. 
메모리 할당과 해제는 다음 표와 같은 쌍으로 이루어져야 한다.

| 할당 | 해제 |
|---|---|
| allocator<T>::allocate()  |  allocator<T>::deallocate() |
|  operator new()/new |  operator delete()/delete |
|  operator new[]()/new[] |  operator delete[]()/delete[] |
|  std::malloc(), std::calloc(), std::realloc() |  std::free() |

#### __예제1__
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
new 로 할당한 포인터를 free() 로 해제하면 안 된다.

#### __대안1__
```cpp
void foo(){
  BarObj *ptr = new BarObj()
  /* do some work with ptr here */
  ...

delete ptr;
}
```
delete 로 올바르게 해제해야 한다.

#### __예제2__
```cpp
void f() {
  int *array = new int[10];
  // ...
  delete array;
}
```
new[] 로 할당한 포인터를 delete 로 해제하면 안 된다.

#### __대안2__
```cpp
void f() {
  int *array = new int[10];
  // ...
  delete[] array;
}
```
new[] 로 할당한 포인터는 반드시 delete [] 로 해제해야 한다.

### 관련 링크
+ [CWE-762: Mismatched Memory Management Routines](http://cwe.mitre.org/data/definitions/762.html)
+ [CERT C++  MEM31-CPP. Properly deallocate dynamically allocated resources](https://www.securecoding.cert.org/confluence/display/cplusplus/MEM31-CPP.+Properly+deallocate+dynamically+allocated+resources)

----
