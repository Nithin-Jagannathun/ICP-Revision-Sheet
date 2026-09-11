# Loops

> **Loops are used whenever we need to perform an action repeatedly or process a sequence of values.**

Suppose you want to:

- Print all numbers from `1` to `100`
- Check every number from `1` to `N`
- Print all even numbers
- Add up all numbers in a range
- Check whether a number is prime
- Find the GCD of two numbers

Writing the same code hundreds of times would obviously be impractical.

**Loops let us write the action once and repeat it automatically.**

---

# 1. The Basic Idea

A loop generally consists of:

1. A **loop variable** — keeps track of where we currently are.
2. A **condition** — determines whether we should continue.
3. An **update** — changes the loop variable so that we eventually stop.
4. The **loop body** — the code that gets repeated.

For example:

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

Here:

```text
i = loop variable
i <= 5 = condition
i++ = update
System.out.println(i) = loop body
```

The loop produces:

```text
1
2
3
4
5
```

---

# 2. `for` Loops

The basic structure of a `for` loop is:

```java
for (initialization; condition; update) {
    // code to repeat
}
```

For example:

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

The execution can be thought of as:

```text
Initialize i
     ↓
Check condition
     ↓
  true?
  ↙   ↘
yes    no → stop
 ↓
Run loop body
 ↓
Update i
 ↓
Go back to condition
```

---

# 3. Loop Variables

The **loop variable** tells us which iteration we are currently on.

For example:

```java
for (int i = 1; i <= 10; i++) {
    System.out.println(i);
}
```

`i` takes the values:

```text
1 → 2 → 3 → 4 → ... → 10
```

The loop variable is extremely useful because we can use it inside the loop.

For example:

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i * i);
}
```

Output:

```text
1
4
9
16
25
```

Here, `i` represents the number whose square we want to calculate.

> **Think of the loop variable as your position in the sequence you're processing.**

---

# 4. The Most Common Loop Pattern: `1` to `N`

One of the most important patterns to memorize:

```java
for (int i = 1; i <= N; i++) {
    // use i
}
```

This visits:

```text
1, 2, 3, ..., N
```

For example:

```java
int N = 10;

for (int i = 1; i <= N; i++) {
    System.out.println(i);
}
```

---

# 5. Iterating from `0` to `N - 1`

Another extremely common pattern:

```java
for (int i = 0; i < N; i++) {
    // use i
}
```

This visits:

```text
0, 1, 2, ..., N - 1
```

This is especially important when working with arrays.

For an array of size `N`:

```java
for (int i = 0; i < N; i++) {
    System.out.println(A[i]);
}
```

The valid indices are:

```text
0 → N - 1
```

---

# 6. Iterating from `L` to `R`

To iterate through an inclusive range:

```java
for (int i = L; i <= R; i++) {
    // use i
}
```

For example:

```java
int L = 5;
int R = 10;

for (int i = L; i <= R; i++) {
    System.out.println(i);
}
```

Output:

```text
5
6
7
8
9
10
```

> **Remember:** `i <= R` includes `R`.

If you write:

```java
i < R
```

then `R` is excluded.

---

# 7. Only Even Numbers

There are several ways to iterate through even numbers.

### Method 1: Check using `%`

```java
for (int i = 1; i <= N; i++) {
    if (i % 2 == 0) {
        System.out.println(i);
    }
}
```

Here:

```text
i % 2 == 0
```

means that `i` is divisible by `2`.

---

### Method 2: Step by `2`

A cleaner approach is:

```java
for (int i = 2; i <= N; i += 2) {
    System.out.println(i);
}
```

This directly visits:

```text
2 → 4 → 6 → 8 → ...
```

If you already know the values you want to visit, **it is usually better to step directly through them rather than checking every number.**

---

# 8. Only Odd Numbers

Similarly:

```java
for (int i = 1; i <= N; i += 2) {
    System.out.println(i);
}
```

This visits:

```text
1 → 3 → 5 → 7 → ...
```

Alternatively:

```java
for (int i = 1; i <= N; i++) {
    if (i % 2 != 0) {
        System.out.println(i);
    }
}
```

Again, stepping by `2` is generally cleaner when you only need odd numbers.

---

# 9. `if-else` Inside a Loop

Loops and `if-else` are often used together.

The loop handles **repetition**, while `if-else` handles **decisions**.

For example, to print whether each number from `1` to `10` is even or odd:

```java
for (int i = 1; i <= 10; i++) {

    if (i % 2 == 0) {
        System.out.println(i + " is even");
    } else {
        System.out.println(i + " is odd");
    }

}
```

Output:

```text
1 is odd
2 is even
3 is odd
4 is even
...
10 is even
```

Think:

```text
Loop
 ↓
