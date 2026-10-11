# Characters and Strings in Java

## TL;DR

- A `char` stores one UTF-16 code unit, written with single quotes: `'A'`.
- A `String` stores a sequence of characters, written with double quotes: `"Hello"`.
- String indices start at `0`; the last valid index is `s.length() - 1`.
- Use `s.length()` for length and `s.charAt(i)` to access a character.
- Use `.equals()` to compare string contents, not `==`.
- Use `Character.isDigit()`, `Character.isLetter()`, and related methods to classify characters.
- Strings are immutable: methods such as `toUpperCase()` return a new string.

---

## 1. Characters and ASCII

A Java `char` stores a single UTF-16 code unit.

```java
char letter = 'A';
char digit = '7';
char symbol = '#';
```

Use single quotes for `char` and double quotes for `String`.

### Common ASCII Values

| Character | ASCII code |
|---|---:|
| `'0'` | 48 |
| `'9'` | 57 |
| `'A'` | 65 |
| `'Z'` | 90 |
| `'a'` | 97 |
| `'z'` | 122 |
| `' '` | 32 |

For English letters and digits, codes are consecutive. Lowercase English letters have codes 32 greater than uppercase letters. Note that Java supports Unicode; not every `char` value is an ASCII character.

```java
char ch = 'A';
int code = ch;

System.out.println(code); // 65
System.out.println((int) 'a'); // 97
```

### Character Arithmetic

```java
char ch = 'A';

System.out.println((char) (ch + 1)); // B
System.out.println((char) (ch + 2)); // C
```

Convert an English digit character to its numeric value by subtracting `'0'`:

```java
char ch = '7';

System.out.println((int) ch); // 55: character code
System.out.println(ch - '0'); // 7: numeric digit
```

Only use `ch - '0'` after confirming that `ch` is between `'0'` and `'9'`.

---

## 2. Type Casting and Conversions

### A. `char` to `int`

```java
char ch = 'B';
int code = ch;

System.out.println(code); // 66
```

### B. `int` to `char`

```java
int code = 67;
char ch = (char) code;

System.out.println(ch); // C
```

### C. String to Integer

```java
String s = "123";
int n = Integer.parseInt(s);

System.out.println(n + 1); // 124
```

If `s` is not a valid integer representation, `Integer.parseInt(s)` throws a `NumberFormatException`.

### D. Integer to String

```java
int n = 123;
String s = String.valueOf(n);

System.out.println(s); // "123"
```

Remember that `"12" + "3"` produces `"123"`, while `12 + 3` produces `15`.

---

## 3. Introduction to Strings

A `String` is a sequence of characters.

```java
String name = "Alice";
String message = "Hello, world!";
String empty = "";
```

### A. `length()`

```java
String s = "Hello";

System.out.println(s.length()); // 5
System.out.println("".length()); // 0
```

For strings, `length()` is a method, so parentheses are required.

### B. `charAt(index)`

```java
String s = "Hello";

System.out.println(s.charAt(0)); // H
System.out.println(s.charAt(1)); // e
System.out.println(s.charAt(4)); // o
```

For a string of length `n`, valid indices are `0` through `n - 1`. An invalid index causes a `StringIndexOutOfBoundsException`.

### C. Traversing a String

```java
String s = "Hello";

for (int i = 0; i < s.length(); i++) {
    System.out.println(s.charAt(i));
}
```

Use `i < s.length()`, not `i <= s.length()`, because the last valid index is `s.length() - 1`.

### D. Traversing Backwards

```java
String s = "Hello";

for (int i = s.length() - 1; i >= 0; i--) {
    System.out.print(s.charAt(i));
}
```

Output:

```text
olleH
```

This is a common starting point for reversing a string or checking whether a string is a palindrome.

---

## 4. Useful String Methods

Assume `String s = "Hello World";`.

