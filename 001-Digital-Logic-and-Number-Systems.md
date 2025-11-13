# Chapter 1: Digital Logic and Number Systems

## Introduction to Chapter 1

Welcome to the beginning of your journey into the world of computer systems. Before we can understand how processors execute instructions or how operating systems manage memory, we must first understand the fundamental language that computers speak. This language is not made of words or sentences, but of electrical signals that can exist in only two states: on or off, high voltage or low voltage, one or zero.

This binary nature of computer hardware might seem limiting at first. After all, how can a system that only understands two symbols possibly represent the rich variety of information we work with every day—numbers, text, images, sound, and video? The answer lies in the clever mathematical systems and logical frameworks that humans have developed to encode all types of information using only these two states.

In this chapter, you will discover how computers represent and manipulate information at the most fundamental level. You will learn to think in binary, to understand the algebra of logic, and to see how all the complex operations a computer performs ultimately reduce to simple manipulations of ones and zeros. These concepts form the bedrock upon which everything else in computing is built, and understanding them deeply will illuminate every topic that follows.

Take your time with this material. The concepts here are deceptively simple yet profoundly important. When you truly grasp how binary representation works and how Boolean logic enables computation, you will have taken the first crucial step toward mastering computer systems at their deepest level.

---

## 1.1 Binary Number Systems

### 1.1.1 Understanding Positional Notation

Before we can understand binary numbers, we must first understand how the decimal number system you use every day actually works. You have been using decimal numbers since childhood, and their operation probably seems natural and obvious. However, taking a moment to examine the underlying principles of decimal notation will make the transition to binary much clearer.

Consider the decimal number 3,482. What does this number actually mean? It represents three thousands, four hundreds, eight tens, and two ones. We can express this more formally as:

$$3482 = (3 \times 1000) + (4 \times 100) + (8 \times 10) + (2 \times 1)$$

Notice that each position in the number represents a power of ten. The rightmost position represents $10^0$ (which equals 1), the next position to the left represents $10^1$ (which equals 10), then $10^2$ (which equals 100), and so on. We can rewrite our example using this exponential notation:

$$3482 = (3 \times 10^3) + (4 \times 10^2) + (8 \times 10^1) + (2 \times 10^0)$$

This system is called **positional notation** because the position of each digit determines its value. The digit 3 in the example above does not simply mean "three"—it means "three thousands" because of its position. If we moved that 3 to the rightmost position, it would mean only "three ones."

The decimal system uses ten as its **base** or **radix** because we have ten distinct symbols (0, 1, 2, 3, 4, 5, 6, 7, 8, 9) to represent quantities. Why ten? The most likely explanation is biological: humans have ten fingers, and early counting systems naturally reflected this physical reality. However, there is nothing mathematically special about the number ten. We could build a number system using any base we choose, and the system would work equally well.

This brings us to binary, the number system that computers use.

### 1.1.2 The Binary Number System

The binary number system uses two as its base. Instead of ten symbols, binary uses only two: 0 and 1. Each position in a binary number represents a power of two rather than a power of ten. Just as the rightmost position in a decimal number represents $10^0$, the rightmost position in a binary number represents $2^0$ (which equals 1). Moving left, the next position represents $2^1$ (which equals 2), then $2^2$ (which equals 4), then $2^3$ (which equals 8), and so on.

Let us examine the binary number 1011. To understand what this represents in decimal, we multiply each digit by its corresponding power of two:

$$1011_2 = (1 \times 2^3) + (0 \times 2^2) + (1 \times 2^1) + (1 \times 2^0)$$

$$1011_2 = (1 \times 8) + (0 \times 4) + (1 \times 2) + (1 \times 1)$$

$$1011_2 = 8 + 0 + 2 + 1 = 11_{10}$$

The small subscript numbers (2 for binary, 10 for decimal) indicate which base we are using. This notation helps prevent confusion when working with multiple number systems simultaneously.

Why do computers use binary? The answer is practical rather than mathematical. Electronic circuits can easily represent two distinct states: a high voltage (typically representing 1) and a low voltage (typically representing 0). Building circuits that could reliably distinguish between ten different voltage levels would be far more complex and error-prone. Binary electronics are simple, fast, and reliable.

Each binary digit is called a **bit**, which is short for "binary digit." A bit is the smallest unit of information in computing. A single bit can represent only two possibilities: true or false, yes or no, on or off, 1 or 0. By combining multiple bits, we can represent larger numbers and more complex information.

### 1.1.3 Converting Decimal to Binary

Now that you understand how binary numbers work, let us learn how to convert decimal numbers into binary. There are several methods for this conversion, but we will focus on the most intuitive approach: repeated division by two.

To convert a decimal number to binary, we repeatedly divide the number by 2 and record the remainders. The remainders, read in reverse order, give us the binary representation. Let us work through an example by converting the decimal number 13 to binary.

**Step 1:** Divide 13 by 2. The quotient is 6 and the remainder is 1.

