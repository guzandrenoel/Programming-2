# Structure Initialization and Aliases

## Overview

After defining a structure, there are several ways to **initialize** and **assign values** to its members.  
Proper initialization ensures your data starts in a known, predictable state — avoiding garbage values.

---

## 1. Direct Initialization

Initialize members immediately when declaring the structure variable.

```c
#include <stdio.h>

typedef struct {
    int age;
    double salary;
} Person;

int main() {
    Person p1 = {25, 45000.50};

    printf("Age: %d\nSalary: %.2f\n", p1.age, p1.salary);
    return 0;
}

/* Output: 
Age: 25
Salary: 45000.50

```

- Simple and clear for small structures
- Members are filled in order

## 2. Assignment After Declaration

You can declare first, then assign values later.

```c
#include <stdio.h>

typedef struct {
    int age;
    double salary;
} Person;

int main() {
    Person p1;

    p1.age = 30;
    p1.salary = 55000.75;

    printf("Age: %d\nSalary: %.2f\n", p1.age, p1.salary);
    return 0;
}

/* Output: 
Age: 30
Salary: 55000.75

```

- Useful when values come from user input or calculations

## 3. Designated Initializers (Recommended)

Designated initializers assign values by name — order doesn’t matter.

```c
#include <stdio.h>

typedef struct {
    int x, y;
} Point;

int main() {
    Point p1 = {.x = 10, .y = 20};
    Point p2 = {.y = 40, .x = 30}; // Order can vary

    printf("p1: (%d, %d)\n", p1.x, p1.y);
    printf("p2: (%d, %d)\n", p2.x, p2.y);
    return 0;
}

/* Output: 
p1: (10, 20)
p2: (30, 40)

```

- Safer and clearer (especially with many members)
- Prevents mix-ups from incorrect order

## Key Points

- Initialize structures when declared to avoid garbage data

- Designated initializers make your code safer and easier to read

- You can assign multiple typedef aliases for convenience

- Always use descriptive names for aliases (e.g., Point, Employee, Book)

## Summary

- There’s no single “best” way to initialize a structure — it depends on context.

- Use direct or designated initialization for fixed data

- Use assignment for runtime or user input

- Use aliases to make your code shorter and clearer