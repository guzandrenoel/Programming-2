# Sorting Algorithms in C (Using Struct Arrays)

## Overview

Sorting helps organize data in a logical order, making it easier to search and display.  
In C, sorting can be done on arrays of:
- **Primitive types** (like integers or floats)
- **Structures** (like students, employees, etc.)

In this lesson, we’ll explore **three basic sorting algorithms**:
1. **Bubble Sort**
2. **Selection Sort**
3. **Insertion Sort**

---

## Example Structure

We’ll reuse the familiar `Student` structure from previous lessons:

```c
struct Student {
    int id;
    char name[30];
    float grade;
};

```

---

## Helper Functions
What is a Helper Function?

A helper function is a small, reusable function that performs a specific task to make your main code cleaner and more organized.

### Display Helper Function

```c
void displayStudents(struct Student s[], int count) {
    printf("\nID\tName\tGrade\n");
    printf("-----------------------\n");
    for (int i = 0; i < count; i++) {
        printf("%d\t%s\t%.1f\n", s[i].id, s[i].name, s[i].grade);
    }
}

```

### Why use helper functions?

- Avoid code repetition

- Make main logic easier to read

- Easy to modify display format in one place

---

## 1. Bubble Sort
How It Works

Bubble Sort **repeatedly compares adjacent elements** and swaps them if they're in the wrong order.
Each pass "bubbles" the largest value to the end.

### Example: Sort Students by Grade (Ascending)

```c
#include <stdio.h>
#include <string.h>

struct Student {
    int id;
    char name[30];
    float grade;
};


void displayStudents(struct Student s[], int count) {
    printf("\nID\tName\tGrade\n");
    printf("-----------------------\n");
    for (int i = 0; i < count; i++) {
        printf("%d\t%s\t%.1f\n", s[i].id, s[i].name, s[i].grade);
    }
}

void bubbleSort(struct Student s[], int count) {
    struct Student temp;
    for (int i = 0; i < count - 1; i++) {
        for (int j = 0; j < count - i - 1; j++) {
            if (s[j].grade > s[j + 1].grade) {
                // Swap the students
                temp = s[j];
                s[j] = s[j + 1];
                s[j + 1] = temp;
            }
        }
    }
}

int main() {
    struct Student students[3] = {
        {1, "Andre", 89.5},
        {2, "Toni", 92.3},
        {3, "Koby", 76.8}
    };

    printf("Before Sorting:");
    displayStudents(students, 3);

    bubbleSort(students, 3);

    printf("\nAfter Sorting by Grade (Ascending):");
    displayStudents(students, 3);

    return 0;
}

/* Output:
Before Sorting:
ID	Name	Grade
-----------------------
1	Andre	89.5
2	Toni	92.3
3	Koby	76.8

After Sorting by Grade (Ascending):
ID	Name	Grade
-----------------------
3	Koby	76.8
1	Andre	89.5
2	Toni	92.3
*/

```

## Bubble Sort Visualization

| Pass | Comparison  | Swap? | Array Order (Grades) |
| ---- | ----------- | ----- | -------------------- |
| 1    | 89.5 > 92.3 | No    | [89.5, 92.3, 76.8]   |
| 1    | 92.3 > 76.8 | Yes   | [89.5, 76.8, 92.3]   |
| 2    | 89.5 > 76.8 | Yes   | [76.8, 89.5, 92.3]   |

Performance Note: Bubble sort becomes very slow with large datasets because it makes many comparisons and swaps.

---

## 2. Selection Sort
How It Works

Selection Sort divides the array into **sorted (left)** and **unsorted (right)** sections.
It repeatedly finds the smallest element from the unsorted section and moves it to the sorted section.

### Example: Sort Students by ID (Ascending)

```c
void selectionSort(struct Student s[], int count) {
    int minIndex;
    struct Student temp;

    for (int i = 0; i < count - 1; i++) {
        minIndex = i;  // Assume current element is smallest
        
        // Find actual smallest in unsorted section
        for (int j = i + 1; j < count; j++) {
            if (s[j].id < s[minIndex].id)
                minIndex = j;
        }
        
        // Swap if we found a smaller element
        if (minIndex != i) {
            temp = s[i];
            s[i] = s[minIndex];
            s[minIndex] = temp;
        }
    }
}

/* Output:
Before Sorting (by ID):
ID	Name	Grade
-----------------------
3	Koby	82.0
1	Andre	89.5
2	Toni	92.3

After Sorting by ID (Ascending):
ID	Name	Grade
-----------------------
1	Andre	89.5
2	Toni	92.3
3	Koby	82.0
*/

```

## Selection Sort Visualization

| Step | Minimum Found | Swap With | New Order (IDs) |
| ---- | ------------- | --------- | --------------- |
| 1    | ID 1          | ID 3      | [1, 3, 2]       |
| 2    | ID 2          | ID 3      | [1, 2, 3]       |

---

## 3. Insertion Sort
How It Works

Insertion Sort works like sorting playing cards —
you take one element at a time and insert it into its correct position in the already-sorted section.

### Example: Sort by Name (Alphabetical Order)

