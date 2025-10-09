# Typedef and Structure Aliases

## Overview

The **typedef** keyword in C allows you to create an **alias** (alternative name) for an existing data type.  
It helps make code more **readable**, **organized**, and **easier to maintain**, especially when working with structures.

---

## Basic Syntax

```c
typedef existing_type new_name;

#include <stdio.h>
typedef float Grade;
typedef char String[50];

int main() {
    Grade average = 92.5;
    String student = "Andre Noel";

    printf("%s's average grade: %.2f\n", student, average);
    return 0;
}

// Output: Andre Noel's average grade: 92.50

```

## Typedef with Structures

### Without typedef
```c
#include <stdio.h>

struct Student {
    int id;
    char name[20];
};

int main() {
    struct Student s1 = {1, "Andre"}; // Notice how we always need the struct keyword
    printf("%d - %s\n", s1.id, s1.name);
    return 0;
}

// Output: 1 - Andre

```

### With typedef
```c
#include <stdio.h>

typedef struct {
    int id;
    char name[20];
} Student;

int main() {
    Student s1 = {1, "Andre"};
    printf("%d - %s\n", s1.id, s1.name);
    return 0;
}

// Output: 1 - Andre

```
- Cleaner syntax: No need to write struct each time
- Better readability: The name Student clearly describes what the type represents

## Typedef with a Structure Tag
```c
#include <stdio.h>

typedef struct Person {
    int age;
    char name[50];
} Person;

int main() {
    Person p1 = {.age = 21, .name = "Andre"};
    printf("%s is %d years old.\n", p1.name, p1.age);
    return 0;
}

// Output: Andre is 21 years old.

```
- Still uses a tag (struct Person) internally
- But lets you declare variables simply as Person p1;

## Nested Structures with typedef
```c
#include <stdio.h>

typedef struct {
    int day, month, year;
} Date;

typedef struct {
    char name[50];
    Date birthday;
} Person;

int main() {
    Person p1 = {"Guz Andre Noel", {15, 3, 2004}};
    printf("%s was born on %d/%d/%d\n",
           p1.name, p1.birthday.day, p1.birthday.month, p1.birthday.year);
    return 0;
}

// Output: Guz Andre Noel was born on 15/3/2004

```

## Key Points

- typedef creates an alias for a type (it does not make a new type)

- Greatly improves readability and reduces repetition

- Commonly used with structures to simplify declarations

- Use descriptive alias names — they should describe what the data represents