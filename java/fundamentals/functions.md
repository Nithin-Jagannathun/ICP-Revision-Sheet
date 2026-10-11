# Functions in Java

## TL;DR

A **function** is a reusable block of code that performs a specific task. You give it some input, it performs a process, and it may return a result.

Functions help us:
- Avoid writing the same code multiple times.
- Break large problems into smaller, manageable tasks.
- Make code easier to read, test, debug, and maintain.

**Key idea:** Write a function when a particular task can be described clearly and may need to be performed independently or reused.

---

## 1. What Are Functions?

### A Simple Analogy

Think of a vending machine:

1. You provide an input (select a product and insert money).
2. The machine performs a process (checks the payment and selection).
3. It produces an output (the selected product).

A function works similarly. It takes input, performs a task, and may produce an output.

For example, suppose we want to calculate the square of a number.

```java
static int square(int n) {
    return n * n;
}
```

If we call `square(5)`, the function calculates \(5 \times 5\) and returns `25`.

We can then reuse it:

```java
System.out.println(square(5));  // 25
System.out.println(square(8));  // 64
System.out.println(square(12)); // 144
```

We don't need to rewrite the multiplication each time.

### Why Use Functions?

Imagine calculating the area of a circle at several places in your program. Without a function, you might repeatedly write:

```java
double area1 = 3.14159 * r1 * r1;
double area2 = 3.14159 * r2 * r2;
double area3 = 3.14159 * r3 * r3;
```

Instead, write one function:

```java
static double areaOfCircle(double radius) {
    return Math.PI * radius * radius;
}
```

Then call it whenever needed:

```java
double area1 = areaOfCircle(r1);
double area2 = areaOfCircle(r2);
double area3 = areaOfCircle(r3);
```

If we ever need to change the formula, we only need to change the function.

**Remember:** A function is not just a way to reduce lines of code. It also gives a name to a task, making your program easier to understand.

---

## 2. Structure of a Function

Consider the following function:

```java
static int add(int a, int b) {
    int sum = a + b;
    return sum;
}
```

Let's break it down.

| Component | Meaning | Example |
|---|---|---|
| `static` | Allows the method to be called from `main` without creating an object | `static` |
| Return type | Specifies the type of value the function returns | `int` |
| Function name | Identifies the function | `add` |
| Parameters | Variables that receive input | `int a, int b` |
| Function body | Contains the instructions to execute | `int sum = a + b;` |
| Return statement | Sends the result back to the caller | `return sum;` |

### General Syntax

```java
static returnType functionName(parameters) {
    // Process the input

    return value;
}
```

For example:

```java
static int multiply(int a, int b) {
    return a * b;
}
```

Here:
- `int` is the return type.
- `multiply` is the function name.
- `a` and `b` are parameters.
- `a * b` is the calculation.
- `return a * b;` sends the result back.

### What Happens When We Call a Function?

```java
int result = multiply(4, 6);
System.out.println(result);
```

The execution proceeds as follows:

1. `multiply(4, 6)` is called.
2. The parameter `a` receives `4`, and `b` receives `6`.
3. The function calculates `4 * 6`.
4. The function returns `24`.
5. The returned value is stored in `result`.
6. The program prints `24`.

The function call is replaced by its returned value in the expression.

For example:

```java
int result = multiply(4, 6) + 10;
```

This is equivalent to:

```java
int result = 24 + 10;
```

Therefore, `result` becomes `34`.

---

## 3. Return Types: `void` vs. Other Types

Functions generally fall into two categories based on whether they return a value.

### A. Functions That Return a Value

If a function calculates something that we need to use later, it should usually return that result.

Example:

```java
static int cube(int n) {
    return n * n * n;
}
```

We can store or use the returned value:

```java
int ans = cube(3);
System.out.println(ans); // 27
```

The return type must match the type of value being returned.

Examples:

```java
static int getAge() {
    return 18;
}

static double getPrice() {
    return 99.50;
}

static boolean isEven(int n) {
    return n % 2 == 0;
}

static char getGrade() {
    return 'A';
}
```

