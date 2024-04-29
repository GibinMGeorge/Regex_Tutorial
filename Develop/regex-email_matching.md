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

Anchors specify the position in the string where the pattern should match. 

In our regex, ^ denotes the start of the string, and $ denotes the end.

These symbols ensures that the entire email address is evaluated against the defined pattern, enhancing the accuracy of email address validation.

Example-

```md
const regex = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/;

// Test email addresses
const email1 = "example@email.com"; // Should match
const email2 = "example_email.com"; // Should not match
const email3 = "user@example.com@extra"; // Should not match (multiple @ symbols)
const email4 = "@example.com"; // Should not match (empty username)
const email5 = "user@.com"; // Should not match (empty domain)
```

### Quantifiers

Quantifiers define how many times a specific character or group should appear in the string. 

For example, {2,6} in our regex means the preceding expression should occur between 2 and 6 times.

This provides flexibility in specifying the allowed repetition of characters or groups, allowing for a range of valid inputs. In the context of email matching, quantifiers enable us to define constraints on the length or occurrence of certain components, such as the username or domain name, ensuring that they meet the desired criteria .

Example-

```md
const testString1 = "123";         // Should match (length: 3)
const testString2 = "1";           // Should not match (length: 1)
const testString3 = "123456789";   // Should not match (length: 9)
const testString4 = "";            // Should not match (empty string)
const testString5 = "aabbcc";      // Should match (length: 6)
const testString6 = "aaaaaaabbbbbbbcccccc"; // Should match (length: 21)
```

also - 

*—Matches the pattern zero or more times

+—Matches the pattern one or more times

?—Matches the pattern zero or one time

### Grouping Constructs

Grouping constructs, denoted by parentheses (), allow us to group parts of the regex together. They allows us to group parts of the regex together, apply quantifiers to those grouped parts, capture matched substrings for later use, and apply alternation to multiple characters or subpatterns.

Example-

The outermost grouping construct () captures the entire email address.

Inside this group, we have three more groups:

( ): Captures the username part.

( ): Captures the domain part.

( ): Captures the top-level domain part.


```md
const emailRegex = /^(([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6}))$/;

const email = "john.doe@example.com";
const match = email.match(emailRegex);

if (match) {
  console.log("Full email:", match[1]); // Full email address
  console.log("Username:", match[2]);   // Username part
  console.log("Domain:", match[3]);     // Domain part
  console.log("Top-Level Domain:", match[4]); // Top-Level Domain part
}
```

consider another example 

```md
const emailRegex = /^(([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6}))$/;

const email1 = "john.doe@example.com";
const email2 = "jane@example.com";
const email3 = "not.an.email@example.com@extra"; // Should not match (multiple @ symbols)
```

### Bracket Expressions

Bracket expressions, enclosed in square brackets [], define a range of characters that should match. 

hyphen (-) used between alphanumeric characters (letters and numbers only) to represent a range of those possible characters.

Additionally, bracket expressions can include other characters or character classes to form complex patterns. In email matching regex, bracket expressions are commonly used to define valid characters for the username and domain parts of the email address

Example : 

[a-z]—The string can contain any lowercase letter between a–z. 

[0-9]—The string can contain any number between 0–9

In our regex, they specify valid characters for the username and domain name parts of the email address.

Example - 

```md
const testString1 = "abc123"; // Should match
const testString2 = "ABC123"; // Should not match (uppercase letters not allowed)
const testString3 = "abc@123"; // Should not match (special characters not allowed)
const testString4 = "aabbcc"; // Should match
const testString5 = "123456"; // Should match
```

### Character Classes

Character classes represent a group of characters that can match a single character in the string. 

For example, the character class \d matches any digit from 0 to 9, while \w matches any alphanumeric character (letters, digits, or underscores)

Similarly, \s matches any whitespace character such as spaces, tabs, or line breaks. 

In the example of email matching regex, character classes are utilized to define valid characters for different parts of the email address, ensuring that it meets expected standards. 

