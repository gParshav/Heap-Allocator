<!-- void * is a pointer type that can point to any data type but does not specify what type it points to.


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
 -->


# Custom Heap Allocator in C

## Overview

This project implements a custom heap allocator in C for managing memory allocation and deallocation efficiently. The heap allocator is built from scratch and manages memory through a simple heap array, using chunk lists to track allocated and freed memory blocks. The allocator handles fragmentation by splitting memory chunks as needed and provides basic garbage collection (yet to be implemented).

## Features

- **Heap Allocation**: Allocates memory from a predefined heap.
- **Memory Deallocation**: Frees memory and makes it available for future allocations.
- **Fragmentation Handling**: Manages memory chunks to reduce fragmentation, ensuring efficient use of available memory.
- **Chunk Management**: Uses chunk lists to track allocated and freed memory regions.
- **Basic Garbage Collection (TBD)**: A placeholder for a garbage collector, designed to scan the heap and free unreachable memory (not yet implemented).

## Key Concepts

### 1. **Pointers and `void *`**

In C, a pointer is a variable that holds a memory address. The actual memory address it holds can point to different types of memory regions (stack, heap, or even static/global).

- **`void *`**: A pointer type that can point to any data type but does not specify what type it points to. It's widely used in C for generic programming, allowing functions and data structures to handle various types without being restricted to a single type. Proper casting is essential when working with `void *` to avoid type-related errors.

### 2. **`size_t`**

- **`size_t`**: A type defined in C (and C++) that represents the size of an object in bytes. It is commonly used for array indexing, loop counting, and memory management functions, such as those dealing with dynamic memory allocation. `size_t` is defined in the `<stddef.h>` and `<stdlib.h>` headers and is an unsigned integral type, meaning it can only represent non-negative numbers.

### 3. **Heap vs. Stack Memory**

- **Stack Memory**:
  - Automatically managed by the compiler.
  - Used for function call frames, local variables, and control information.
  - Limited in size, usually faster to allocate/deallocate.
  - Variables declared inside functions (like local variables) are stored on the stack.
  - When a function returns, its stack frame is cleaned up.

- **Heap Memory**:
  - Manually managed by the programmer using functions like `malloc` and `free`.
  - Used for dynamic memory allocation.
  - Generally larger than the stack but slower to allocate/deallocate.
  - Persistent until explicitly deallocated using `free`.

### 4. **Memory Management Strategies**

When managing memory, particularly in a heap allocator:

- **Iterative Search**: To allocate memory, you might iterate through the entire heap-like structure to find an available block that meets the requirements. This approach has a time complexity of O(N).

- **Chunk List**: To improve efficiency, another array can store pointers to and addresses of empty blocks of storage. This allows O(1) time complexity for allocation and deallocation when all blocks are of a common size. However, managing different block sizes can be more complex.

### 5. **`typedef` in C**

- **`typedef`**: A keyword in C and C++ that allows you to create an alias for a data type. It simplifies the use of complex data types by providing a more intuitive name. For example, `typedef` can be used to create an alias for a struct, making the code easier to read and maintain.

## Files and Functions

### 1. **Main Code**

- **`heap_alloc(size_t size)`**: Allocates a block of memory of a specified size from the heap. It checks for available space in the `freed_chunks` list and, if space is available, allocates the memory, updates the chunk lists, and returns a pointer to the allocated block.
  
- **`heap_free(void *ptr)`**: Frees a previously allocated block of memory. It finds the corresponding chunk in the `alloced_chunks` list, moves it to the `freed_chunks` list, and ensures that freed memory can be reused.

- **`heap_collect()`**: Placeholder for garbage collection logic. This function will scan the heap to identify unreachable memory blocks and free them. (To be implemented.)

### 2. **Chunk List Management**

- **`chunk_list_insert(Chunk_List *list, void *start, size_t size)`**: Inserts a new memory chunk (pointer and size) into a chunk list, maintaining the list in sorted order by memory address.

- **`chunk_list_remove(Chunk_List *list, size_t index)`**: Removes a chunk from a chunk list based on the index, adjusting the list to close the gap left by the removed chunk.

- **`chunk_list_find(const Chunk_List *list, void *ptr)`**: Searches for a specific chunk (by memory address) in a chunk list and returns its index.

- **`chunk_list_dump(const Chunk_List *list)`**: Outputs a summary of all chunks in a list, displaying their starting address and size.

### 3. **Helper Functions**

- **`chunk_start_compar(const void *a, const void *b)`**: Compares two memory chunks based on their starting address. This is used to sort or search chunk lists efficiently.

### 4. **Data Structures**

- **`Chunk`**: Represents a memory chunk with a pointer to the start of the allocated block and the block’s size.
  
- **`Chunk_List`**: Represents a list of memory chunks, with two instances used to track allocated and freed chunks.

## Example Usage

In the `main()` function, you can see how to allocate and free memory using the heap allocator:

```c
int main() {
    for (int i = 0; i < 10; i++) {
        void *p = heap_alloc(i);
        if (i % 2 == 0) {
            heap_free(p);
        }
    }

    chunk_list_dump(&alloced_chunks);
    chunk_list_dump(&freed_chunks);

    return 0;
}