| Method | Purpose |
|---|---|
| `s.length()` | Length of the string |
| `s.charAt(i)` | Character at index `i` |
| `s.substring(a, b)` | Characters from index `a` through `b - 1` |
| `s.contains(t)` | Checks whether `t` occurs in `s` |
| `s.indexOf(t)` | First index of `t`, or `-1` if absent |
| `s.equals(t)` | Checks exact string contents |
| `s.equalsIgnoreCase(t)` | Checks equality ignoring case |
| `s.compareTo(t)` | Lexicographic comparison |
| `s.toUpperCase()` | Returns an uppercase version |
| `s.toLowerCase()` | Returns a lowercase version |
| `s.trim()` | Removes certain leading and trailing characters |
| `s.replace(a, b)` | Replaces characters or sequences |

### A. `substring()`

```java
String s = "Computer";

System.out.println(s.substring(0, 4)); // Comp
System.out.println(s.substring(3)); // puter
```

`substring(start, end)` includes `start` but excludes `end`.

### B. `contains()`

```java
String s = "Hello World";

System.out.println(s.contains("World")); // true
System.out.println(s.contains("world")); // false
```

`contains()` is case-sensitive.

### C. `indexOf()`

```java
String s = "banana";

System.out.println(s.indexOf('a')); // 1
System.out.println(s.indexOf("na")); // 2
System.out.println(s.indexOf('z')); // -1
```

It returns the index of the first occurrence, or `-1` if the character or substring is not found.

### D. `equals()`

```java
System.out.println("Hello".equals("Hello")); // true
System.out.println("Hello".equals("hello")); // false
```

String equality is case-sensitive.

### E. `equalsIgnoreCase()`

```java
System.out.println("Hello".equalsIgnoreCase("HELLO")); // true
```

This checks equality without distinguishing uppercase from lowercase letters.

### F. `compareTo()`

`compareTo()` compares strings lexicographically. Its result is negative if the first string comes before the second, zero if they are equal, and positive if it comes after.

```java
System.out.println("apple".compareTo("banana") < 0); // true
System.out.println("cat".compareTo("cat") == 0); // true
System.out.println("dog".compareTo("cat") > 0); // true
```

Do not assume the result is exactly `-1`, `0`, or `1`. Only its sign matters.

### G. `toUpperCase()` and `toLowerCase()`

```java
String s = "HeLLo";

System.out.println(s.toUpperCase()); // HELLO
System.out.println(s.toLowerCase()); // hello
```

These methods return new strings; they do not modify the original string.

```java
String s = "hello";
s.toUpperCase();

System.out.println(s); // hello
```

To keep the result:

```java
s = s.toUpperCase();

System.out.println(s); // HELLO
```

### H. `trim()`

```java
String s = "  hello  ";

System.out.println(s.trim()); // "hello"
```

It removes certain leading and trailing characters, not spaces from the middle.

### I. `replace()`

```java
String s = "banana";

System.out.println(s.replace('a', 'o')); // bonono
System.out.println(s.replace("na", "XY")); // baXYXY
```

Like other string methods, `replace()` returns a new string.

---

## 5. Comparing Strings: `==` vs. `.equals()`

For strings, `==` checks whether two references point to the same object. `.equals()` checks whether their contents are equal.

```java
String a = new String("hello");
String b = new String("hello");

System.out.println(a == b); // false
System.out.println(a.equals(b)); // true
```

The strings contain the same text, but they are different objects.

For normal string-content comparisons, use `.equals()`.

---

## 6. Taking Input: `next()` vs. `nextLine()`

### A. `next()`

Reads the next token, stopping at whitespace.

```java
Scanner sc = new Scanner(System.in);

String name = sc.next();
```

If the input is:

```text
Alice Bob
```

`name` receives `"Alice"`.

### B. `nextLine()`

Reads the remainder of the current line, including spaces.

```java
String sentence = sc.nextLine();
```

If the input is:

```text
Alice Bob
```

`sentence` receives `"Alice Bob"`.

### C. Reading a Character

`Scanner` does not have a `nextChar()` method.

One common approach is:

```java
char ch = sc.next().charAt(0);
```

This reads the first character of the next token. Make sure the token is not empty.

### D. The `nextInt()` and `nextLine()` Trap

Consider:

```java
Scanner sc = new Scanner(System.in);

int age = sc.nextInt();
String name = sc.nextLine();
```

After `nextInt()` reads the number, the line separator remains. The next `nextLine()` may read only the remainder of that line, giving an empty string.

