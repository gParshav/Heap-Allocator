Pointers in C

What's a pointer?
Pointer is something that points to the memory location.

How do you declare a pointer?
int* a/int *a

- A pointer variable is something that can help store and deal with addresses of variables of the same type.

Types of Pointers:
1. Typed Pointer
 - Points to a specific type of data.
 - For ex, an integer pointer(int*) only points to integer data.
2. Untyped Pointer(Also known as Generic Pointer)
 - Can point to any kind of data.
 - How is it declared? - void*

Operators with Pointers:
1. Address Operator(&) - Returns the address of a particular variable.
2. Pointer Operator(*) - Return the value contained at a particular memory address.

Note:
- You can't store the address of an integer in another non-pointer integer.
- You can only store the address of an integer in a pointer variable.
For example, this is incorrect code.
<!-- #include <stdio.h>

int main() {
    int a = 0;
    int b = &a;
    printf("%d", b);

    return 0;
} -->

Code Snippets that explain important things:-

1.  #include <stdio.h>

    int main() {
        int a = 0;
        int *b = &a;
        printf("%d", b);

        return 0;
    }

Output - 1485877956

2.  #include <stdio.h>

    int main() {
        int a = 0;
        int *b = &a;
        printf("%d", *b);

        return 0;
    }

Output - 0

3. printf("%d", *(&i)) -> This prints i

&i means that give me the address of i
* means give me the value at whatever address
*(&i) means that give me the value at the address of i which is i


Size of an integer and the size of the pointer, both differs from compiler to compiler,
and depends on the compiler type.

Compiler Type - 16bit, Integer Size - 2 Bytes, Pointer Size - 2 Bytes
Compiler Type - 32bit, Integer Size - 4 Bytes, Pointer Size - 4 Bytes

A 16 bit compiler means that it can have 2^16 different memory locations.
Number of memory locations depends on the size of the compiler.

Another very interesting insight is that pointers of all types occupy the same amount of memory, and that does not depend on the pointer type.
A struct pointer pointing to a struct that has 20 variables inside, and a normal int pointer both occupy the same amount of memory because at the end of the day, both of them are storing addresses the size of which doesn't really depend upon the type of the pointer.

Also since all pointers essentially only contain addresses, all of them actually store the same kind of data. Irrespective of what kind of pointer variable it is. That is just so unimportant.

Pointers just contain addresses.
Pointer Size is normally 2 bytes.