### B. Functions That Return Nothing: `void`

Sometimes, a function performs an action rather than calculating a value that needs to be returned.

For example:

```java
static void greet() {
    System.out.println("Hello!");
}
```

Calling it:

```java
greet();
```

Output:

```text
Hello!
```

Since the function only prints a message, it doesn't need to return a value.

Another example:

```java
static void printSum(int a, int b) {
    System.out.println(a + b);
}
```

Calling `printSum(3, 5)` prints `8`, but the function does not return `8` to the caller.

Compare:

```java
static int sum(int a, int b) {
    return a + b;
}
```

with:

```java
static void printSum(int a, int b) {
    System.out.println(a + b);
}
```

The first function **returns** a result; the second **prints** a result.

This distinction matters because printing a value and returning a value are not the same thing.

### Can a `void` Function Use `return`?

Yes! A `void` function can use a bare `return;` to exit early.

```java
static void printPositive(int n) {
    if (n <= 0) {
        return;
    }

    System.out.println(n);
}
```

If `n` is zero or negative, the function exits without printing anything.

However, you cannot return a value from a `void` function:

```java
static void example() {
    return 10; // Compilation error
}
```

Also, a non-`void` function must return a value of the correct type on every possible path through the function.

---

## 4. Function Rules You Should Know

### Rule 1: Match the Return Type

The declared return type must match the returned value.

```java
static int getNumber() {
    return 5; // Correct
}
```

```java
static int getNumber() {
    return 5.5; // Compilation error
}
```

The second function tries to return a `double` value from a function declared to return `int`.

### Rule 2: Match the Parameters

Parameters specify the input a function expects.

```java
static int add(int a, int b) {
    return a + b;
}
```

Valid calls:

```java
add(3, 5);
add(10, 20);
```

Invalid calls:

```java
add(3);       // Too few arguments
add(3, 5, 7); // Too many arguments
```

Passing an incompatible type can also cause a compilation error:

```java
add("hello", 5); // Compilation error
```

### Rule 3: A Non-`void` Function Must Return a Value

```java
static int doubleNumber(int n) {
    int ans = n * 2;
    return ans;
}
```

This is valid.

But:

```java
static int doubleNumber(int n) {
    int ans = n * 2;
}
```

This is invalid because the function may finish without returning an `int`.

### Rule 4: Understand Parameters and Arguments

These terms are related but different.

```java
static int square(int n) {
    return n * n;
}
```

Here, `n` is a **parameter**.

When we call:

```java
square(7);
```

The value `7` is an **argument**.

Parameters are the variables declared in the function definition; arguments are the values supplied when calling the function.

### Rule 5: Java Passes Arguments by Value

For primitive types such as `int`, the function receives a copy of the value.

```java
static void change(int x) {
    x = 100;
}

public static void main(String[] args) {
    int a = 5;
    change(a);
    System.out.println(a);
}
```

Output:

```text
5
```

Changing `x` inside the function does not change `a`. The function modified its local copy.

### Rule 6: Functions Must Be Defined Inside a Class

In Java, methods are declared inside a class, not directly inside another method.

A basic program looks like this:

```java
public class Main {

    static int square(int n) {
        return n * n;
    }

    public static void main(String[] args) {
        System.out.println(square(5));
    }
}
```

For competitive programming, helper functions are commonly declared as `static` methods inside `Main`, alongside `main`.

---

## 5. Predefined Functions

Java already provides many useful methods. These are often called predefined functions or library methods.

Instead of implementing everything from scratch, use the methods that already exist.

### Common Examples

