# 2D Arrays in Java

## TL;DR

- A **2D array** is an array of arrays. It stores data arranged in rows and columns.
- Access an element with `arr[row][col]`.
- The number of rows is `arr.length`.
- The number of columns in row `r` is `arr[r].length`.
- Use nested loops: the outer loop usually controls rows, and the inner loop usually controls columns.
- A 2D array can be passed to a function and returned from a function.
- A transpose swaps rows and columns. For a rectangular matrix, the transposed matrix has `columns` rows and `rows` columns.

---

## 1. What Is a 2D Array?

A 1D array stores values in a sequence:

```java
int[] arr = {10, 20, 30, 40};
```

A 2D array lets us arrange values in rows and columns, like a table or spreadsheet.

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

It looks like this:

| | Column 0 | Column 1 | Column 2 |
|---|---:|---:|---:|
| Row 0 | 1 | 2 | 3 |
| Row 1 | 4 | 5 | 6 |
| Row 2 | 7 | 8 | 9 |

For example:

- `matrix[0][0]` is `1`.
- `matrix[1][2]` is `6`.
- `matrix[2][1]` is `8`.

### Intuition: An Array of Arrays

In Java, a 2D array is really an **array whose elements are references to other arrays**.

You can think of it as:

- `matrix[0]` refers to the first row.
- `matrix[1]` refers to the second row.
- `matrix[2]` refers to the third row.

Each row is itself a 1D array.

This is why we write `matrix[row][col]`: first select the row, then select an element inside that row.

**Important:** Java supports *jagged arrays*, where different rows can have different lengths. A rectangular matrix is a common special case, not a requirement of the language.

---

## 2. Declaring and Creating a 2D Array

### A. Create a Matrix with a Fixed Size

```java
int rows = 3;
int cols = 4;

int[][] matrix = new int[rows][cols];
```

This creates three rows, each containing four integers. Every element is initially `0`.

### B. Initialize with Values

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};
```

This matrix has two rows and three columns.

### C. Access and Update Elements

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};

System.out.println(matrix[0][1]); // 2

matrix[0][1] = 99;
System.out.println(matrix[0][1]); // 99
```

Remember that both indices start at `0`.

### D. Getting Height and Width

For a matrix:

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};
```

- Number of rows (height): `matrix.length`, which is `2`.
- Number of columns in row `r`: `matrix[r].length`, which is `3` for both rows here.

```java
int rows = matrix.length;
int cols = matrix[0].length;
```

This last line assumes the matrix has at least one row. For a possibly empty matrix, check `matrix.length` first.

**Do not confuse these:**

- `matrix.length` gives the number of rows.
- `matrix[r].length` gives the length of row `r`.
- `matrix[0].length` gives the first row's length, if a first row exists.

For a jagged array, rows can have different lengths, so there may not be one universal column count.

---

## 3. Taking Input for a 2D Array

Suppose the input gives the number of rows and columns, followed by all the matrix elements.

```java
Scanner sc = new Scanner(System.in);

int rows = sc.nextInt();
int cols = sc.nextInt();

int[][] matrix = new int[rows][cols];

