# Structures in Functions and Pointers

## Overview

Structures can be **passed to functions** just like normal variables.  
They can be passed by **value** (copy) or by **reference** (using pointers).

---

## 1. Passing by Value

When you pass a structure **by value**, a **copy** is made.  
Changes inside the function **don’t affect** the original variable.

```c
#include <stdio.h>

typedef struct {
    int x;
    int y;
} Point;

void display(Point p) {
    printf("x: %d, y: %d\n", p.x, p.y);
}

int main() {
    Point p1 = {10, 20};
    display(p1); // sends a copy
    return 0;
}

// Output: x: 10, y: 20

```

## 2. Passing by Reference (Using Pointers)

When you pass a pointer, the function can directly modify the structure.

```c
#include <stdio.h>

typedef struct {
    int x;
    int y;
} Point;

void move(Point *p) {
    p->x += 5;
    p->y += 10;
}

int main() {
    Point p1 = {10, 20};
    move(&p1); // send address of structure
    printf("New position: (%d, %d)\n", p1.x, p1.y);
    return 0;
}

// Output: New position: (15, 30)

```

- No copying → faster for large structures
- Allows direct modification
- Requires careful pointer use

## 3. Returning a Structure from a Function

A function can return a structure, just like returning int or float.

```c
#include <stdio.h>

typedef struct {
    int x;
    int y;
} Point;

Point createPoint(int a, int b) {
    Point temp = {a, b};
    return temp;
}

int main() {
    Point p1 = createPoint(5, 15);
    printf("Created Point: (%d, %d)\n", p1.x, p1.y);
    return 0;
}

// Output: Created Point: (5, 15)

```

- Clean and readable
- No need for global variables

## Two Ways to Access Structure Members Through Pointers

### Method 1: Dereference (*) + Dot Operator (.)

```c
#include <stdio.h>

typedef struct {
    int age;
    char name[20];
} Person;

int main() {
    Person p = {21, "Noel"};
    Person *ptr = &p;

    printf("Name: %s\n", (*ptr).name);
    printf("Age: %d\n", (*ptr).age);
    return 0;
}

/* Output:
Name: Noel
Age: 21
*/

```

### Method 2: Arrow Operator (->) — Preferred

```c
#include <stdio.h>

typedef struct {
    int age;
    char name[20];
} Person;

int main() {
    Person p = {21, "Noel"};
    Person *ptr = &p;

    printf("Name: %s\n", ptr->name);
    printf("Age: %d\n", ptr->age);
    return 0;
}

/* Output: 
Name: Noel
Age: 21
*/

```

- ptr->member is shorthand for (*ptr).member
- Cleaner and easier to read

## Structure Pointer Access Methods

| Method | Syntax | Readability | Usage |
|--------|--------|-------------|-------|
| Dereference + Dot | `(*ptr).member` | Cluttered | Rare |
| Arrow Operator | `ptr->member` | Clean | Common |

## Key Points

- Use by value for small, read-only structures

- Use by reference when modifying or saving memory

- The arrow operator (->) is essential for structure pointers

- Functions can return whole structures safely

## Summary

- Passing structures to and from functions improves modularity and code clarity.
- Use pointers when you need efficiency or direct modification — and always remember to initialize your structures before use.