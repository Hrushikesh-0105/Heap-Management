# Heap Management Simulation (Best Fit Method)

## Project Overview
This project implements a heap memory management system in C using the Best Fit method. It provides custom implementations of `malloc` and `free` functions to dynamically allocate and deallocate memory within a simulated heap.

**Author:** Hrushikesh Musaloj (BT23CSE024)

## Features
- **Custom Memory Allocation:** Implements `my_malloc` using the Best Fit technique to allocate memory efficiently.
- **Memory Deallocation:** Implements `my_free` to release memory back to the heap.
- **Heap Initialization:** Simulates a 1 MB heap with block splitting and merging.
- **Metadata Management:** Uses a `MetaDataBlock` structure to track block sizes and manage free/allocated lists.
- **Memory Optimization:** Merges adjacent free blocks to minimize fragmentation.

## Technical Details
- **Heap Size:** 1 MB + metadata overhead.
- **Minimum Allocation:** `MIN_ALLOC_SIZE = sizeOfMetadata + sizeof(int)`.
- **Memory Alignment:** Allocates memory in multiples of 4 bytes.

### Data Structures
```c
typedef struct MetaDataBlock {
    size_t size;
    struct MetaDataBlock *next;
} MetaDataBlock;
```
- `size`: Size of the memory block (excluding metadata).
- `next`: Pointer to the next free block.

### Constants
- `MAX_HEAP_SIZE = 1048576 + sizeof(MetaDataBlock)`
- `MIN_ALLOC_SIZE = sizeOfMetadata + sizeof(int)`

## Functions Implemented

### 1. `initializeHeap()`
Initializes the heap and sets up the free list with a single large free block.

### 2. `my_malloc(size_t sizeRequest)`
- Allocates memory using the Best Fit strategy.
- Splits blocks if necessary.
- Returns a pointer to the allocated memory.

### 3. `my_free(void *freeDataPtr)`
- Frees the allocated memory.
- Merges adjacent free blocks to reduce fragmentation.

### 4. `printMetaDataList(MetaDataBlock *head)`
Prints the details of all blocks in the given list (free or allocated).

### 5. `findNearestMultipleOf4(size_t size)`
Rounds up the size to the nearest multiple of 4 for memory alignment.

### 6. `mergeCurrentAndNext()` and `mergePrevAndCurrent()`
Merge adjacent free blocks to maintain contiguous free memory.

## Compilation Instructions
1. Open a terminal in the project directory.
2. Compile using `gcc`:
```bash
gcc -o heap_management heap_management.c
```
3. Run the program:
```bash
./heap_management
```

## Usage Example
```c
int *ptr1 = (int*)my_malloc(50);
int *ptr2 = (int*)my_malloc(100);
my_free(ptr1);
my_free(ptr2);
printMetaDataList(freeListHead);
```

## Output Example
```
Allocated 50 bytes
Allocated 100 bytes
Freed 50 bytes
Freed 100 bytes
Address of Free block: 0x100000
Size of Free block: 1048576
Number of free blocks: 1
```

## Error Handling
- **Zero-size Allocation:** Prints an error if zero bytes are requested.
- **Out-of-bounds Free:** Detects and handles invalid free requests.
- **Allocation Failure:** Prints an error if no suitable block is found.

## Optimization Techniques
- **Best Fit Allocation:** Minimizes external fragmentation.
- **Block Merging:** Merges adjacent free blocks during deallocation.
- **Memory Alignment:** Ensures all allocations are aligned to 4-byte boundaries.

## Potential Improvements
- Implementing `realloc` and `calloc`.
- Tracking memory utilization.
- Improving allocation efficiency.
