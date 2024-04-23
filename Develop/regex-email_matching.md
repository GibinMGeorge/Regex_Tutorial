# Title -  Matching an Email Address Using Regular Expressions

Regular expressions (regex) are powerful tools for pattern matching in strings. When included in code or search algorithms, regular expressions can be used to find certain patterns of characters within a string, or to find and replace a character or sequence of characters within a string. They are also frequently used to validate input.
In this tutorial, we will explore a regex pattern for matching email addresses and discuss its various components.

## Summary

We will describe a regex pattern that matches email addresses. This regex ensures that the email follows a standard format, including a valid usernames, domain names and top-level domain. 
Here's the regex pattern:

/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

Code snippet and it's expected output - 

```md
const emailRegex = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/;
console.log(emailRegex.test("user@example.com")); // true
console.log(emailRegex.test("john.doe123@gmail.com")); // true
console.log(emailRegex.test("jane_doe-123@yahoo.co.uk")); // true
console.log(emailRegex.test("info@company.com")); // true
console.log(emailRegex.test("support123@domain.net")); // true

console.log(emailRegex.test("notanemail")); // false
console.log(emailRegex.test("user@example")); // false
console.log(emailRegex.test("@example.com")); // false
console.log(emailRegex.test("user@.com")); // false
console.log(emailRegex.test("user@123.456")); // false
```


## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors

Anchors specify the position in the string where the pattern should match. In our regex, ^ denotes the start of the string, and $ denotes the end.

Example-

```md
const regex = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/;

// Test email addresses
const email1 = "example@email.com"; // Should match
const email2 = "example_email.com"; // Should not match
```

### Quantifiers

Quantifiers define how many times a specific character or group should appear in the string. For example, {2,6} in our regex means the preceding expression should occur between 2 and 6 times.

Example-

```md
const testString1 = "123";         // Should match (length: 3)
const testString3 = "1";           // Should not match (length: 1)
const testString4 = "123456789";   // Should not match (length: 9)
```

also - 

*—Matches the pattern zero or more times

+—Matches the pattern one or more times

?—Matches the pattern zero or one time

### Grouping Constructs

Grouping constructs, denoted by parentheses (), allow us to group parts of the regex together. They allows us to group parts of the regex together, apply quantifiers to those grouped parts, capture matched substrings for later use, and apply alternation to multiple characters or subpatterns.

### Bracket Expressions

Bracket expressions, enclosed in square brackets [], define a range of characters that should match. 

hyphen (-) used between alphanumeric characters (letters and numbers only) to represent a range of those possible characters.

Example : 

[a-z]—The string can contain any lowercase letter between a–z. 

[0-9]—The string can contain any number between 0–9

In our regex, they specify valid characters for the username and domain name parts of the email address.

### Character Classes

Character classes represent a group of characters that can match a single character in the string. 

Example : include \d for digits and \w for word characters.

### The OR Operator

The OR operator | allows us to specify alternative matches. It's commonly used within bracket expressions or grouping constructs to match different patterns.

### Flags

Flags are optional modifiers that affect how the regex engine interprets the pattern. 

Common flags include:  g for global matching and i for case-insensitive matching.

### Character Escapes

Character escapes are denoted by a backslash \, allows us to match special characters literally. 

For example, the open curly brace ({) is used to begin a quantifier, \. matches a literal dot character etc.

## Author

This tutorial was written by Gibin M George. 

Github -  https://github.com/GibinMGeorge