for (int r = 0; r < rows; r++) {
    for (int c = 0; c < cols; c++) {
        matrix[r][c] = sc.nextInt();
    }
}
```

Example input:

```text
2 3
1 2 3
4 5 6
```

The matrix becomes:

```text
1 2 3
4 5 6
```

The outer loop chooses the row. The inner loop fills every column of that row before moving to the next row.

---

## 4. Iterating Through a 2D Array

Most 2D array problems use nested loops.

### A. Print Row by Row (Top to Bottom)

```java
for (int r = 0; r < matrix.length; r++) {
    for (int c = 0; c < matrix[r].length; c++) {
        System.out.print(matrix[r][c] + " ");
    }
    System.out.println();
}
```

The outer loop moves from the first row to the last. The inner loop prints each element from left to right.

For the matrix:

```text
1 2 3
4 5 6
7 8 9
```

The output is:

```text
1 2 3
4 5 6
7 8 9
```

### B. Print Column by Column (Left to Right)

To visit every element in the first column, then every element in the second column, swap the roles of the loops:

```java
for (int c = 0; c < matrix[0].length; c++) {
    for (int r = 0; r < matrix.length; r++) {
        System.out.print(matrix[r][c] + " ");
    }
    System.out.println();
}
```

For the same matrix, this prints:

```text
1 4 7
2 5 8
3 6 9
```

This code assumes a non-empty rectangular matrix. For jagged arrays, you must handle each row's length carefully.

### Row-Wise vs. Column-Wise

| Traversal | Outer loop | Inner loop |
|---|---|---|
| Row-wise | Rows | Columns |
| Column-wise | Columns | Rows |

**Key idea:** The outer loop decides what you finish before moving on. If the outer loop is `r`, you complete each row before moving to the next row. If the outer loop is `c`, you complete each column before moving to the next column.

---

## 5. Thinking in 2D: How to Dry Run a Matrix Problem

A 1D array has one index, `arr[i]`. A 2D array has two: `matrix[r][c]`.

When solving a matrix problem, always ask:

1. What does the row index represent?
2. What does the column index represent?
3. Which index should change first?
4. What are the valid ranges of both indices?
5. Am I processing rows, columns, diagonals, or neighbours?

### Example: Trace a Row-Wise Traversal

Matrix:

```text
1 2 3
4 5 6
```

Code:

```java
for (int r = 0; r < matrix.length; r++) {
    for (int c = 0; c < matrix[r].length; c++) {
        System.out.print(matrix[r][c] + " ");
    }
}
```

Trace:

| `r` | `c` | Accessed element |
|---:|---:|---:|
| 0 | 0 | `matrix[0][0] = 1` |
| 0 | 1 | `matrix[0][1] = 2` |
| 0 | 2 | `matrix[0][2] = 3` |
| 1 | 0 | `matrix[1][0] = 4` |
| 1 | 1 | `matrix[1][1] = 5` |
| 1 | 2 | `matrix[1][2] = 6` |

Notice that `c` resets to `0` each time `r` increases.

### A Useful Mental Model

Treat each `matrix[r][c]` as a cell:

- `r` tells you which horizontal row you are in.
- `c` tells you which position within that row you are in.

Write down a small matrix and manually trace the first few iterations whenever the loop order feels confusing.

---

## 6. Common Matrix Operations

### A. Sum of All Elements

```java
int sum = 0;

for (int r = 0; r < matrix.length; r++) {
    for (int c = 0; c < matrix[r].length; c++) {
        sum += matrix[r][c];
    }
}

System.out.println(sum);
```

Each cell is added exactly once.

### B. Sum of Every Row

```java
for (int r = 0; r < matrix.length; r++) {
    int sum = 0;

    for (int c = 0; c < matrix[r].length; c++) {
        sum += matrix[r][c];
    }

    System.out.println("Row " + r + ": " + sum);
}
```

Notice that `sum` is reset to `0` at the start of each row. If it were declared outside the outer loop, the result would keep accumulating across rows.

### C. Sum of Every Column

```java
if (matrix.length > 0) {
    for (int c = 0; c < matrix[0].length; c++) {
        int sum = 0;

        for (int r = 0; r < matrix.length; r++) {
            sum += matrix[r][c];
        }

        System.out.println("Column " + c + ": " + sum);
    }
}
```

The outer loop chooses a column, and the inner loop visits every row in that column. This version assumes a rectangular matrix.

### D. Find the Maximum Element

```java
int max = matrix[0][0];

for (int r = 0; r < matrix.length; r++) {
    for (int c = 0; c < matrix[r].length; c++) {
        if (matrix[r][c] > max) {
            max = matrix[r][c];
        }
    }
}

System.out.println(max);
```

This assumes the matrix has at least one row and that the first row has at least one element.

### E. Print the Main and Anti-Diagonals

For a square matrix:

```text
1 2 3
4 5 6
7 8 9
```

The **main diagonal** contains:

```text
1 5 9
```

Its elements have matching row and column indices: `matrix[i][i]`.

The **anti-diagonal** contains:

```text
3 5 7
```

For an `n x n` matrix, its elements are `matrix[i][n - 1 - i]`.

```java
int n = matrix.length;

