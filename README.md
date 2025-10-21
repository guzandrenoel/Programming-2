# Programming 2 - C Language

This repository contains my comprehensive notes, code examples, and learning materials for **Programming 2** using the **C language**.  
It continues from Programming 1, focusing on **structures**, **pointers**, **dynamic memory**, and **data structures**.

---

## Topics Covered

### Foundation Refreshers
- **00a-ctype-functions.md** — Character analysis and transformation using `<ctype.h>` (`isalpha()`, `isdigit()`, `toupper()`, etc.)

---

### Structures and Data Types (01–06)

| File | Topic |
|------|--------|
| **01-structures-basics.md** | Defining and declaring `struct` |
| **02-typedef-and-aliases.md** | Simplifying struct names using `typedef` |
| **03-structure-initialization.md** | Initializing structure members |
| **04-structures-functions-pointers.md** | Passing structs by value and by reference |
| **05-arrays-and-nested-structures.md** | Using arrays inside structs and nested structures |
| **06-unions-and-enums.md** | Memory sharing with `union` and defining constants with `enum` |

---

### Pointers and Dynamic Memory (07–08)

| File | Topic |
|------|--------|
| **07-struct-pointers.md** | Accessing struct members using pointers and the `->` operator |
| **08-dynamic-memory.md** | Using `malloc()`, `calloc()`, and `free()` for struct and array allocation |

---

### Arrays of Structures and Record Management (09–12)

| File | Topic |
|------|--------|
| **09-array-of-structs.md** | Managing multiple records using arrays of structs |
| **10-search-in-structs.md** | Searching records by ID, name, or field |
| **11-update-delete-structs.md** | Updating and deleting struct records |
| **12-sorting-algorithms.md** | Sorting records using Bubble, Selection, and Insertion Sort |

---

### Linked Lists (13–15)

| File | Topic |
|------|--------|
| **13-linkedlist-basics.md** | Understanding nodes, pointers, and traversal |
| **14-linkedlist-insert-delete.md** | Inserting and deleting nodes in a linked list |
| **15-linkedlist-full.md** | Complete menu-driven linked list implementation (create, search, delete, and display) |

---

## How to Use This Repository

1. **Study Notes** – Follow the numbered `.md` files in order for progressive learning  
2. **Review Code** – Check the examples inside each topic for syntax and logic  
3. **Compile and Run** – Use a C compiler (e.g., GCC) to test the examples  

---

## Compilation Instructions

```bash
# Compile a C program
gcc program.c -o program

# Run the compiled program
./program