```c
void insertionSort(struct Student s[], int count) {
    struct Student key;
    int j;

    for (int i = 1; i < count; i++) {
        key = s[i];  // Element to insert
        j = i - 1;   // Start comparing with previous element

        // Shift elements greater than key to the right
        while (j >= 0 && strcmp(s[j].name, key.name) > 0) {
            s[j + 1] = s[j];
            j--;
        }
        s[j + 1] = key;  // Insert key in correct position
    }
}

/* Output:
Before Sorting (by Name):
ID	Name	Grade
-----------------------
1	Andre	89.5
2	Toni	92.3
3	Koby	82.0

After Sorting by Name (Alphabetical):
ID	Name	Grade
-----------------------
1	Andre	89.5
3	Koby	82.0
2	Toni	92.3
*/

```

## Insertion Sort Visualization

| Step | Key  | Compare With | New Order (Names)   |
| ---- | ---- | ------------ | ------------------- |
| 1    | Toni | Andre → Keep | [Andre, Toni, Koby] |
| 2    | Koby | Toni → Andre | [Andre, Koby, Toni] |

---

## Algorithm Comparison

| Algorithm          | Best For                       | Swaps  | Memory Used | Notes                        |
| ------------------ | ------------------------------ | ------ | ----------- | ---------------------------- |
| **Bubble Sort**    | Learning, small datasets       | Many   | Low         | Simplest to understand       |
| **Selection Sort** | When swaps are expensive       | Few    | Low         | Always finds minimum first   |
| **Insertion Sort** | Nearly-sorted data, small sets | Medium | Low         | Fast for already-sorted data |

---

## Complete Example with All Sorts

```c
#include <stdio.h>
#include <string.h>

struct Student {
    int id;
    char name[30];
    float grade;
};

// Helper function to display students
void displayStudents(struct Student s[], int count) {
    printf("\nID\tName\tGrade\n");
    printf("-----------------------\n");
    for (int i = 0; i < count; i++) {
        printf("%d\t%s\t%.1f\n", s[i].id, s[i].name, s[i].grade);
    }
}

// Bubble Sort - Sort by grade
void bubbleSortByGrade(struct Student s[], int count) {
    struct Student temp;
    for (int i = 0; i < count - 1; i++) {
        for (int j = 0; j < count - i - 1; j++) {
            if (s[j].grade > s[j + 1].grade) {
                temp = s[j];
                s[j] = s[j + 1];
                s[j + 1] = temp;
            }
        }
    }
}

// Selection Sort - Sort by ID
void selectionSortByID(struct Student s[], int count) {
    int minIndex;
    struct Student temp;
    
    for (int i = 0; i < count - 1; i++) {
        minIndex = i;
        for (int j = i + 1; j < count; j++) {
            if (s[j].id < s[minIndex].id)
                minIndex = j;
        }
        if (minIndex != i) {
            temp = s[i];
            s[i] = s[minIndex];
            s[minIndex] = temp;
        }
    }
}

// Insertion Sort - Sort by name
void insertionSortByName(struct Student s[], int count) {
    struct Student key;
    int j;
    
    for (int i = 1; i < count; i++) {
        key = s[i];
        j = i - 1;
        
        while (j >= 0 && strcmp(s[j].name, key.name) > 0) {
            s[j + 1] = s[j];
            j--;
        }
        s[j + 1] = key;
    }
}

int main() {
    // Create array of students
    struct Student students[4] = {
        {3, "Koby", 76.8},
        {1, "Andre", 89.5},
        {4, "Noel", 91.0},
        {2, "Toni", 92.3}
    };
    
    printf("=== ORIGINAL ARRAY ===");
    displayStudents(students, 4);
    
    // Test Bubble Sort (by grade)
    printf("\n=== BUBBLE SORT - BY GRADE ===");
    struct Student students1[4] = {{3, "Koby", 76.8}, {1, "Andre", 89.5}, {4, "Noel", 91.0}, {2, "Toni", 92.3}};
    bubbleSortByGrade(students1, 4);
    displayStudents(students1, 4);
    
    // Test Selection Sort (by ID)
    printf("\n=== SELECTION SORT - BY ID ===");
    struct Student students2[4] = {{3, "Koby", 76.8}, {1, "Andre", 89.5}, {4, "Noel", 91.0}, {2, "Toni", 92.3}};
    selectionSortByID(students2, 4);
    displayStudents(students2, 4);
    
    // Test Insertion Sort (by name)
    printf("\n=== INSERTION SORT - BY NAME ===");
    struct Student students3[4] = {{3, "Koby", 76.8}, {1, "Andre", 89.5}, {4, "Noel", 91.0}, {2, "Toni", 92.3}};
    insertionSortByName(students3, 4);
    displayStudents(students3, 4);
    
    return 0;
}

```

---

## Key Takeaways

- Sorting makes data more usable for display and searching

- Bubble Sort is the easiest to understand but slow for large data

- Selection Sort minimizes swaps but still slow for large data

- Insertion Sort is efficient for small or nearly-sorted data

- Helper functions keep your code organized and reusable

- All three algorithms work in-place (don’t need extra arrays)