| Method | Purpose | Example |
|---|---|---|
| `Math.max(a, b)` | Returns the larger value | `Math.max(4, 9)` gives `9` |
| `Math.min(a, b)` | Returns the smaller value | `Math.min(4, 9)` gives `4` |
| `Math.abs(x)` | Returns the absolute value | `Math.abs(-7)` gives `7` |
| `Math.sqrt(x)` | Calculates the square root | `Math.sqrt(25)` gives `5.0` |
| `Math.pow(a, b)` | Calculates \(a^b\) | `Math.pow(2, 3)` gives `8.0` |
| `Math.floor(x)` | Rounds down to an integer-valued `double` | `Math.floor(4.8)` gives `4.0` |
| `Math.ceil(x)` | Rounds up to an integer-valued `double` | `Math.ceil(4.2)` gives `5.0` |

Example:

```java
int a = 10;
int b = 20;

System.out.println(Math.max(a, b)); // 20
System.out.println(Math.min(a, b)); // 10
```

Notice that `Math.pow()` returns a `double`, even when the result looks like an integer.

```java
double ans = Math.pow(2, 3);
System.out.println(ans); // 8.0
```

Do not assume every predefined function returns an `int`.

---

## 6. Writing Functions for Common Problems

### A. Factorial of N

The factorial of a non-negative integer \(N\) is the product of all positive integers from `1` to `N`.

\[
N! = N \times (N-1) \times \cdots \times 2 \times 1
\]

Special case:

\[
0! = 1
\]

For example:

\[
5! = 5 \times 4 \times 3 \times 2 \times 1 = 120
\]

#### How to Approach It

We already know how to calculate factorials using loops. Now we can put that logic inside a function.

Ask yourself:

1. What input does the function need? `N`.
2. What should it return? The factorial, a number.
3. What return type should we use? `long` for a wider range than `int`.
4. What process do we need? Multiply all integers from `1` to `N`.

#### Implementation

```java
static long factorial(int n) {
    long ans = 1;

    for (int i = 1; i <= n; i++) {
        ans *= i;
    }

    return ans;
}
```

Using the function:

```java
System.out.println(factorial(5)); // 120
System.out.println(factorial(0)); // 1
System.out.println(factorial(3)); // 6
```

#### Dry Run: `factorial(4)`

| `i` | `ans` before multiplication | `ans` after multiplication |
|---:|---:|---:|
| 1 | 1 | 1 |
| 2 | 1 | 2 |
| 3 | 2 | 6 |
| 4 | 6 | 24 |

The function returns `24`.

**Important:** Factorials grow very quickly. Even `long` overflows for sufficiently large inputs; `20!` fits in a Java `long`, but `21!` does not. Always check the constraints of the problem.

---

### B. Calculating N Choose R: \(nCr\)

The number of ways to choose `r` objects from `n` objects, when order does not matter, is called a combination.

\[
{n \choose r} = \frac{n!}{r!(n-r)!}
\]

For example:

\[
{5 \choose 2} = \frac{5!}{2! \times 3!} = 10
\]

There are 10 ways to choose 2 objects from 5.

#### How to Approach It

We can reuse the factorial function we just wrote!

Instead of calculating factorial three times from scratch in separate pieces of code, call our helper function.

```java
static long factorial(int n) {
    long ans = 1;

    for (int i = 1; i <= n; i++) {
        ans *= i;
    }

    return ans;
}

static long nCr(int n, int r) {
    return factorial(n) / (factorial(r) * factorial(n - r));
}
```

Usage:

```java
System.out.println(nCr(5, 2)); // 10
System.out.println(nCr(6, 3)); // 20
System.out.println(nCr(4, 0)); // 1
```

#### Dry Run: `nCr(5, 2)`

The function evaluates:

- `factorial(5)` = `120`
- `factorial(2)` = `2`
- `factorial(5 - 2)` = `factorial(3)` = `6`

Therefore:

\[
{5 \choose 2} = \frac{120}{2 \times 6} = 10
\]

**Important constraints:**

- This formula assumes `0 <= r <= n`.
- The factorial implementation above can overflow for larger values of `n`.
- The intermediate product `factorial(r) * factorial(n-r)` can overflow even when the final answer fits in a `long`.
- For large constraints, use a more suitable combination algorithm rather than relying directly on factorials.

