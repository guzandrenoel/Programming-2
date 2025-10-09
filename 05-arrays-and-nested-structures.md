# Structures with Arrays and Nested Structures

## Overview

Structures can be **grouped in arrays** to store multiple records of the same type.
They can also **contain other structures** as members (nested structures).

---

## 1. Arrays of Structures

You can create an array of structures to store multiple records of the same type (like a list of students or employees).

```c
#include <stdio.h>

typedef struct {
    char name[50];
    int age;
} Person;

int main() {
    Person people[3] = {
        {"Alice", 25},
        {"Bob", 30},
        {"Charlie", 35}
    };

    for (int i = 0; i < 3; i++) {
        printf("Person %d: %s, %d\n", i + 1, people[i].name, people[i].age);
    }

    return 0;
}

/* Output:
Person 1: Alice, 25
Person 2: Bob, 30
Person 3: Charlie, 35
*/

```

### Key Points:

- Useful when storing lists of similar data.

- Each element in the array is a full structure.

- Access using array[index].member.


## 2. Nested Structures

Structures can contain other structures as members — called nested structures.

```c
#include <stdio.h>

typedef struct {
    int day;
    int month;
    int year;
} Date;

typedef struct {
    char name[50];
    Date birthdate;  // Nested structure
    double salary;
} Employee;

int main() {
    Employee emp1 = {"John", {15, 8, 2004}, 50000.00};

    printf("Name: %s\n", emp1.name);
    printf("Birthdate: %d/%d/%d\n", 
           emp1.birthdate.day, 
           emp1.birthdate.month, 
           emp1.birthdate.year);
    printf("Salary: $%.2f\n", emp1.salary);

    return 0;
}

/* Output:
Name: John
Birthdate: 15/8/2004
Salary: $50000.00
*/

```

## Key Points:

- Nested structures allow hierarchical data.

- Access inner members using outer.inner.member.

- Makes large, organized data models possible (e.g., Student → Address → Date).


## 3. Initializing Nested Structures

You can use designated initializers for clarity.

```c
Employee emp2 = {
    .name = "Andre",
    .birthdate = {.day = 9, .month = 10, .year = 2025},
    .salary = 60000.00
};

```

This method improves readability and reduces initialization mistakes.


## 4. Why Use Nested and Array Structures?

- Organized data — keeps related information together
- Scalable — supports multiple entries easily
- Structured access — makes code cleaner and easier to maintain

## Summary

- Arrays of structures store multiple structured records efficiently.

- Nested structures enable grouping of complex, related data.

- Always use designated initializers and dot notation for readability.