$$13 \div 2 = 6 \text{ remainder } 1$$

**Step 2:** Divide the quotient (6) by 2. The new quotient is 3 and the remainder is 0.

$$6 \div 2 = 3 \text{ remainder } 0$$

**Step 3:** Divide 3 by 2. The quotient is 1 and the remainder is 1.

$$3 \div 2 = 1 \text{ remainder } 1$$

**Step 4:** Divide 1 by 2. The quotient is 0 and the remainder is 1.

$$1 \div 2 = 0 \text{ remainder } 1$$

When the quotient reaches 0, we stop. Now we read the remainders from bottom to top: 1, 1, 0, 1. Therefore:

$$13_{10} = 1101_2$$

We can verify this result by converting back to decimal:

$$1101_2 = (1 \times 8) + (1 \times 4) + (0 \times 2) + (1 \times 1) = 8 + 4 + 0 + 1 = 13_{10}$$

Why does this method work? Each time we divide by 2, we are essentially asking "how many groups of 2 can we make from this number?" The remainder tells us whether we need an additional 1 to represent what is left over. By working from the original number down to zero, we determine which powers of 2 are needed to reconstruct that number.

Let us practice with another example. We will convert 42 to binary:

$$42 \div 2 = 21 \text{ remainder } 0$$
$$21 \div 2 = 10 \text{ remainder } 1$$
$$10 \div 2 = 5 \text{ remainder } 0$$
$$5 \div 2 = 2 \text{ remainder } 1$$
$$2 \div 2 = 1 \text{ remainder } 0$$
$$1 \div 2 = 0 \text{ remainder } 1$$

Reading the remainders from bottom to top: 101010. Therefore:

$$42_{10} = 101010_2$$

Verification:

$$101010_2 = (1 \times 32) + (0 \times 16) + (1 \times 8) + (0 \times 4) + (1 \times 2) + (0 \times 1) = 32 + 8 + 2 = 42_{10}$$

### 1.1.4 Powers of Two: The Foundation of Binary

To work effectively with binary numbers, you should become familiar with powers of two. Just as you probably know your multiplication tables in decimal, familiarity with powers of two will make binary arithmetic much easier. Here are the first sixteen powers of two:

$$2^0 = 1$$
$$2^1 = 2$$
$$2^2 = 4$$
$$2^3 = 8$$
$$2^4 = 16$$
$$2^5 = 32$$
$$2^6 = 64$$
$$2^7 = 128$$
$$2^8 = 256$$
$$2^9 = 512$$
$$2^{10} = 1024$$
$$2^{11} = 2048$$
$$2^{12} = 4096$$
$$2^{13} = 8192$$
$$2^{14} = 16384$$
$$2^{15} = 32768$$

Notice that $2^{10} = 1024$, which is approximately 1000. In computing, we often use the prefix "kilo" to mean 1024 rather than 1000. Similarly, "mega" means $1024^2 = 1,048,576$ (approximately one million), and "giga" means $1024^3 = 1,073,741,824$ (approximately one billion). This explains why a "1 gigabyte" hard drive does not have exactly one billion bytes but rather about 1.07 billion bytes.

The number of values you can represent with $n$ bits follows a simple formula:

$$\text{Number of values} = 2^n$$

For example, with 8 bits, you can represent $2^8 = 256$ different values (from 0 to 255 if representing unsigned integers). With 16 bits, you can represent $2^{16} = 65,536$ different values. This exponential relationship means that adding just one more bit doubles the number of values you can represent.

### 1.1.5 Hexadecimal: A Compact Representation

Binary numbers, while fundamental to computers, can become unwieldy for humans to read and write. Consider representing the decimal number 250 in binary: 11111010. That is eight digits compared to three in decimal. For larger numbers, binary notation becomes even more cumbersome.

To solve this problem, computer scientists use **hexadecimal** (base 16) as a more compact way to represent binary numbers. Hexadecimal uses sixteen symbols: 0-9 for values zero through nine, and A-F for values ten through fifteen:

- 0 = 0, 1 = 1, 2 = 2, 3 = 3, 4 = 4, 5 = 5, 6 = 6, 7 = 7, 8 = 8, 9 = 9
- A = 10, B = 11, C = 12, D = 13, E = 14, F = 15

The beauty of hexadecimal is that each hexadecimal digit represents exactly four binary digits (bits). Since $2^4 = 16$, four bits can represent values from 0 to 15, which corresponds perfectly to a single hexadecimal digit. This makes conversion between binary and hexadecimal trivial.

Let us convert the binary number 11111010 to hexadecimal. We start by grouping the bits into sets of four, working from right to left:

$$1111 \quad 1010$$

Now we convert each group to its hexadecimal equivalent:

- $1111_2 = (8 + 4 + 2 + 1) = 15_{10} = \text{F}_{16}$
- $1010_2 = (8 + 0 + 2 + 0) = 10_{10} = \text{A}_{16}$