If the number is on its own line and the name is on the next line, use:

```java
int age = sc.nextInt();
sc.nextLine(); // Consume the remainder of the current line

String name = sc.nextLine();
```

Alternatively, if all input is token-based, use `next()` for the name.

### Choosing the Correct Input Method

| Situation | Method |
|---|---|
| One word | `next()` |
| Full sentence with spaces | `nextLine()` |
| Integer | `nextInt()` |
| Decimal number | `nextDouble()` |
| First character of a token | `next().charAt(0)` |

When mixing token-based and line-based input, think carefully about which part of the current line remains unread.

---

## 7. Uppercase, Lowercase, and Character Classification

Java provides the `Character` class for classifying individual characters.

### A. Checking Whether a Character Is a Digit

```java
char ch = '7';

if (Character.isDigit(ch)) {
    System.out.println("Digit");
}
```

### B. Checking Whether a Character Is a Letter

```java
char ch = 'A';

if (Character.isLetter(ch)) {
    System.out.println("Letter");
}
```

### C. Checking Uppercase and Lowercase

```java
char ch = 'G';

System.out.println(Character.isUpperCase(ch)); // true
System.out.println(Character.isLowerCase(ch)); // false
```

### D. Checking for a Letter or Digit

```java
char ch = '8';

if (Character.isLetterOrDigit(ch)) {
    System.out.println("Letter or digit");
} else {
    System.out.println("Something else");
}
```

For a special character such as `'#'`, `Character.isLetterOrDigit(ch)` returns `false`.

**Important:** `Character.isDigit()` and `Character.isLetter()` support Unicode characters, not only ASCII English characters. If a problem specifically restricts input to English letters and digits, direct comparisons can be clearer:

```java
if (ch >= '0' && ch <= '9') {
    System.out.println("ASCII digit");
} else if (ch >= 'A' && ch <= 'Z') {
    System.out.println("Uppercase English letter");
} else if (ch >= 'a' && ch <= 'z') {
    System.out.println("Lowercase English letter");
} else {
    System.out.println("Other character");
}
```

### E. Converting a Character's Case

```java
char ch = 'a';

char upper = Character.toUpperCase(ch);
char lower = Character.toLowerCase('B');

System.out.println(upper); // A
System.out.println(lower); // b
```

For a full string, use `toUpperCase()` or `toLowerCase()`.

### F. Counting Character Types in a String

```java
String s = "Abc123!";

int upper = 0;
int lower = 0;
int digits = 0;
int other = 0;

for (int i = 0; i < s.length(); i++) {
    char ch = s.charAt(i);

    if (Character.isUpperCase(ch)) {
        upper++;
    } else if (Character.isLowerCase(ch)) {
        lower++;
    } else if (Character.isDigit(ch)) {
        digits++;
    } else {
        other++;
    }
}

System.out.println("Uppercase: " + upper);
System.out.println("Lowercase: " + lower);
System.out.println("Digits: " + digits);
System.out.println("Other: " + other);
```

Output:

```text
Uppercase: 1
Lowercase: 2
Digits: 3
Other: 1
```

This is a common problem-solving pattern: traverse a string, classify each character, and update counters.

---

## 8. Checking Whether a Character Is a Vowel or Consonant

The English vowels are `a`, `e`, `i`, `o`, and `u`. The remaining English letters are consonants. A character that is not an English letter is neither.

```java
static void checkVowelOrConsonant(char ch) {
    ch = Character.toLowerCase(ch);

    if (ch < 'a' || ch > 'z') {
        System.out.println("Not an English letter");
    } else if (ch == 'a' || ch == 'e' || ch == 'i'
            || ch == 'o' || ch == 'u') {
        System.out.println("Vowel");
    } else {
        System.out.println("Consonant");
    }
}
```

Examples:

```java
checkVowelOrConsonant('A'); // Vowel
checkVowelOrConsonant('z'); // Consonant
checkVowelOrConsonant('7'); // Not an English letter
```

Converting to lowercase first lets the same checks handle uppercase and lowercase vowels.

---

## 9. String Immutability

Strings in Java are immutable. This means that once a `String` object has been created, its contents cannot be changed.

