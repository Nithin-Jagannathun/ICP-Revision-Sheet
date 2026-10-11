# Pattern Printing in Java

## TL;DR

Pattern printing is about deciding **what to print at each row and column**. Most patterns can be built with nested loops:

- The **outer loop** usually controls the rows.
- The **inner loop(s)** control what gets printed on each row.
- Use spaces deliberately when a pattern needs alignment.
- Before coding, write down how the number of stars, spaces, or numbers changes from row to row.

Pattern printing is an extension of loops: the main skill is translating a visual pattern into loop bounds.

---

## 1. The Basic Idea

Suppose we want to print:

```text
*
**
***
****
```

There are four rows. Row 1 has one star, row 2 has two, and so on.

```java
for (int row = 1; row <= 4; row++) {
    for (int col = 1; col <= row; col++) {
        System.out.print("*");
    }
    System.out.println();
}
```

- `row` tells us which line we are printing.
- `col` counts how many stars to print on that line.
- `System.out.println()` moves to the next line after a row is complete.

**Important:** `print()` stays on the same line. `println()` moves to the next line.

---

## 2. Three Basic Patterns

### A. Staircase

Output for `n = 5`:

```text
*
**
***
****
*****
```

The number of stars equals the row number.

```java
int n = 5;

for (int row = 1; row <= n; row++) {
    for (int col = 1; col <= row; col++) {
        System.out.print("*");
    }
    System.out.println();
}
```

**Loop rule:** On row `row`, print `row` stars.

### B. Reverse Staircase

Output for `n = 5`:

```text
*****
****
***
**
*
```

The number of stars decreases as the row number increases.

```java
int n = 5;

for (int row = 1; row <= n; row++) {
    for (int col = row; col <= n; col++) {
        System.out.print("*");
    }
    System.out.println();
}
```

The inner loop runs from `row` to `n`, so it prints `n - row + 1` stars.

An equivalent version uses a decreasing count:

```java
for (int row = n; row >= 1; row--) {
    for (int col = 1; col <= row; col++) {
        System.out.print("*");
    }
    System.out.println();
}
```

**Key idea:** A reversed pattern often comes from reversing the loop direction or changing the loop's starting and ending values.

### C. Right-Aligned Triangle of Stars

Output for `n = 5`:

```text
    *
   **
  ***
 ****
*****
```

This is a right-aligned triangle. Each row contains leading spaces followed by stars.

```java
int n = 5;

for (int row = 1; row <= n; row++) {
    for (int space = 1; space <= n - row; space++) {
        System.out.print(" ");
    }

    for (int star = 1; star <= row; star++) {
        System.out.print("*");
    }

    System.out.println();
}
```

For each row:

- Spaces: `n - row`
- Stars: `row`

The spaces are printed **before** the stars. Changing their order changes the pattern.

---

## 3. How to Approach an Unfamiliar Pattern

Don't start by writing nested loops immediately. First, turn the picture into rules.

### Step 1: Write Down the Output Carefully

Number the rows and inspect a few columns. Ask:

- How many rows are there?
- What changes from one row to the next?
- Which parts stay the same?
- Are there spaces before, between, or after the symbols?

### Step 2: Make a Row-by-Row Table

For the right-aligned triangle with `n = 5`:

| Row | Leading spaces | Stars |
|---:|---:|---:|
| 1 | 4 | 1 |
| 2 | 3 | 2 |
| 3 | 2 | 3 |
| 4 | 1 | 4 |
| 5 | 0 | 5 |

The pattern becomes much easier once you find the rule:

- Leading spaces = `n - row`
- Stars = `row`

### Step 3: Split Each Row into Smaller Parts

A row might consist of:

1. Leading spaces
2. A block of stars
3. Another block of spaces
4. A block of numbers

Give each part its own loop when that makes the logic clearer. You don't need to force the whole row into one complicated loop.

### Step 4: Work Out Loop Bounds

For every loop, answer these questions:

- Where does the counter start?
- When does it stop?
- Is the endpoint inclusive (`<=`) or exclusive (`<`)?
- How many times should it run?

For example, if `row = 2` and `n = 5`, a loop from `col = row` through `col <= n` runs four times: `2, 3, 4, 5`.

### Step 5: Build and Test One Row First

Trace the first row, a middle row, and the last row. These often reveal off-by-one errors before you test the entire pattern.

---

## 4. Example Run: An Arrowhead Pattern

Let's print this pattern for `n = 5`:

```text
    *
   **
  ***
 ****
*********
 ****
  ***
   **
    *
```

The pattern has `2 * n - 1` rows.

Notice the structure:

- The upper half has `n - 1` rows. Each row has fewer leading spaces and more stars.
- The middle row has `2 * n - 1` stars.
- The lower half mirrors the upper half.

We can split it into three parts.

```java
int n = 5;

// Upper half
for (int row = 1; row < n; row++) {
    for (int space = 1; space <= n - row; space++) {
        System.out.print(" ");
    }

    for (int star = 1; star <= row; star++) {
        System.out.print("*");
    }

    System.out.println();
}

// Middle row
for (int star = 1; star <= 2 * n - 1; star++) {
    System.out.print("*");
}
System.out.println();

// Lower half
for (int row = n - 1; row >= 1; row--) {
    for (int space = 1; space <= n - row; space++) {
        System.out.print(" ");
    }

    for (int star = 1; star <= row; star++) {
        System.out.print("*");
    }

    System.out.println();
}
```