**Key takeaway:** Functions allow us to reuse smaller solutions to solve larger problems.

---

### C. Armstrong Number Using Functions

An Armstrong number is a non-negative integer that equals the sum of its digits, each raised to the power of the number of digits.

For example, `153` has three digits:

\[
1^3 + 5^3 + 3^3 = 1 + 125 + 27 = 153
\]

Therefore, `153` is an Armstrong number.

Similarly, `123` is not an Armstrong number because:

\[
1^3 + 2^3 + 3^3 = 36 \ne 123
\]

#### How to Approach It

Instead of putting everything into one large function, divide the task into smaller functions:

1. `countDigits(n)` counts the number of digits.
2. `isArmstrong(n)` checks whether the number satisfies the condition.

This makes each function responsible for one clear task.

#### Implementation

```java
static int countDigits(int n) {
    if (n == 0) {
        return 1;
    }

    int count = 0;

    while (n > 0) {
        count++;
        n /= 10;
    }

    return count;
}

static boolean isArmstrong(int n) {
    if (n < 0) {
        return false;
    }

    int digits = countDigits(n);
    int temp = n;
    long sum = 0;

    while (temp > 0) {
        int digit = temp % 10;
        sum += (long) Math.pow(digit, digits);
        temp /= 10;
    }

    return sum == n;
}
```

Usage:

```java
System.out.println(isArmstrong(153)); // true
System.out.println(isArmstrong(123)); // false
System.out.println(isArmstrong(0));   // true
```

#### Dry Run: `isArmstrong(153)`

The number has three digits, so `digits = 3`.

| Current number | Extracted digit | Digit cubed | Running sum |
|---:|---:|---:|---:|
| 153 | 3 | 27 | 27 |
| 15 | 5 | 125 | 152 |
| 1 | 1 | 1 | 153 |

At the end, `sum == n`, so the function returns `true`.

**Note:** `Math.pow()` returns a `double`. For larger inputs, floating-point precision can become a concern. For general-purpose implementations, integer exponentiation is preferable when exact integer arithmetic is required. Also, `long` can overflow for sufficiently large inputs.

---

### D. Floor and Ceil Functions

Java provides two predefined methods in the `Math` class:

- `Math.floor(x)` returns the greatest integer less than or equal to `x`.
- `Math.ceil(x)` returns the smallest integer greater than or equal to `x`.

The results are returned as `double` values.

#### Examples

| Input | `Math.floor(x)` | `Math.ceil(x)` |
|---:|---:|---:|
| `4.2` | `4.0` | `5.0` |
| `4.0` | `4.0` | `4.0` |
| `4.9` | `4.0` | `5.0` |
| `-4.2` | `-5.0` | `-4.0` |
| `-4.9` | `-5.0` | `-4.0` |

Notice that floor and ceil are not the same as simply removing the decimal part.

For example:

```java
System.out.println(Math.floor(-4.2)); // -5.0
System.out.println(Math.ceil(-4.2));  // -4.0
```

Floor moves toward negative infinity, while ceil moves toward positive infinity.

#### How to Use Them

```java
double x = 4.7;

double down = Math.floor(x);
double up = Math.ceil(x);

System.out.println(down); // 4.0
System.out.println(up);   // 5.0
```

If you need an integer result, you can cast the result:

```java
int down = (int) Math.floor(4.7); // 4
int up = (int) Math.ceil(4.2);    // 5
```

**Warning:** Casting a `double` to `int` truncates the fractional part toward zero. It does not perform floor or ceil automatically.

```java
System.out.println((int) -4.2);       // -4
System.out.println(Math.floor(-4.2));  // -5.0
```

### When Are Floor and Ceil Useful?

Suppose you need to divide `n` items into groups of size `k`.

The number of completely filled groups is:

\[
\left\lfloor \frac{n}{k} \right\rfloor
\]

The number of groups needed to accommodate all items, allowing the last group to be incomplete, is:

\[
\left\lceil \frac{n}{k} \right\rceil
\]

