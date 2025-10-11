# Pointers to Structures in C

## Overview

Pointers can point to **structures** just like any other variable.  
Using pointers with structures allows **direct access** and **modification** of data, especially when passing to functions or allocating dynamically.

The **arrow operator (`->`)** is used to access structure members through a pointer.

---

## 1. Declaring and Using Structure Pointers

```c
#include <stdio.h>

typedef struct {
    char name[20];
    int age;
} Person;

int main() {
    Person p = {"Noel", 21};
    Person *ptr = &p;

    // Accessing members using pointer
    printf("Name: %s\n", ptr->name);
    printf("Age: %d\n", ptr->age);

    return 0;
}

/* Output:
Name: Noel
Age: 21
*/

```

### Key Points

- Person *ptr = &p; → pointer to structure.

- ptr->member → shorthand for (*ptr).member.

- The arrow operator (->) improves readability and is the standard way to access struct members via pointer.


## 2. Dereference and Dot Operator (Alternative Way)

You can also use the dereference operator * with the dot operator .
But you must use parentheses, because the dot operator has higher precedence than *.

```c
#include <stdio.h>

typedef struct {
    char name[20];
    int age;
} Person;

int main() {
    Person person1 = {"Alice", 25};
    Person *ptr = &person1;

    (*ptr).age = 30;                    // Correct
    printf("Name: %s\n", (*ptr).name);
    printf("Age: %d\n", (*ptr).age);

    return 0;
}

/* Output:
Name: Alice
Age: 30
*/

```

Simplified Rule:
You need parentheses — *ptr.age ❌ is invalid because . takes priority over *.


## 3. Array of Structure Pointers

You can create an array of pointers to structures, useful for dynamic or large data sets.

```c
#include <stdio.h>

typedef struct {
    char name[20];
    int score;
} Student;

int main() {
    Student s1 = {"Andre", 90};
    Student s2 = {"Guz", 85};
    Student s3 = {"Noel", 95};

    Student *arr[3] = {&s1, &s2, &s3};

    for (int i = 0; i < 3; i++) {
        printf("Student %d: %s - %d\n", i + 1, arr[i]->name, arr[i]->score);
    }

    return 0;
}

/* Output:
Student 1: Andre - 90
Student 2: Guz - 85
Student 3: Noel - 95
*/

```

### Why Use This?

- Saves memory by storing pointers instead of full copies.

- Useful when dealing with dynamic allocation or linked structures.


## 4. Dynamic Allocation of Structures

We can allocate structure memory dynamically using malloc() or calloc().

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    char name[30];
    int age;
} Person;

int main() {
    Person *p1 = (Person *) malloc(sizeof(Person));

    strcpy(p1->name, "Andre");
    p1->age = 21;

    printf("Name: %s, Age: %d\n", p1->name, p1->age);

    free(p1); // release allocated memory
    return 0;
}

/* Output:
Name: Andre, Age: 21
*/

```

### Key Points

- malloc(sizeof(Person)) → allocates memory for one structure.

- Always free() dynamically allocated memory.

- Perfect for when you don’t know how many structures you’ll need at runtime.


## 5. Dynamic Array of Struct Pointers

Here’s how to manage multiple dynamic structures:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    char name[30];
    int score;
} Student;

int main() {
    int n = 3;
    Student *students = (Student *) malloc(n * sizeof(Student));

    strcpy(students[0].name, "Alice");
    students[0].score = 90;

    strcpy(students[1].name, "Bob");
    students[1].score = 85;

    strcpy(students[2].name, "Charlie");
    students[2].score = 95;

    for (int i = 0; i < n; i++) {
        printf("%s - %d\n", students[i].name, students[i].score);
    }

    free(students);
    return 0;
}

/* Output:
Alice - 90
Bob - 85
Charlie - 95
*/

```

## Summary

- -> is the shorthand for accessing structure members through pointers.

- Use pointers to structures for efficient data passing and modification.

- malloc() allows creating structures dynamically.

- Always use free() to avoid memory leaks.

- Arrays of pointers and dynamic allocation are essential for advanced data structures like linked lists.
