# Understanding `calloc` in C

## Overview
In C programming, the `calloc` function is used for memory allocation. We discussed two specific uses:

1. `(int*)calloc(5, sizeof(int))`
2. `(int*)calloc(10, sizeof(int))`

## Details

### `(int*)calloc(5, sizeof(int))`
- **Purpose**: Allocates memory for an array of 5 integers.
- **Memory Allocation**: If an `int` is 4 bytes, this allocates `5 * 4 = 20` bytes.

### `(int*)calloc(10, sizeof(int))`
- **Purpose**: Allocates memory for an array of 10 integers.
- **Memory Allocation**: If an `int` is 4 bytes, this allocates `10 * 4 = 40` bytes.

## Key Points
- Both expressions allocate memory and initialize it to zero.
- The size of the allocated memory depends on the size of `int` on the system.
- It is crucial to free the allocated memory to avoid memory leaks.

## Example Code
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // Using calloc for array of 5 and 10 integers
    int* array1 = (int*)calloc(5, sizeof(int));
    int* array2 = (int*)calloc(10, sizeof(int));
    // ... (rest of the code)
    return 0;
}
```

array1 byte size -> 5 * 4 = 20
array2 byte size -> 10 * 4 = 40