Process each value
 ↓
if-else decides what to do with that value
```

This combination is **extremely common in programming problems**.

---

# 10. Finding the GCD

Loops are useful for repeatedly checking possible answers.

One simple way to find the GCD of two numbers is to check every possible divisor.

For example:

```java
int a = 24;
int b = 36;

int gcd = 1;

for (int i = 1; i <= Math.min(a, b); i++) {

    if (a % i == 0 && b % i == 0) {
        gcd = i;
    }

}

System.out.println(gcd);
```

Output:

```text
12
```

Why does this work?

A number `i` is a common divisor if:

```text
a % i == 0
AND
b % i == 0
```

As we iterate from small to large values, every new common divisor replaces the previous answer.

Therefore, the last common divisor we find is the GCD.

### Complexity

We check up to:

```text
min(a, b)
```

values.

So the complexity is:

```text
O(min(a, b))
```

> There are much faster ways to calculate GCD, such as the Euclidean algorithm. The important point here is understanding how a loop can systematically check a range of possibilities.

---

# 11. Checking if a Number is Prime

A prime number has exactly two positive divisors:

```text
1 and itself
```

To check whether `N` is prime, we can try dividing it by every number from `2` to `N - 1`.

```java
boolean prime = true;

for (int i = 2; i < N; i++) {

    if (N % i == 0) {
        prime = false;
    }

}

if (prime) {
    System.out.println("Prime");
} else {
    System.out.println("Not Prime");
}
```

For example, if:

```text
N = 7
```

we check:

```text
7 % 2
7 % 3
7 % 4
7 % 5
7 % 6
```

None are `0`, so `7` is prime.

If:

```text
N = 12
```

we find:

```text
12 % 2 == 0
```

so `12` is not prime.

---

## A Better Version

We don't actually need to check all the way up to `N - 1`.

If `N` has a divisor greater than `sqrt(N)`, it must have a corresponding divisor smaller than `sqrt(N)`.

Therefore, we only need to check:

```java
boolean prime = true;

for (int i = 2; i * i <= N; i++) {

    if (N % i == 0) {
        prime = false;
        break;
    }

}

if (prime) {
    System.out.println("Prime");
} else {
    System.out.println("Not Prime");
}
```

This reduces the complexity from:

```text
O(N)
```

to:

```text
O(sqrt(N))
```

The `break` is also useful here because once we find a divisor, **we already know the answer** and don't need to continue checking.

> **General lesson:** If you already know the answer, don't keep doing unnecessary work.

---

# 12. Loop Termination

Every loop needs to eventually **terminate**.

Consider:

```java
for (int i = 1; i <= 10; i++) {
    System.out.println(i);
}
```

The loop terminates because:

```text
i starts at 1
↓
i increases every iteration
↓
eventually i = 11
↓
i <= 10 becomes false
↓
loop stops
```

When writing a loop, always ask:

> **What causes my loop condition to eventually become false?**

---

# 13. Infinite Loops

An **infinite loop** is a loop that never terminates.

For example:

```java
int i = 1;

