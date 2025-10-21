# Insertion and Deletion in Linked Lists

## Overview

Now that you understand how a linked list is formed, the next step is learning how to **add** (insert) and **remove** (delete) nodes.

A linked list is flexible — you can insert or delete elements **anywhere** by adjusting pointers. However, it’s important to manage these pointers properly to avoid losing access to nodes or creating memory leaks.

---

## 1. Inserting Nodes

There are **three main positions** where insertion can occur:

| Type | Description |
|------|--------------|
| Insert at Beginning | Adds a new node before the current head |
| Insert in the Middle (After a Node) | Adds a node between existing nodes |
| Insert at End | Adds a new node after the last node |

---

### A. Insert at the Beginning

We create a new node and make it point to the current head, then update the head pointer.

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *next;
};

// Insert a new node at the beginning
void insertAtBeginning(struct Node **head_ref, int new_data) {
    // Step 1: Allocate memory
    struct Node *new_node = (struct Node*) malloc(sizeof(struct Node));

    // Step 2: Assign data
    new_node->data = new_data;

    // Step 3: Make new node point to current head
    new_node->next = *head_ref;

    // Step 4: Move head to point to new node
    *head_ref = new_node;
}

// Print the list
void printList(struct Node *n) {
    while (n != NULL) {
        printf("%d -> ", n->data);
        n = n->next;
    }
    printf("NULL\n");
}

int main() {
    struct Node *head = NULL;

    insertAtBeginning(&head, 30);
    insertAtBeginning(&head, 20);
    insertAtBeginning(&head, 10);

    printf("Linked List after insertions:\n");
    printList(head);

    return 0;
}

/* Output:  
Linked List after insertions:
10 -> 20 -> 30 -> NULL
*/

```

| Step | Action    | List                   |
| ---- | --------- | ---------------------- |
| 1    | Insert 30 | 30 -> NULL             |
| 2    | Insert 20 | 20 -> 30 -> NULL       |
| 3    | Insert 10 | 10 -> 20 -> 30 -> NULL |

---

### B. Insert After a Given Node

Sometimes you may want to insert after a specific node, not just at the start or end.

```c
int main() {
    struct Node *head = NULL;
    struct Node *second = NULL;
    struct Node *third = NULL;

    head = (struct Node*) malloc(sizeof(struct Node));
    second = (struct Node*) malloc(sizeof(struct Node));
    third = (struct Node*) malloc(sizeof(struct Node));

    head->data = 10; head->next = second;
    second->data = 20; second->next = third;
    third->data = 30; third->next = NULL;

    printf("Before insertion:\n");
    printList(head);

    insertAfter(second, 25);

    printf("After inserting 25 after 20:\n");
    printList(head);

    return 0;
}

/*
Before insertion:
10 -> 20 -> 30 -> NULL
After inserting 25 after 20:
10 -> 20 -> 25 -> 30 -> NULL
*/

```

---

### C. Insert at the End

To insert a node at the end, traverse the list until the last node (where next == NULL), then connect the new node.

```c
void insertAtEnd(struct Node **head_ref, int new_data) {
    struct Node *new_node = (struct Node*) malloc(sizeof(struct Node));
    struct Node *last = *head_ref;

    new_node->data = new_data;
    new_node->next = NULL;

    // If list is empty, new node becomes head
    if (*head_ref == NULL) {
        *head_ref = new_node;
        return;
    }

    // Traverse until last node
    while (last->next != NULL)
        last = last->next;

    // Link last node to new node
    last->next = new_node;
}

```

### Example Use

```c
int main() {
    struct Node *head = NULL;

    insertAtEnd(&head, 10);
    insertAtEnd(&head, 20);
    insertAtEnd(&head, 30);

    printf("Linked List after insertions at end:\n");
    printList(head);

    return 0;
}

/*
Linked List after insertions at end:
10 -> 20 -> 30 -> NULL
*/

```

---

## 2. Deleting Nodes

There are **three common deletion cases**:

| Type                | Description                      |
| ------------------- | -------------------------------- |
| Delete at Beginning | Remove the first node            |
| Delete by Value     | Remove a node with specific data |
| Delete at End       | Remove the last node             |

---

### A. Delete the First Node

```c
void deleteAtBeginning(struct Node **head_ref) {
    if (*head_ref == NULL) {
        printf("List is empty.\n");
        return;
    }

    struct Node *temp = *head_ref;
    *head_ref = (*head_ref)->next;
    free(temp);
}

```

### Example

```c
int main() {
    struct Node *head = NULL;

    insertAtEnd(&head, 10);
    insertAtEnd(&head, 20);
    insertAtEnd(&head, 30);

    printf("Before deletion:\n");
    printList(head);

    deleteAtBeginning(&head);

    printf("After deleting first node:\n");
    printList(head);

    return 0;
}

/*
Before deletion:
10 -> 20 -> 30 -> NULL
After deleting first node:
20 -> 30 -> NULL
*/

```

---

### B. Delete by Value

```c
void deleteByValue(struct Node **head_ref, int key) {
    struct Node *temp = *head_ref, *prev = NULL;

    // If head node itself holds the key
    if (temp != NULL && temp->data == key) {
        *head_ref = temp->next;
        free(temp);
        return;
    }

    // Search for the key
    while (temp != NULL && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }

    // If key not found
    if (temp == NULL) return;

    // Unlink the node
    prev->next = temp->next;
    free(temp);
}

/*
Before deletion:
10 -> 20 -> 30 -> NULL
After deleting 20:
10 -> 30 -> NULL
*/

```

---

### C. Delete the Last Node

```c
void deleteAtEnd(struct Node **head_ref) {
    if (*head_ref == NULL) {
        printf("List is empty.\n");
        return;
    }

    struct Node *second_last = *head_ref;

    // If there is only one node
    if (second_last->next == NULL) {
        free(second_last);
        *head_ref = NULL;
        return;
    }

    // Traverse to the second last node
    while (second_last->next->next != NULL)
        second_last = second_last->next;

    // Delete last node
    free(second_last->next);
    second_last->next = NULL;
}

```

### Example

```c
int main() {
    struct Node *head = NULL;

    insertAtEnd(&head, 10);
    insertAtEnd(&head, 20);
    insertAtEnd(&head, 30);

    printf("Before deletion:\n");
    printList(head);

    deleteAtEnd(&head);

    printf("After deleting last node:\n");
    printList(head);

    return 0;
}

/*
Before deletion:
10 -> 20 -> 30 -> NULL
After deleting last node:
10 -> 20 -> NULL
*/

```

---

## 3. Summary Table

| Operation           | Description             | Example Result       |
| ------------------- | ----------------------- | -------------------- |
| Insert at Beginning | Add before current head | 5 -> 10 -> 20        |
| Insert After Node   | Add after given node    | 10 -> 20 -> 25 -> 30 |
| Insert at End       | Add at the tail         | 10 -> 20 -> 30 -> 40 |
| Delete at Beginning | Remove first node       | 20 -> 30             |
| Delete by Value     | Remove specific data    | 10 -> 30             |
| Delete at End       | Remove last node        | 10 -> 20             |

---

## 4. Key Takeaways

- Inserting or deleting in a linked list only needs pointer adjustments — no shifting elements like arrays.

- Always check for NULL pointers before accessing or freeing nodes.

- Use free() to release deleted node memory.

- Losing the head pointer means losing the entire list.

- Mastering insertion and deletion builds the foundation for stacks, queues, and linked structures.