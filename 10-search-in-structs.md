# Searching in Struct Arrays

## 1. Overview

Once you have a list or array of structures (like students or employees),  
you often need to **find a specific record** — for example, searching by ID, name, or grade.

Two common methods are:
- **Linear Search** — simple but slower (checks each record one by one)
- **Binary Search** — faster, but only works on *sorted* arrays

---

## 2. Linear Search

Linear search goes through each record until it finds a match.

### Example — Search Student by ID

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Student {
    int id;
    char name[30];
    float grade;
};

int main() {
    int n, searchID, found = 0;
    struct Student *students;

    printf("Enter number of students: ");
    scanf("%d", &n);

    students = (struct Student*) malloc(n * sizeof(struct Student));

    for (int i = 0; i < n; i++) {
        printf("\nStudent %d:\n", i + 1);
        printf("ID: ");
        scanf("%d", &students[i].id);
        printf("Name: ");
        scanf(" %[^\n]", students[i].name);
        printf("Grade: ");
        scanf("%f", &students[i].grade);
    }

    printf("\nEnter ID to search: ");
    scanf("%d", &searchID);

    for (int i = 0; i < n; i++) {
        if (students[i].id == searchID) {
            printf("\nRecord Found!\n");
            printf("ID: %d\nName: %s\nGrade: %.2f\n", students[i].id, students[i].name, students[i].grade);
            found = 1;
            break;
        }
    }

    if (!found)
        printf("No student found with ID %d\n", searchID);

    free(students);
    return 0;
}

```

- Advantages: Works even if data is unsorted.
- Disadvantages: Slow for large data sets.

---

## 3. Linear Search by Name

You can use the strcmp() function from <string.h> to compare strings.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Student {
    int id;
    char name[30];
    float grade;
};

int main() {
    int n, found = 0;
    char target[30];
    struct Student *students;

    printf("Enter number of students: ");
    scanf("%d", &n);
    students = (struct Student*) malloc(n * sizeof(struct Student));

    for (int i = 0; i < n; i++) {
        printf("\nStudent %d:\n", i + 1);
        printf("ID: ");
        scanf("%d", &students[i].id);
        printf("Name: ");
        scanf(" %[^\n]", students[i].name);
        printf("Grade: ");
        scanf("%f", &students[i].grade);
    }

    printf("\nEnter name to search: ");
    scanf(" %[^\n]", target);

    for (int i = 0; i < n; i++) {
        if (strcmp(students[i].name, target) == 0) {
            printf("\nRecord Found!\n");
            printf("ID: %d\nName: %s\nGrade: %.2f\n", students[i].id, students[i].name, students[i].grade);
            found = 1;
            break;
        }
    }

    if (!found)
        printf("No student found with name '%s'\n", target);

    free(students);
    return 0;
}

```

---

## 4. Binary Search (on Sorted Arrays)

Binary search repeatedly divides the array in half to find the target.
It only works if the array is sorted by ID.

### Example — Binary Search by ID

```c
#include <stdio.h>
#include <stdlib.h>

struct Student {
    int id;
    char name[30];
    float grade;
};

int binarySearch(struct Student arr[], int n, int key) {
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid].id == key)
            return mid;
        else if (arr[mid].id < key)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return -1;
}

int main() {
    struct Student students[4] = {
        {1001, "Andre", 89.5},
        {1002, "Noel", 91.0},
        {1003, "Toni", 92.5},
        {1004, "Kyle", 86.0}
    };

    int id, pos;
    printf("Enter student ID to search: ");
    scanf("%d", &id);

    pos = binarySearch(students, 4, id);

    if (pos != -1)
        printf("Found: %s (%.2f)\n", students[pos].name, students[pos].grade);
    else
        printf("Student ID %d not found.\n", id);

    return 0;
}

```

---

## 5. Comparison Summary

| Method        | Works on | Speed | Requires Sorted Data | Use Case       |
| ------------- | -------- | ----- | -------------------- | -------------- |
| Linear Search | Unsorted | Slow  | ❌                    | Small datasets |
| Binary Search | Sorted   | Fast  | ✅                    | Large datasets |

---

## 6. Key Takeaways

- Linear search → simple and flexible.

- Binary search → efficient but requires sorting first.

- Always validate input and memory allocations.

- strcmp() helps when comparing strings.