// Main diagonal
for (int i = 0; i < n; i++) {
    System.out.print(matrix[i][i] + " ");
}
System.out.println();

// Anti-diagonal
for (int i = 0; i < n; i++) {
    System.out.print(matrix[i][n - 1 - i] + " ");
}
System.out.println();
```

This assumes a non-empty square matrix. In an odd-sized square matrix, the two diagonals share the center element.

---

## 7. Transpose of a Matrix

The transpose of a matrix swaps its rows and columns.

For example, the original matrix is:

```text
1 2 3
4 5 6
```

Its transpose is:

```text
1 4
2 5
3 6
```

The element at position `(r, c)` moves to position `(c, r)`.

`transpose[c][r] = matrix[r][c]`

### A. Transpose Using a New Matrix

For a matrix with `rows` rows and `cols` columns, its transpose has `cols` rows and `rows` columns.

```java
int rows = matrix.length;
int cols = matrix[0].length;

int[][] transpose = new int[cols][rows];

for (int r = 0; r < rows; r++) {
    for (int c = 0; c < cols; c++) {
        transpose[c][r] = matrix[r][c];
    }
}
```

**Why create an array of size `[cols][rows]`?** The original has `rows` rows and `cols` columns. After swapping the dimensions, the transpose must have `cols` rows and `rows` columns.

### B. Transpose a Square Matrix In Place

For a square matrix, we can transpose without creating another matrix by swapping elements across the main diagonal.

```java
int n = matrix.length;

for (int r = 0; r < n; r++) {
    for (int c = r + 1; c < n; c++) {
        int temp = matrix[r][c];
        matrix[r][c] = matrix[c][r];
        matrix[c][r] = temp;
    }
}
```

Why does the inner loop start at `c = r + 1`?

- Elements on the main diagonal do not need to move.
- Each pair above and below the diagonal should be swapped only once.
- If we swapped every pair twice, we would undo our own changes.

This version assumes a square matrix.

---

## 8. Functions That Accept and Return Arrays

Arrays are objects in Java. When an array is passed to a method, the method receives a copy of the reference to the same array. That means the method can modify the array's elements.

### A. Passing an Array to a Function

```java
static void doubleElements(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        arr[i] *= 2;
    }
}
```

Calling it:

```java
int[] values = {1, 2, 3};

doubleElements(values);

System.out.println(Arrays.toString(values)); // [2, 4, 6]
```

The original array changes because both the caller and the function refer to the same array object.

### B. Returning an Array from a Function

A method can return an array just like it can return an `int` or a `String`.

```java
static int[] createArray() {
    int[] arr = {10, 20, 30};
    return arr;
}
```

Usage:

```java
int[] values = createArray();

System.out.println(Arrays.toString(values)); // [10, 20, 30]
```

The returned reference lets the caller access the array.

### C. Returning a New Array Instead of Modifying the Original

```java
static int[] doubledCopy(int[] arr) {
    int[] result = new int[arr.length];

    for (int i = 0; i < arr.length; i++) {
        result[i] = arr[i] * 2;
    }

    return result;
}
```

Usage:

```java
int[] original = {1, 2, 3};
int[] doubled = doubledCopy(original);

System.out.println(Arrays.toString(original)); // [1, 2, 3]
System.out.println(Arrays.toString(doubled));  // [2, 4, 6]
```

The original remains unchanged because the function creates a separate array.

### D. Important Reference-Type Concept

```java
int[] a = {1, 2, 3};
int[] b = a;

b[0] = 99;

