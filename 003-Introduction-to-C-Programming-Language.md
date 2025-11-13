# Chapter 3: Introduction to the C Programming Language

## Introduction to Chapter 3

You now understand how computers are organized and how they execute instructions at a fundamental level. But writing programs directly in machine code or assembly language is tedious, error-prone, and time-consuming. High-level programming languages exist to provide abstraction—allowing you to express algorithms and logic without worrying about every detail of the underlying hardware.

Among high-level languages, C occupies a unique position. Created in the early 1970s by Dennis Ritchie at Bell Labs, C was designed specifically for systems programming—writing operating systems, compilers, and other low-level software. C provides enough abstraction to be practical and portable, yet it remains close enough to the hardware that you can understand exactly what the computer will do when executing your code.

This proximity to the hardware makes C the ideal language for understanding how software interacts with computer systems. When you write in C, you work directly with memory addresses through pointers. You can manipulate individual bits. You can see how data structures are laid out in memory. You can even embed assembly language directly in your C code. These capabilities make C both powerful and dangerous—the language gives you the tools to do almost anything, but it does not prevent you from making mistakes that can crash your program or create security vulnerabilities.

In this chapter, you will learn C with a focus on understanding how your code maps to the underlying hardware. You will see how variables correspond to memory locations, how function calls use the stack, and how data structures are organized in memory. This understanding is essential not only for writing C programs but also for the assembly language programming and reverse engineering you will learn in later chapters.

C has influenced countless other languages—C++, Java, C#, JavaScript, and many others borrow syntax and concepts from C. Learning C well provides a foundation for understanding many modern programming languages. More importantly, learning C with an understanding of the underlying hardware will make you a better programmer in any language because you will understand what really happens when your programs run.

---

## 3.1 C Fundamentals and Memory Model

### 3.1.1 The First C Program

Let us begin with the traditional first program in any language—a program that prints "Hello, World!" to the screen:

```c
#include <stdio.h>

int main(void) {
    printf("Hello, World!\n");
    return 0;
}
```

While simple, this program introduces several important concepts that we will explore in depth.

**Preprocessor Directives:**

The line `#include <stdio.h>` is a **preprocessor directive**. Before the compiler translates your C code into machine code, a program called the **preprocessor** processes all lines beginning with `#`. The `#include` directive tells the preprocessor to insert the contents of the file `stdio.h` (standard input/output header) at this point in the source code.

Header files like `stdio.h` contain declarations of functions and types that your program uses. In this case, `stdio.h` declares the `printf` function, which we use to display output. Without including this header, the compiler would not know how to handle the `printf` function call.

**The main Function:**

Every C program must have exactly one function named `main`. This is the **entry point** of your program—when you run the program, execution begins at the first statement inside `main`. The `main` function has a specific signature:

```c
int main(void)
```

This declares that `main`:

- Returns an `int` (integer) value to the operating system
- Takes no parameters (indicated by `void`)

The return value serves as an **exit status code**. By convention, returning 0 indicates successful execution, while non-zero values indicate various error conditions. The operating system can check this value to determine whether the program completed successfully.

**Statements:**

The body of `main` contains two statements:

```c
printf("Hello, World!\n");
return 0;
```

Each statement ends with a semicolon. This is mandatory in C—the semicolon is not optional, and forgetting it is one of the most common mistakes beginners make.

The `printf` function call displays text to the screen. The `\n` at the end of the string is an **escape sequence** representing a newline character. Escape sequences allow you to include special characters in strings:

- `\n` = newline
- `\t` = tab
- `\\` = backslash
- `\"` = double quote
- `\0` = null character (marks the end of strings)

The `return 0;` statement terminates the `main` function and returns the value 0 to the operating system.

**Compilation and Execution:**

To run this program, you must first **compile** it—translate the C source code into executable machine code. Using the GCC compiler on Linux:

```bash
gcc -o hello hello.c
./hello
```

The compiler reads your source file (`hello.c`), checks for syntax errors, translates the code into assembly language, assembles that into machine code, links it with necessary libraries, and produces an executable file (`hello`). You can then run this executable, and it will print "Hello, World!" to the terminal.

### 3.1.2 Variables and Data Types

Variables are named storage locations that hold values. When you declare a variable in C, you are asking the compiler to set aside a region of memory to store a value, and you give that region a name so you can refer to it in your code.

**Basic Integer Types:**

C provides several integer types of different sizes:

```c
char c = 'A';           // Usually 1 byte (8 bits)
short s = 100;          // Usually 2 bytes (16 bits)
int i = 1000;           // Usually 4 bytes (32 bits)
long l = 100000L;       // Usually 4 or 8 bytes (32 or 64 bits)
long long ll = 1000000LL;  // Usually 8 bytes (64 bits)
```

Notice the word "usually"—the C standard does not specify exact sizes for these types, only minimum ranges they must support. The actual size depends on the compiler and target architecture. You can use the `sizeof` operator to determine the exact size on your system:

```c
printf("Size of int: %zu bytes\n", sizeof(int));
```

On most modern systems:

- `char` is 1 byte (by definition—sizeof(char) is always 1)
- `short` is 2 bytes
- `int` is 4 bytes
- `long` is 4 bytes on 32-bit systems, 8 bytes on 64-bit systems
- `long long` is 8 bytes

Each integer type can be **signed** (can represent negative numbers) or **unsigned** (only non-negative numbers). By default, integer types are signed. You can explicitly specify:

```c
unsigned int positive_only = 42;
signed int can_be_negative = -10;  // 'signed' is usually redundant
```

