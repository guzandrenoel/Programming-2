# Linked List Basics in C

## Overview

Arrays store elements in **contiguous memory** (all elements placed next to each other), but they have a **fixed size** — once declared, their size cannot change.

A **linked list** solves this by using **nodes** connected by **pointers**. Each node is created dynamically, allowing the list to grow or shrink as needed.

---

## 1. What is a Linked List?

A **linked list** is a sequence of elements (called **nodes**) where each node contains:
- **Data** (e.g., a number, string, or structure)
- A **pointer** to the next node in the list

Unlike arrays, nodes in a linked list are **not stored next to each other** in memory — they can be anywhere, connected by pointers.

---

## 2. Declaring a Node Structure

Each node is represented using a `struct`:

```c
struct Node {
    int data;            // Stores the actual data (number, string, etc.)
    struct Node *next;   // Pointer to the next node in the list
};

```

Think of each node as a box that holds:

- Your data

- The address of the next box

---

## 3. Creating a Linked List Step by Step

Let's create a linked list with three nodes containing values 10, 20, and 30.

### Step 1: Create Pointer Variables

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *next;
};

int main() {
    // Create pointers to hold addresses of our nodes
    struct Node *head = NULL;       // Points to FIRST node - the "head" of list
    struct Node *second = NULL;     // Points to second node
    struct Node *third = NULL;      // Points to third node

```

### Step 2: Allocate Memory for Each Node

```c
    // Create actual nodes in memory using malloc()
    head = (struct Node*) malloc(sizeof(struct Node));
    second = (struct Node*) malloc(sizeof(struct Node));
    third = (struct Node*) malloc(sizeof(struct Node));

```

### Step 3: Store Data in Each Node

```c
    // Put data into each node using arrow operator
    head->data = 10;     // Store 10 in head node
    second->data = 20;   // Store 20 in second node
    third->data = 30;    // Store 30 in third node

```

### Step 4: Connect the Nodes

```c
    // Link the nodes together to form the chain
    head->next = second;   // Head node points to second node
    second->next = third;  // Second node points to third node
    third->next = NULL;    // Third node points to NULL (end of list)

```

### Step 5: Complete Creation Code

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *next;
};

int main() {
    struct Node *head = NULL;
    struct Node *second = NULL;
    struct Node *third = NULL;

    // Allocate memory
    head = (struct Node*) malloc(sizeof(struct Node));
    second = (struct Node*) malloc(sizeof(struct Node));
    third = (struct Node*) malloc(sizeof(struct Node));

    // Assign data
    head->data = 10;
    second->data = 20;
    third->data = 30;

    // Connect nodes
    head->next = second;
    second->next = third;
    third->next = NULL;

    return 0;
}

```

---

## 4. Understanding the Pointer Variables
What are head, second, and third?

- head → Pointer to the FIRST node (the "head" of the list)

- second → Pointer to the second node

- third → Pointer to the third node

### Node Connection Table

| Pointer | Points To Node With | Next Points To |
| ------- | ------------------- | -------------- |
| head    | data: 10            | second         |
| second  | data: 20            | third          |
| third   | data: 30            | NULL           |

### Memory Visualization

| Pointer Variable | Memory Address | Node Contents | Points To |
|------------------|----------------|---------------|-----------|
| `head` | 0x1000 | [10 \| 0x2000] | → second node |
| `second` | 0x2000 | [20 \| 0x3000] | → third node |
| `third` | 0x3000 | [30 \| NULL] | → END OF LIST |

Key Insight:
- The head pointer is special — it’s our entry point to the entire list.
- If we lose head, we lose access to the whole list.

---

## 5. Traversing the Linked List

Traversal means visiting each node to access or display its data.