By using character classes, regex patterns become more versatile and capable of handling various input scenarios effectively.

Example - 

```md
const emailRegex = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/;

const email1 = "user@example.com"; // Should match
const email2 = "user123@example.com"; // Should match
const email3 = "user@ex@mple@example.com"; // Should not match
const email4 = "user@example"; // Should not match (missing top-level domain)
const email5 = "user@123.123"; // Should not match (invalid domain)

```

### The OR Operator

The OR operator | allows us to specify alternative matches. It's commonly used within bracket expressions or grouping constructs to match different patterns.

For example, in the email matching regex, the OR operator can be used to specify alternative top-level domains such as .com, .net, or .org. By utilizing the OR operator, regex patterns become more flexible and adaptable to various input possibilities, enhancing the robustness of the matching process.


Example - 

```md
const emailRegex = /^(([a-z0-9_\.-]+)@([\da-z\.-]+)\.(com|net|org))$/;

const email1 = "abc@xyz.com";           // Should match
const email2 = "test@test.net";         // Should match
const email3 = "user@domain.org";       // Should match
const email4 = "invalid_email@gmail.xyz";  // Should not match
const email5 = "user@example.gov.inc";      // Should not match
```
Here the OR operator allows the regex to match email addresses with ".com", ".net", or ".org" top-level domains.

### Flags

Flags are optional modifiers that affect how the regex engine interprets the pattern. These modifiers can alter the behavior of the regex pattern, providing additional functionalities or constraints.

Common flags include:  g for global matching and i for case-insensitive matching, which enables the regex engine to ignore the distinction between uppercase and lowercase characters when performing matching operations. 

Example -

```md
const emailRegex = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/i; // Added 'i' flag for case-insensitive matching

const email1 = "USER@example.COM"; // Should match (case-insensitive)
const email2 = "user123@eXample.cOm"; // Should match (case-insensitive)
const email3 = "usER@EXAMPLE.CoM"; // Should match (case-insensitive)
const email4 = "invalid_email@GMAIL.ccc"; // Should not match (case-sensitive)
```

Consider an example for demonstrating the use of -g, global matching -

```md

const text = "hello world hello hello";
const pattern = /hello/g;

const matches = text.match(pattern);

console.log(matches); // Output: ["hello", "hello", "hello"]

```

In this example, the regex pattern /hello/g is used to match all occurrences of the word "hello" within the input string text. By including the "g" flag, the match() method returns an array containing all matched substrings, rather than just the first match.


### Character Escapes

Character escapes are denoted by a backslash \, allows us to match special characters literally. 

For example, the open curly brace ({) is used to begin a quantifier, \. matches a literal dot character etc.

Or if we want to add a special character, we can implement by folloing,

```md
// Original email regex pattern without character escapes
const emailRegex = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.(com|net|org)$/;

// Test email string with special characters
const testEmail = "test.email*test@example.com";

// Test the regex pattern without character escapes
console.log(emailRegex.test(testEmail)); // Output: false as special character is not matched

// Modify the regex pattern with character escapes to match special characters
const emailRegexWithEscapes = /^([a-z0-9_\.-]*)@([\da-z\.-]+)\.(com|net|org)$/;

// Test the modified regex pattern with character escapes
console.log(emailRegexWithEscapes.test(testEmail)); // Output: true as special character is matched

```
Consider another Example - 

```md
// Original email regex pattern without character escapes
const emailRegex = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.(com|net|org)$/;

// Test email string with special characters
const testEmail1 = "test.email*test@example.com"; // Should not match (special character *)
const testEmail2 = "test!email@example.com"; // Should not match (special character !)
const testEmail3 = "test.email.test@example.com"; // Should match (no special characters)
```

## Author

This tutorial was written by Gibin M George. 

Github -  https://github.com/GibinMGeorge

Linedin - : https://www.linkedin.com/in/gibin-m-george-a71994244