System.out.println(a[0]); // 99
```

`a` and `b` refer to the same array. Assigning `b = a` does not create a copy of the array.

If you need an independent copy:

```java
int[] b = Arrays.copyOf(a, a.length);
```

Java passes the reference **by value**. The function receives a copy of the reference, not a separate copy of the array. Therefore, changing an element affects the shared array, but assigning the parameter to a different array does not change the caller's variable.

---

## 9. Common Mistakes

### A. Mixing Up Rows and Columns

For `matrix[r][c]`:

- The first index selects the row.
- The second index selects the column.

### B. Using the Wrong Loop Bound

For row-wise traversal, use:

```java
for (int r = 0; r < matrix.length; r++) {
    for (int c = 0; c < matrix[r].length; c++) {
        // Process matrix[r][c]
    }
}
```

Do not use `r <= matrix.length` or `c <= matrix[r].length`.

### C. Confusing Height and Width

- Height / number of rows: `matrix.length`
- Width of row `r`: `matrix[r].length`

For a rectangular, non-empty matrix, `matrix[0].length` gives the number of columns.

### D. Assuming the Matrix Is Non-Empty

This can fail if there are no rows:

```java
int cols = matrix[0].length;
```

Check `matrix.length > 0` before accessing the first row. Also check row lengths when working with potentially jagged arrays.

### E. Resetting a Sum at the Wrong Time

For row sums, initialize `sum = 0` inside the outer loop. Otherwise, the sum from earlier rows carries over.

### F. Transposing into the Wrong Dimensions

For an original matrix of size `rows x cols`, create a transpose of size `cols x rows`, not `rows x cols`, unless the matrix is square.

### G. Transposing a Square Matrix Incorrectly

When transposing in place, swap only one side of the main diagonal with the other. Swapping both directions will undo the transpose.

### H. Accidentally Sharing an Array

`int[] b = a;` does not copy the array. Use `Arrays.copyOf()` or create a new array and copy the elements when you need independent data.

---

## 10. Quick Revision

| Task | Key idea |
|---|---|
| Create a matrix | `int[][] matrix = new int[rows][cols];` |
| Access an element | `matrix[r][c]` |
| Number of rows | `matrix.length` |
| Number of columns in row `r` | `matrix[r].length` |
| Row-wise traversal | Outer loop rows, inner loop columns |
| Column-wise traversal | Outer loop columns, inner loop rows |
| Sum all elements | Add every `matrix[r][c]` |
| Row sum | Reset sum for each row |
| Main diagonal | `matrix[i][i]` in a square matrix |
| Anti-diagonal | `matrix[i][n - 1 - i]` in a square matrix |
| Transpose | `transpose[c][r] = matrix[r][c]` |
| Pass an array to a method | The method receives a copy of the reference |
| Return an array | Use a return type such as `int[]` |
| Copy an array | `Arrays.copyOf(arr, arr.length)` |

---

## 11. Practice Questions

### Beginner

1. Read a matrix and print it row by row.
2. Print a matrix column by column.
3. Find the sum of all elements.
4. Find the sum of each row.
5. Find the sum of each column.
6. Find the maximum element in the matrix.
7. Print the main diagonal and anti-diagonal of a square matrix.

### Intermediate

8. Find the transpose of a rectangular matrix using a new array.
9. Transpose a square matrix in place.
10. Check whether a square matrix is symmetric, meaning `matrix[r][c] == matrix[c][r]` for all valid indices.
11. Count the number of even and odd elements in a matrix.
12. Find the row with the largest sum.
13. Write a function that takes an `int[]` and returns a new array containing the elements in reverse order.
14. Write a function that takes a matrix and returns a new matrix containing twice every element.

### Challenge

15. Find the sum of the main diagonal and anti-diagonal of a square matrix without counting the center twice.
16. Rotate a square matrix by 90 degrees.
17. Search for a value in a matrix that is sorted row-wise and column-wise.
18. Write a function that returns a new matrix containing the element-wise sum of two matrices of the same dimensions.

For each problem:

- Identify the row and column indices.
- Write down the valid bounds for both loops.
- Trace the first few iterations on a small matrix.
- Check whether the matrix is square or rectangular.
- Decide whether the original matrix should be modified or a new matrix should be returned.
- Test edge cases such as one row, one column, and a single-element matrix when allowed.

**Final takeaway:** A 2D array is an array of row arrays. Once you understand `matrix[r][c]`, nested loops, dimensions, and reference behaviour, most beginner matrix problems become a matter of choosing the correct traversal and index relationships.