Therefore:

$$11111010_2 = \text{FA}_{16}$$

Converting from hexadecimal to binary is equally straightforward. Each hexadecimal digit expands to four binary digits. For example, to convert $\text{3C}_{16}$ to binary:

- $3_{16} = 0011_2$
- $\text{C}_{16} = 1100_2$

Therefore:

$$\text{3C}_{16} = 00111100_2$$

In practice, you will encounter hexadecimal notation frequently when working with computer systems. Memory addresses, machine code instructions, and color codes are typically written in hexadecimal. By convention, hexadecimal numbers are often prefixed with "0x" to distinguish them from decimal numbers. So the hexadecimal value FA would be written as 0xFA, and 3C would be written as 0x3C.

### 1.1.6 Converting Between Hexadecimal and Decimal

While converting between binary and hexadecimal is simple, converting between hexadecimal and decimal requires more calculation. Let us examine both directions.

**Hexadecimal to Decimal:**

To convert from hexadecimal to decimal, we use the same positional notation principle we saw earlier, but with base 16. Each position represents a power of 16.

Let us convert $\text{2A3}_{16}$ to decimal:

$$\text{2A3}_{16} = (2 \times 16^2) + (10 \times 16^1) + (3 \times 16^0)$$

$$\text{2A3}_{16} = (2 \times 256) + (10 \times 16) + (3 \times 1)$$

$$\text{2A3}_{16} = 512 + 160 + 3 = 675_{10}$$

**Decimal to Hexadecimal:**

To convert from decimal to hexadecimal, we use repeated division by 16, similar to our binary conversion method.

Let us convert $675_{10}$ to hexadecimal:

$$675 \div 16 = 42 \text{ remainder } 3$$
$$42 \div 16 = 2 \text{ remainder } 10 \text{ (which is A in hexadecimal)}$$
$$2 \div 16 = 0 \text{ remainder } 2$$

Reading the remainders from bottom to top: 2, A, 3. Therefore:

$$675_{10} = \text{2A3}_{16}$$

### 1.1.7 Binary Arithmetic Operations

Now that you understand binary representation, let us explore how to perform arithmetic operations in binary. These operations follow the same principles as decimal arithmetic, but with the rules adapted for base 2.

**Binary Addition:**

Binary addition follows simple rules:

- $0 + 0 = 0$
- $0 + 1 = 1$
- $1 + 0 = 1$
- $1 + 1 = 10$ (0 with a carry of 1)
- $1 + 1 + 1 = 11$ (1 with a carry of 1, when adding a carry bit)

Let us add two binary numbers: $1011_2 + 1101_2$

```
    1 1     <- carry bits
    1 0 1 1
  + 1 1 0 1
  ---------
  1 1 0 0 0
```

Working from right to left:

- Column 1: $1 + 1 = 10$. Write 0, carry 1.
- Column 2: $1 + 0 + 1 \text{ (carry)} = 10$. Write 0, carry 1.
- Column 3: $0 + 1 + 1 \text{ (carry)} = 10$. Write 0, carry 1.
- Column 4: $1 + 1 + 1 \text{ (carry)} = 11$. Write 1, carry 1.
- Column 5: Just the carry of 1 remains.

Result: $11000_2$

We can verify this in decimal:

- $1011_2 = 11_{10}$
- $1101_2 = 13_{10}$
- $11000_2 = 24_{10}$
- Indeed, $11 + 13 = 24$

**Binary Subtraction:**

Binary subtraction uses borrowing, just like decimal subtraction:

- $0 - 0 = 0$
- $1 - 0 = 1$
- $1 - 1 = 0$
- $0 - 1 = 1$ (with a borrow of 1 from the next position)

Let us subtract: $1101_2 - 1011_2$

```
   ₀1 1 0 1
 - 1 0 1 1
 ---------
   0 0 1 0
```

Working from right to left:

- Column 1: $1 - 1 = 0$
- Column 2: $0 - 1$ requires borrowing. The 1 in column 3 becomes 0, and column 2 becomes $10 - 1 = 1$
- Column 3: $0 - 0 = 0$ (after the borrow)
- Column 4: $1 - 1 = 0$

Result: $0010_2 = 10_2$

Verification: $13 - 11 = 2$

**Binary Multiplication:**

Binary multiplication is actually simpler than decimal multiplication because the only possible products are 0 or the original number:

- $0 \times 0 = 0$
- $0 \times 1 = 0$
- $1 \times 0 = 0$
- $1 \times 1 = 1$

Let us multiply: $101_2 \times 11_2$

```
      1 0 1
    ×   1 1
    -------
      1 0 1  (101 × 1)
    1 0 1    (101 × 1, shifted left)
    -------
    1 1 1 1
```

Result: $1111_2$

Verification:

- $101_2 = 5_{10}$
- $11_2 = 3_{10}$
- $1111_2 = 15_{10}$
- Indeed, $5 \times 3 = 15$

**Binary Division:**

