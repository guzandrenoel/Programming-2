# Updating and Deleting Records in Struct Arrays

## Overview

When managing multiple records using **arrays of structures**, you will often need to:

- **Update** a record → change stored data  
- **Delete** a record → remove an entry and shift others to fill the gap

These operations are essential for handling small databases such as lists of students, employees, or products.

---

## Example Structure

```c
#include <stdio.h>
#include <string.h>

struct Student {
    int id;
    char name[30];
    float grade;
};

```

---

## Input and Display

```c
void inputStudents(struct Student s[], int count) {
    for (int i = 0; i < count; i++) {
        printf("Enter details for student %d:\n", i + 1);
        printf("ID: ");
        scanf("%d", &s[i].id);
        printf("Name: ");
        scanf(" %[^\n]", s[i].name);
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
    for (int i = 0; i < count; i++) {
        if (s[i].id == id) {
            s[i].grade = newGrade;
            printf("%s's grade updated to %.1f!\n", s[i].name, newGrade);
            return;
        }
    }
    printf("Student with ID %d not found.\n", id);
}

```

---

## Deleting a Record

We can delete a record by shifting the remaining elements to the left:

```c
int deleteStudent(struct Student s[], int count, int id) {
    for (int i = 0; i < count; i++) {
        if (s[i].id == id) {
            for (int j = i; j < count - 1; j++) {
                s[j] = s[j + 1];
            }
            printf("Student with ID %d has been removed.\n", id);
            return count - 1;
        }
    }
    printf("Student with ID %d not found.\n", id);
    return count;
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
        printf("Enter details for student %d:\n", i + 1);
        printf("ID: ");
        scanf("%d", &s[i].id);
        printf("Name: ");
        scanf(" %[^\n]", s[i].name);
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

void updateGrade(struct Student s[], int count, int id, float newGrade) {
    for (int i = 0; i < count; i++) {
        if (s[i].id == id) {
            s[i].grade = newGrade;
            printf("%s's grade updated to %.1f!\n", s[i].name, newGrade);
            return;
        }
    }
    printf("Student with ID %d not found.\n", id);
}

int deleteStudent(struct Student s[], int count, int id) {
    for (int i = 0; i < count; i++) {
        if (s[i].id == id) {
            for (int j = i; j < count - 1; j++) {
                s[j] = s[j + 1];
            }
            printf("Student with ID %d has been removed.\n", id);
            return count - 1;
        }
    }
    printf("Student with ID %d not found.\n", id);
    return count;
}

int main() {
    int count = 3;
    struct Student students[count];

    printf("Enter 3 students:\n");
    inputStudents(students, count);

    printf("\nInitial Records:\n");
    displayStudents(students, count);

    int updateID;
    float newGrade;
    printf("\nEnter ID of student to update: ");
    scanf("%d", &updateID);
    printf("Enter new grade: ");
    scanf("%f", &newGrade);
    updateGrade(students, count, updateID, newGrade);

    int deleteID;
    printf("\nEnter ID of student to delete: ");
    scanf("%d", &deleteID);
    count = deleteStudent(students, count, deleteID);

    printf("\nUpdated Records:\n");
    displayStudents(students, count);

    return 0;
}

/*
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

Enter ID of student to update: 3
Enter new grade: 82
Koby's grade updated to 82.0!

Enter ID of student to delete: 2
Student with ID 2 has been removed.

Updated Records:
ID	Name	Grade
-----------------------
1	Andre	89.5
3	Koby	82.0
*/

```

## Visual Representations

### Before Update

| Index | 0     | 1    | 2    |
| ----- | ----- | ---- | ---- |
| ID    | 1     | 2    | 3    |
| Name  | Andre | Toni | Koby |
| Grade | 89.5  | 92.3 | 76.8 |


### After Updating Koby

| Index | 0     | 1    | 2        |
| ----- | ----- | ---- | -------- |
| ID    | 1     | 2    | 3        |
| Name  | Andre | Toni | Koby     |
| Grade | 89.5  | 92.3 | **82.0** |


### After Deleting Toni

| Index | 0     | 1    |
| ----- | ----- | ---- |
| ID    | 1     | 3    |
| Name  | Andre | Koby |
| Grade | 89.5  | 82.0 |

---

## Summary

| Operation | Description                                  | Key Idea                             |
| --------- | -------------------------------------------- | ------------------------------------ |
| Update    | Change a record’s data (e.g., grade or name) | Search by ID and modify the field    |
| Delete    | Remove a record                              | Shift elements left and reduce count |
| Display   | Print all records                            | View current list after operations   |


