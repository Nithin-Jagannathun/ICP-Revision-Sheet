# Data Types

Java data types tell Java **what kind of data a variable stores** and how that data should be interpreted.

Java has two broad categories of data types:

- **Primitive data types** → directly store simple values.
- **Reference data types** → store a reference to an object/data structure.

> For ICP, the primitive types are the most important ones to know. Reference types such as `String` and arrays will be used later on.

---

## Primitive Data Types

Java has **8 primitive data types**:

| Type | What it stores | Size |
|---|---|---:|
| `byte` | Small integers | 8 bits |
| `short` | Small integers | 16 bits |
| `int` | Integers | 32 bits |
| `long` | Large integers | 64 bits |
| `float` | Decimal numbers | 32 bits |
| `double` | Decimal numbers | 64 bits |
| `char` | A single character | 16 bits |
| `boolean` | `true` / `false` | — |

---

## Integers

### `int`

The default integer type in Java.

```java
int x = 100;
```

Range:

$$
-2^{31} \text{ to } 2^{31}-1
$$

Approximately:

```text
-2 × 10^9 to +2 × 10^9
```

Use `int` for most ordinary integer calculations.

---

### `long`

Used when an integer may be too large for an `int`.

```java
long x = 10000000000L;
```

Range:

$$
-2^{63} \text{ to } 2^{63}-1
$$

Approximately:

```text
-9 × 10^18 to +9 × 10^18
```

> **Important:** Put `L` after a large integer literal to explicitly make it a `long`.

```java
long x = 10000000000L;
```

---

### `byte` and `short`

These are smaller integer types:

```java
byte a = 100;
short b = 10000;
```

Their ranges are:

| Type | Range |
|---|---|
| `byte` | $-2^7$ to $2^7-1$ |
| `short` | $-2^{15}$ to $2^{15}-1$ |

These are rarely used.

---

## Decimals

### `float`

Stores decimal numbers with less precision than `double`.

```java
float x = 3.14f;
```

> **Important:** Decimal literals such as `3.14` are `double` by default, so use `f` when assigning one directly to a `float`.

---

### `double`

The usual choice for decimal values.

```java
double x = 3.14;
```

It provides more precision than `float`.

In most situations, prefer `double` over `float` unless there is a specific reason to use `float`.

---

## `char`

Stores a **single character**.

```java
char c = 'A';
```

Characters use **single quotes**:

```java
'A'
```

whereas strings use **double quotes**:

```java
"Hello"
```

A `char` is internally represented using a numeric Unicode value, so arithmetic with characters is possible.

```java
char c = 'A';
int x = c + 1;

System.out.println(x);  // 66
```

---

## `boolean`

Stores only two possible values:

```java
true
false
```

Example:

```java
boolean passed = true;
```

Booleans are mainly used for conditions and logical operations.

---

# Reference Data Types

Reference types don't directly store the object itself. Instead, a variable stores a **reference to an object**.

Examples include:

```java
String name = "Nithin";
int[] numbers = {1, 2, 3};
```

`String` is a class, while arrays are array types. Both are **reference types**.

Other examples include:

- Classes
- Objects
- Arrays
- `String`
- `ArrayList`
- Other data structures

> You don't need to worry too much about the details of references yet. We'll cover them properly when we get to objects and data structures.

---

# Typecasting

**Typecasting** means explicitly converting a value from one data type to another.

```java
int x = 10;
double y = (double) x;
```

Now:

```text
x = 10       → int
y = 10.0     → double
```

The general syntax is:

```java
(new_type) value
```

For example:

```java
double x = 10.5;
int y = (int) x;
```

---

# Widening Conversion

A value can generally be converted from a **smaller-range numeric type to a larger-range compatible type** automatically.

```java
int x = 10;
long y = x;
```

Here, Java automatically converts the `int` to a `long`.

A simplified numeric hierarchy to remember is:

```text
byte → short → int → long → float → double
```

So:

```java
int x = 10;
double y = x;
```

is valid without explicitly casting.

This is called **widening conversion**.

> **General idea:** A value from a smaller type can generally fit inside a larger compatible type, so Java can perform the conversion automatically.

---

# Narrowing Conversion

Going from a larger type to a smaller type is generally **not done automatically**, because information may be lost.

```java
double x = 10.5;
int y = (int) x;
```

The explicit cast is required.

The result is:

```text
y = 10
```