For non-negative integers and `k > 0`, integer arithmetic can calculate these directly:

```java
int fullGroups = n / k;
int groupsNeeded = (n + k - 1) / k;
```

For example, if `n = 10` and `k = 3`:

- Completely filled groups: `10 / 3 = 3`
- Groups needed: `(10 + 3 - 1) / 3 = 4`

This integer formula is often useful in competitive programming because it avoids floating-point arithmetic.

---

## 7. How to Approach Writing Functions

Whenever you solve a problem, ask yourself whether the logic should be placed in a separate function.

### Step 1: Identify the Task

Ask: What is this piece of code supposed to do?

Examples:
- Calculate a factorial.
- Check whether a number is prime.
- Count the digits of a number.
- Determine whether a number is an Armstrong number.

### Step 2: Decide the Inputs

What information does the function need?

For a factorial function, the only input is `n`.

```java
factorial(n);
```

For a function that checks whether a number is even:

```java
isEven(n);
```

### Step 3: Decide What It Should Return

Ask: Do I need the answer somewhere else in my program?

If yes, return it.

```java
static boolean isEven(int n) {
    return n % 2 == 0;
}
```

If the function only performs an action, such as printing a message, `void` may be appropriate.

```java
static void printMessage() {
    System.out.println("Hello!");
}
```

### Step 4: Write the Function Signature

A function signature consists of its name and parameter types. In a method declaration, you also specify a return type.

For example:

```java
static boolean isEven(int n)
```

This tells us that `isEven` receives an `int` and returns a `boolean`.

### Step 5: Implement the Logic

Use the concepts you already know: loops, conditionals, arithmetic, and so on.

```java
static boolean isEven(int n) {
    return n % 2 == 0;
}
```

### Step 6: Test It Independently

Try multiple cases:

```java
System.out.println(isEven(4));  // true
System.out.println(isEven(7));  // false
System.out.println(isEven(0));  // true
System.out.println(isEven(-2)); // true
```

Testing edge cases is important. Here, zero and negative numbers help verify that the function works beyond positive integers.

### Step 7: Reuse It

Once the function works, call it whenever needed instead of rewriting the same logic.

**A useful rule:** A function should ideally perform one clearly defined task. If a function is becoming too long or is responsible for several unrelated tasks, consider splitting it into smaller functions.

---

## 8. Common Mistakes

### A. Wrong Return Type

```java
static int getValue() {
    return "Hello";
}
```

This causes a compilation error because the function promises to return an `int`, but returns a `String`.

**Fix:** Either return an integer or change the return type to `String`.

### B. Missing Return Statement

```java
static int square(int n) {
    int ans = n * n;
}
```

This function may finish without returning an integer.

**Fix:**

```java
static int square(int n) {
    int ans = n * n;
    return ans;
}
```

### C. Returning from Only One Branch

Consider:

```java
static int absoluteValue(int n) {
    if (n >= 0) {
        return n;
    }
}
```

This is invalid because the function does not return a value when `n < 0`.

**Fix:**

```java
static int absoluteValue(int n) {
    if (n >= 0) {
        return n;
    } else {
        return -n;
    }
}
```

Alternatively, use:

```java
static int absoluteValue(int n) {
    if (n >= 0) {
        return n;
    }

    return -n;
}
```

### D. Accidentally Returning Inside a Loop

Consider:

```java
static int sumToN(int n) {
    int sum = 0;

    for (int i = 1; i <= n; i++) {
        sum += i;
        return sum;
    }

    return sum;
}
```

The `return sum;` inside the loop ends the entire function immediately. For `n = 5`, the function returns `1` because the loop stops after the first iteration.

**Fix:**

```java
static int sumToN(int n) {
    int sum = 0;

    for (int i = 1; i <= n; i++) {
        sum += i;
    }

    return sum;
}
```

The return statement belongs after the loop because we want the complete sum.

**Important:** Returning inside a loop is not always wrong. It is correct when you intentionally want to stop as soon as a condition is met, such as when searching for an element.

