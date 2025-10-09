# Structures in C (Overview & Declaration)

## Overview

A **structure** is a user-defined data type that groups together variables of **different data types** under one name.  
It allows for **organized data management** and makes programs more readable, especially when handling related information.

---

## Syntax

```c
struct Person {
    char name[50];
    int age;
    double salary;
};

```

- struct — keyword to define a structure

- Person — name (or tag) of the structure

- Members: variables inside the structure (e.g., name, age, salary)


## Declaration Methods

### Method 1: Separate Declaration
```c
int main() {
    struct Person person1, person2, person3;
    person1.age = 25;  // Access using the dot operator
    return 0;
}

```

### Method 2: Immediate Initialization
```c
struct Person {
    int age;
    double salary;
} person1 = {25, 5440.50}, person2 = {22, 5000.50};

```

### Method 3: Designated Initializers (Recommended)
```c
struct Person {
    int age;
    char name[50];
};

int main() {
    struct Person person1 = {.age = 20, .name = "John"};
    struct Person person2 = {.name = "Jane", .age = 21};  // Order doesn’t matter
    return 0;
}

```

## Key Points:

- Use designated initializers for clarity and safety

- Access members using the dot operator (.)

- Initialize structures during declaration when possible

## Don’t:

- Use designated initializers outside of declaration

- Forget that each structure variable has its own copy of all members

- Mix different structure types without defining them properly

## Best Practices

- Group related data using structures for organization

- Use descriptive names for both structures and their members

- Initialize values clearly using designated initializers

### Example: Structure with User Input
```c
#include <stdio.h>

struct Employee {
    int age;
    char name[50];
};

int main() {
    struct Employee employee1;

    printf("Enter age: ");
    scanf("%d", &employee1.age);

    // Clear input buffer
    while (getchar() != '\n');

    printf("Enter full name: ");
    fgets(employee1.name, sizeof(employee1.name), stdin);

    printf("\n--- Employee Info ---\n");
    printf("Name: %s", employee1.name);
    printf("Age: %d\n", employee1.age);

    return 0;
}

/* Output:
Enter age: 21
Enter full name: Andre Noel

--- Employee Info ---
Name: Andre Noel
Age: 21
*/

```

## Summary:
Structures help group multiple variables of different data types under one logical unit — making C programs cleaner, modular, and easier to maintain.