Binary division works like long division in decimal. Let us divide $1111_2$ by $11_2$:

```
       1 0 1
     -------
11 | 1 1 1 1
     1 1
     ----
       0 1 1
         1 1
         ---
         0 0
```

Result: $101_2$ with no remainder.

Verification: $15 \div 3 = 5$

### 1.1.8 Octal: Another Historical System

While hexadecimal is dominant today, you may occasionally encounter **octal** (base 8) numbers, particularly in older systems and in Unix file permissions. Octal uses eight symbols: 0, 1, 2, 3, 4, 5, 6, 7.

Each octal digit represents exactly three binary bits, since $2^3 = 8$. Converting between binary and octal follows the same grouping principle as hexadecimal, but with groups of three bits instead of four.

Example: Convert $101110_2$ to octal.

Group into threes from right to left: $101 \quad 110$

- $101_2 = 5_8$
- $110_2 = 6_8$

Therefore: $101110_2 = 56_8$

While less common today, understanding octal helps you work with legacy systems and Unix permission masks (like 755 or 644).

---

## 1.2 Boolean Algebra and Logic Gates

### 1.2.1 Introduction to Boolean Algebra

In 1854, the English mathematician George Boole published "An Investigation of the Laws of Thought," in which he developed an algebraic system for logic. This system, now called Boolean algebra, deals with binary variables and logical operations. A century later, engineers realized that Boole's mathematical framework could be applied to the design of digital circuits, where the binary values true and false correspond naturally to high and low voltages.

Boolean algebra operates on values from the set {0, 1} or equivalently {false, true}. In this system, there are three fundamental operations: AND, OR, and NOT. From these three operations, we can build arbitrarily complex logical expressions and, ultimately, entire computer systems.

Understanding Boolean algebra is crucial because every operation a computer performs—whether adding numbers, comparing values, or making decisions—ultimately reduces to Boolean logic implemented in hardware through logic gates.

### 1.2.2 The NOT Operation

The NOT operation is the simplest Boolean operation. It takes a single input and produces the opposite value. If the input is 1, the output is 0. If the input is 0, the output is 1. The NOT operation is also called **negation** or **inversion**.

We can represent the NOT operation using several notations:

- $\overline{A}$ (overbar notation)
- $\neg A$ (negation symbol)
- $A'$ (prime notation)
- $!A$ (in programming languages)

This course will primarily use the overbar notation.

The behavior of the NOT operation can be completely described using a **truth table**, which lists all possible input values and their corresponding outputs:

| $A$ | $\overline{A}$ |
| --- | -------------- |
| 0   | 1              |
| 1   | 0              |

In hardware, the NOT operation is implemented using an **inverter** or **NOT gate**. The standard logic symbol for a NOT gate is a triangle pointing right with a small circle at the output (the circle indicates inversion).

### 1.2.3 The AND Operation

The AND operation takes two inputs and produces an output of 1 only when both inputs are 1. In all other cases, the output is 0. This corresponds to the logical meaning of "and" in everyday language: "it is raining AND it is cold" is true only when both conditions are true.

The AND operation is denoted as:

- $A \cdot B$ (multiplication symbol)
- $A \land B$ (logical AND symbol)
- $AB$ (juxtaposition)
- $A$ && $B$ (in programming)

We will primarily use $A \cdot B$ or simply $AB$.

The truth table for AND:

| $A$ | $B$ | $A \cdot B$ |
| --- | --- | ----------- |
| 0   | 0   | 0           |
| 0   | 1   | 0           |
| 1   | 0   | 0           |
| 1   | 1   | 1           |

The AND operation has several important properties:

**Identity:** $A \cdot 1 = A$  
Multiplying by 1 leaves the value unchanged.

**Null Element:** $A \cdot 0 = 0$  
Multiplying by 0 always gives 0.

**Idempotent:** $A \cdot A = A$  
ANDing a value with itself gives the same value.

**Commutative:** $A \cdot B = B \cdot A$  
The order of operands does not matter.

**Associative:** $(A \cdot B) \cdot C = A \cdot (B \cdot C)$  
Grouping does not affect the result.

### 1.2.4 The OR Operation

The OR operation takes two inputs and produces an output of 1 when at least one input is 1. The output is 0 only when both inputs are 0. This is called an **inclusive OR** because the output is true when both inputs are true as well as when just one is true.

The OR operation is denoted as:

- $A + B$ (addition symbol)
- $A \lor B$ (logical OR symbol)
- $A$ || $B$ (in programming)

We will primarily use $A + B$.

The truth table for OR:

| $A$ | $B$ | $A + B$ |
| --- | --- | ------- |
| 0   | 0   | 0       |
| 0   | 1   | 1       |
| 1   | 0   | 1       |
| 1   | 1   | 1       |

The OR operation also has important properties:

**Identity:** $A + 0 = A$  
ORing with 0 leaves the value unchanged.