```java
String s = "hello";
s.toUpperCase();

System.out.println(s); // hello
```

The method returns a new string, but we ignored the result.

Correct:

```java
String s = "hello";
s = s.toUpperCase();

System.out.println(s); // HELLO
```

You cannot assign directly to a character position in a string:

```java
String s = "cat";
// s.charAt(0) = 'b'; // Invalid
```

If you need to change individual characters, convert the string to a character array:

```java
String s = "cat";
char[] arr = s.toCharArray();

arr[0] = 'b';

String result = new String(arr);
System.out.println(result); // bat
```

---

## 10. Basic String Problems

### A. Check Whether a Password Is Valid

Suppose a password must satisfy all these conditions:

1. At least 8 characters long.
2. Contains at least one uppercase English letter.
3. Contains at least one lowercase English letter.
4. Contains at least one digit.
5. Contains at least one special character.

For this example, a special character means anything that is not an English letter or digit.

```java
static boolean isValidPassword(String password) {
    if (password.length() < 8) {
        return false;
    }

    boolean hasUpper = false;
    boolean hasLower = false;
    boolean hasDigit = false;
    boolean hasSpecial = false;

    for (int i = 0; i < password.length(); i++) {
        char ch = password.charAt(i);

        if (ch >= 'A' && ch <= 'Z') {
            hasUpper = true;
        } else if (ch >= 'a' && ch <= 'z') {
            hasLower = true;
        } else if (ch >= '0' && ch <= '9') {
            hasDigit = true;
        } else {
            hasSpecial = true;
        }
    }

    return hasUpper && hasLower && hasDigit && hasSpecial;
}
```

Usage:

```java
System.out.println(isValidPassword("Abcdef1!")); // true
System.out.println(isValidPassword("abcdef1!")); // false
System.out.println(isValidPassword("Abcdefgh")); // false
System.out.println(isValidPassword("Abcdef12")); // false
```

#### Dry Run: `"Abcdef1!"`

| Character | Category | Flag updated |
|---|---|---|
| `A` | Uppercase | `hasUpper = true` |
| `b` | Lowercase | `hasLower = true` |
| `c` | Lowercase | No change |
| `d` | Lowercase | No change |
| `e` | Lowercase | No change |
| `f` | Lowercase | No change |
| `1` | Digit | `hasDigit = true` |
| `!` | Special | `hasSpecial = true` |

The length is 8 and all four flags are true, so the password is valid.

The definition of a special character depends on the problem's requirements.

### B. Count Vowels in a String

```java
static int countVowels(String s) {
    int count = 0;

    for (int i = 0; i < s.length(); i++) {
        char ch = Character.toLowerCase(s.charAt(i));

        if (ch == 'a' || ch == 'e' || ch == 'i'
                || ch == 'o' || ch == 'u') {
            count++;
        }
    }

    return count;
}
```

Example:

```java
System.out.println(countVowels("Hello World")); // 3
```

### C. Reverse a String

```java
static String reverse(String s) {
    String result = "";

    for (int i = s.length() - 1; i >= 0; i--) {
        result += s.charAt(i);
    }

    return result;
}
```

This is easy to understand, but repeated string concatenation can be inefficient for long strings. A more efficient approach uses `StringBuilder`:

```java
static String reverse(String s) {
    return new StringBuilder(s).reverse().toString();
}
```

### D. Check Whether a String Is a Palindrome

A palindrome reads the same forwards and backwards. Examples include `"racecar"`, `"level"`, and `"1221"`.

```java
static boolean isPalindrome(String s) {
    int left = 0;
    int right = s.length() - 1;

    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) {
            return false;
        }

        left++;
        right--;
    }

    return true;
}
```

This implementation is case-sensitive and includes spaces and punctuation. If a problem asks to ignore case or non-alphanumeric characters, normalize or filter the string first.

### E. Count Occurrences of a Character

```java
static int countOccurrences(String s, char target) {
    int count = 0;

    for (int i = 0; i < s.length(); i++) {
        if (s.charAt(i) == target) {
            count++;
        }
    }

    return count;
}
```

Example:

```java
System.out.println(countOccurrences("banana", 'a')); // 3
```

---

## 11. Common Mistakes

