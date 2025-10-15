# Managing Arrays of Structures (Dynamic Allocation)

## Overview

In many real-world programs, you often need to store **multiple records of structured data** — for example, multiple students, employees, or products.  

An **array of structures** lets you store many related structs under one variable, and using **dynamic allocation**, you can make the array size flexible (decided at runtime).

---

## 1. Static Array of Structures

You can create a fixed-size array of structures directly, like this:

```c
#include <stdio.h>

struct Student {
    int id;
    char name[30];
    float grade;
};

int main() {
    struct Student students[3] = {
        {1, "Andre", 89.5},
        {2, "Toni", 92.0},
        {3, "Noel", 85.0}
    };

    for (int i = 0; i < 3; i++)
        printf("%d. %s — %.2f\n", students[i].id, students[i].name, students[i].grade);

    return 0;
}

/* Output: 
1. Andre — 89.50
2. Toni — 92.00
3. Noel — 85.00
*/

```

## 2. Dynamic Array of Structures

To make the number of records variable, we use heap memory with malloc().

Steps:

- Ask the user how many records are needed.

- Allocate memory for that many structures.

- Accept data from the user.

- Display all records.

- Release memory with free().

```c

#include <stdio.h>
#include <stdlib.h>

struct Student {
    int id;
    char name[30];
    float grade;
};

int main() {
    int n;
    struct Student *students;

    printf("Enter number of students: ");
    scanf("%d", &n);

    if (n <= 0) {
        printf("Error: number must be positive!\n");
        return 1;
    }

    students = (struct Student*) malloc(n * sizeof(struct Student));

    if (students == NULL) {
        printf("Memory allocation failed!\n");
        return 1;
    }

    for (int i = 0; i < n; i++) {
        printf("\nStudent %d:\n", i + 1);
        printf("ID: ");
        scanf("%d", &students[i].id);
        printf("Name: ");
        scanf(" %[^\n]", students[i].name);
        printf("Grade: ");
        scanf("%f", &students[i].grade);
    }

    printf("\n--- Student Records ---\n");
    for (int i = 0; i < n; i++)
        printf("%d. %s — %.2f\n", students[i].id, students[i].name, students[i].grade);

    free(students);
    return 0;
}

/* Output: 
Enter number of students: 2

Student 1:
ID: 101
Name: Andre
Grade: 90.5

Student 2:
ID: 102
Name: Toni
Grade: 92.0

--- Student Records ---
101. Andre — 90.50
102. Toni — 92.00
*/

```

## 3. Explanation

| Concept                  | Description                                    |
| ------------------------ | ---------------------------------------------- |
| `malloc()`               | Allocates memory for `n` students dynamically. |
| `sizeof(struct Student)` | Ensures correct memory size for each record.   |
| `students[i]`            | Accesses each record using array indexing.     |
| `free(students)`         | Prevents memory leaks.                         |


## 4. Practical Notes

- Always check if malloc() returned NULL.

- Always free() dynamically allocated arrays after use.

- You can later resize the array with realloc() if you want to add more records.

- Use scanf(" %[^\n]", str) to safely read names with spaces.

## 5. Quick Summary

| Task                       | Static Array | Dynamic Array |
| -------------------------- | ------------ | ------------- |
| Size known at compile time | ✅            | ❌             |
| Size decided at runtime    | ❌            | ✅             |
| Memory location            | Stack        | Heap          |
| Must call `free()`         | ❌            | ✅             |