**Null Element:** $A + 1 = 1$  
ORing with 1 always gives 1.

**Idempotent:** $A + A = A$  
ORing a value with itself gives the same value.

**Commutative:** $A + B = B + A$  
The order of operands does not matter.

**Associative:** $(A + B) + C = A + (B + C)$  
Grouping does not affect the result.

### 1.2.5 De Morgan's Laws

Two of the most important theorems in Boolean algebra are **De Morgan's Laws**, named after the mathematician Augustus De Morgan. These laws describe how to distribute the NOT operation over AND and OR operations:

**First De Morgan's Law:**

$$\overline{A \cdot B} = \overline{A} + \overline{B}$$

This states that the negation of an AND operation equals the OR of the negations. In words: "not (A and B)" is equivalent to "(not A) or (not B)."

**Second De Morgan's Law:**

$$\overline{A + B} = \overline{A} \cdot \overline{B}$$

This states that the negation of an OR operation equals the AND of the negations. In words: "not (A or B)" is equivalent to "(not A) and (not B)."

Let us verify the first law with a truth table:

| $A$ | $B$ | $A \cdot B$ | $\overline{A \cdot B}$ | $\overline{A}$ | $\overline{B}$ | $\overline{A} + \overline{B}$ |
| --- | --- | ----------- | ---------------------- | -------------- | -------------- | ----------------------------- |
| 0   | 0   | 0           | 1                      | 1              | 1              | 1                             |
| 0   | 1   | 0           | 1                      | 1              | 0              | 1                             |
| 1   | 0   | 0           | 1                      | 0              | 1              | 1                             |
| 1   | 1   | 1           | 0                      | 0              | 0              | 0                             |

Notice that the columns for $\overline{A \cdot B}$ and $\overline{A} + \overline{B}$ are identical, confirming that the expressions are equivalent.

De Morgan's Laws are invaluable for simplifying Boolean expressions and for converting between different forms of logic gates in circuit design.

### 1.2.6 Additional Boolean Operations

While AND, OR, and NOT are the fundamental operations, several other operations are commonly used in digital logic:

**XOR (Exclusive OR):**

The XOR operation produces 1 when the inputs are different and 0 when they are the same. It is denoted $A \oplus B$.

| $A$ | $B$ | $A \oplus B$ |
| --- | --- | ------------ |
| 0   | 0   | 0            |
| 0   | 1   | 1            |
| 1   | 0   | 1            |
| 1   | 1   | 0            |

XOR can be expressed in terms of AND, OR, and NOT:

$$A \oplus B = (A \cdot \overline{B}) + (\overline{A} \cdot B)$$

XOR is particularly useful for detecting differences, parity checking, and encryption. It has the interesting property that $A \oplus A = 0$ and $A \oplus 0 = A$, which makes it useful for toggling bits and for simple encryption schemes.

**NAND (NOT AND):**

NAND is the negation of AND. It produces 0 only when all inputs are 1.

| $A$ | $B$ | $\overline{A \cdot B}$ |
| --- | --- | ---------------------- |
| 0   | 0   | 1                      |
| 0   | 1   | 1                      |
| 1   | 0   | 1                      |
| 1   | 1   | 0                      |

NAND is a **universal gate**, meaning that any Boolean function can be implemented using only NAND gates. This is significant in hardware design because it simplifies manufacturing to have circuits built from a single type of gate.

**NOR (NOT OR):**

NOR is the negation of OR. It produces 1 only when all inputs are 0.

| $A$ | $B$ | $\overline{A + B}$ |
| --- | --- | ------------------ |
| 0   | 0   | 1                  |
| 0   | 1   | 0                  |
| 1   | 0   | 0                  |
| 1   | 1   | 0                  |

Like NAND, NOR is also a universal gate.

**XNOR (Exclusive NOR):**

XNOR is the negation of XOR. It produces 1 when the inputs are the same.

| $A$ | $B$ | $\overline{A \oplus B}$ |
| --- | --- | ----------------------- |
| 0   | 0   | 1                       |
| 0   | 1   | 0                       |
| 1   | 0   | 0                       |
| 1   | 1   | 1                       |

XNOR is also called the equivalence function because it returns 1 when its inputs are equivalent.

### 1.2.7 Boolean Expression Simplification

In circuit design, simpler expressions translate to fewer gates, which means lower cost, less power consumption, and higher reliability. Several techniques exist for simplifying Boolean expressions.

**Algebraic Simplification:**

We can use the properties and laws of Boolean algebra to simplify expressions algebraically. Consider this expression:

$$F = A \cdot B + A \cdot \overline{B}$$

We can factor out $A$:

$$F = A \cdot (B + \overline{B})$$

Since $B + \overline{B} = 1$ (a value is always either true or false):

$$F = A \cdot 1 = A$$

So the original expression simplifies to just $A$.

Let us try another example:

$$F = A \cdot B \cdot C + A \cdot B \cdot \overline{C} + A \cdot \overline{B} \cdot C$$

