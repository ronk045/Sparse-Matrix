# Sparse-Matrix


A C implementation of **sparse matrix operations** using a **linked list of tuples**. This project focuses on efficient storage and manipulation of matrices where most values are zero.

---

## Overview

A **sparse matrix** is a matrix in which most elements are zero. Instead of storing every value, this project stores only **non-zero entries** using a linked list of tuples:

Each node stores:
```
(row, col, value)
```

These nodes are kept in **row-major sorted order**.

This approach significantly reduces memory usage and improves performance for large sparse matrices.

---

## Features

- Load sparse matrices from text files
- Store matrices using linked lists of tuples
- Retrieve and modify values efficiently
- Automatically insert, update, or delete entries
- Save sparse matrices back to file
- Add two sparse matrices efficiently
- Proper memory management (no leaks)

---

## File Format

Each matrix is stored in a `.txt` file:

```
rows cols
row col value
row col value
...
```

Example:

```text
4 3
0 1 2
1 1 4
1 2 5
3 2 1
```

Represents:

```
0 2 0
0 4 5
0 0 0
0 0 1
```

---

## Data Structure

Each matrix is represented as:

- `sp_tuples` struct:
  - number of rows
  - number of columns
  - number of non-zero elements (`nz`)
  - pointer to head of linked list

- Each node:
  - row index
  - column index
  - value

The list is always sorted in **row-major order**.

---

## Implemented Functions

### `load_tuples()`

Loads a matrix from a file into a sparse representation.

Responsibilities:

- Read matrix dimensions
- Insert tuples into linked list
- Handle duplicate entries (latest value wins)
- Remove entries with value 0
- Maintain sorted order

---

### `gv_tuples()`

Gets the value at a specific position.

Returns:

- value if tuple exists
- `0` if not found

---

### `set_tuples()`

Sets a value in the matrix.

Behavior:

- If value = 0 → remove node if it exists
- If node exists → update value
- If node does not exist → insert new node
- Maintains sorted order
- Updates `nz`

---

### `save_tuples()`

Saves matrix back to file.

Responsibilities:

- Traverse linked list
- Write in row-major order
- Output format matches input spec

---

### `add_tuples()`

Adds two sparse matrices.

Returns a new matrix:

```
C = A + B
```

Approach:

- Traverse non-zero nodes of A
- Insert into C
- Traverse non-zero nodes of B
- Accumulate values in C

Returns `NULL` if dimensions mismatch.

---

### `destroy_tuples()`

Frees all memory.

Responsibilities:

- Free every node
- Free matrix structure
- Prevent memory leaks

---

## Concepts Used

- C programming
- Linked lists
- Dynamic memory allocation
- Sparse data structures
- File I/O
- Data structure manipulation
- Memory management
- Algorithm optimization for sparse data

---

## Why Sparse Matrices?

Instead of storing:

```
1000 x 1000 = 1,000,000 values
```

We only store non-zero values, which can be drastically fewer:

```
~O(k) where k << n*m
```

This saves:
- Memory
- Computation time
- Processing overhead

---

## Project Structure

```text
sparsemat.c     -> implementation
sparsemat.h     -> definitions
main.c          -> driver program
cmp_mat.o       -> matrix comparison utilities
Makefile        -> build system
matrices/       -> input/output test files
```

---

## Build Instructions

Clean build:

```bash
make clean
```

Compile:

```bash
make
```

---

## Running the Program

Run:

```bash
./mp10
```

Save output:

```bash
./mp10 > matrices/output_mats/mp10_output.txt
```

Compare with reference:

```bash
diff matrices/output_mats/mp10_output.txt matrices/output_mats/gold/mp10_output.txt
```

---

## Testing Individual Outputs

Example:

```bash
diff matrices/output_mats/a_Ct.txt matrices/output_mats/gold/a_Ct.txt
```

---

## Debugging Tips

- Always initialize pointers to `NULL`
- Watch for segmentation faults during list traversal
- Use `valgrind` to detect memory leaks
- Ensure correct linked list ordering (row-major)
- Carefully handle duplicate entries in `load_tuples`

---

## Skills Demonstrated

- Sparse data structures
- Linked list manipulation
- Dynamic memory management
- File parsing and serialization
- Algorithm optimization
- Pointer-heavy C programming
- Matrix operations without dense storage
- Debugging memory issues
