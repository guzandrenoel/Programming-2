# Updating and Deleting Records in Struct Arrays

## Overview

When managing multiple records using **arrays of structures**, you will often need to:

- **Update** a record → change stored data  
- **Delete** a record → remove an entry and shift others to fill the gap

These operations are essential for handling small databases such as lists of students, employees, or products.

---

## Example Structure

```c
struct Student {
    int id;           // Unique identifier
    char name[30];    // Student name
    float grade;      // Academic grade
};

```

---

## Input and Display function

```c
void inputStudents(struct Student s[], int count) {
    for (int i = 0; i < count; i++) {
        printf("Enter details for student %d:\n", i + 1);
        
        printf("ID: ");
        scanf("%d", &s[i].id);
        
        printf("Name: ");
        scanf(" %[^\n]", s[i].name);  // Space before % reads leftover newline
        
        printf("Grade: ");
        scanf("%f", &s[i].grade);
    }
}

void displayStudents(struct Student s[], int count) {
    printf("\nID\tName\tGrade\n");
    printf("-----------------------\n");
    for (int i = 0; i < count; i++) {
        printf("%d\t%s\t%.1f\n", s[i].id, s[i].name, s[i].grade);
    }
}

```

---

## Updating a Record

We’ll search for a student by ID and update their grade:

```c
void updateGrade(struct Student s[], int count, int id, float newGrade) {
    // Search through all students
    for (int i = 0; i < count; i++) {
        // Check if current student has the matching ID
        if (s[i].id == id) {
            // Update the grade
            s[i].grade = newGrade;
            printf("%s's grade updated to %.1f!\n", s[i].name, newGrade);
            return;  // Exit function after successful update
        }
    }
    // If we get here, no student was found with that ID
    printf("Student with ID %d not found.\n", id);
}

```

Key Points:

- We use linear search to find the student

- return stops the function once we find the student

- Always handle the "not found" case

---

## Deleting a Record

We can delete a record by shifting the remaining elements to the left:

```c
int deleteStudent(struct Student s[], int count, int id) {
    // Search for the student to delete
    for (int i = 0; i < count; i++) {
        if (s[i].id == id) {
            // Found the student! Now shift all subsequent elements left
            for (int j = i; j < count - 1; j++) {
                s[j] = s[j + 1];  // Copy next element to current position
            }
            printf("Student with ID %d has been removed.\n", id);
            return count - 1;  // Return new, smaller count
        }
    }
    // Student not found
    printf("Student with ID %d not found.\n", id);
    return count;  // Return original count (no change)
}

```

---

## Complete Program 

```c
#include <stdio.h>
#include <string.h>

struct Student {
    int id;
    char name[30];
    float grade;
};

void inputStudents(struct Student s[], int count) {
    for (int i = 0; i < count; i++) {
        printf("\nEnter details for student %d:\n", i + 1);
        
        printf("ID: ");
        scanf("%d", &s[i].id);
        
        printf("Name: ");
        scanf(" %[^\n]", s[i].name);
        
        printf("Grade: ");
        scanf("%f", &s[i].grade);
    }
}

void displayStudents(struct Student s[], int count) {
    if (count == 0) {
        printf("No students to display.\n");
        return;
    }
    
    printf("\nID\tName\tGrade\n");
    printf("-----------------------\n");
    for (int i = 0; i < count; i++) {
        printf("%d\t%s\t%.1f\n", s[i].id, s[i].name, s[i].grade);
    }
}

void updateGrade(struct Student s[], int count, int id, float newGrade) {
    for (int i = 0; i < count; i++) {
        if (s[i].id == id) {
            float oldGrade = s[i].grade;  // Store old value for message
            s[i].grade = newGrade;
            printf("%s's grade updated from %.1f to %.1f!\n", 
                   s[i].name, oldGrade, newGrade);
            return;
        }
    }
    printf("Error: Student with ID %d not found.\n", id);
}

int deleteStudent(struct Student s[], int count, int id) {
    for (int i = 0; i < count; i++) {
        if (s[i].id == id) {
            printf("Removing %s (ID: %d) from records...\n", s[i].name, id);
            
            // Shift all elements after the deletion point
            for (int j = i; j < count - 1; j++) {
                s[j] = s[j + 1];
            }
            
            return count - 1;  // Important: return new count
        }
    }
    printf("Error: Student with ID %d not found.\n", id);
    return count;
}

int main() {
    int count = 3;
    struct Student students[count];

    printf("=== Student Management System ===\n");
    printf("Enter %d students:\n", count);
    inputStudents(students, count);

    printf("\nInitial Records:");
    displayStudents(students, count);

    // Update a student's grade
    int updateID;
    float newGrade;
    printf("\nUpdate Operation");
    printf("\nEnter ID of student to update: ");
    scanf("%d", &updateID);
    printf("Enter new grade: ");
    scanf("%f", &newGrade);
    updateGrade(students, count, updateID, newGrade);

    // Delete a student
    int deleteID;
    printf("\nDelete Operation");
    printf("\nEnter ID of student to delete: ");
    scanf("%d", &deleteID);
    count = deleteStudent(students, count, deleteID);

    printf("\nUpdated Records:");
    displayStudents(students, count);

    return 0;
}

/*
=== Student Management System ===
Enter 3 students:

Enter details for student 1:
ID: 1
Name: Andre
Grade: 89.5

Enter details for student 2:
ID: 2
Name: Toni
Grade: 92.3

Enter details for student 3:
ID: 3
Name: Koby
Grade: 76.8

Initial Records:
ID	Name	Grade
-----------------------
1	Andre	89.5
2	Toni	92.3
3	Koby	76.8

Update Operation
Enter ID of student to update: 3
Enter new grade: 82
Koby's grade updated from 76.8 to 82.0!

Delete Operation
Enter ID of student to delete: 2
Removing Toni (ID: 2) from records...

Updated Records:
ID	Name	Grade
-----------------------
1	Andre	89.5
3	Koby	82.0
*/

```

## Visual Guide to Array Operations

### Initial State
| Index | ID | Name  | Grade | Address |
|-------|----|-------|-------|---------|
| 0     | 1  | Andre | 89.5  | 0x1000  |
| 1     | 2  | Toni  | 92.3  | 0x101C  |
| 2     | 3  | Koby  | 76.8  | 0x1038  |

**Count: 3**

### After Updating Koby's Grade
| Index | ID | Name  | Grade  | Address |
|-------|----|-------|--------|---------|
| 0     | 1  | Andre | 89.5   | 0x1000  |
| 1     | 2  | Toni  | 92.3   | 0x101C  |
| 2     | 3  | Koby  | **82.0** | 0x1038  |

**Count: 3**

### After Deleting Toni
| Index | ID | Name  | Grade | Address |
|-------|----|-------|-------|---------|
| 0     | 1  | Andre | 89.5  | 0x1000  |
| 1     | 3  | Koby  | 82.0  | 0x101C  |

**Count: 2**

### Delete Process Steps:
1. **Find**: Locate Toni at index 1 (address 0x101C)
2. **Shift**: Copy Koby from index 2 (0x1038) to index 1 (0x101C)
3. **Reduce**: Update count from 3 to 2

### Key Points:
- **Update**: Modifies data at same memory address
- **Delete**: Copies data to fill gaps, reduces active count
- **Memory**: Physical addresses remain allocated, logical size tracked by `count`
- **Address Calculation**: Each struct uses 28 bytes (4 + 30 + 4)


