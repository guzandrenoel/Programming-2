# Complete Linked List Implementation

## Overview

This comprehensive example combines all linked list operations into a single, functional program with a menu-driven interface. This demonstrates how linked lists work in a real-world scenario.

---

## Complete Linked List Program

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *next;
};

// Function prototypes
void insertAtBeginning(struct Node **head_ref, int new_data);
void insertAtEnd(struct Node **head_ref, int new_data);
void insertAfter(struct Node *prev_node, int new_data);
void deleteNode(struct Node **head_ref, int key);
void deleteAtBeginning(struct Node **head_ref);
void deleteAtEnd(struct Node **head_ref);
void displayList(struct Node *node);
int searchNode(struct Node *head, int key);
int getListSize(struct Node *head);

int main() {
    struct Node *head = NULL;
    int choice, value, position, searchValue;
    
    printf("=== Linked List Operations ===\n");
    
    do {
        printf("\nMenu:\n");
        printf("1. Insert at beginning\n");
        printf("2. Insert at end\n");
        printf("3. Insert after value\n");
        printf("4. Delete by value\n");
        printf("5. Delete at beginning\n");
        printf("6. Delete at end\n");
        printf("7. Display list\n");
        printf("8. Search value\n");
        printf("9. Get list size\n");
        printf("0. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        
        switch(choice) {
            case 1:
                printf("Enter value to insert: ");
                scanf("%d", &value);
                insertAtBeginning(&head, value);
                printf("Inserted %d at beginning\n", value);
                break;
                
            case 2:
                printf("Enter value to insert: ");
                scanf("%d", &value);
                insertAtEnd(&head, value);
                printf("Inserted %d at end\n", value);
                break;
                
            case 3:
                printf("Enter value to insert after: ");
                scanf("%d", &position);
                printf("Enter new value: ");
                scanf("%d", &value);
                // Find the node with the given value
                struct Node *temp = head;
                while(temp != NULL && temp->data != position) {
                    temp = temp->next;
                }
                if(temp != NULL) {
                    insertAfter(temp, value);
                    printf("Inserted %d after %d\n", value, position);
                } else {
                    printf("Value %d not found in list\n", position);
                }
                break;
                
            case 4:
                printf("Enter value to delete: ");
                scanf("%d", &value);
                deleteNode(&head, value);
                break;
                
            case 5:
                deleteAtBeginning(&head);
                printf("Deleted first node\n");
                break;
                
            case 6:
                deleteAtEnd(&head);
                printf("Deleted last node\n");
                break;
                
            case 7:
                printf("Linked List: ");
                displayList(head);
                break;
                
            case 8:
                printf("Enter value to search: ");
                scanf("%d", &searchValue);
                if(searchNode(head, searchValue)) {
                    printf("Value %d found in list\n", searchValue);
                } else {
                    printf("Value %d not found in list\n", searchValue);
                }
                break;
                
            case 9:
                printf("List size: %d\n", getListSize(head));
                break;
                
            case 0:
                printf("Exiting program\n");
                break;
                
            default:
                printf("Invalid choice! Please try again.\n");
        }
    } while(choice != 0);
    
    // Free all remaining nodes before exit
    while(head != NULL) {
        deleteAtBeginning(&head);
    }
    
    return 0;
}

// Insert at beginning
void insertAtBeginning(struct Node **head_ref, int new_data) {
    struct Node *new_node = (struct Node*) malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = *head_ref;
    *head_ref = new_node;
}

// Insert at end
void insertAtEnd(struct Node **head_ref, int new_data) {
    struct Node *new_node = (struct Node*) malloc(sizeof(struct Node));
    struct Node *last = *head_ref;
    
    new_node->data = new_data;
    new_node->next = NULL;
    
    if(*head_ref == NULL) {
        *head_ref = new_node;
        return;
    }
    
    while(last->next != NULL) {
        last = last->next;
    }
    
    last->next = new_node;
}

// Insert after a given node
void insertAfter(struct Node *prev_node, int new_data) {
    if(prev_node == NULL) {
        printf("Previous node cannot be NULL\n");
        return;
    }
    
    struct Node *new_node = (struct Node*) malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = prev_node->next;
    prev_node->next = new_node;
}

// Delete node by value
void deleteNode(struct Node **head_ref, int key) {
    struct Node *temp = *head_ref, *prev = NULL;
    
    if(temp != NULL && temp->data == key) {
        *head_ref = temp->next;
        free(temp);
        printf("Deleted %d from list\n", key);
        return;
    }
    
    while(temp != NULL && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }
    
    if(temp == NULL) {
        printf("Value %d not found in list\n", key);
        return;
    }
    
    prev->next = temp->next;
    free(temp);
    printf("Deleted %d from list\n", key);
}

// Delete first node
void deleteAtBeginning(struct Node **head_ref) {
    if(*head_ref == NULL) {
        printf("List is empty\n");
        return;
    }
    
    struct Node *temp = *head_ref;
    *head_ref = (*head_ref)->next;
    free(temp);
}

// Delete last node
void deleteAtEnd(struct Node **head_ref) {
    if(*head_ref == NULL) {
        printf("List is empty\n");
        return;
    }
    
    struct Node *temp = *head_ref;
    
    if(temp->next == NULL) {
        free(temp);
        *head_ref = NULL;
        return;
    }
    
    while(temp->next->next != NULL) {
        temp = temp->next;
    }
    
    free(temp->next);
    temp->next = NULL;
}

// Display the linked list
void displayList(struct Node *node) {
    while(node != NULL) {
        printf("%d -> ", node->data);
        node = node->next;
    }
    printf("NULL\n");
}

// Search for a value in the list
int searchNode(struct Node *head, int key) {
    struct Node *current = head;
    while(current != NULL) {
        if(current->data == key) {
            return 1;
        }
        current = current->next;
    }
    return 0;
}

// Get the size of the list
int getListSize(struct Node *head) {
    int count = 0;
    struct Node *current = head;
    while(current != NULL) {
        count++;
        current = current->next;
    }
    return count;
}

```

### Sample Program Output

```
=== Linked List Operations ===

Menu:
1. Insert at beginning
2. Insert at end
3. Insert after value
4. Delete by value
5. Delete at beginning
6. Delete at end
7. Display list
8. Search value
9. Get list size
0. Exit
Enter your choice: 1
Enter value to insert: 10
Inserted 10 at beginning

Enter your choice: 2
Enter value to insert: 30
Inserted 30 at end

Enter your choice: 3
Enter value to insert after: 10
Enter new value: 20
Inserted 20 after 10

Enter your choice: 7
Linked List: 10 -> 20 -> 30 -> NULL

Enter your choice: 8
Enter value to search: 20
Value 20 found in list

Enter your choice: 9
List size: 3

Enter your choice: 4
Enter value to delete: 20
Deleted 20 from list

Enter your choice: 7
Linked List: 10 -> 30 -> NULL

Enter your choice: 0
Exiting program

```

---

## Key Features Demonstrated

| Feature            | Implementation                              |
|--------------------|----------------------------------------------|
| Complete CRUD      | Create, Read, Update, Delete operations      |
| Menu Interface     | User-friendly interactive menu               |
| Error Handling     | Checks for empty list, invalid operations    |
| Memory Management  | Proper allocation and freeing of nodes       |
| Search Function    | Find if value exists in list                 |
| Size Counter       | Track number of elements in list             |

---

## Learning Outcomes

- Practical Implementation: See how all linked list concepts work together

- Memory Management: Proper use of malloc() and free()

- User Interaction: Building interactive programs with menus

- Error Handling: Dealing with edge cases and invalid operations

- Code Organization: Structuring code with clear functions and prototypes