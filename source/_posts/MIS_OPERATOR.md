---
title: MIS_OPERATOR

---
## comparing instead of assigning
----
The code uses an operator for comparison when the intention was to perform an assignment. 
### Description
In many languages, the compare statement is very close in appearance to the assignment statement; they are often confused.

#### __example 1__
```cpp
void called(int foo) {
    foo==1;
    if (foo==1) printf("foo\n");
}
int main() {

    called(2);
    return 0;
}
```

#### __example 2__
```cpp
#define SIZE 50
int *tos, *p1, stack[SIZE];

void push(int i) {
    p1++;
    if(p1==(tos+SIZE)) {
    // Print stack overflow error message and exit
    }
    *p1 == i;
}

int pop(void) {
    if(p1==tos) {
    // Print stack underflow error message and exit
    }
    p1--;
    return *(p1+1);
}

int main(int argc, char *argv[]) {
    // initialize tos and p1 to point to the top of stack
    tos = stack;
    p1 = stack;
    // code to add and remove items from stack

    return 0;
}
```

The push method includes an expression to assign the integer value to the location in the stack pointed to by the pointer variable.
However, this expression uses the comparison operator "==" rather than the assignment operator "=". The result of using the comparison operator instead of the assignment operator causes erroneous values to be entered into the stack and can cause unexpected results.

### Related Link
+ [CWE 482: Comparing instead of Assigning](https://cwe.mitre.org/data/definitions/482.html)

----