### A. Using an Invalid Index

```java
String s = "hello";
// System.out.println(s.charAt(s.length())); // Error
System.out.println(s.charAt(s.length() - 1)); // o
```

### B. Using `<=` Instead of `<`

Incorrect:

```java
for (int i = 0; i <= s.length(); i++) {
    System.out.println(s.charAt(i));
}
```

Correct:

```java
for (int i = 0; i < s.length(); i++) {
    System.out.println(s.charAt(i));
}
```

### C. Comparing Strings with `==`

Use `.equals()` when comparing string contents.

### D. Forgetting That String Methods Return New Strings

Incorrect if you expect `s` to change:

```java
s.toLowerCase();
```

Correct:

```java
s = s.toLowerCase();
```

### E. Confusing a Digit Character with a Number

```java
char ch = '8';

System.out.println((int) ch); // 56
System.out.println(ch - '0'); // 8
```

### F. Forgetting Case Sensitivity

```java
System.out.println("Java".equals("java")); // false
```

Use `equalsIgnoreCase()` if the problem asks for case-insensitive comparison.

### G. Mishandling `nextLine()`

After `nextInt()`, a leftover line separator can cause the next `nextLine()` to return an empty string. Consume the remainder of the line when appropriate.

### H. Calling `charAt(0)` on an Empty String

An empty string has no valid character index. Check that `s.length() > 0` before calling `charAt(0)`.

---

## 12. Quick Revision

| Task | Method or technique |
|---|---|
| Get string length | `s.length()` |
| Get character at index | `s.charAt(i)` |
| Extract substring | `s.substring(start, end)` |
| Compare string contents | `s.equals(t)` |
| Compare ignoring case | `s.equalsIgnoreCase(t)` |
| Lexicographic comparison | `s.compareTo(t)` |
| Check for substring | `s.contains(t)` |
| Find first occurrence | `s.indexOf(t)` |
| Convert case | `s.toUpperCase()`, `s.toLowerCase()` |
| Check digit | `Character.isDigit(ch)` |
| Check letter | `Character.isLetter(ch)` |
| Check uppercase/lowercase | `Character.isUpperCase(ch)`, `Character.isLowerCase(ch)` |
| Digit character to integer | `ch - '0'`, after validating |
| Read one token | `sc.next()` |
| Read a full line | `sc.nextLine()` |
| Convert string to integer | `Integer.parseInt(s)` |
| Convert integer to string | `String.valueOf(n)` |

Before submitting a string solution, check:

- Are all indices valid?
- Am I using `.equals()` for string-content comparisons?
- Does the problem distinguish uppercase and lowercase?
- Do I need `next()` or `nextLine()`?
- Am I treating digit characters and integer values correctly?
- Does my solution handle an empty string if allowed?

---

## 13. Practice Questions

### Beginner

1. Read a string and print its length.
2. Read a string and print each character on a separate line.
3. Count uppercase letters, lowercase letters, digits, and special characters.
4. Check whether a character is a vowel, consonant, digit, or other character.
5. Convert all lowercase English letters in a string to uppercase.
6. Count the occurrences of a given character in a string.

### Intermediate

7. Check whether two strings are equal, ignoring case.
8. Reverse a string.
9. Check whether a string is a palindrome.
10. Count the vowels and consonants in a string.
11. Check whether a password satisfies the five rules in Section 10.
12. Extract and print the first word of a sentence.
13. Check whether a string contains only English letters and digits.

### Challenge

14. Find the first character that appears only once in a string.
15. Check whether two strings are anagrams, meaning they contain the same characters with the same frequencies.
16. Remove all spaces from a string.
17. Find the most frequently occurring character in a string.
18. Check whether a string is a palindrome while ignoring case and non-alphanumeric characters.

For each question, identify the relevant string methods first. Then decide whether you need a loop, counters, flags, or two pointers. Test cases with uppercase letters, digits, spaces, punctuation, and empty strings whenever the problem allows them.

**Final takeaway:** Most beginner string problems involve traversing the string, inspecting each character, and maintaining some state. Get comfortable with `length()`, `charAt()`, character classification, and string comparison; these are the building blocks for more advanced problems.
