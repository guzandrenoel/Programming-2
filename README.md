# Programming 2 - C Language

This repository contains my comprehensive notes, code examples, and learning materials for **Programming 2** using the C language.  
It continues from Programming 1, focusing on **structures, pointers, dynamic memory**, and **data structures**.

---

## 📚 Topics Covered

### Foundation Refreshers (00a–00b)
- **Character (ctype) Functions** – Using `<ctype.h>` for character analysis and transformation (`isalpha()`, `isdigit()`, `toupper()`, etc.)
- **2D Arrays** – Working with multi-dimensional arrays and nested loops

---

### Structures and Data Types (01–06)
- **Structures Basics** – Definition, declaration, and usage of `struct`
- **Typedef and Aliases** – Cleaner syntax using `typedef`
- **Structure Initialization** – Setting initial values for struct members
- **Structures in Functions and Pointers** – Passing structs by value and by reference
- **Arrays and Nested Structures** – Combining arrays within structs and nesting structures
- **Unions and Enums** – Memory sharing with `union` and defining named constants with `enum`

---

### Pointers and Dynamic Memory (07–08)
- **Struct Pointers** – Accessing members with pointers and the `->` operator
- **Dynamic Structs** – Using `malloc()`, `calloc()`, and `free()` to allocate structs on the heap

---

### Arrays of Structures (09–12)
- **Array of Structs** – Managing multiple records (e.g., list of students)
- **Searching in Structs** – Finding records by name, ID, or other fields
- **Update and Delete in Structs** – Modifying and removing records
- **Sorting Structs** – Sorting based on fields such as name or grade

---

### Linked Lists (13–15)
- **Linked List Basics** – Building self-referential structs for dynamic lists
- **Insert and Delete Operations** – Adding or removing nodes efficiently
- **Complete Linked List** – Menu-driven CRUD implementation as a capstone

---

## 🚀 How to Use This Repository

1. **Study Notes** – Follow the numbered `.md` files in order for progressive learning  
2. **Review Code** – Check the examples inside each topic for reference  
3. **Compile and Run** – Use a C compiler (e.g., GCC) to test sample programs  

---

## 💻 Compilation Instructions

```bash
# Compile a C program
gcc program.c -o program

# Run the compiled program
./program