### E. Confusing `print` with `return`

```java
static int square(int n) {
    System.out.println(n * n);
}
```

Printing the result does not satisfy the requirement to return an `int`.

**Fix:**

```java
static int square(int n) {
    return n * n;
}
```

You can print the returned value when calling the function:

```java
System.out.println(square(5));
```

### F. Passing the Wrong Number of Arguments

```java
static int add(int a, int b) {
    return a + b;
}
```

This is invalid:

```java
add(5);
```

The function requires two arguments.

**Fix:** Supply both arguments:

```java
add(5, 10);
```

### G. Forgetting to Store or Use a Returned Value

```java
factorial(5);
```

This calculates the factorial, but the result is discarded.

If you need the result, write:

```java
long ans = factorial(5);
```

Or:

```java
System.out.println(factorial(5));
```

### H. Incorrect Function Calls

A function declared inside a class must be called in a way that is valid for its declaration.

For example, a `static` helper method can be called directly from `main`:

```java
static int square(int n) {
    return n * n;
}

public static void main(String[] args) {
    System.out.println(square(4));
}
```

If a method is not `static`, calling it directly from a static context such as `main` requires an object, unless the method is otherwise accessible through a valid reference.

### I. Incorrect Assumptions About `Math.pow()`

```java
int ans = Math.pow(2, 3);
```

This causes a compilation error because `Math.pow()` returns `double`, not `int`.

Use:

```java
double ans = Math.pow(2, 3);
```

If you know the result is within the `int` range and want an integer, you may cast it:

```java
int ans = (int) Math.pow(2, 3);
```

However, casting is not a general solution for floating-point precision problems.

---

## 9. Quick Revision

| Concept | Remember |
|---|---|
| Function | Reusable block of code for a specific task |
| Return type | Type of value the function returns |
| Parameters | Inputs declared in the function definition |
| Arguments | Values passed during a function call |
| `void` | Function does not return a value |
| `return value;` | Ends the function and sends back a value |
| `return;` | Exits a `void` function early |
| `Math.floor(x)` | Greatest integer less than or equal to `x`, returned as `double` |
| `Math.ceil(x)` | Smallest integer greater than or equal to `x`, returned as `double` |
| Reusability | Write logic once and call it whenever needed |

Before submitting a solution, check:

- Does the function have the correct return type?
- Does every possible path in a non-`void` function return a value?
- Are the correct arguments being passed?
- Is the `return` statement in the correct location?
- Am I returning the result or merely printing it?
- Have I tested edge cases?

---

## 10. Practice Questions

### Beginner

1. Write a function `isPositive(int n)` that returns `true` if `n` is positive and `false` otherwise.
2. Write a function `maxOfThree(int a, int b, int c)` that returns the largest of three integers.
3. Write a function `countDigits(int n)` that returns the number of digits in a non-negative integer. Treat `0` as having one digit.
4. Write a function `sumToN(int n)` that returns the sum of all integers from `1` to `n`.

### Intermediate

5. Write a function `factorial(int n)` that returns the factorial of `n`.
6. Write a function `nCr(int n, int r)` using a helper function for factorial.
7. Write a function `isPrime(int n)` that returns whether `n` is prime.
8. Write a function `isArmstrong(int n)` that checks whether a number is an Armstrong number.
9. Write a function that returns the floor and ceil of a given number, and explain why the return type matters.

### Debugging Challenge

10. Find and fix the errors in this function:

```java
static int sumToN(int n) {
    int sum = 0;

    for (int i = 1; i <= n; i++) {
        sum += i;
        return sum;
    }
}
```

11. Find and fix the error:

```java
static void square(int n) {
    return n * n;
}
```

12. Find and fix the error:

```java
static int getNumber(boolean positive) {
    if (positive) {
        return 1;
    }
}
```

For each question, first decide the inputs and return type, then implement the logic, and finally test several cases.

**Final takeaway:** Identify the task, choose the inputs, decide what should be returned, implement the logic, and test the function independently before using it in a larger solution.