### Trace a Few Rows

For `n = 5`:

| Part | `row` | Spaces | Stars |
|---|---:|---:|---:|
| Upper | 1 | 4 | 1 |
| Upper | 2 | 3 | 2 |
| Upper | 3 | 2 | 3 |
| Upper | 4 | 1 | 4 |
| Middle | — | 0 | 9 |
| Lower | 4 | 1 | 4 |
| Lower | 3 | 2 | 3 |
| Lower | 2 | 3 | 2 |
| Lower | 1 | 4 | 1 |

**Why stop the upper half at `row < n`?** The middle row is printed separately. Using `row <= n` would add an extra row before the middle.

**Why start the lower half at `n - 1`?** The middle row has already been printed, so we must not print it twice.

The general lesson: when a pattern has symmetry, print one half, handle the middle if needed, and then print the reversed half.

---

## 5. Example Run: Pyramid of Numbers

For `n = 5`, print:

```text
    1
   121
  12321
 1234321
123454321
```

Each row has two parts:

1. Increasing numbers from `1` to `row`
2. Decreasing numbers from `row - 1` to `1`

Leading spaces align the pyramid.

```java
int n = 5;

for (int row = 1; row <= n; row++) {
    // Leading spaces
    for (int space = 1; space <= n - row; space++) {
        System.out.print(" ");
    }

    // Increasing: 1, 2, ..., row
    for (int num = 1; num <= row; num++) {
        System.out.print(num);
    }

    // Decreasing: row - 1, ..., 1
    for (int num = row - 1; num >= 1; num--) {
        System.out.print(num);
    }

    System.out.println();
}
```

### Trace Row 4

For `row = 4` and `n = 5`:

- Spaces: `5 - 4 = 1`
- Increasing part: `1234`
- Decreasing part: `321`
- Combined row: ` 1234321`

**Why does the decreasing loop start at `row - 1`?** The number `row` was already printed by the increasing loop. Starting at `row` would print it twice, producing `12344321` for row 4.

This is a common pattern-printing technique: split a row into independent pieces, and make sure the pieces don't overlap.

---

## 6. Common Debugging Tips

### A. Straggling Spaces

If the output looks misaligned, check:

- Are spaces printed before or after the symbols?
- Is the number of spaces correct for the first and last rows?
- Are you printing trailing spaces that aren't needed?

Trailing spaces are not always visible in a terminal, so compare the output row by row. In online judges, exact output formatting can matter.

### B. Off-by-One Errors

A loop using `<=` runs one more time than the corresponding loop using `<`, when the other bounds are unchanged.

For example:

```java
for (int col = 1; col <= row; col++)
```

prints `row` symbols, while:

```java
for (int col = 1; col < row; col++)
```

prints `row - 1` symbols.

When the pattern has a wrong number of symbols, check the start and end values first.

### C. Incorrect Row Count

If a pattern is supposed to have `2 * n - 1` rows, check whether the middle row is being counted twice or omitted.

### D. Reversed Patterns That Aren't Quite Reversed

Write the row counts in order. For example:

```text
1, 2, 3, 4, 5
```

Reversed, this should be:

```text
5, 4, 3, 2, 1
```

If you get `5, 4, 3, 2`, the final row is missing. If you get `5, 4, 3, 2, 1, 0`, the loop runs one time too many.

### E. Accidentally Printing on the Same Line

Make sure `System.out.println()` appears **after the inner loops**, not inside them. Otherwise, each symbol may appear on a separate line.

### F. Reusing a Counter Incorrectly

Use distinct names such as `row`, `space`, `star`, and `num` for nested loops. This makes the code easier to trace and reduces accidental changes to the wrong counter.

### G. Debug with a Small Input

Start with `n = 3` or `n = 4`. Smaller outputs are easier to inspect manually. Once the pattern is correct, test `n = 1` as well if that input is allowed.

---

## 7. Quick Revision

- **Outer loop:** usually controls rows.
- **Inner loop:** controls symbols within a row.
- **Staircase:** stars increase with the row number.
- **Reverse staircase:** stars decrease with the row number.
- **Right-aligned triangle:** print `n - row` spaces, then `row` stars.
- **Symmetric pattern:** separate the upper half, middle row, and lower half.
- **Number pyramid:** split each row into increasing and decreasing sequences.
- **Debugging:** check loop bounds, spaces, row count, and where `println()` appears.

A reliable rule: **observe → split into parts → derive counts → write loops → trace small cases → test edge cases.**

---

## 8. Practice

Try these without looking at the earlier examples. For each one, write down the number of spaces and symbols on each row before coding.

### Beginner

1. Print a staircase of `n` rows using `#` instead of `*`.
2. Print a reverse staircase of `n` rows.
3. Print a right-aligned triangle of `n` rows.

### Intermediate

4. Print this pattern for `n = 4`:

   ```text
   1
   22
   333
   4444
   ```

5. Print this pattern for `n = 4`:

   ```text
   1
   12
   123
   1234
   ```

6. Print a centered pyramid of stars for `n = 4`:

   ```text
      *
     ***
    *****
   *******
   ```

### Challenge

7. Print the pyramid of numbers from Section 5 for a user-provided `n`.
8. Print the arrowhead pattern from Section 4 for a user-provided `n`.
9. Print a hollow square of size `n`, where only the border contains stars.

**For each problem:** test `n = 1`, a small value such as `n = 3`, and the largest reasonable input. Check both the shape and the exact number of rows.