Factor out $A \cdot B$ from the first two terms:

$$F = A \cdot B \cdot (C + \overline{C}) + A \cdot \overline{B} \cdot C$$

$$F = A \cdot B \cdot 1 + A \cdot \overline{B} \cdot C$$

$$F = A \cdot B + A \cdot \overline{B} \cdot C$$

Factor out $A$:

$$F = A \cdot (B + \overline{B} \cdot C)$$

Using the absorption law $X + \overline{X} \cdot Y = X + Y$:

$$F = A \cdot (B + C)$$

The expression has been significantly simplified.

**Karnaugh Maps:**

For expressions with up to four or five variables, Karnaugh maps (K-maps) provide a visual method for simplification. A K-map is a grid where each cell represents one possible combination of input values. Adjacent cells differ in only one variable, allowing us to identify and eliminate redundant terms.

While K-maps are extremely useful, their graphical nature makes them less suitable for this text-based format. When you encounter them in circuit design courses, remember that they are visual tools for applying the same algebraic principles we have been discussing.

### 1.2.8 Logic Gates

In hardware, Boolean operations are implemented using electronic circuits called **logic gates**. Each gate takes one or more binary inputs and produces a binary output according to a specific Boolean function.

**Gate Symbols:**

Standard symbols exist for each type of gate. While we cannot draw these symbols perfectly in text, understanding their function is crucial:

- **NOT Gate (Inverter):** Takes one input and produces the inverted output
- **AND Gate:** Takes two or more inputs; output is 1 only if all inputs are 1
- **OR Gate:** Takes two or more inputs; output is 1 if any input is 1
- **NAND Gate:** An AND gate followed by an inverter
- **NOR Gate:** An OR gate followed by an inverter
- **XOR Gate:** Output is 1 if inputs are different
- **XNOR Gate:** Output is 1 if inputs are the same

**Gate Implementation:**

At the transistor level, gates are built using MOSFETs (Metal-Oxide-Semiconductor Field-Effect Transistors). A simple NOT gate can be built with just two transistors, while other gates require more complex arrangements. The details of transistor-level design are beyond our current scope, but it is worth knowing that all the complex logic operations computers perform ultimately reduce to the switching behavior of millions or billions of transistors.

**Propagation Delay:**

Real physical gates do not switch instantaneously. There is a small but non-zero time delay, called **propagation delay**, between when the inputs change and when the output reflects that change. This delay is typically measured in nanoseconds (billionths of a second) or even picoseconds (trillionths of a second) in modern circuits.

Propagation delay becomes important in high-speed circuits because it limits how fast the circuit can operate. The maximum clock speed of a processor is largely determined by the propagation delays through its longest path of logic gates.

---

## 1.3 Data Representation

### 1.3.1 Representing Unsigned Integers

The most straightforward way to represent positive whole numbers in binary is called **unsigned integer representation**. In this scheme, each bit position represents a power of two, and we simply add up the values of the positions where there is a 1.

With $n$ bits, we can represent integers from 0 to $2^n - 1$. For example:

- 8 bits: 0 to 255
- 16 bits: 0 to 65,535
- 32 bits: 0 to 4,294,967,295
- 64 bits: 0 to 18,446,744,073,709,551,615

This representation is efficient and straightforward, but it has one significant limitation: it cannot represent negative numbers. For applications that need to work with both positive and negative values, we need a different representation scheme.

### 1.3.2 Representing Signed Integers

Several schemes have been developed for representing signed integers in binary. Let us examine three approaches and understand why modern computers use the third.

**Sign-Magnitude Representation:**

The simplest approach is to use one bit (typically the leftmost bit) to represent the sign, with 0 meaning positive and 1 meaning negative. The remaining bits represent the magnitude (absolute value) of the number.

For example, with 8 bits:

- $01101010$ = +106
- $11101010$ = -106

This representation is intuitive and symmetric, but it has two significant problems:

1. There are two representations of zero: +0 (00000000) and -0 (10000000)
2. Addition and subtraction circuits become complex because they must handle the sign bit separately

**One's Complement Representation:**

In one's complement, negative numbers are represented by inverting all bits of the positive representation. To negate a number, flip all the bits.

For example, with 8 bits:

- $+5 = 00000101$
- $-5 = 11111010$ (all bits flipped)

One's complement solves some problems but still has two representations of zero:

- $+0 = 00000000$
- $-0 = 11111111$

**Two's Complement Representation:**

The modern solution, used in virtually all computers today, is **two's complement**. To negate a number in two's complement:

