# If-Else Statements

> **If-else is the bread and butter of programming logic.**

Almost every program needs to make decisions:

- Is this number positive or negative?
- Did the student pass?
- Is this number divisible by 3?
- Which of these two numbers is larger?
- Does this person get a discount?

**If-else statements allow your program to make these decisions.**

---

# 1. Comparisons

Before understanding `if-else`, you need to understand **comparisons**.

A comparison asks a question whose answer is either:

```text
true
```

or

```text
false
```

For example:

```java
5 > 3
```

is `true`, while:

```java
5 < 3
```

is `false`.

These expressions produce a `boolean` value.

---

## Comparison Operators

| Operator | Meaning | Example |
|---|---|---|
| `==` | Equal to | `x == 5` |
| `!=` | Not equal to | `x != 5` |
| `>` | Greater than | `x > 5` |
| `<` | Less than | `x < 5` |
| `>=` | Greater than or equal to | `x >= 5` |
| `<=` | Less than or equal to | `x <= 5` |

For example:

```java
int x = 10;

x == 10    // true
x != 10    // false
x > 5      // true
x < 5      // false
x >= 10     // true
x <= 10     // true
```

---

## ⚠️ `=` vs `==`

This is one of the most common beginner mistakes.

```java
x = 5;
```

means:

> **Assign 5 to `x`.**

Whereas:

```java
x == 5
```

means:

> **Check whether `x` is equal to 5.**

Remember:

```text
=   → assignment
==  → comparison
```

---

# 2. The Basic `if` Statement

An `if` statement executes some code **only if a condition is true**.

```java
if (condition) {
    // code to execute
}
```

Example:

```java
int x = 10;

if (x > 5) {
    System.out.println("x is greater than 5");
}
```

Since:

```text
x > 5
10 > 5
true
```

the code inside the `if` executes.

---

# 3. `if-else`

Often, we want to do one thing if a condition is true and something else if it is false.

```java
if (condition) {
    // condition is true
} else {
    // condition is false
}
```

Example:

```java
int x = 10;

if (x > 5) {
    System.out.println("Greater");
} else {
    System.out.println("Not greater");
}
```

Since `x > 5` is true, the output is:

```text
Greater
```

---

# 4. `else if`

Sometimes there are more than two possibilities.

For example, suppose we want to classify a number:

```text
Positive
Negative
Zero
```

We can use:

```java
if (x > 0) {
    System.out.println("Positive");
} else if (x < 0) {
    System.out.println("Negative");
} else {
    System.out.println("Zero");
}
```

The general structure is:

```java
if (condition1) {
    // ...
} else if (condition2) {
    // ...
} else if (condition3) {
    // ...
} else {
    // ...
}
```

---

# 5. How `if-else` Actually Executes

This is **very important**.

In an `if - else if - else` chain, Java checks conditions **from top to bottom**.

As soon as it finds a condition that is `true`, it executes that block and **skips the rest of the chain**.

For example:

```java
int x = 10;

if (x > 0) {
    System.out.println("Positive");
} else if (x > 5) {
    System.out.println("Greater than 5");
} else {
    System.out.println("Something else");
}
```

Java checks:

```text
x > 0
10 > 0
true
```

So it executes:

```text
Positive
```

and **does not check**:

```text
x > 5
```

even though that condition is also true.

---

## Why Order Matters

Consider:

```java
if (x > 0) {
    System.out.println("Positive");
} else if (x > 100) {
    System.out.println("Greater than 100");
}
```

The second condition is effectively useless.

Why?

Every number greater than `100` is already greater than `0`.

So whenever:

```text
x > 100
```

is true, this was already true:

```text
x > 0
```

and the first condition would have executed.

Therefore:

> **In an if-else chain, earlier conditions have priority over later conditions.**

---

# 6. Nested `if`

An `if` statement can exist inside another `if`.

```java
if (condition1) {

    if (condition2) {
        // ...
    }

}
```

Example:

```java
int age = 20;
boolean hasID = true;

if (age >= 18) {
    if (hasID) {
        System.out.println("Entry allowed");
    }
}
```

Nested `if`s are useful when one decision only matters after another decision has been made.

However, **don't nest conditions unnecessarily**. Often, multiple conditions can be combined using logical operators.

---

# 7. Logical Operators

Logical operators allow us to combine multiple conditions.

## AND — `&&`

```text
condition1 && condition2
```

is true **only when both conditions are true**.

Example:

```java
int x = 10;

if (x > 5 && x < 20) {
    System.out.println("x is between 5 and 20");
}
```

Think:

> **AND = both must be true.**

| A | B | `A && B` |
|---|---|---|
| false | false | false |
| false | true | false |
| true | false | false |
| true | true | true |

---

## OR — `||`

```text
condition1 || condition2
```

is true when **at least one** condition is true.

Example:

```java
if (x == 0 || x == 1) {
    System.out.println("x is 0 or 1");
}
```

Think:

> **OR = at least one must be true.**

| A | B | `A || B` |
|---|---|---|
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | true |

---

## NOT — `!`

`!` reverses a boolean value.

```java
!true   // false
!false  // true
```

Example:

```java
boolean raining = false;

if (!raining) {
    System.out.println("Go outside!");
}
```

Think:

> **NOT = flip the answer.**

---

# 8. Combining Comparisons

Logical operators become especially useful when combined with comparisons.

For example:

```java
int x = 15;

if (x >= 10 && x <= 20) {
    System.out.println("x is in the range [10, 20]");
}
```

This checks:

```text
x >= 10
AND
x <= 20
```

Both must be true.

---

# 9. Short-Circuit Evaluation

Java evaluates logical expressions from **left to right**.

With `&&`:

```java
A && B
```

