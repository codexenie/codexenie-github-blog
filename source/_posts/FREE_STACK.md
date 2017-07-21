## Memory_Free_On_Stack_Variable Prohibit invalid size when allocating a memory by malloc
----
When allocating a memory by malloc, the size shall be a valid value.
### Description
The result of arithmetic operation in program can be bigger than the maximum value of that type or be smaller than the minimum value of that type. If it is used as the size of memory allocation without checking the result value of calculation, it can reference invalid memory.

#### __example 1__
```cpp
void foo(){
record_t bar[MAX_SIZE];

/* do something interesting with bar */
...
free(bar);
}
```
In the example, if the size of num_imgs is a big number, it can be a value unexpected by a developer due to overflow.

#### __alternative 1__
```cpp
void foo(){
record_t *bar = (record_t*)malloc(MAX_SIZE*sizeof(record_t));

/* do something interesting with bar */
...
free(bar);
}
```
Using the unexpected value shall be prevented by examining the preceding conditions before using it.

### Related Rule

+ [RTE_Mismatched_Memory_Management Prohibit allocating and deallocating dynamic memory not consistent with each other](RTE_Mismatched_Memory_Management.html)

### Related LInk
+ [CWE-590: Free of Memory not on the Heap](http://cwe.mitre.org/data/definitions/590.html)
+ [CERT C MEM34-C. Only free memory allocated dynamically](https://www.securecoding.cert.org/confluence/display/seccode/MEM34-C.+Only+free+memory+allocated+dynamically)
----
