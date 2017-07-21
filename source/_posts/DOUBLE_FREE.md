---
title: DOUBLE_FREE
---

## Double_Free Prohibit deallocating memory duplication
----
If the deallocated pointer variable is deallocated again, the unexpected memory location can be changed. 
### Description
If the same pointer variable is deallocated twice, the data structure for controlling the memory can be damaged. Due to this damage, the program can be ended or two times memory allocation can return the same pointer. If the memory allocation returns the same value twice and the attacker can control this memory area, he can attack by buffer overflow. 

#### __example 1__
```cpp
char* ptr = (char*)malloc (SIZE);
...
if (abrt) {
    free(ptr);
}
    ...
free(ptr);
```
Generally, the memory duplication deallocation is occurred by the following two reasons.

+ Error condition or exception situation
+ Confused situation which part of program is responsible for memory deallocation.

Several duplication deallocation weaknesses are not more complicated than the example, but in certain case, they can be occurred apart from more than hundreds lines or in the other file. A programmer frequently deallocates the global variable in particular twice.


### Related Link
+ [CWE 415: Double Free](http://cwe.mitre.org/data/definitions/415.html)

----