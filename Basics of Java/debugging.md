
# Debugging Basics

> **Debugging = finding and fixing problems in your code.**

When your code doesn't work, don't randomly change things. First figure out **what kind of error you have**, then narrow down where it is happening.

---

## 1. Compilation Errors

### Error Type
A **compilation error** occurs when Java cannot understand or compile your code. The program **does not run at all**.

### Common Examples

**Missing `;` or incorrect syntax:**
java
// Missing semicolon
int x = 10 

// Missing closing parenthesis
if (x > 5 { 
    System.out.println(x);
}


**Using an undeclared variable:**

```java
// Error: 'y' was never declared
System.out.println(y); 

```

**Incompatible types:**

```java
// Error: cannot assign String to int
int x = "hello"; 

```

### How to Find It

Read the compiler error message. Java will usually tell you:

* What went wrong
* Which line it thinks the problem is on
* What it expected instead

*Example:*

```text
error: ';' expected

```

> **Important:** The line reported by the compiler isn't always the true cause. Sometimes the actual mistake is on the line immediately before it.

### How to Fix It

1. Read the error message.
2. Go to the indicated line.
3. Check the syntax and variable types.
4. Check the lines immediately before it.
5. Fix the error and compile again.

*Tip: Fix errors one at a time — fixing one error can make several other error messages disappear.*

---

## 2. Lossy Conversion Errors

### Error Type

A lossy conversion occurs when you try to put a value into a type that cannot safely represent the original value.

*Example:*

```java
double x = 10.5;
int y = x; // Compilation Error

```

Java gives an error because converting `double` → `int` can lose decimal precision.

### How to Find It

Look for an error involving incompatible types or possible loss of precision:

```text
possible lossy conversion from double to int

```

Check the types on both sides of the assignment (`int y = x;`) and ask: *"Am I trying to put a larger/more precise type into a smaller/less precise type?"*

### How to Fix It

* **Option 1: Use the correct type** (If you need to keep the decimal):
```java
double y = x;

```


* **Option 2: Explicitly cast** (If you intentionally want to discard the decimal):
```java
double x = 10.5;
int y = (int) x; // y becomes 10
System.out.println(y); 

```



> **Warning:** Don't blindly add a cast just to suppress the error. Make sure you are intentionally okay with losing information.

---

## 3. Runtime Errors

### Error Type

A **runtime error** occurs while the program is running. The code successfully compiles, but an invalid operation triggers a crash during execution.

*Example:*

```java
int x = 10;
int y = 0;

System.out.println(x / y); // Causes ArithmeticException at runtime

```

### Common Examples

* Division by zero
* Accessing an invalid array index
* Dereferencing a `null` reference
* Invalid object type casting

### How to Find It

Read the error message or **stack trace**:

```text
Exception in thread "main" java.lang.ArithmeticException: / by zero
    at Main.main(Main.java:5)

```

The stack trace provides:

1. What type of exception occurred
2. The exact line number where it crashed

Instead of just asking *"What's wrong with this line?"*, ask: **"Why did `y` become 0 at this point?"** The root cause usually happens earlier in the execution flow.

### How to Fix It

1. Locate the line specified in the stack trace.
2. Inspect the values involved at runtime.
3. Trace backwards to find where those values were generated or modified incorrectly.
4. Add input validation or handle edge cases to prevent invalid states.

---

## 4. Logical Errors

### Error Type

A **logical error** occurs when your program runs successfully without crashing, but produces the **wrong output**.

*Example:*

```java
int a = 10;
int b = 20;

// Incorrect: outputs 20 because of operator precedence (b / 2 happens first)
int average = a + b / 2; 

// Correct: outputs 15
int average = (a + b) / 2; 

```

### How to Find It

Logical errors are usually the hardest to diagnose. Check for:

* Discrepancies between expected vs. actual output
* Incorrect logical operators (`&&` vs `||`) or loop bounds (`<` vs `<=`)
* Operator precedence issues
* Unhandled edge cases

**Use Small Test Cases:**
Instead of testing large inputs (e.g., $N = 100000$), test minimal inputs you can calculate by hand ($N = 1, 2, 5$). Manually trace variable states step-by-step.

### How to Fix It

1. Pinpoint where **Expected Value $\neq$ Actual Value**.
2. Trace execution backwards from that point to isolate where the state first diverged from your expectations.

---

## 5. Diagnostic Workflow

When your code doesn't work, follow this structured process:

```
Step 1: Does it compile?
├── NO  ─> Compilation Error
│          └─ Read compiler message ─> Fix syntax/type issue
└── YES ─> Continue to Step 2

Step 2: Does it run without crashing?
├── NO  ─> Runtime Error
│          └─ Read stack trace ─> Find crash line ─> Trace variable values backwards
└── YES ─> Continue to Step 3

Step 3: Is the output correct?
└── NO  ─> Logical Error
           └─ Run small test cases ─> Trace execution ─> Find where state deviates

```

---

## 6. Debugging Checklist

Ask these three questions in order:

1. **Does the code compile?**
* *If no:* Check syntax, missing semicolons, matching brackets, and variable declarations.


2. **Does the program run?**
* *If no:* Read the stack trace, identify the exception type, and check for null references or out-of-bounds access.


3. **Is the output correct?**
* *If no:* Test edge cases, trace logic with small inputs, and print intermediate variable states.



---

## Quick Revision Table

| Error Type | What Happens? | How to Find It |
| --- | --- | --- |
| **Compilation Error** | Code cannot compile or build. | Read compiler error message and check indicated line. |
| **Lossy Conversion** | Conversion between types risks data loss. | Check variable types on assignment statements. |
| **Runtime Error** | Program crashes during execution. | Read exception name and stack trace line number. |
| **Logical Error** | Program runs, but output is wrong. | Test small inputs and manually trace logic step-by-step. |

---

> **Rule of Thumb:** Don't guess—diagnose. Treat error messages as clues rather than obstacles.

```

```