An $n$-bit unsigned integer can represent values from $0$ to $2^n - 1$. An $n$-bit signed integer (using two's complement, which is universal in modern systems) can represent values from $-2^{n-1}$ to $2^{n-1} - 1$.

For example, with `int` as 4 bytes (32 bits):

- `unsigned int` range: $0$ to $2^{32} - 1 = 4,294,967,295$
- `signed int` range: $-2^{31}$ to $2^{31} - 1 = -2,147,483,648$ to $2,147,483,647$

**Floating-Point Types:**

For representing real numbers (numbers with fractional parts), C provides:

```c
float f = 3.14f;        // Usually 4 bytes (32 bits, single-precision)
double d = 3.14159265359;  // Usually 8 bytes (64 bits, double-precision)
long double ld = 3.14159265359L;  // Usually 10, 12, or 16 bytes (extended precision)
```

These types follow the IEEE 754 floating-point standard you learned about in Chapter 1. The `float` type provides approximately 6-7 decimal digits of precision, while `double` provides approximately 15-16 digits. For most purposes, `double` is the preferred choice—modern processors handle double-precision arithmetic efficiently, and the extra precision helps avoid accumulated rounding errors.

**The char Type and Characters:**

The `char` type is special—it is both an integer type (8 bits) and the type used to represent individual characters:

```c
char letter = 'A';      // Single character (uses ASCII/UTF-8 encoding)
char number = 65;       // Same as 'A' (ASCII code for 'A' is 65)
```

Single characters are enclosed in single quotes. Remember from Chapter 1 that characters are represented as numbers using an encoding scheme like ASCII. The character 'A' and the number 65 are identical to the computer.

**Boolean Values:**

C did not originally have a boolean type. Traditionally, integers were used with the convention that 0 means false and any non-zero value means true. C99 (the 1999 revision of the C standard) added a boolean type:

```c
#include <stdbool.h>

bool flag = true;       // true and false are defined in stdbool.h
bool condition = false;
```

Without `stdbool.h`, you would use integers:

```c
int flag = 1;           // 1 for true
int condition = 0;      // 0 for false
```

**Type Qualifiers:**

C provides qualifiers that modify the properties of types:

**const:** Declares that a variable's value cannot be changed after initialization:

```c
const int max_size = 100;
max_size = 200;  // ERROR: cannot modify const variable
```

The `const` qualifier tells both the compiler (which can optimize based on knowing the value will not change) and other programmers (documenting that this value is meant to be constant) that the variable is read-only.

**volatile:** Indicates that a variable's value might change in ways the compiler cannot predict (for example, hardware registers or variables shared with interrupt handlers):

```c
volatile int sensor_reading;
```

This prevents the compiler from optimizing away reads of the variable, since the value might change at any time.

### 3.1.3 Operators and Expressions

C provides a rich set of operators for manipulating values. Understanding these operators and their precedence is essential for writing correct programs.

**Arithmetic Operators:**

```c
int a = 10, b = 3;

int sum = a + b;        // Addition: 13
int diff = a - b;       // Subtraction: 7
int prod = a * b;       // Multiplication: 30
int quot = a / b;       // Integer division: 3 (not 3.333...)
int rem = a % b;        // Remainder (modulo): 1 (10 = 3*3 + 1)
```

Note that division of integers performs **integer division**, discarding any fractional part. If you want floating-point division, at least one operand must be a floating-point type:

```c
double result = 10.0 / 3;     // 3.333...
double result2 = (double)10 / 3;  // 3.333... (type cast)
```

The modulo operator `%` gives the remainder after division. It is only defined for integer types.

**Increment and Decrement:**

```c
int x = 5;
x++;        // Post-increment: use current value, then add 1 (x becomes 6)
++x;        // Pre-increment: add 1, then use new value (x becomes 7)
x--;        // Post-decrement: use current value, then subtract 1 (x becomes 6)
--x;        // Pre-decrement: subtract 1, then use new value (x becomes 5)
```

The difference between pre and post variants matters when the expression is part of a larger statement:

```c
int a = 5;
int b = a++;    // b gets 5, then a becomes 6
int c = ++a;    // a becomes 7, then c gets 7
```

**Relational Operators:**

These operators compare values and return 1 (true) or 0 (false):

```c
int a = 5, b = 10;

a == b      // Equal to: 0 (false)
a != b      // Not equal to: 1 (true)
a < b       // Less than: 1 (true)
a <= b      // Less than or equal: 1 (true)
a > b       // Greater than: 0 (false)
a >= b      // Greater than or equal: 0 (false)
```

A common mistake is using `=` (assignment) when you mean `==` (comparison):

```c
if (x = 5)  // WRONG: assigns 5 to x, then tests if 5 is true (it is)
if (x == 5) // CORRECT: compares x to 5
```

**Logical Operators:**

These operators combine boolean values:

```c
int a = 1, b = 0;

!a          // Logical NOT: 0 (negates the value)
a && b      // Logical AND: 0 (true only if both are true)
a || b      // Logical OR: 1 (true if either is true)
```

These operators use **short-circuit evaluation**. In `a && b`, if `a` is false, `b` is not evaluated because the result must be false regardless of `b`. Similarly, in `a || b`, if `a` is true, `b` is not evaluated.

**Bitwise Operators:**

These operators work on individual bits, using the Boolean operations you learned in Chapter 1:

```c
unsigned int a = 0b1010;  // Binary literal (some compilers)
unsigned int b = 0b1100;

a & b       // Bitwise AND: 0b1000 (8)
a | b       // Bitwise OR: 0b1110 (14)
a ^ b       // Bitwise XOR: 0b0110 (6)
~a          // Bitwise NOT: 0b...11110101 (inverts all bits)
a << 2      // Left shift: 0b101000 (40) - shifts bits left, fills with 0
a >> 1      // Right shift: 0b0101 (5) - shifts bits right
```

Left shifting by $n$ positions is equivalent to multiplying by $2^n$ (for unsigned types or positive signed values). Right shifting by $n$ positions is equivalent to dividing by $2^n$ and rounding toward zero.

Bitwise operations are essential for:

- Setting, clearing, or toggling specific bits
- Efficient multiplication/division by powers of 2
- Implementing protocols that use bit fields
- Low-level hardware manipulation

**Assignment Operators:**

C provides compound assignment operators that combine an operation with assignment:

```c
int x = 10;

x += 5;     // Equivalent to: x = x + 5;
x -= 3;     // Equivalent to: x = x - 3;
x *= 2;     // Equivalent to: x = x * 2;
x /= 4;     // Equivalent to: x = x / 4;
x %= 3;     // Equivalent to: x = x % 3;
x &= 0xFF;  // Equivalent to: x = x & 0xFF;
x |= 0x10;  // Equivalent to: x = x | 0x10;
x ^= 0x0F;  // Equivalent to: x = x ^ 0x0F;
x <<= 2;    // Equivalent to: x = x << 2;
x >>= 1;    // Equivalent to: x = x >> 1;
```

**Operator Precedence:**

When an expression contains multiple operators, precedence rules determine the order of evaluation. For example:

```c
int result = 2 + 3 * 4;  // result is 14, not 20
```

Multiplication has higher precedence than addition, so `3 * 4` is evaluated first, giving 12, then 2 is added.

The complete precedence hierarchy is complex. Key points to remember:

- Unary operators (like `!`, `~`, `++`) have high precedence
- Multiplicative operators (`*`, `/`, `%`) precede additive (`+`, `-`)
- Relational operators (`<`, `>`, etc.) precede equality (`==`, `!=`)
- Logical AND (`&&`) precedes logical OR (`||`)
- Assignment operators have very low precedence

When in doubt, use parentheses to make the order explicit:

```c
int result = 2 + (3 * 4);  // Clearer, though parentheses are not needed here
```

### 3.1.4 Control Flow Structures

Programs need to make decisions and repeat operations. C provides several control flow structures for this purpose.

**The if Statement:**

The `if` statement executes code conditionally based on whether an expression is true (non-zero):

```c
int age = 20;

if (age >= 18) {
    printf("You are an adult.\n");
}
```

You can add an `else` clause for the false case:

```c
if (age >= 18) {
    printf("You are an adult.\n");
} else {
    printf("You are a minor.\n");
}
```

For multiple conditions, use `else if`:

```c
if (age < 13) {
    printf("Child\n");
} else if (age < 18) {
    printf("Teenager\n");
} else if (age < 65) {
    printf("Adult\n");
} else {
    printf("Senior\n");
}
```

If the body of an `if`, `else if`, or `else` contains only one statement, the braces are optional, but using them is good practice to avoid errors:

```c
if (age >= 18)
    printf("Adult\n");  // Works, but risky

if (age >= 18) {
    printf("Adult\n");  // Safer and clearer
}
```

**The switch Statement:**

The `switch` statement provides multi-way branching based on the value of an integer expression:

```c
int day = 3;

switch (day) {
    case 1:
        printf("Monday\n");
        break;
    case 2:
        printf("Tuesday\n");
        break;
    case 3:
        printf("Wednesday\n");
        break;
    case 4:
        printf("Thursday\n");
        break;
    case 5:
        printf("Friday\n");
        break;
    case 6:
    case 7:
        printf("Weekend\n");
        break;
    default:
        printf("Invalid day\n");
        break;
}
```

The `break` statement is crucial—without it, execution **falls through** to the next case. This is occasionally useful (as shown with cases 6 and 7, which both execute the same code), but usually it is a bug. The compiler may warn you about fall-through cases.

**The while Loop:**

The `while` loop repeats code as long as a condition remains true:

```c
int count = 0;

while (count < 5) {
    printf("%d\n", count);
    count++;
}
```

This prints numbers 0 through 4. The condition is checked before each iteration, so if the condition is initially false, the loop body never executes.

**The do-while Loop:**

The `do-while` loop is similar to `while`, but it checks the condition after each iteration, guaranteeing that the loop body executes at least once:

```c
int count = 0;

do {
    printf("%d\n", count);
    count++;
} while (count < 5);
```

**The for Loop:**

The `for` loop is typically used when you know how many iterations you need:

```c
for (int i = 0; i < 5; i++) {
    printf("%d\n", i);
}
```

The `for` loop has three parts, separated by semicolons:

1. **Initialization:** Executed once before the loop begins (`int i = 0`)
2. **Condition:** Checked before each iteration (`i < 5`)
3. **Update:** Executed after each iteration (`i++`)

This is equivalent to:

```c
int i = 0;          // Initialization
while (i < 5) {     // Condition
    printf("%d\n", i);
    i++;            // Update
}
```

Any of the three parts can be omitted (but the semicolons remain):

```c
for (;;) {
    // Infinite loop
}
```

**Loop Control Statements:**

The `break` statement immediately exits the innermost loop:

```c
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break;  // Exit loop when i equals 5
    }
    printf("%d\n", i);
}
// Prints 0 through 4
```

The `continue` statement skips the rest of the current iteration and moves to the next iteration:

```c
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue;  // Skip even numbers
    }
    printf("%d\n", i);
}
// Prints 1, 3, 5, 7, 9
```

### 3.1.5 Functions

Functions allow you to organize code into reusable units. A function is a named block of code that performs a specific task.

**Function Declaration and Definition:**

A function definition includes:

1. Return type (the type of value the function returns)
2. Function name
3. Parameter list (inputs to the function)
4. Function body (the code to execute)

```c
// Function that adds two integers
int add(int a, int b) {
    int sum = a + b;
    return sum;
}

// Function that prints a message (returns nothing)
void greet(void) {
    printf("Hello!\n");
}

// Call the functions
int result = add(5, 3);     // result = 8
greet();                     // Prints "Hello!"
```

Functions with return type `void` do not return a value. Functions with any other return type must return a value of that type using a `return` statement.

**Function Prototypes:**

Before you can call a function, the compiler must know its signature. If you define the function before you call it, no problem. But if you call it before defining it, you need a **function prototype** (also called a forward declaration):

```c
// Prototype declares the function signature
int add(int a, int b);

int main(void) {
    int result = add(5, 3);  // Call is valid
    printf("%d\n", result);
    return 0;
}

// Definition can come later
int add(int a, int b) {
    return a + b;
}
```

Prototypes are typically placed in header files (`.h` files), allowing multiple source files to use the same functions.

**Pass by Value:**

C uses **pass by value** for all parameters. This means that when you pass a variable to a function, the function receives a copy of the value, not the original variable. Changes to parameters inside the function do not affect the original variables:

```c
void try_to_modify(int x) {
    x = 100;    // Modifies the local copy only
}

int main(void) {
    int value = 5;
    try_to_modify(value);
    printf("%d\n", value);  // Still prints 5, not 100
    return 0;
}
```

To modify the original variable, you must use pointers (which we will cover next).

**Recursion:**

A function can call itself, a technique called **recursion**. Recursive functions must have a **base case** that stops the recursion:

```c
// Compute factorial: n! = n * (n-1) * (n-2) * ... * 1
int factorial(int n) {
    if (n <= 1) {
        return 1;  // Base case
    }
    return n * factorial(n - 1);  // Recursive case
}

// factorial(5) = 5 * factorial(4)
//              = 5 * 4 * factorial(3)
//              = 5 * 4 * 3 * factorial(2)
//              = 5 * 4 * 3 * 2 * factorial(1)
//              = 5 * 4 * 3 * 2 * 1
//              = 120
```

Recursion is elegant for certain problems but uses more memory than iterative solutions (because each recursive call adds a new stack frame). We will explore the stack in detail later.

### 3.1.6 Arrays

An array is a collection of elements of the same type stored in contiguous memory locations. Arrays allow you to work with multiple related values using a single name.

**Array Declaration:**

```c
int numbers[5];  // Array of 5 integers
```

This declares an array named `numbers` containing 5 integer elements. The elements are not initialized—they contain whatever values happened to be in memory (garbage values).

**Array Initialization:**

You can initialize arrays when you declare them:

```c
int numbers[5] = {10, 20, 30, 40, 50};
```

If you provide an initializer, you can omit the size—the compiler will infer it:

```c
int numbers[] = {10, 20, 30, 40, 50};  // Size is 5
```

If you provide fewer initializers than the size, the remaining elements are set to zero:

```c
int numbers[5] = {10, 20};  // {10, 20, 0, 0, 0}
```

**Array Indexing:**

Array elements are accessed using square brackets with an index. **Indices start at 0**, not 1:

```c
int numbers[5] = {10, 20, 30, 40, 50};

int first = numbers[0];   // first = 10
int third = numbers[2];   // third = 30
numbers[4] = 100;         // Modify last element
```

Valid indices for an array of size $n$ are 0 through $n-1$. Accessing outside this range (like `numbers[5]` or `numbers[-1]`) is **undefined behavior**—it might crash, might corrupt data, or might appear to work. C does not check array bounds for you.

**Memory Layout:**

Arrays are stored in contiguous memory. If `numbers` starts at address 1000 and integers are 4 bytes each, the layout is:

```
Address:  1000  1004  1008  1012  1016
Element:  [0]   [1]   [2]   [3]   [4]
Value:    10    20    30    40    50
```

This contiguous layout is important for understanding how array indexing works at the hardware level. The address of `numbers[i]` is:

$$\text{Address of numbers}[i] = \text{Base address} + (i \times \text{Size of element})$$

For our example:

$$\text{Address of numbers}[2] = 1000 + (2 \times 4) = 1008$$

**Multi-Dimensional Arrays:**

You can create arrays of arrays:

```c
int matrix[3][4];  // 3 rows, 4 columns (12 total elements)
```

Initialization:

```c
int matrix[3][4] = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};
```

Access elements with multiple indices:

```c
int value = matrix[1][2];  // Value in row 1, column 2 (value is 7)
```

In memory, multi-dimensional arrays are stored in **row-major order**—all elements of row 0, then all elements of row 1, and so on:

```
[1][2][3][4][5][6][7][8][9][10][11][12]
```

**Arrays and Loops:**

Arrays and loops work naturally together:

```c
int numbers[5] = {10, 20, 30, 40, 50};
int sum = 0;

for (int i = 0; i < 5; i++) {
    sum += numbers[i];
}

printf("Sum: %d\n", sum);  // Sum: 150
```

### 3.1.7 Pointers: The Key to Understanding Memory

Pointers are one of the most important and most confusing features of C. A **pointer** is a variable that stores a memory address. Instead of holding a value directly (like an integer or floating-point number), a pointer holds the address of another variable.

Understanding pointers is essential because:

- They allow functions to modify variables outside their scope
- They enable dynamic memory allocation
- They provide efficient access to arrays and data structures
- They are fundamental to understanding how computers work

**Declaring Pointers:**

A pointer declaration specifies the type of data the pointer points to, followed by an asterisk:

```c
int *p;        // p is a pointer to an int
double *q;     // q is a pointer to a double
char *r;       // r is a pointer to a char
```

The pointer itself stores an address (typically 8 bytes on 64-bit systems), regardless of what type it points to. But the type is important because it tells the compiler how to interpret the data at that address.

**The Address-Of Operator (&):**

The `&` operator gets the address of a variable:

```c
int x = 42;
int *p = &x;   // p now holds the address of x
```

If `x` is stored at memory address 1000, then `p` contains the value 1000.

**The Dereference Operator (\*):**

The `*` operator (in an expression, not a declaration) accesses the value at the address stored in a pointer. This is called **dereferencing**:

```c
int x = 42;
int *p = &x;

printf("%d\n", *p);  // Prints 42 (the value at the address p holds)

*p = 100;            // Changes the value at the address p holds
printf("%d\n", x);   // Prints 100 (x has been modified through the pointer)
```

**Pointer Example:**

Let us trace through a complete example:

```c
int a = 5;
int b = 10;
int *ptr;

ptr = &a;        // ptr points to a
*ptr = 20;       // Changes a to 20 through the pointer

ptr = &b;        // ptr now points to b
*ptr = 30;       // Changes b to 30 through the pointer

printf("a = %d, b = %d\n", a, b);  // Prints: a = 20, b = 30
```

**Pointers and Functions:**

Pointers allow functions to modify variables in the calling code. Remember that C uses pass by value, so passing a pointer provides the address, and the function can dereference it to modify the original variable:

```c
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main(void) {
    int x = 5, y = 10;
    printf("Before: x=%d, y=%d\n", x, y);

    swap(&x, &y);  // Pass addresses

    printf("After: x=%d, y=%d\n", x, y);
    return 0;
}
```

Output:

```
Before: x=5, y=10
After: x=10, y=5
```

**NULL Pointers:**

A pointer can be set to NULL (usually defined as `(void *)0`) to indicate that it does not point to any valid address:

```c
int *p = NULL;

if (p != NULL) {
    *p = 100;  // Safe to dereference
} else {
    printf("Pointer is NULL\n");
}
```

Dereferencing a NULL pointer is undefined behavior and typically causes a program crash (segmentation fault).

**Pointer Arithmetic:**

You can perform arithmetic on pointers. When you add an integer to a pointer, the pointer advances by that many elements (not bytes):

```c
int numbers[5] = {10, 20, 30, 40, 50};
int *p = numbers;  // p points to first element (numbers[0])

printf("%d\n", *p);     // Prints 10

p++;                    // Move to next element
printf("%d\n", *p);     // Prints 20

p += 2;                 // Move forward 2 elements
printf("%d\n", *p);     // Prints 40
```

If `p` initially holds address 1000, then `p++` increases it by `sizeof(int)` (typically 4), so `p` becomes 1004. The compiler handles the scaling automatically based on the pointed-to type.

You can subtract pointers to find the distance between them:

```c
int numbers[5] = {10, 20, 30, 40, 50};
int *p1 = &numbers[1];
int *p2 = &numbers[4];

ptrdiff_t diff = p2 - p1;  // diff is 3 (three elements apart)
```

**Arrays and Pointers:**

In most contexts, an array name is equivalent to a pointer to its first element:

```c
int numbers[5] = {10, 20, 30, 40, 50};

int *p = numbers;       // Same as: int *p = &numbers[0];
printf("%d\n", p[2]);   // Prints 30 (can index a pointer like an array)
printf("%d\n", *(p+2)); // Also prints 30 (pointer arithmetic)
```

In fact, the expression `numbers[i]` is equivalent to `*(numbers + i)`. Array indexing is syntactic sugar for pointer arithmetic.

However, there is a difference: an array name is not a modifiable lvalue—you cannot reassign it:

```c
int numbers[5];
numbers = something;  // ERROR: cannot assign to array
```

### 3.1.8 Strings

C does not have a built-in string type. Instead, strings are represented as arrays of characters terminated by a null character (`'\0'`).

**String Literals:**

A string literal is written in double quotes:

```c
char *message = "Hello, World!";
```

The compiler allocates memory for the string (including the null terminator) and `message` points to that memory. The string "Hello, World!" is actually stored as:

```
['H']['e']['l']['l']['o'][','][' ']['W']['o']['r']['l']['d']['!']['\0']
```

**Character Arrays as Strings:**

You can also create strings as character arrays:

```c
char greeting[6] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

Or more conveniently:

```c
char greeting[6] = "Hello";  // Compiler adds '\0' automatically
char greeting[] = "Hello";   // Size inferred (6 characters including '\0')
```

**String Functions:**

The `<string.h>` header provides functions for working with strings:

```c
#include <string.h>

char str1[20] = "Hello";
char str2[20] = "World";

// Get string length (not including '\0')
size_t len = strlen(str1);  // len = 5

// Copy string
strcpy(str1, "Goodbye");    // str1 is now "Goodbye"

// Concatenate strings
strcat(str1, " ");          // str1 is now "Goodbye "
strcat(str1, str2);         // str1 is now "Goodbye World"

// Compare strings (returns 0 if equal)
int cmp = strcmp(str1, str2);
```

**Important:** These functions do not check buffer sizes. Using `strcpy` or `strcat` with a destination buffer that is too small causes buffer overflow, a serious security vulnerability. Safer alternatives exist:

```c
strncpy(dest, src, sizeof(dest));  // Copies at most sizeof(dest) characters
strncat(dest, src, sizeof(dest) - strlen(dest) - 1);  // Limits concatenation
```

**String Iteration:**

You can process strings character by character:

```c
char str[] = "Hello";

for (int i = 0; str[i] != '\0'; i++) {
    printf("%c ", str[i]);
}
// Prints: H e l l o
```

Or using a pointer:

```c
char str[] = "Hello";
char *p = str;

while (*p != '\0') {
    printf("%c ", *p);
    p++;
}
```

### 3.1.9 Memory Layout of a C Program

Understanding how a C program is organized in memory is crucial for understanding pointers, arrays, function calls, and dynamic allocation.

A typical C program's memory is divided into several segments:

**Text Segment (Code Segment):**

This segment contains the executable machine code instructions of your program. It is typically read-only to prevent the program from accidentally modifying its own code. This segment is loaded from the executable file when the program starts.

**Data Segment:**

Contains initialized global and static variables:

```c
int global_initialized = 42;  // Stored in data segment
```

**BSS Segment (Block Started by Symbol):**

Contains uninitialized global and static variables, which are automatically initialized to zero:

```c
int global_uninitialized;  // Stored in BSS segment, initialized to 0
```

The BSS segment does not actually store all these zeros in the executable file—it just records how much zero-initialized space is needed. This saves disk space.

**Heap:**

The heap is used for dynamic memory allocation (which we will cover next). Memory allocated with `malloc` comes from the heap. The heap grows upward (toward higher addresses) as more memory is allocated.

**Stack:**

The stack stores local variables, function parameters, and return addresses. Each time a function is called, a new **stack frame** is pushed onto the stack, containing that function's local variables. When the function returns, its stack frame is popped off. The stack grows downward (toward lower addresses) on most systems.

**Typical Memory Layout:**

```
High addresses
+------------------+
|   Stack          | ← Grows downward
|        ↓         |
+------------------+
|                  |
|   (unused)       |
|                  |
+------------------+
|        ↑         |
|   Heap           | ← Grows upward
+------------------+
|   BSS            | (uninitialized global/static)
+------------------+
|   Data           | (initialized global/static)
+------------------+
|   Text (Code)    | (read-only, executable)
+------------------+
Low addresses
```

**Example:**

```c
int global_var = 100;      // Data segment

void function(int param) {  // param on stack
    int local_var = 200;    // Stack
    static int static_var = 300;  // Data segment (initialized once)

    int *heap_var = malloc(sizeof(int));  // Pointer on stack
    *heap_var = 400;        // Allocated memory on heap

    free(heap_var);
}
```

### 3.1.10 Dynamic Memory Allocation

So far, all variables we have seen have **automatic storage duration**—they are created when execution enters their scope and destroyed when execution leaves. The size of arrays must be known at compile time. But what if you need to allocate memory whose size is determined at runtime? This is where dynamic memory allocation comes in.

**The malloc Function:**

`malloc` (memory allocate) requests a block of memory from the heap:

```c
#include <stdlib.h>

int *p = malloc(sizeof(int) * 10);  // Allocate array of 10 ints
```

`malloc` takes the number of bytes to allocate and returns a pointer to the allocated memory. If allocation fails (not enough memory available), it returns NULL.

Always check if `malloc` succeeded:

```c
int *p = malloc(sizeof(int) * 10);
if (p == NULL) {
    printf("Memory allocation failed\n");
    return 1;
}
```

**Using Allocated Memory:**

Once allocated, you use the memory like any other:

```c
int *numbers = malloc(sizeof(int) * 5);
if (numbers == NULL) {
    return 1;
}

for (int i = 0; i < 5; i++) {
    numbers[i] = i * 10;
}

for (int i = 0; i < 5; i++) {
    printf("%d ", numbers[i]);
}

free(numbers);  // Must free when done
```

**The free Function:**

Memory allocated with `malloc` is not automatically freed when it goes out of scope. You must explicitly free it with `free`:

```c
free(p);
```

Failing to free allocated memory causes **memory leaks**—the program accumulates more and more allocated memory that it is not using, eventually exhausting available memory.

**Rules for Dynamic Memory:**

1. Always check if `malloc` returned NULL
2. Always `free` memory when you are done with it
3. Never `free` the same memory twice (undefined behavior)
4. Never use memory after freeing it (dangling pointer)
5. Never `free` memory that was not allocated with `malloc` (or `calloc` or `realloc`)

**Other Allocation Functions:**

**calloc** (contiguous allocation) allocates memory and initializes it to zero:

```c
int *p = calloc(10, sizeof(int));  // 10 integers, all initialized to 0
```

**realloc** (reallocation) resizes a previously allocated block:

```c
int *p = malloc(sizeof(int) * 10);
// ... use p ...
p = realloc(p, sizeof(int) * 20);  // Expand to 20 integers
```

If `realloc` cannot expand the existing block in place, it allocates a new block, copies the old data to it, and frees the old block. If reallocation fails, it returns NULL and the original block remains valid.

---

## 3.2 Advanced C Concepts

### 3.2.1 Structures

A **structure** (or **struct**) is a user-defined data type that groups related variables of different types:

```c
struct Person {
    char name[50];
    int age;
    double salary;
};
```

This defines a new type called `struct Person`. Each instance of this type contains three members: a name (character array), an age (integer), and a salary (double).

**Declaring Structure Variables:**

```c
struct Person employee;
```

**Accessing Members:**

Use the dot operator (`.`) to access structure members:

```c
struct Person employee;

strcpy(employee.name, "John Doe");
employee.age = 30;
employee.salary = 50000.0;

printf("Name: %s\n", employee.name);
printf("Age: %d\n", employee.age);
printf("Salary: %.2f\n", employee.salary);
```

**Initializing Structures:**

You can initialize structures when declaring them:

```c
struct Person employee = {"John Doe", 30, 50000.0};
```

Or with designated initializers (C99):

```c
struct Person employee = {
    .name = "John Doe",
    .age = 30,
    .salary = 50000.0
};
```

**Typedef for Structures:**

Using `typedef` allows you to create an alias, eliminating the need to write `struct` every time:

```c
typedef struct {
    char name[50];
    int age;
    double salary;
} Person;

Person employee;  // No need for 'struct' keyword
```

**Pointers to Structures:**

You can create pointers to structures:

```c
Person employee = {"John Doe", 30, 50000.0};
Person *ptr = &employee;
```

When accessing members through a pointer, use the arrow operator (`->`) instead of the dot operator:

```c
printf("Name: %s\n", ptr->name);
printf("Age: %d\n", ptr->age);
printf("Salary: %.2f\n", ptr->salary);
```

The arrow operator `ptr->member` is equivalent to `(*ptr).member`, but it is more concise and clearer.

**Structures and Memory Layout:**

Structure members are stored in memory in the order they are declared, but there may be **padding** between members to satisfy alignment requirements:

```c
struct Example {
    char a;      // 1 byte
    int b;       // 4 bytes
    char c;      // 1 byte
};
```

You might expect this structure to be 6 bytes (1 + 4 + 1), but it is actually larger due to padding:

```
Offset 0:   a (1 byte)
Offset 1-3: padding (3 bytes)
Offset 4-7: b (4 bytes)
Offset 8:   c (1 byte)
Offset 9-11: padding (3 bytes, to align entire structure)
Total: 12 bytes
```

The compiler inserts padding to ensure that `b` starts at an address divisible by 4 (its alignment requirement). You can use `sizeof` to determine the actual size:

```c
printf("Size: %zu\n", sizeof(struct Example));  // Prints 12, not 6
```

To minimize wasted space, order structure members from largest to smallest:

```c
struct Optimized {
    int b;       // 4 bytes
    char a;      // 1 byte
    char c;      // 1 byte
    // 2 bytes padding at end
};
// Total: 8 bytes instead of 12
```

### 3.2.2 Unions

A **union** is similar to a structure, but all members share the same memory location. A union can hold only one member at a time:

```c
union Data {
    int i;
    double d;
    char str[20];
};
```

The size of a union is the size of its largest member:

```c
printf("Size: %zu\n", sizeof(union Data));  // Size of char[20] = 20
```

**Using Unions:**

```c
union Data data;

data.i = 42;
printf("Integer: %d\n", data.i);

data.d = 3.14;  // Overwrites the integer value
printf("Double: %f\n", data.d);
```

Once you assign to `data.d`, the previous integer value is lost—you cannot access both simultaneously because they occupy the same memory.

Unions are useful when you need to store different types at different times but never simultaneously, saving memory. They are also used in low-level programming to reinterpret the bits of one type as another type (a technique called **type punning**).

### 3.2.3 Bit Fields

Sometimes you need to work with data at the bit level, especially when interfacing with hardware or implementing protocols. **Bit fields** allow you to specify the exact number of bits for each member of a structure:

```c
struct Flags {
    unsigned int flag1 : 1;  // 1 bit
    unsigned int flag2 : 1;  // 1 bit
    unsigned int flag3 : 1;  // 1 bit
    unsigned int value : 5;  // 5 bits
};
```

This structure uses only 8 bits (1 byte) instead of 16 bytes (four `unsigned int` variables).

**Using Bit Fields:**

```c
struct Flags flags = {0};

flags.flag1 = 1;
flags.value = 15;

if (flags.flag1) {
    printf("Flag 1 is set\n");
}
```

Bit fields have limitations:

- You cannot take the address of a bit field (cannot create a pointer to it)
- Bit field layout is implementation-defined
- They are less portable than explicit bit manipulation

For portable code, explicit bitwise operations are often preferred:

```c
#define FLAG1 (1 << 0)  // 0x01
#define FLAG2 (1 << 1)  // 0x02
#define FLAG3 (1 << 2)  // 0x04

unsigned int flags = 0;

flags |= FLAG1;          // Set FLAG1
flags &= ~FLAG2;         // Clear FLAG2
if (flags & FLAG3) {     // Test FLAG3
    // ...
}
```

### 3.2.4 Enumerations

An **enumeration** (or **enum**) defines a set of named integer constants:

```c
enum Color {
    RED,      // 0
    GREEN,    // 1
    BLUE      // 2
};
```

By default, enumeration constants start at 0 and increment by 1. You can specify explicit values:

```c
enum Status {
    SUCCESS = 0,
    ERROR = -1,
    PENDING = 100
};
```

**Using Enumerations:**

```c
enum Color favorite = BLUE;

if (favorite == BLUE) {
    printf("Your favorite color is blue\n");
}
```

Enumerations make code more readable than using raw numbers:

```c
// Without enum
if (status == 0) { ... }  // What does 0 mean?

// With enum
if (status == SUCCESS) { ... }  // Much clearer
```

### 3.2.5 Function Pointers

Functions also have addresses in memory (they reside in the text segment). A **function pointer** stores the address of a function, allowing you to call functions indirectly:

```c
// Function that adds two integers
int add(int a, int b) {
    return a + b;
}

// Function that subtracts two integers
int subtract(int a, int b) {
    return a - b;
}

int main(void) {
    // Declare a function pointer
    int (*operation)(int, int);

    // Point to the add function
    operation = add;
    printf("10 + 5 = %d\n", operation(10, 5));

    // Point to the subtract function
    operation = subtract;
    printf("10 - 5 = %d\n", operation(10, 5));

    return 0;
}
```

The declaration `int (*operation)(int, int)` reads as: "`operation` is a pointer to a function that takes two `int` parameters and returns an `int`."

**Function Pointers for Callbacks:**

Function pointers are commonly used for **callbacks**—functions passed as arguments to other functions:

```c
void process_array(int *arr, int size, int (*callback)(int)) {
    for (int i = 0; i < size; i++) {
        arr[i] = callback(arr[i]);
    }
}

int square(int x) {
    return x * x;
}

int cube(int x) {
    return x * x * x;
}

int main(void) {
    int numbers[] = {1, 2, 3, 4, 5};

    process_array(numbers, 5, square);  // Square each element
    process_array(numbers, 5, cube);    // Cube each element

    return 0;
}
```

### 3.2.6 The Preprocessor

The C preprocessor runs before the actual compilation, performing text substitution and conditional compilation.

**Macro Definitions:**

`#define` creates a macro:

```c
#define PI 3.14159
#define MAX(a, b) ((a) > (b) ? (a) : (b))

double area = PI * radius * radius;
int maximum = MAX(x, y);
```

The preprocessor performs simple text substitution—`PI` is replaced with `3.14159` wherever it appears. Function-like macros like `MAX` are also replaced textually.

**Important:** Use parentheses liberally in macros to avoid precedence issues:

```c
#define SQUARE(x) x * x         // Dangerous
int result = SQUARE(2 + 3);     // Expands to: 2 + 3 * 2 + 3 = 11 (not 25!)

#define SQUARE(x) ((x) * (x))   // Safe
int result = SQUARE(2 + 3);     // Expands to: ((2 + 3) * (2 + 3)) = 25
```

**Conditional Compilation:**

Preprocessor directives allow you to include or exclude code based on conditions:

```c
#define DEBUG

#ifdef DEBUG
    printf("Debug: x = %d\n", x);
#endif
```

This is useful for:

- Including debug code only in debug builds
- Platform-specific code (Windows vs. Linux)
- Feature flags

**Include Guards:**

Header files use include guards to prevent multiple inclusion:

```c
#ifndef MY_HEADER_H
#define MY_HEADER_H

// Header contents here

#endif
```

If the file is included multiple times, only the first inclusion has an effect.

### 3.2.7 Storage Classes

Storage classes specify the lifetime and visibility of variables:

**auto:** The default for local variables. Variables are created when entering the block and destroyed when leaving:

```c
void function(void) {
    auto int x = 5;  // 'auto' is usually omitted
}
```

**register:** Suggests that the variable be stored in a CPU register for faster access:

```c
register int counter;
```

This is only a suggestion—the compiler may ignore it. In modern C, compilers are better at register allocation than humans, so `register` is rarely used.

**static:** Changes the lifetime of local variables to the entire program duration, not just the scope:

```c
void function(void) {
    static int call_count = 0;  // Initialized only once
    call_count++;
    printf("Called %d times\n", call_count);
}
```

Each time `function` is called, `call_count` retains its value from previous calls.

For global variables, `static` limits visibility to the current source file:

```c
static int internal_variable = 0;  // Not visible in other files
```

**extern:** Declares a variable defined in another source file:

```c
// In file1.c
int global_var = 42;

// In file2.c
extern int global_var;  // Declares (does not define) global_var
printf("%d\n", global_var);  // Can use it
```

### 3.2.8 Type Casting

**Implicit Casting:**

C automatically converts between compatible types in some situations:

```c
int i = 42;
double d = i;  // int implicitly converted to double
```

**Explicit Casting:**

You can explicitly convert types using a **cast**:

```c
double d = 3.14;
int i = (int)d;  // i = 3 (fractional part discarded)
```

Casts are important when you need to force a specific conversion or when working with pointers:

```c
void *generic_ptr = malloc(sizeof(int));
int *int_ptr = (int *)generic_ptr;  // Cast void* to int*
```

**Dangerous Casts:**

Casting between pointer types can be dangerous:

```c
int x = 0x12345678;
char *p = (char *)&x;

// p[0], p[1], p[2], p[3] access individual bytes of x
// The order depends on endianness
```

This technique (called **type punning**) can violate strict aliasing rules and should be used carefully.

### 3.2.9 The const and volatile Qualifiers

**const:**

The `const` qualifier indicates that a variable's value should not change:

```c
const int max = 100;
max = 200;  // ERROR: cannot modify const variable
```

`const` with pointers can be tricky:

```c
const int *p;        // Pointer to const int: cannot modify *p
int const *p;        // Same as above
int * const p;       // Const pointer to int: cannot modify p (but can modify *p)
const int * const p; // Const pointer to const int: cannot modify p or *p
```

**volatile:**

The `volatile` qualifier tells the compiler that a variable's value can change unexpectedly, so optimizations that assume the value remains constant are disabled:

```c
volatile int sensor_reading;

while (sensor_reading < 100) {
    // Without volatile, the compiler might optimize this to an infinite loop
    // if it thinks sensor_reading never changes
}
```

`volatile` is used for:

- Hardware registers (memory-mapped I/O)
- Variables modified by interrupt handlers
- Variables shared between threads

### 3.2.10 Memory Alignment and Padding

As mentioned earlier with structures, the compiler inserts padding to satisfy alignment requirements. Understanding alignment is important for:

- Optimizing structure sizes
- Interfacing with hardware
- Avoiding performance penalties

**Alignment Rules:**

Most systems require that multi-byte values be aligned to addresses that are multiples of their size:

- 2-byte values: addresses divisible by 2
- 4-byte values: addresses divisible by 4
- 8-byte values: addresses divisible by 8

**The offsetof Macro:**

The `offsetof` macro (from `<stddef.h>`) tells you the byte offset of a member within a structure:

```c
#include <stddef.h>

struct Example {
    char a;
    int b;
    char c;
};

printf("Offset of a: %zu\n", offsetof(struct Example, a));  // 0
printf("Offset of b: %zu\n", offsetof(struct Example, b));  // 4 (not 1, due to padding)
printf("Offset of c: %zu\n", offsetof(struct Example, c));  // 8
printf("Total size: %zu\n", sizeof(struct Example));         // 12
```

**Packed Structures:**

Some compilers allow you to disable padding using attributes or pragmas:

```c
struct __attribute__((packed)) Packed {
    char a;
    int b;
    char c;
};
// sizeof(struct Packed) = 6 (no padding)
```

Packed structures save space but may cause performance issues and alignment errors on some architectures.

---

## Chapter 3 Summary

In this chapter, you have learned the C programming language with a focus on how it relates to the underlying computer system:

**C Fundamentals:** You now understand variables, data types, operators, control flow, functions, and arrays. You can write complete C programs that compile and run.

**Pointers:** You have learned one of C's most powerful and dangerous features. Pointers give you direct access to memory addresses, allowing you to understand exactly what happens at the hardware level. You can use pointers to pass data efficiently, create dynamic data structures, and interface with system-level code.

**Memory Model:** You understand how C programs are organized in memory, with distinct segments for code, data, BSS, heap, and stack. This knowledge is essential for understanding how programs execute and for debugging memory-related issues.

**Advanced Features:** You have explored structures, unions, enumerations, function pointers, bit manipulation, and type casting. These features allow you to write sophisticated programs that work efficiently with hardware.

**Dynamic Memory:** You can allocate and free memory at runtime, giving you the flexibility to create data structures of any size. This power comes with the responsibility to manage memory correctly to avoid leaks and corruption.

C serves as the bridge between high-level programming concepts and low-level hardware operation. When you write C code, you can visualize exactly what the processor will do: how variables map to memory locations and registers, how function calls use the stack, how pointers dereference memory addresses. This understanding is invaluable not only for writing efficient C programs but also for everything that follows in this curriculum.

The next phase will take you deeper into computer architecture, beginning with a detailed study of the x86-64 architecture. You will see how the C concepts you have learned—variables, functions, structures, pointers—are implemented at the instruction level. You will understand how the compiler translates C code into assembly language, and eventually into the machine code that the processor executes.

Before proceeding to Phase 2, ensure you are comfortable with all the concepts in this chapter. Write C programs that use pointers, dynamic memory, structures, and functions. Experiment with different data types and observe their sizes and alignment. Use a debugger to step through your code and watch how variables are stored in memory. The time you invest in mastering C will pay dividends throughout your study of computer systems.

When you are ready, we will begin our deep dive into the x86-64 architecture, where you will see how everything you have learned so far comes together at the hardware level.