1. Invert all bits (one's complement)
2. Add 1 to the result

For example, with 8 bits:

- Start with $+5 = 00000101$
- Invert: $11111010$
- Add 1: $11111011 = -5$ in two's complement

Two's complement has several advantages:

1. There is only one representation of zero
2. Addition and subtraction use the same circuitry regardless of sign
3. The leftmost bit still indicates sign (0 = positive, 1 = negative)

The range of values for an $n$-bit two's complement number is $-2^{n-1}$ to $2^{n-1} - 1$. Notice that there is one more negative number than positive numbers. For 8 bits:

- Range: -128 to +127
- The number -128 (10000000) has no positive counterpart

The mathematical formula for interpreting an $n$-bit two's complement number is:

$$V = -a_{n-1} \cdot 2^{n-1} + \sum_{i=0}^{n-2} a_i \cdot 2^i$$

The leftmost bit (sign bit) contributes a negative value if it is 1, while all other bits contribute positive values as usual.

Let us verify our earlier example of $-5 = 11111011$:

$$V = -(1 \cdot 128) + (1 \cdot 64) + (1 \cdot 32) + (1 \cdot 16) + (1 \cdot 8) + (0 \cdot 4) + (1 \cdot 2) + (1 \cdot 1)$$

$$V = -128 + 64 + 32 + 16 + 8 + 2 + 1 = -128 + 123 = -5$$

### 1.3.3 Sign Extension

When converting a number from a smaller representation to a larger one, we must be careful to preserve the value. For unsigned numbers, we simply pad with zeros on the left. For signed numbers in two's complement, we use **sign extension**: we copy the sign bit into all the new higher-order positions.

For example, extending 8-bit $-5 = 11111011$ to 16 bits:

$$11111011 \rightarrow 1111111111111011$$

This preserves the value because all those additional 1 bits contribute $-(2^{15}) + 2^{14} + 2^{13} + ... + 2^{8}$, which equals $-2^{7}$ (the original contribution of the 8th bit).

Sign extension is crucial when mixing different integer sizes in expressions and when loading smaller values into larger registers.

### 1.3.4 Representing Floating-Point Numbers

Most real-world quantities cannot be represented as integers. Temperatures, distances, financial calculations, and scientific measurements often require fractional values. To represent these numbers, computers use **floating-point** representation, which is analogous to scientific notation.

In scientific notation, we write numbers like $6.022 \times 10^{23}$ (Avogadro's number) or $1.602 \times 10^{-19}$ (charge of an electron). This separates the **significand** (6.022 or 1.602) from the **exponent** (23 or -19), allowing us to represent both very large and very small numbers efficiently.

The most widely used floating-point standard is **IEEE 754**, which defines formats for single-precision (32-bit) and double-precision (64-bit) numbers.

**Single-Precision Format (32 bits):**

The 32 bits are divided into three fields:

- **Sign bit** (1 bit): 0 for positive, 1 for negative
- **Exponent** (8 bits): Represents the power of 2
- **Mantissa/Fraction** (23 bits): Represents the fractional part

The value is calculated as:

$$V = (-1)^s \times 2^{e-127} \times (1 + m)$$

where:

- $s$ is the sign bit
- $e$ is the 8-bit exponent (interpreted as an unsigned integer)
- $m$ is the mantissa interpreted as a binary fraction (0.something)

The exponent uses a **bias** of 127. This means the actual exponent is the stored value minus 127. For example, if the stored exponent is 130, the actual exponent is $130 - 127 = 3$, so we multiply by $2^3 = 8$.

The mantissa represents a fractional value between 0 and 1. Because normalized numbers always have a leading 1 (in binary scientific notation), this leading 1 is implicit and not stored, giving us an extra bit of precision. This is called the **hidden bit** or **implicit bit**.

**Example:** Let us represent the decimal number 12.375 in IEEE 754 single-precision format.

First, convert to binary:

- $12 = 1100_2$
- $0.375 = 0.011_2$ (since $0.25 + 0.125 = 0.375$)
- $12.375 = 1100.011_2$

Normalize to binary scientific notation:
$$1100.011_2 = 1.100011_2 \times 2^3$$

Now we can identify the components:

- Sign: 0 (positive)
- Exponent: $3 + 127 = 130 = 10000010_2$
- Mantissa: $.100011$ (we drop the leading 1)

Padding the mantissa to 23 bits:
$$10001100000000000000000_2$$

The complete representation:
$$0 \quad 10000010 \quad 10001100000000000000000$$

**Double-Precision Format (64 bits):**

Double-precision uses 64 bits divided as:

- Sign: 1 bit
- Exponent: 11 bits (bias of 1023)
- Mantissa: 52 bits

The formula is similar:

$$V = (-1)^s \times 2^{e-1023} \times (1 + m)$$

Double-precision provides greater range and precision than single-precision, but requires twice the memory and often takes longer to compute.

**Special Values:**

IEEE 754 defines several special values:

- **Zero:** Exponent and mantissa all zeros (separate +0 and -0)
- **Infinity:** Exponent all ones, mantissa all zeros
- **NaN (Not a Number):** Exponent all ones, mantissa non-zero

These special values allow programs to handle exceptional conditions like division by zero or undefined operations (like the square root of a negative number).

**Precision and Rounding:**

Floating-point representation can only approximate most real numbers. For example, the decimal number 0.1 cannot be represented exactly in binary floating-point, just as 1/3 cannot be represented exactly in decimal (0.333...). This leads to small rounding errors that can accumulate in long calculations.

These rounding errors are why you should never compare floating-point numbers for exact equality. Instead, check if two numbers are within a small tolerance (epsilon) of each other.

### 1.3.5 Character Encoding

Beyond numbers, computers must represent text. Characters are encoded as numbers using standardized encoding schemes.

**ASCII (American Standard Code for Information Interchange):**

ASCII uses 7 bits to represent 128 characters, including:

- Uppercase letters A-Z (65-90)
- Lowercase letters a-z (97-122)
- Digits 0-9 (48-57)
- Punctuation and special symbols
- Control characters (newline, tab, etc.)

For example:

- 'A' = 65 = 01000001
- 'a' = 97 = 01100001
- '0' = 48 = 00110000
- ' ' (space) = 32 = 00100000

Notice that lowercase letters are exactly 32 more than their uppercase equivalents. This difference of 32 corresponds to flipping a single bit (bit 5), which makes case conversion very efficient.

**Extended ASCII and Code Pages:**

The 8th bit in a byte allows for 128 additional characters (codes 128-255). Different "code pages" assigned different characters to these values, allowing support for various languages. However, this approach was limited and incompatible across systems.

**Unicode:**

Unicode is a comprehensive character encoding system designed to represent all characters from all writing systems used on earth. Unicode assigns a unique number (called a **code point**) to each character. For example:

- 'A' = U+0041
- '€' = U+20AC
- '中' = U+4E2D

**UTF-8 Encoding:**

UTF-8 is the dominant encoding for Unicode. It uses 1 to 4 bytes per character:

- ASCII characters (0-127) use 1 byte (identical to ASCII)
- Other characters use 2, 3, or 4 bytes

This makes UTF-8 backward-compatible with ASCII while supporting all Unicode characters. UTF-8 is the standard encoding for web pages, modern programming languages, and operating systems.

### 1.3.6 Endianness: Byte Ordering

When multi-byte values (like 32-bit integers or 64-bit floating-point numbers) are stored in memory, the order of the bytes matters. Two conventions exist:

**Big-Endian:**

The most significant byte is stored at the lowest memory address. This matches how we write numbers, with the most significant digit first.

Example: The 32-bit number 0x12345678 stored at address 0x1000:

```
Address:  0x1000  0x1001  0x1002  0x1003
Value:    0x12    0x34    0x56    0x78
```

**Little-Endian:**

The least significant byte is stored at the lowest memory address.

Example: The 32-bit number 0x12345678 stored at address 0x1000:

```
Address:  0x1000  0x1001  0x1002  0x1003
Value:    0x78    0x56    0x34    0x12
```

x86 and x86-64 processors use little-endian byte ordering. Other architectures (like PowerPC and some ARM configurations) use big-endian. Network protocols typically use big-endian (called "network byte order").

Endianness matters when:

- Sharing data files between systems
- Network communication
- Reading binary files
- Casting between pointer types

When working with individual bytes or viewing memory in a debugger, you must account for endianness to correctly interpret multi-byte values.

---

## Chapter 1 Summary

In this chapter, you have learned the fundamental concepts that underlie all of digital computing:

**Number Systems:** You now understand how to represent numbers in binary, hexadecimal, and octal. You can convert between different bases and perform arithmetic operations in binary. You have seen that while decimal is natural for humans due to our ten fingers, binary is natural for computers due to the two-state nature of electronic circuits.

**Boolean Algebra:** You have learned the three fundamental operations (AND, OR, NOT) and how they can be combined to create complex logical expressions. You understand De Morgan's Laws and how to simplify Boolean expressions. These operations form the basis of all digital logic circuits.

**Data Representation:** You know how computers represent different types of data—unsigned integers, signed integers (using two's complement), floating-point numbers (using IEEE 754), and characters (using ASCII and Unicode). You understand the trade-offs between different representation schemes and the limitations of finite precision.

These concepts are not merely theoretical. Every program you write, every calculation a computer performs, and every byte of data stored in memory ultimately relies on these fundamental principles. Binary numbers are the native language of computers. Boolean logic is the mathematics of digital circuits. Data representation schemes determine what information computers can process and how accurately they can process it.

As you proceed to the next chapter, you will see how these concepts combine to create the functional components of a computer system. The number systems you have learned will be used in memory addresses and machine code. The Boolean operations will be implemented in hardware as logic gates and combined to form arithmetic circuits. The data representation schemes will determine how values are stored in memory and registers.

Take time to practice these concepts. Convert numbers between different bases until it becomes second nature. Work through Boolean expressions and verify your simplifications with truth tables. Understand the limitations of floating-point representation and the implications of two's complement arithmetic. These skills will serve you throughout your study of computer systems and in your career working with computers at any level.

The foundation is now in place. You are ready to build upon it.