if `A` is already false, Java **doesn't need to check `B`**, because the entire expression must be false.

Similarly, with `||`:

```java
A || B
```

if `A` is already true, Java doesn't need to check `B`, because the entire expression must be true.

This is called **short-circuit evaluation**.

Example:

```java
if (x != 0 && 10 / x > 2) {
    ...
}
```

If `x == 0`, the first condition is false, so Java doesn't evaluate:

```java
10 / x
```

This prevents division by zero.

---

# 10. Writing Conditions Clearly

A condition should communicate **exactly what you want to check**.

For example, instead of:

```java
if (x >= 5) {
    ...
}
```

when you actually mean:

```text
5 <= x <= 10
```

write:

```java
if (x >= 5 && x <= 10) {
    ...
}
```

Remember that Java does **not** support mathematical chained comparisons like:

```java
5 <= x <= 10   // ❌ Wrong
```

Use:

```java
5 <= x && x <= 10   // ✅ Correct
```

---

# 11. Writing Clean `if-else` Conditions

Good conditional logic isn't just about getting the right answer. **The order and structure of your conditions matter.**

## Put More Specific Conditions First

Suppose we want to classify a score:

```text
90+  → Excellent
75+  → Good
50+  → Pass
<50  → Fail
```

A clean implementation is:

```java
if (score >= 90) {
    System.out.println("Excellent");
} else if (score >= 75) {
    System.out.println("Good");
} else if (score >= 50) {
    System.out.println("Pass");
} else {
    System.out.println("Fail");
}
```

Notice the order:

```text
Most specific / restrictive
        ↓
    score >= 90
        ↓
    score >= 75
        ↓
    score >= 50
        ↓
Most general
        ↓
       else
```

Why does this work?

If:

```text
score = 95
```

then:

```text
score >= 90 → true
```

so the chain stops immediately.

If:

```text
score = 80
```

then:

```text
score >= 90 → false
score >= 75 → true
```

so we get `"Good"`.

---

## Put General Conditions at the Bottom

Consider:

```java
if (score >= 50) {
    System.out.println("Pass");
} else if (score >= 90) {
    System.out.println("Excellent");
}
```

This is wrong.

Any score greater than or equal to `90` is also greater than or equal to `50`.

Therefore, the first condition catches everything that the second condition could have caught.

The correct order is:

```java
if (score >= 90) {
    System.out.println("Excellent");
} else if (score >= 50) {
    System.out.println("Pass");
}
```

> **Rule of thumb:** In an `if-else` chain, put the **more specific conditions first** and the **more general conditions later**.

---

# 12. Fuse Conditions When Possible

Sometimes you may write:

```java
if (x > 0) {
    if (x < 100) {
        System.out.println("Valid");
    }
}
```

This can be simplified to:

```java
if (x > 0 && x < 100) {
    System.out.println("Valid");
}
```

The second version is:

- Shorter
- Easier to read
- Easier to modify
- Less deeply nested

Another example:

```java
if (x == 1) {
    ...
} else if (x == 2) {
    ...
} else if (x == 3) {
    ...
}
```

If the same action is required for all three cases:

```java
if (x == 1 || x == 2 || x == 3) {
    ...
}
```

> **If multiple conditions lead to the same action, consider combining them.**

---

# 13. Avoid Unnecessary Conditions

Don't write:

```java
if (x > 0) {
    System.out.println("Positive");
} else if (x <= 0) {
    System.out.println("Not positive");
}
```

The second condition doesn't need to be checked.

Use:

```java
if (x > 0) {
    System.out.println("Positive");
} else {
    System.out.println("Not positive");
}
```

The `else` automatically represents:

```text
NOT (x > 0)
```

---

# 14. `if-else` vs Multiple `if`s

These are **not the same**.

### Multiple `if`s

```java
if (x > 0) {
    System.out.println("Positive");
}

if (x > 5) {
    System.out.println("Greater than 5");
}
```

Both conditions are checked.

For:

```text
x = 10
```

both blocks execute.

Output:

```text
Positive
Greater than 5
```

---

### `if-else if`

```java
if (x > 0) {
    System.out.println("Positive");
} else if (x > 5) {
    System.out.println("Greater than 5");
}
```

Only the **first true condition** executes.

For:

```text
x = 10
```

the output is:

```text
Positive
```

The second condition isn't checked.

### Remember

```text
Multiple ifs
→ Multiple conditions can execute

if → else if → else
→ At most ONE block executes
```

This distinction is extremely important.

---

# Quick Revision

## Comparison Operators

```text
==   Equal to
!=   Not equal to
>    Greater than
<    Less than
>=   Greater than or equal to
<=   Less than or equal to
```

## Logical Operators

```text
&&   AND → both must be true
||   OR  → at least one must be true
!    NOT → flips true/false
```

## Basic Structure

```java
if (condition) {
    // ...
} else if (condition) {
    // ...
} else {
    // ...
}
```

## Execution

```text
Check conditions from top → bottom

First TRUE condition
        ↓
Execute its block
        ↓
Skip the rest of the chain
```

## Multiple `if`s vs `else if`

```text
if
if
if
→ multiple blocks can execute

if
else if
else
→ at most one block executes
```

## Clean Conditions

```text
More specific
      ↓
More general
      ↓
     else
```

And:

```text
Multiple nested conditions
        ↓
Try combining with && / ||
        ↓
Cleaner code
```

### Most important things to remember

> **1. `=` assigns, `==` compares.**

> **2. Conditions evaluate to `true` or `false`.**

> **3. In an `if-else` chain, only the first true condition executes.**

> **4. Put specific conditions before general conditions.**

> **5. If multiple conditions lead to the same action, consider fusing them with `&&` or `||`.**