while (i <= 10) {
    System.out.println(i);
}
```

This never ends.

Why?

Because `i` is never changed.

It stays:

```text
i = 1
```

forever.

Therefore:

```text
i <= 10
```

always remains true.

---

## Another Common Mistake

```java
for (int i = 1; i <= 10; i--) {
    System.out.println(i);
}
```

Here:

```text
i = 1
↓
i--
↓
0
↓
-1
↓
-2
↓
...
```

`i` is moving **away from** the termination condition.

The condition:

```text
i <= 10
```

will therefore always remain true.

This produces an infinite loop.

The correct version is:

```java
for (int i = 1; i <= 10; i++) {
    System.out.println(i);
}
```

---

# 14. How to Avoid Infinite Loops

Before running a loop, check three things:

### 1. Where does the loop variable start?

```java
int i = 1;
```

### 2. What condition keeps the loop running?

```java
i <= N
```

### 3. How does the variable change?

```java
i++
```

Then ask:

> **Does the update move the variable towards making the condition false?**

For example:

```java
for (int i = 1; i <= N; i++)
```

```text
Start:    i = 1
Condition: i <= N
Update:   i++
Direction: i increases
End:      i > N
```

This terminates.

---

# 15. The `while` Loop

A `while` loop is useful when we want to **keep repeating something while a condition is true**.

The basic structure is:

```java
while (condition) {
    // code to repeat
}
```

For example:

```java
int i = 1;

while (i <= 5) {
    System.out.println(i);
    i++;
}
```

Output:

```text
1
2
3
4
5
```

The important difference is that the initialization and update are written separately:

```java
int i = 1;       // initialization

while (i <= 5) { // condition
    System.out.println(i);

    i++;         // update
}
```

---

# 16. `for` vs `while`

Both loops can perform the same tasks.

For example:

### `for`

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

### `while`

```java
int i = 1;

while (i <= 5) {
    System.out.println(i);
    i++;
}
```

Both produce:

```text
1
2
3
4
5
```

A useful rule of thumb:

### Use `for` when

You have a clear iteration pattern:

```text
Start → End → Step
```

For example:

```java
for (int i = 1; i <= N; i++)
```

### Use `while` when

The number of iterations isn't necessarily known beforehand, and you mainly care about a condition.

For example:

```java
while (x > 0) {
    ...
}
```

> The distinction isn't absolute — either loop can often be used. Choose the one that makes the logic clearer.

---

# 17. Common Loop Patterns

These are worth memorizing.

### `1` to `N`

```java
for (int i = 1; i <= N; i++) {
    ...
}
```

### `0` to `N - 1`

```java
for (int i = 0; i < N; i++) {
    ...
}
```

### `L` to `R`

```java
for (int i = L; i <= R; i++) {
    ...
}
```

### Even numbers

```java
for (int i = 2; i <= N; i += 2) {
    ...
}
```

### Odd numbers

```java
for (int i = 1; i <= N; i += 2) {
    ...
}
```

### Countdown

```java
for (int i = N; i >= 1; i--) {
    ...
}
```

### While a condition is true

```java
while (condition) {
    ...
}
```

---

# Quick Revision

## Why do we need loops?

> To perform an action repeatedly or process a sequence of values.

## A loop generally has

```text
Initialization
      ↓
Condition
      ↓
Loop body
      ↓
Update
      ↓
Repeat
```

## Common patterns

```java
// 1 → N
for (int i = 1; i <= N; i++)

// 0 → N-1
for (int i = 0; i < N; i++)

// L → R
for (int i = L; i <= R; i++)

// Even
for (int i = 2; i <= N; i += 2)

// Odd
for (int i = 1; i <= N; i += 2)

// Countdown
for (int i = N; i >= 1; i--)
```

## `while`

```java
int i = 1;

while (condition) {
    // code

    i++; // update
}
```

## Avoiding infinite loops

Always know:

```text
Where does my variable start?
        ↓
What keeps the loop running?
        ↓
How does the variable change?
        ↓
Does it eventually make the condition false?
```

> **The most important habit:** Whenever you write a loop, be able to explain **why it stops**.
