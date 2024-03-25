# Regex-Tutorial

## Description
Hello! In this tutorial, I will be attempting to educate you on how matching a hex value works. In this tutorial we will be breaking down the regex and explaining each individual section, the matching process and some examples. The regex that will be discussed in this tutorial is " /^#?([a-f0-9]{6}|[a-f0-9]{3})$/ ". 


## Table of contents
-[Overview](#overview)
-[The Challenge](#the-challenge)
-[Matching Headecimal Colour Values](#matching-headecimal-colour-values)
-[Understanding the Regex](#understanding-the-regex)
-[How do we match it?](#how-do-we-match-it)
-[Examples](#examples)
-[Conclusion](#conclusion)
-[Author Links](#author-links)

# Overview

## The Challenge
Developers write code, but they also write about code. Take a moment to search the web for tutorials about any of the subjects you’ve learned so far in this course. You’re likely to find thousands of tutorials written by developers of all skill levels, including junior developers—like yourself!

Your assignment this week is to create a tutorial that explains how a specific regular expression, or regex, functions by breaking down each part of the expression and describing what it does. You'll use the template provided in the starter code to create your walkthrough.

## User Story
```md
AS A web development student
I WANT a tutorial explaining a specific regex
SO THAT I can understand the search pattern the regex defines
```

## Acceptance Criteria 
```md
GIVEN a regex tutorial
WHEN I open the tutorial
THEN I see a descriptive title and introductory paragraph explaining the purpose of the tutorial, a summary describing the regex featured in the tutorial, a table of contents linking to different sections that break down each component of the regex and explain what it does, and a section about the author with a link to the author’s GitHub profile
WHEN I click on the links in the table of contents
THEN I am taken to the corresponding sections of the tutorial
WHEN I read through each section of the tutorial
THEN I find a detailed explanation of what a specific component of the regex does
WHEN I reach the end of the tutorial
THEN I find a section about the author and a link to the author’s GitHub profile
```

# Matching Headecimal Colour Values

## Understanding the Regex

To begin, lets start by breaking down the regex into individual compenents to really understand what this `/^#?([a-f0-9]{6}|[a-f0-9]{3})$/` even means. 
1) `^` Asserts the start of the string. This ensures that the regex matches from the beginning of the string. 
2) `#?` Matches an optional `#` character. The `?` is a quanitfier that indicates that the `#` character may appear zero or one time. So, the hex colour code may start with or without the `#`.
3) `([a-f0-9]{6}|[a-f0-9]{3})` This part is a capturing group that matches either six hexadecimal characters [a-f0-9]{6} or three hexadecimal characters [a-f0-9]{3}. Here's what each sub-part means:

- `[a-f0-9]`: This character class matches any character that is either a lowercase letter from 'a' to 'f', a digit from '0' to '9'. This covers all valid hexadecimal digits.
- `{6}`: This quantifier specifies that the preceding character class [a-f0-9] must appear exactly 6 times. This enforces a match for a full 6-character hex color code.
- `|` This is an alternation operator (OR operator), allowing either the preceding pattern (6 hexadecimal characters) or the next pattern (3 hexadecimal characters) to match.
- `[a-f0-9]{3}`: Similar to the first part, this matches exactly 3 hexadecimal characters, enforcing a match for shorthand 3-character hex color codes.
4) `$`: Asserts the end of the string. This ensures that the regex matches until the end of the string.

So, in summary: 
- `^`: Start of string.
- `#?` : Optional # character.
- `([a-f0-9]{6}|[a-f0-9]{3})`: Capturing group matching either a full 6-character hex color code or a shorthand 3-character hex color code.
- `$`: End of string.

## How do we match it?

Now that we understand what each section does and how they work together, lets start understanding HOW they work together to get us a colour. To start matching a hex value using this regex, follow these steps:

1) Start with the regex pattern: `/^#?([a-f0-9]{6}|[a-f0-9]{3})$/`
2) Begin with the start of the string using the `^` character.
3) Optionaly match a `#` character. 
4) Match either six hexadecimal characters `[a-f0-9]{6}` or three hexadecimal characters `[a-f0-9]{3}`.
5) End the string using the `$` character. 

## Examples 

Let's see some examples to further understand how the regex works:

Valid Hex Values: 
- `#FF0000`
- `#F00`
- `#00FF00`
- `#0F0`
- `#0000FF`
- `#00F`

In these examples, you can see that all the hex values are within the capturing group: `([a-f0-9]{6}|[a-f0-9]{3})`. 

Invalid Hex Values
- `#1234567` (too long)
- `#ggg` (invalid characters)
- `#123abc` (invalid characters)
- `#12345` (too short)

In these examples we can see that they are wrong. Yes I can hear you "oh but example 2 and 3 are within the capturing group!!!!". You are right BUT, as provided, this regex is CASE-SENSITIVE by default, meaning that it would only match uppercase characters in the range of `a-f`. We can fix this by making the regex case-INSENSITIVE by modifying the regex so that it would match both uppercase and lowercase. For example: `/^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/`. We can also fix this by using a case-insensitive flag (if your programming language supports it). For example, in JavaScript, you can use `/^#?([a-f0-9]{6}|[a-f0-9]{3})$/i`. By making the regex case-insensitive, it will match color codes like `#123abc` because it will accept both lowercase and uppercase letters in the range `a-f`.

## How can I implement this into code??????

Glad you asked. For Javascript:

const regex = /^#?([a-f0-9]{6}|[a-f0-9]{3})$/i;
const isValidHex = regex.test("#ff0000"); // Example hex value
console.log(isValidHex); // Output: true

For python: 

import re
pattern = re.compile(r'^#?([a-f0-9]{6}|[a-f0-9]{3})$', re.IGNORECASE)
is_valid_hex = pattern.match("#ff0000") # Example hex value
print(bool(is_valid_hex)) # Output: True

As we can see, we have implemented the case-insensitive flag for JavaScript using the `i` tag and for python we used the `re.IGNORECASE` flag. 

# Conclusion

By understanding and implementing this regex, you can effectively match hexadecimal color values in your applications or scripts, ensuring data integrity and correctness when dealing with color representations. Thank you for coming to my TedTalk. 

# Author Links
This is my github link : https://github.com/darrendoan