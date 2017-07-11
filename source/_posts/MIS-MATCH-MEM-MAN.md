---
title: MIS_MATCH_MEM_MAN
date: 
tags: 
    - CWE-762
    - Mismatched Memory Management Rosutines
---
# mismatched memory management routines
 > 메모리 할당과 해제시 잘못된 object 사용 

## Relationships

|Nature	    |  	Type		|		ID|	Name|
|-----------|---------------|----------|----|
|ChildOf	|	Category		|	399	|	Resource Management Errors	|
|ChildOf	|	Weakness Base	|	763	|	Release of Invalid Pointer or Reference	|
|ChildOf	|	Category		|	876	|	CERT C++ Secure Coding Section 08 - Memory Management (MEM)	|
|ChildOf	|	Category		|	969	|	SFP Secondary Cluster: Faulty Memory Release	|
|ParentOf	|Weakness Variant|	590	|	Free of Memory not on the Heap|
    
## CODE
	
```cpp
//GOOD CASE
    class A{
        void foo(bool);
    };

    void A::foo(bool heap) {
        int localArray[2] = {11,22};
        int *p = localArray;
        
        if (heap){
            p = new int[2];
        }
        delete[] p;
    }

//BAD CASE
    class A {
        void foo();
    };
    void A::foo(){
        int *ptr;
        ptr = (int*)malloc(sizeof(int));
        delete ptr;
    }
```
