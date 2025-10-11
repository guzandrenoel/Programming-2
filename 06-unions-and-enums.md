# Unions and Enums in C

## Overview

C provides two special data types — **union** and **enum** — that extend the flexibility of structures.

- **Union** allows multiple members to share the **same memory space**.  
- **Enum** allows creating **named integer constants** for easier code readability.

Both are often used together with `struct` for more advanced data modeling.

---

## 1. Unions

A **union** is like a structure, but all its members **share the same memory location**.  
This means only **one member** can store a valid value at a time.

```c
#include <stdio.h>

union Data {
    int i;
    float f;
    char str[20];
};

int main() {
    union Data data;

    data.i = 10;
    printf("data.i = %d\n", data.i);

    data.f = 220.5;
    printf("data.f = %.2f\n", data.f);

    // Now data.i’s value is overwritten by data.f
    printf("data.i (after writing f) = %d\n", data.i);

    return 0;
}

/* Output:
data.i = 10
data.f = 220.50
data.i (after writing f) = random/garbage value
*/

```

### Key Points:

- Only one member is active at a time.

- All members share the same memory address.

- Useful for memory-efficient programs where only one type of data is needed at a time (e.g., sensors, packets, or device data).


## 2. Enums

An **enum** (short for enumeration) assigns names to integer constants for better readability.

```c
#include <stdio.h>

enum Day { SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY };

int main() {
    enum Day today = WEDNESDAY;

    printf("Today is day number: %d\n", today);

    return 0;
}

/* Output:
Today is day number: 3
*/

```

### Key Points:

- The first value starts at 0 by default.

- You can assign custom values: enum Level { LOW = 1, MEDIUM = 5, HIGH = 10 };

- Enums make code self-explanatory and reduce the need for magic numbers.


## 3. Combining Struct, Union, and Enum

They can be combined for real-world scenarios, like flexible data storage.

```c
#include <stdio.h>

enum DataType { INT, FLOAT, STRING };

union Value {
    int i;
    float f;
    char str[20];
};

typedef struct {
    enum DataType type;
    union Value data;
} Item;

int main() {
    Item item1 = {INT, .data.i = 42};
    Item item2 = {STRING, .data.str = "Hello"};

    if (item1.type == INT)
        printf("Item1 is an integer: %d\n", item1.data.i);

    if (item2.type == STRING)
        printf("Item2 is a string: %s\n", item2.data.str);

    return 0;
}

/* Output:
Item1 is an integer: 42
Item2 is a string: Hello
*/

```

### Key Points:

- enum defines the data type category.

- union stores the actual data (only one active at a time).

- struct combines both for organized handling.

## Summary

- Union → Shares memory among all members (efficient but only one valid at a time).

- Enum → Assigns readable names to integers (cleaner logic).

- Struct + Union + Enum → Together, they make flexible, efficient, and readable programs.

### Quick Tip:
Use union for space-saving data that changes type,
and enum for clear, named constants instead of numbers.