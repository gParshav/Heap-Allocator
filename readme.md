void * is a pointer type that can point to any data type but does not specify what type it points to.


It’s widely used in C for generic programming, allowing functions and data structures to handle various types without being restricted to a single type.
Proper casting is essential when working with void * to avoid type-related errors.


For a heap allocator, consider something like an array that has blocks of storage.
Few are occupied, few are available.
Now, someone comes and asks for some storage. 
You will have to iterate the entire array like structure until you find a block that is empty and meets our requirements. - O(N)
Or, you can have another array to simply store pointers to and addresses of empty blocks of storage. This will be O(1)
This makes some sense, when all blocks of storage have a common size, which makes it easier in allocating and deallocating.
Suppose, one block is 4 bytes. I need 16. I will simply give away first 4 addresses in my array.
Could be a bit messy with different sizes.

Stack Memory:

    Automatically managed by the compiler.
    Used for function call frames, local variables, and control information.
    Limited in size, usually faster to allocate/deallocate.
    Variables declared inside functions (like local variables) are stored on the stack.
    When a function returns, its stack frame is cleaned up.


Heap Memory:

    Manually managed by the programmer using functions like malloc and free.
    Used for dynamic memory allocation.
    Generally larger than the stack but slower to allocate/deallocate.
    Persistent until explicitly deallocated using free.
    Pointers and Memory
    
    
In C, a pointer is just a variable that holds a memory address. The actual memory address it holds can point to different types of memory regions (stack, heap, or even static/global).

size_t is a type defined in C (and C++) that represents the size of an object in bytes. It is commonly used for array indexing, loop counting, and memory management functions, such as those dealing with dynamic memory allocation.

size_t is defined in the <stddef.h> and <stdlib.h> headers (among others).
It is an unsigned integral type, meaning it can only represent non-negative numbers.


3 scenarios while freeing memory from the stack:-
- You provide the correct pointer to the memory block. Correct pointer is the pointer you got during allocation. It is the one that points to the start of the allocated memory.
- You provide a pointer that lies within the allocated memory. This is not something we want and is therefore not correct. You can also call it an invalid pointer.
- You provide a pointer that lies outside the allocated memory. This is not something we want and is therefore not correct. You can also call it an invalid pointer.

You need to correctly handle all these scenarios.

What exactly is typedef in C?
typedef is a keyword in C and C++ that allows you to create an alias for a data type. 
Basically this means that imagine you have a datatype that is not int and not char and not something traditional and one dimensional. You actually have something much more random and something that is a collection of a few normal things. IN this case you will use typedef to define such a data structure.

Notes on pointers in C:

