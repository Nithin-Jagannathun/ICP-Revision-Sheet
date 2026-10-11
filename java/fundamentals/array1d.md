# 1D Arrays in Java

## TL;DR

- An **array** stores multiple values of the same type under one variable name.
- Array indices start at `0`; the last valid index is `arr.length - 1`.
- Arrays have a fixed length after creation.
- Use `arr[i]` to access or update an element.
- Use ordinary `for` loops to traverse arrays by index.
- Common tasks include finding a sum, average, maximum, reversing an array, and checking for patterns.
- Always check your loop bounds to avoid `ArrayIndexOutOfBoundsException`.

---

## 1. Why Do We Need Arrays?

Suppose we want to store the marks of five students.

Without an array, we might write:

```java
int mark1 = 78;
int mark2 = 91;
int mark3 = 65;
int mark4 = 88;
int mark5 = 73;
```

This becomes difficult when there are 100, 1,000, or more students. It is also inconvenient to process each variable using a loop.

Instead, use an array:

```java
int[] marks = {78, 91, 65, 88, 73};
```

Now all five marks are stored under one variable, `marks`, and we can access each mark using an index.

```java
for (int i = 0; i < marks.length; i++) {
    System.out.println(marks[i]);
}
```

### Why Arrays Are Useful

- **Group related data:** store all marks, prices, scores, or measurements together.
- **Use loops:** process many values without writing the same code repeatedly.
- **Access by index:** retrieve or update an element directly.
- **Implement algorithms:** arrays are the foundation for sorting, searching, prefix sums, frequency counting, and many other techniques.

**Important:** An array stores elements of one declared type. An `int[]` stores integers, a `double[]` stores doubles, and a `char[]` stores characters.

---

## 2. Array Syntax

### A. Declaring an Array

```java
int[] arr;
```

This declares a variable that can refer to an integer array. It does not create the array yet.

### B. Creating an Array

```java
int[] arr = new int[5];
```

This creates an array of length `5`.

For primitive arrays, Java initializes each element to its default value. For an `int[]`, every element initially contains `0`.

```java
System.out.println(arr[0]); // 0
System.out.println(arr[4]); // 0
```

Other common defaults include `0.0` for `double`, `false` for `boolean`, and `null` for reference types such as `String`.

### C. Initializing with Values

```java
int[] arr = {10, 20, 30, 40};
```

Java creates an array with four elements.

You can also write:

```java
int[] arr = new int[]{10, 20, 30, 40};
```

### D. Updating an Element

```java
int[] arr = {10, 20, 30};

arr[1] = 99;

System.out.println(arr[1]); // 99
```

Array elements can be changed, unlike characters inside a `String`.

### E. Getting the Length

```java
int[] arr = {10, 20, 30};

System.out.println(arr.length); // 3
```

Notice that arrays use the field `arr.length`, without parentheses. Strings use the method `s.length()`.

---

## 3. How Arrays Work Behind the Scenes

An array is a fixed-length object whose elements are laid out in indexed order. For primitive arrays such as `int[]`, the values are stored in a contiguous sequence of element slots. This layout allows efficient direct access by index.

Imagine this array:

```java
int[] arr = {12, 25, 7, 40, 18};
```

Conceptually:

| Index | Value |
|---:|---:|
| `0` | `12` |
| `1` | `25` |
| `2` | `7` |
| `3` | `40` |
| `4` | `18` |

The index tells Java which element to access.

### Why Does Indexing Start at Zero?

The index is an offset from the beginning of the array:

- Index `0` means the first element.
- Index `1` means one element position after the first.
- Index `2` means two element positions after the first.

This makes direct indexing efficient. Accessing `arr[i]` takes **O(1)** time, meaning the time does not grow with the array length.

### Important Properties

- Array length is fixed after creation.
- Elements can be updated.
- Each element is accessed using an index.
- Valid indices are from `0` to `arr.length - 1`.
- Accessing an invalid index throws `ArrayIndexOutOfBoundsException`.

**Note:** For arrays of objects such as `String[]`, the array slots store references to objects. The objects themselves are not necessarily stored next to one another in memory.

---

## 4. Indexing: The Most Important Rule

For an array of length `n`:

- First index: `0`
- Last valid index: `n - 1`

For example:

```java
int[] arr = {5, 10, 15, 20};
```

- `arr[0]` is `5`.
- `arr[1]` is `10`.
- `arr[3]` is `20`.
- `arr[4]` is invalid.

### A Common Mistake

Incorrect:

```java
for (int i = 0; i <= arr.length; i++) {
    System.out.println(arr[i]);
}
```

When `i == arr.length`, the index is out of bounds.

Correct:

```java
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

### Dos and Don'ts of Indexing

**Do:**
- Use `i < arr.length` when traversing every element from left to right.
- Check that an index is valid before accessing an array when the index comes from input or calculations.
- Use `arr.length - 1` for the last element, provided the array is not empty.
- Test boundary cases such as arrays of length `1`.

**Don't:**
- Assume the last index equals the array length.
- Access `arr[0]` without checking whether the array is empty.
- Use a negative index.
- Change an index inside a loop without understanding how it affects the next iteration.
- Assume arrays grow automatically when you assign beyond their current length.

---

## 5. Taking Array Input

A common way to read an array using `Scanner` is:

```java
Scanner sc = new Scanner(System.in);

int n = sc.nextInt();
int[] arr = new int[n];

for (int i = 0; i < n; i++) {
    arr[i] = sc.nextInt();
}
```

Example input:

```text
5
10 20 30 40 50
```

After reading the input, `arr` contains:

```text
[10, 20, 30, 40, 50]
```

### What Is Happening?

1. Read `n`, the number of elements.
2. Create an array of length `n`.
3. Run a loop from `0` to `n - 1`.
4. Read one value into each position.

If `n` might be zero, an empty array can be created, but you must not access any element of it.

---

## 6. Iterating Through an Array

Iteration means visiting elements one by one.

### A. Print Every Element

```java
for (int i = 0; i < arr.length; i++) {
    System.out.print(arr[i] + " ");
}
System.out.println();
```

We use the index `i` to access `arr[i]`.

### B. Update Every Element

```java
for (int i = 0; i < arr.length; i++) {
    arr[i] *= 2;
}
```

Every element is multiplied by two.

For example, `[1, 2, 3]` becomes `[2, 4, 6]`.

### C. Iterate Backwards

```java
for (int i = arr.length - 1; i >= 0; i--) {
    System.out.print(arr[i] + " ");
}
System.out.println();
```

This prints the array from the last element to the first.

### D. Find the Sum

```java
int sum = 0;

for (int i = 0; i < arr.length; i++) {
    sum += arr[i];
}

System.out.println(sum);
```

Initialize `sum` to zero before adding the elements.

### E. Find the Average

```java
int sum = 0;

for (int i = 0; i < arr.length; i++) {
    sum += arr[i];
}

double average = (double) sum / arr.length;
System.out.println(average);
```

The cast `(double)` is important. Without it, dividing two integers performs integer division.

For example, `5 / 2` is `2`, but `5.0 / 2` is `2.5`.

Only calculate the average after ensuring the array is not empty.

---

## 7. Common Array Patterns

### A. Finding the Maximum Element

```java
int max = arr[0];

for (int i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
        max = arr[i];
    }
}

System.out.println(max);
```

**Why initialize `max` to `arr[0]`?**

The maximum must be an element of the array. Starting at zero would fail if every element were negative.

This implementation assumes the array is non-empty.

### B. Finding the Minimum Element

```java
int min = arr[0];

for (int i = 1; i < arr.length; i++) {
    if (arr[i] < min) {
        min = arr[i];
    }
}

System.out.println(min);
```

The same reasoning applies: initialize from an actual element.

### C. Counting Elements That Satisfy a Condition

Suppose we want to count even elements.

```java
int count = 0;

for (int i = 0; i < arr.length; i++) {
    if (arr[i] % 2 == 0) {
        count++;
    }
}

System.out.println(count);
```

This generalizes to counting positive numbers, negative numbers, elements above a threshold, and many other conditions.

### D. Finding an Element

Suppose we want to know whether `target` appears in the array.

```java
int target = 10;
boolean found = false;

for (int i = 0; i < arr.length; i++) {
    if (arr[i] == target) {
        found = true;
        break;
    }
}

System.out.println(found);
```

The `break` exits the loop once the target is found. If you need the index, store `i` instead of just setting a boolean.

### E. Checking Whether an Array Is a Palindrome

An array is a palindrome if it reads the same forwards and backwards.

For example, `[1, 2, 3, 2, 1]` is a palindrome, but `[1, 2, 3]` is not.

```java
boolean palindrome = true;

for (int i = 0; i < arr.length / 2; i++) {
    if (arr[i] != arr[arr.length - 1 - i]) {
        palindrome = false;
        break;
    }
}

System.out.println(palindrome);
```

We only need to compare the first half with the corresponding elements in the second half.

For index `i`, its matching index from the end is:

`arr.length - 1 - i`

If any pair differs, the array is not a palindrome.

### F. Reversing an Array In Place

Reversing in place means changing the original array without creating another array.

```java
int left = 0;
int right = arr.length - 1;

while (left < right) {
    int temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;

    left++;
    right--;
}
```

We swap the first and last elements, then move inward.

Example:

```text
Before: [1, 2, 3, 4, 5]
After:  [5, 4, 3, 2, 1]
```

This uses **O(1) extra space** because only one temporary variable is needed.

### G. Finding the Sum of All Elements

For `[2, 4, 6, 8]`:

| Index | Element | Sum so far |
|---:|---:|---:|
| 0 | 2 | 2 |
| 1 | 4 | 6 |
| 2 | 6 | 12 |
| 3 | 8 | 20 |

The key pattern is to maintain a running total:

```java
sum += arr[i];
```

### H. Finding the Maximum Frequency

A simple approach for a small array is to count how many times each element occurs by checking it against every other element. This takes O(n²) time.

```java
int maxFreq = 0;

for (int i = 0; i < arr.length; i++) {
    int freq = 0;

    for (int j = 0; j < arr.length; j++) {
        if (arr[j] == arr[i]) {
            freq++;
        }
    }

    maxFreq = Math.max(maxFreq, freq);
}

System.out.println(maxFreq);
```

This is a useful first example of nested loops. For larger arrays or more complex frequency questions, a frequency array or a `HashMap` may be more efficient.

---

## 8. Useful Array Utilities

Java provides the `Arrays` class in `java.util`.

Add this import:

```java
import java.util.Arrays;
```

### A. Printing an Array

```java
System.out.println(Arrays.toString(arr));
```

This prints the contents in a readable form, such as `[1, 2, 3]`.

Printing `arr` directly usually prints a reference-style representation, not the elements.

### B. Sorting an Array

```java
Arrays.sort(arr);
```

This sorts the array in ascending order.

**Important:** Sorting changes the array's order. If the original order matters, make a copy before sorting.

### C. Filling an Array

```java
Arrays.fill(arr, 0);
```

This sets every element to zero.

### D. Copying an Array

```java
int[] copy = Arrays.copyOf(arr, arr.length);
```

This creates a separate array containing the same element values. Updating an element in `copy` does not update the corresponding element in `arr`.

---

## 9. Common Mistakes

### A. Going Out of Bounds

Incorrect:

```java
for (int i = 0; i <= arr.length; i++) {
    System.out.println(arr[i]);
}
```

Correct:

```java
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

### B. Accessing an Empty Array

```java
int[] arr = new int[0];
// System.out.println(arr[0]); // Error
```

An empty array has no valid indices. Check its length before accessing an element.

### C. Incorrect Maximum Initialization

Incorrect:

```java
int max = 0;
```

This fails when every array element is negative.

Correct for a non-empty array:

```java
int max = arr[0];
```

### D. Forgetting Integer Division

Incorrect when a fractional average is needed:

```java
double avg = sum / arr.length;
```

If both operands are integers, division happens before assignment to `double`.

Correct:

```java
double avg = (double) sum / arr.length;
```

Also, check that `arr.length > 0`.

### E. Updating the Wrong Index

```java
for (int i = 0; i < arr.length; i++) {
    arr[i + 1] = arr[i];
}
```

When `i` reaches the final index, `i + 1` is out of bounds. Even before then, the assignment overwrites values that may still be needed.

Think carefully about whether an algorithm should move left to right or right to left.

### F. Confusing Array Length with Last Index

For an array of length `n`, the last index is `n - 1`, not `n`.

- Length: `arr.length`
- Last valid index: `arr.length - 1`

### G. Accidentally Changing the Original Array

`Arrays.sort(arr)` changes `arr` itself. If you need the original order later, make a copy first.

### H. Forgetting That Arrays Have Fixed Length

You cannot increase an array's length after creating it. If you need a dynamically growing collection, consider `ArrayList` once you have learned collections.

### I. Integer Overflow in the Sum

If an array contains large integers, the sum may exceed the range of `int`.

```java
long sum = 0;

for (int i = 0; i < arr.length; i++) {
    sum += arr[i];
}
```

Use `long` when the constraints require it. Choose data types based on the maximum possible result.

---

## 10. Quick Revision

| Task | Pattern |
|---|---|
| Create an array | `int[] arr = new int[n];` |
| Get length | `arr.length` |
| Access element | `arr[i]` |
| Update element | `arr[i] = value;` |
| Traverse forward | `for (int i = 0; i < arr.length; i++)` |
| Traverse backward | Start at `arr.length - 1`, decrease to `0` |
| Sum | `sum += arr[i]` |
| Average | `(double) sum / arr.length` |
| Maximum | Initialize with `arr[0]`, then compare |
| Count matching elements | Use a counter and condition |
| Check palindrome | Compare `arr[i]` with `arr[n - 1 - i]` |
| Reverse in place | Swap left and right elements, moving inward |
| Print array | `Arrays.toString(arr)` |
| Sort array | `Arrays.sort(arr)` |

---

## 11. Practice Questions

### Beginner

1. Read `n` integers into an array and print them.
2. Find the sum and average of all array elements.
3. Find the maximum and minimum elements.
4. Count the number of even and odd elements.
5. Count how many elements are greater than a given value `k`.
6. Print the array in reverse order without modifying it.

### Intermediate

7. Reverse an array in place.
8. Check whether an array is a palindrome.
9. Find the second-largest distinct element.
10. Count how many pairs of elements have a sum equal to `k`.
11. Find the element that appears an odd number of times, assuming exactly one such element exists and all others appear an even number of times.
12. Check whether an array is sorted in non-decreasing order.
13. Find the frequency of a given element.

### Challenge

14. Move all zeros to the end while maintaining the relative order of non-zero elements.
15. Remove duplicates from a sorted array.
16. Find the maximum sum of a contiguous subarray.
17. Rotate an array to the right by `k` positions.
18. Find a pair of elements with the smallest absolute difference.

For every problem:

- Identify the valid index range.
- Decide whether you need one loop or nested loops.
- Consider empty arrays and arrays of length `1` when allowed.
- Test cases with all negative values, repeated values, and zeros.
- Check whether the task requires modifying the original array or only printing a result.

**Final takeaway:** Arrays let you store and process many related values efficiently. Master indexing, ordinary loops, running totals, comparisons, and two-pointer techniques; these form the foundation for more advanced array algorithms.
