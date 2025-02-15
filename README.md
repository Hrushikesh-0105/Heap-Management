﻿# Heap-Management Simulation (Best fit method)
Project Overview

This project simulates heap memory management in C using the Best Fit allocation strategy. It implements custom versions of malloc and free to manage memory dynamically within a fixed-size heap.

Author: Hrushikesh Musaloj 

Features

Custom implementation of malloc and free

Best Fit memory allocation technique

Memory fragmentation reduction through block merging

Metadata management for memory blocks

Simple, lightweight, and efficient design

How It Works

The program uses an array as a simulated heap. Each memory block is preceded by metadata that stores the block size and a pointer to the next free block. The Best Fit strategy selects the smallest free block that can accommodate the requested memory.

Memory Block Structure

typedef struct MetaDataBlock {
    size_t size;
    struct MetaDataBlock *next;
} MetaDataBlock;

Key Constants

MAX_HEAP_SIZE: 1 MB (1,048,576 bytes) + metadata size

MIN_ALLOC_SIZE: Minimum size to allocate, ensuring space for metadata and data

Core Functions

1. void *my_malloc(size_t sizeRequest)

Allocates a memory block of the requested size using the Best Fit strategy.

Returns: Pointer to allocated memory or NULL if allocation fails.

2. void my_free(void *freeDataPtr)

Frees a previously allocated memory block.

Merges adjacent free blocks to minimize fragmentation.

3. void initializeHeap()

Initializes the heap by setting the initial free block.

4. void printMetaDataList(MetaDataBlock *head)

Displays the free memory blocks and their sizes.

Allocation Strategy: Best Fit

The Best Fit strategy searches the free list for the smallest block that can accommodate the requested size, reducing external fragmentation.

Memory Merging (Defragmentation)

After freeing a block, the program merges adjacent free blocks whenever possible to maintain contiguous free memory.

Usage

Compilation

gcc -o heap_manager heap_manager.c

Execution

./heap_manager

Sample Code Usage

#include <stdio.h>

int main() {
    initializeHeap();

    int *arr1 = (int *)my_malloc(50);
    printf("Allocated 50 bytes\n");

    int *arr2 = (int *)my_malloc(100);
    printf("Allocated 100 bytes\n");

    my_free(arr1);
    printf("Freed first block\n");

    printMetaDataList(freeListHead);

    return 0;
}

Expected Output (Simplified)

Allocated 50 bytes
Allocated 100 bytes
Freed first block
Address of Free block: 0x...
Size of Free block: 52
Number of free blocks: 1

Error Handling

Allocation of zero bytes is not allowed.

Freeing NULL pointers is prohibited.

Attempting to free memory outside the heap boundaries results in an error.

Performance Insights

Best Fit reduces external fragmentation but may increase allocation time.

Merging adjacent free blocks helps maintain large contiguous memory areas.

Possible Improvements

Implementing additional allocation strategies like First Fit or Worst Fit.

Introducing more detailed logging and statistics.

Developing a user-friendly interface for memory usage visualization.