The decimal part is discarded.

Another example:

```java
long x = 100000;
int y = (int) x;
```

This is allowed because we explicitly tell Java to perform the conversion.

However, if the value is too large for the destination type, the result may be incorrect due to overflow.

For example:

```java
int x = 10000000000;       // ❌ Doesn't fit in int
int y = (int) 10000000000L;
```

The second conversion is allowed, but the value cannot be represented correctly as an `int`.

---

# Data Types in Operations

When different numeric types are involved in an operation, Java **promotes the operands to a wider compatible type** before performing the operation.

For example:

```java
int x = 5;
long y = 10;

long z = x + y;
```

The `int` is promoted to `long`, so the operation is effectively:

```text
long + long → long
```

Similarly:

```java
int x = 5;
double y = 2.5;

double z = x + y;
```

The `int` is promoted to `double`:

```text
double + double → double
```

---

## Numeric Promotion

A simplified hierarchy to remember is:

```text
byte → short → int → long → float → double
```

When different numeric types are used together, Java generally promotes the smaller type to the wider type.

For example:

```java
int a = 5;
double b = 2.5;

double c = a + b;
```

Conceptually:

```text
int + double
     ↓
double + double
     ↓
double
```

> **Important:** The exact rules are more detailed for some types, but this hierarchy is sufficient for most basic problems.

---

# ⚠️ Common Trap: Integer Division

Consider:

```java
int x = 5;
int y = 2;

double z = x / y;
```

You might expect:

```text
2.5
```

But the answer is:

```text
2.0
```

Why?

Both operands are `int`:

```text
int / int → int
```

The division happens **before** the result is assigned to `double`.

So:

```text
5 / 2 → 2
```

and then:

```text
2 → 2.0
```

To get `2.5`, make at least one operand a `double`:

```java
double z = (double) x / y;
```

Now:

```text
double / int → double
```

so:

```text
z = 2.5
```

You could also write:

```java
double z = x / 2.0;
```

---

# ⚠️ Common Trap: Assignment Does Not Change the Operation

Consider:

```java
int a = 5;
int b = 2;

double result = a / b;
```

The fact that `result` is a `double` **does not make `a / b` a floating-point division**.

The operation is determined by the types of the operands:

```text
a / b
↓
int / int
↓
int
↓
2
```

Only after this does the result get assigned to `double`.

Therefore:

```java
double result = (double) a / b;
```

is required if you want `2.5`.

> **Remember:** The types of the operands determine how an operation is performed. The type of the variable receiving the result does not retroactively change the operation.

---

# ⚠️ Common Trap: Character Arithmetic

Characters can participate in arithmetic because `char` has a numeric Unicode value.

```java
char c = 'A';

System.out.println(c + 1);
```

Output:

```text
66
```

This happens because:

```text
'A' → 65
65 + 1 → 66
```

However:

```java
char c = 'A';

System.out.println(c + 1);
```

produces an `int`, not a `char`.

If you want the resulting character:

```java
char c = 'A';

char next = (char)(c + 1);

System.out.println(next);  // B
```

---

# Typecasting vs Automatic Conversion

### Automatic conversion

Java can automatically widen a value:

```java
int x = 10;
double y = x;
```

### Explicit conversion

You need to explicitly cast when narrowing:

```java
double x = 10.5;
int y = (int) x;
```

Think:

```text
Smaller → Larger     ✅ Usually automatic
Larger  → Smaller    ⚠️ Usually requires casting
```

---

# Quick Revision

## Primitive Types

```text
byte      → 8-bit integer
short     → 16-bit integer
int       → 32-bit integer
long      → 64-bit integer

float     → 32-bit decimal
double    → 64-bit decimal

char      → single character
boolean   → true / false
```

## Important Ranges

```text
int:
-2^31 to 2^31 - 1

long:
-2^63 to 2^63 - 1
```

## Numeric Promotion

```text
byte → short → int → long → float → double
```

## Conversion

```text
Smaller → Larger     ✅ Usually automatic
Larger  → Smaller    ❌ Usually requires casting
```

## Typecasting

```java
(new_type) value
```

Example:

```java
int x = (int) 10.5;  // 10
```

## Integer Division

```java
5 / 2       // 2
5.0 / 2     // 2.5
(double)5/2 // 2.5
```

## Remember

> **The operands determine the type of the operation, not the variable receiving the result.**
