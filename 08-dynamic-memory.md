# Memory Allocation in C

## 1. Overview

**Memory allocation** is the process of reserving space in RAM for variables, arrays, and data structures.  
C provides both **automatic (stack)** and **manual (heap)** memory management.

---

## 1.1 Memory Layout (Stack vs Heap)

A simplified view of how memory is organized during program execution:

| Memory Area           | Grows...         | Contains                          |
|-----------------------|------------------|-----------------------------------|
| Stack                 | Downward ▼       | Local Variables, Return Addresses |
|                       | (Lower Addresses) |                                   |
| Heap                  | Upward ▲         | Dynamic Allocation (malloc, etc.) |
|                       | (Higher Addresses)|                                   |
| Global & Static       | (Fixed)          | Global/Static Variables           |
| Code                  | (Fixed)          | Program Instructions              |

- **Stack** → fast, automatically managed, limited in size.  
- **Heap** → flexible, manually managed using `malloc()`, `calloc()`, `realloc()`, and `free()`.

---

## 1.2 Why Memory Management Matters
As a C programmer, you have direct control over memory - this is both powerful and dangerous! Understanding memory allocation helps you:

- Create programs that use memory efficiently

- Build data structures that can grow/shrink as needed

- Avoid crashes and security vulnerabilities

- Prevent memory leaks that slow down systems

### Key Concepts for Beginners
- Stack: Fast, automatic memory that cleans itself up

- Heap: Flexible memory you control manually

- Scope: Where variables are accessible in your code

- Lifetime: How long variables exist in memory

---

## 2. Stack Allocation (Automatic)

### Characteristics
- **How:** Managed automatically by the compiler.
- **When:** For local variables, function parameters, and return addresses.
- **Lifetime:** Variables exist only within their function scope.
- **Principle:** LIFO (Last In, First Out).
- **Direction:** Stack grows downward (from high to low memory addresses).

### Example

```c
#include <stdio.h>

void myFunction(int c, int d) {
    printf("Inside myFunction: c = %d, d = %d\n", c, d);
}

int main() {
    int a = 4;  
    int b = 7;  
    myFunction(a, b);
    printf("Back in main: a = %d, b = %d\n", a, b);
    return 0;
}

```

### Memory Snapshot (During myFunction())

| Memory Address  | Variable | Value | Notes                   |
| --------------- | -------- | ----- | ----------------------- |
| 0x7ffe3a44a200  | a        | 4     | From main()             |
| 0x7ffe3a44a1fc  | b        | 7     | From main()             |
| 0x7ffe3a44a1f8  | c        | 4     | Copy of a               |
| 0x7ffe3a44a1f4  | d        | 7     | Copy of b               |

LIFO Behavior:
- Last in → c and d added when function was called.
- First out → c and d removed when the function ends.

---

## 3. Heap Allocation (Dynamic)

The **heap** is used when memory must persist beyond the scope of a single function
or when the **required size isn’t known** at compile time.

## Functions for Dynamic Memory

| Function    | Purpose                                  |
| ----------- | ---------------------------------------- |
| `malloc()`  | Allocates uninitialized memory.          |
| `calloc()`  | Allocates zero-initialized memory.       |
| `realloc()` | Resizes an existing allocated block.     |
| `free()`    | Frees allocated memory to prevent leaks. |

---

## 4. malloc() — Memory Allocation

### Syntax:

```c
pointer = (cast-type*) malloc(number_of_bytes);
```

### Notes:

- Allocates raw memory of a specified size.

- Returns a void* pointer (must be cast to the appropriate type).

- Contains garbage values by default.

- Returns NULL if allocation fails.

```c
#include <stdlib.h>
#include <stdio.h>

int main() {
    int *arr;
    int size = 5;

    arr = (int*) malloc(size * sizeof(int));

    if (arr == NULL) {
        printf("Memory allocation failed!\n");
        return 1;
    }

    for (int i = 0; i < size; i++)
        arr[i] = i + 1;

    printf("Array: ");
    for (int i = 0; i < size; i++)
        printf("%d ", arr[i]);

    free(arr);
    return 0;
}

// Output: Array: 1 2 3 4 5

```

