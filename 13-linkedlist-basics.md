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

### What are `head`, `second`, and `third`?
- **`head`** = Pointer to the FIRST node (the "head" of the list)
- **`second`** = Pointer to the second node  
- **`third`** = Pointer to the third node

### Linked List Structure Overview

| Pointer Variable | Memory Address | Data | Next Points To | Description |
|------------------|----------------|------|----------------|-------------|
| `head` | 0x1000 | 10 | 0x2000 | First node, points to second |
| `second` | 0x2000 | 20 | 0x3000 | Second node, points to third |
| `third` | 0x3000 | 30 | NULL | Last node, marks end of list |

### Visual Flow:

head (0x1000) → [10 | 0x2000] → second (0x2000) → [20 | 0x3000] → third (0x3000) → [30 | NULL]

Key Insight:
- The head pointer is special — it’s our entry point to the entire list.
- If we lose head, we lose access to the whole list.

---

## 5. Traversing the Linked List

Traversal means visiting each node to access or display its data.

```c
void printList(struct Node *n) {
    // Start from the given node (usually head)
    while (n != NULL) {
        printf("%d -> ", n->data);
        n = n->next;  // Move to next node
    }
    printf("NULL\n");
}

```

### Using the Traversal Function

```c
int main() {
    // ... [linked list creation code from above] ...
    
    printf("Linked List Elements:\n");
    printList(head);  // Start traversal from head

    return 0;
}

```

### Traversal Steps

| Step | Current Node | Data Printed | Next Pointer Moves To |
| ---- | ------------ | ------------ | --------------------- |
| 1    | head         | 10           | second                |
| 2    | second       | 20           | third                 |
| 3    | third        | 30           | NULL                  |

When next becomes NULL, we’ve reached the end of the list.

## Complete Example with Memory Management

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *next;
};

// Function to print all nodes
void printList(struct Node *n) {
    while (n != NULL) {
        printf("%d -> ", n->data);
        n = n->next;
    }
    printf("NULL\n");
}

int main() {
    struct Node *head = NULL;
    struct Node *second = NULL;
    struct Node *third = NULL;

    // Allocate memory for 3 nodes
    head = (struct Node*) malloc(sizeof(struct Node));
    second = (struct Node*) malloc(sizeof(struct Node));
    third = (struct Node*) malloc(sizeof(struct Node));

    // Check if allocation succeeded
    if (head == NULL || second == NULL || third == NULL) {
        printf("Memory allocation failed!\n");
        return 1;
    }

    // Assign data and link them
    head->data = 10;
    head->next = second;

    second->data = 20;
    second->next = third;

    third->data = 30;
    third->next = NULL;

    printf("Linked List:\n");
    printList(head);

    // Free allocated memory
    free(head);
    free(second);
    free(third);

    return 0;
}

/* Output: 
Linked List:
10 -> 20 -> 30 -> NULL
*/

```

---

## Why Use Linked Lists?

| Feature      | Array                      | Linked List                  |
| ------------ | -------------------------- | ---------------------------- |
| Memory       | Fixed size                 | Grows dynamically            |
| Insertion    | Expensive (shift elements) | Easy (adjust pointers)       |
| Access       | Fast (indexing)            | Slower (traverse from start) |
| Deletion     | Expensive (shift elements) | Easy (unlink a node)         |
| Memory Usage | Predictable                | Extra memory for pointers    |

Summary:

- Arrays are better for fast random access and fixed-size data.

- Linked lists are better for flexible memory and dynamic data structures.

---

## Common Mistakes to Avoid

1. Forgetting to set last node’s next to NULL
```c
third->next = NULL;  // Don't forget this!

```

2. Not checking if malloc() returned NULL
```c
head = malloc(sizeof(struct Node));
if (head == NULL) {
    printf("Memory allocation failed!\n");
    return 1;
}

```

3. Losing the head pointer
```c
// Always keep track of your head!
struct Node *current = head;  // Use temp for traversal
while (current != NULL) {
    printf("%d ", current->data);
    current = current->next;  // Don't move head!
}

```

4. Forgetting to free memory
```c
free(head);    
free(second);
free(third);

```

## Key Points

- Each node has data and a pointer to the next.

- The head pointer always points to the first node — don’t lose it.

- Use malloc() to dynamically allocate memory.

- Use free() to release memory and prevent leaks.

- Use loops to traverse and display all elements.

- End of list is marked with NULL.

- Use the arrow operator -> to access struct members through pointers.

- Nodes can be anywhere in memory — connected by pointers, not physical order.