---

## 5. calloc() — Contiguous Allocation

### Syntax:

```c
pointer = (cast-type*) calloc(num_elements, size_of_each);
```

### Notes:

- Allocates memory for multiple elements.

- Automatically initializes all bytes to zero.

- Returns NULL if allocation fails.

```c
#include <stdlib.h>
#include <stdio.h>

int main() {
    int *arr;
    int size = 5;

    arr = (int*) calloc(size, sizeof(int));

    if (arr == NULL) {
        printf("Memory allocation failed!\n");
        return 1;
    }

    printf("Initial values (zero-initialized): ");
    for (int i = 0; i < size; i++)
        printf("%d ", arr[i]);

    free(arr);
    return 0;
}

// Output: Initial values (zero-initialized): 0 0 0 0 0

```

---

## 6. realloc() — Resize Allocated Memory

### Syntax:

```c
pointer = realloc(existing_pointer, new_size_in_bytes);
```

### Notes:

- Changes the size of previously allocated memory.

- Copies old data to the new block automatically.

- Returns a new pointer (which may differ from the original).

- Returns NULL if resizing fails — old memory remains unchanged.

```c
#include <stdlib.h>
#include <stdio.h>

int main() {
    int *arr;
    int size = 3;

    arr = (int*) malloc(size * sizeof(int));

    for (int i = 0; i < size; i++)
        arr[i] = i + 1;

    printf("Before realloc: ");
    for (int i = 0; i < size; i++)
        printf("%d ", arr[i]);

    // Resize array to hold 5 integers
    size = 5;
    arr = (int*) realloc(arr, size * sizeof(int));

    // Initialize new elements
    arr[3] = 4;
    arr[4] = 5;

    printf("\nAfter realloc: ");
    for (int i = 0; i < size; i++)
        printf("%d ", arr[i]);

    free(arr);
    return 0;
}


/* Output:
Before realloc: 1 2 3 
After realloc: 1 2 3 4 5
*/

```

---

## 7. free() — Releasing Memory

### Syntax:

```c
free(pointer);
```

### Notes:

- Frees previously allocated memory.

- Must be called once for every malloc(), calloc(), or realloc().

- After calling free(), the pointer becomes invalid.

### Best Practice:

```c
free(arr);
arr = NULL; // avoid dangling pointer
```

## 8. Practical Example — Dynamic Array of Ages

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n;
    int *ages;

    printf("Enter the number of children: ");
    scanf("%d", &n);

    if (n <= 0) {
        printf("Error: Number must be positive!\n");
        return 1;
    }

    ages = (int*) malloc(n * sizeof(int));

    if (ages == NULL) {
        printf("Memory allocation failed!\n");
        return 1;
    }

    printf("Enter %d ages:\n", n);
    for (int i = 0; i < n; i++) {
        printf("Age %d: ", i + 1);
        scanf("%d", &ages[i]);
    }

    printf("\nStored ages: ");
    for (int i = 0; i < n; i++)
        printf("%d ", ages[i]);

    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += ages[i];
    printf("\nAverage age: %.2f\n", (float)sum / n);

    free(ages);
    return 0;
}

/* 
Sample Output:

Enter the number of children: 3
Enter 3 ages:
Age 1: 5
Age 2: 8
Age 3: 6

Stored ages: 5 8 6
Average age: 6.33
*/ 

```

---

## 9. Summary
| Function    | Initializes Memory | Can Resize | Must Be Freed |
| ----------- | ------------------ | ---------- | ------------- |
| `malloc()`  | No                 | No         | Yes           |
| `calloc()`  | Yes (zeroes)       | No         | Yes           |
| `realloc()` | N/A                | Yes        | Yes           |
| `free()`    | N/A                | N/A        | N/A           |


## Key Takeaways

- Use sizeof() for portability.

- Always check if the returned pointer is NULL.

- Always call free() to release memory.

- Stack is automatic; heap is manual.

- Use realloc() carefully — it may move memory blocks.


