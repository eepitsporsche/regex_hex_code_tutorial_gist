# Identifying Hex Codes with Regex

The following is a comprehensive guide to provide an understanding of regex components and patterns. Regular expressions, referred to as regex, are a specified set of characters used to identify a desired string.
The focus of this guide is to identify and explain the components of the regex pattern used to validate hex codes. Hexidecimal codes, referred to as hex codes, are written in base-16 format and used to define colors in front-end engineering.

## Summary

This guide will break down the components of the following regular expression used to identify hex codes:
```
/^#?([A-F0-9]{6}|[A-F0-9]{3})$/
```

The regex components discussed in this tutorial include: anchors, character classes, quantifiers, grouping constructs, bracket expressions, the OR operator, flags, and character escapes.

## Table of Contents

- [Anchors](#anchors)
- [Character Classes](#character-classes)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors

Anchors are special characters in regular expressions that define the boundaries of the text the regex should match.

The entire expression is contained within two forward slashes. The start anchor `^` asserts that the pattern must match the start of the string. The end anchor `$` asserts that the pattern must match the end of a string.

> **Start example:** <code>/^W</code> will match a string that begins with 'W', such as 'World'. This would not, however, match the string 'Hello World', since this string begins with 'H'.

> **End example:** <code>o$/</code> will match a string that ends with 'o', such as 'Hello'. This would not, however, match the string 'Hello World', since this string ends with 'd'.

### Character Classes

Character classes, also known as character sets, are used to simplify and shorten regex patterns, making the regex more concise and easier to read. In the regex, square brackets <code>[]</code> can contain character sets, meta character sets, and repeating character classes, all of which contribute to more versatile regex patterns.

Character classes are case-sensitive, meaning the regex will only match characters that have the same case as specified in the pattern.

The character class contained within the hex code regex <code>[A-F0-9]</code> specifies a matching string should contain only capital letters A-F and numbers 0-9.

Since hex codes may be written in lower case, a regex to include all letter cases would look like:

```
/^#?([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$/
```

### Quantifiers

Regex quantifiers are used to specify how many times a pattern should match. The word <i>quantify</i> comes from the latin <i>quantis</i>, meaning 'how much'. Quantifiers are placed before or after a character, character class, or group, in order to determine the minimum or maximum number of times preceding patterns should occur.

Hex codes themselves are quantifiers of color. Excluding the # symbol, the length of a hex code is six characters. The first two characters indicate the amount of red, the next two characters indicate the amount of green, and the final two indicate the amount of blue, otherwise expressed as #RRGGBB.

The hex code regex quantifiers are <code>{6}</code> and <code>{3}</code>. The first quantifier, <code>{6}</code>, specifies the string should match a length of six characters.

RGB values can span numbers 0 to 255. However, the hexadecimal numeral system uses a base of sixteen, referred to as base-16. The base-16 values are as follows:

<code>0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F</code>

The letters A-F in the base-16 system represent numbers 10 through 15, respectively.

> **Example:**<br>
The color pure red in RGB form is (255, 0, 0). However, the hex code for pure red would not be #25500. This would translate to 25 red, 50, green, 0 blue.<br><br>
To find the hex code value of pure red, divide its RGB red value of 255 by 16. This returns 15.9375. The first whole number is 15, represented in base-16 with the letter F, which will be the first character of the hex code. The remainder of .9375 is then multiplied by 16, with a product of 15. 15 will again be represented in base-16 by F and will be the second character of the hex code.<br><br>
Since the green and blue values of the pure red color are zero, the finished hex code is #FF0000, meeting the 6 character specification of the regex quantifier.

The second quantifier, <code>{3}</code>, specifies the string should match a length of three characters. This quantifier acts a secondary quantifier under a disjunction. For information on disjunctions, see [The OR Operator](#the-or-operator) section of this guide.

### Grouping Constructs

Grouping constructs are used to match repeated sequences of characters or sub-expressions, and treat them as a single unit within the regex.

Enclosed in parenthesis <code>()</code>, grouping constructs serve the following purposes:

* apply quantifiers to a group of characters
* capture the designated portion of the match for later use
* create back reference for a previously matched group
* apply [alternation](#the-or-operator) to a group of characters

The hex code regex discussed in this guide contains one grouping construct, consisting of [bracket expressions](#bracket-expressions) and [quantifiers](#quantifiers).

### Bracket Expressions

Bracket expressions are used to define a set of characters that can be matched within a single position in the string. Namely, they are denoted by square brackets <code>[]</code>, and the characters enclosed within the brackets will become part of the allowed set. Bracket expressions can contain individual characters and/or define character ranges with a hyphen <code>-</code>, to create more flexible patterns.

In the instance of the hex code regex, the bracket expression contains the [character classes](#character-classes), <code>[A-F0-9]</code>.

### The OR Operator

Similarily to the [pipe operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR) in JavaScript, the character <code>|</code> represents an 'OR' case in regex. The OR operator, also known as alternation, allows regex to match one pattern condition or an alternate for more flexible and adaptable patterns.

<code>[A-F0-9]{6}</code> tells the regex to match a string that is 6 characters long, and includes only capital letters A-F and numbers 0-9.

Since hex codes can be written as #RRGGBB or #RGB, the <code>|</code> disjunction adds the parameter to alternatively match a string that is 3 characters long.
So <code>[A-F0-9]{3}</code> tells the regex to match a string that is 3 characters long, and includes only capital letters A-F and numbers 0-9.

The pure red hex code exampled previously can be written as #FF0000 or #F00. Regex will accept and indentify each form through use of the <code>|</code> OR operator.

### Flags

Flags are modifiers which affect the behavior of regualr expressions by enabling or disabling certain features and are appended to the end of the regex pattern, outside the slashes <code>/</code>.

Though the hex code regex discussed in this guide does not utilize flags, it is still important to understand their function in regex patterns. Flags can control case-sensitivity, multiline matching, and global matching, among other things.

> **Common flag types:**
1. <code>i</code> (ignore case): Enable the regex case-insensitive, matching both uppercase and lowercase characters.
2. <code>m</code> (multiline): Enables start <code>^</code> and end <code>$</code> anchors to match at the beginning and end of each line in a multiline string, rather than just the beginning and end of the entire string.
3. <code>g</code> (global): Enables global matching wherein the regex engine finds all matches in the input string.
4. <code>s</code> (dotAll): Enables dot <code>.</code> meta character to match any character, including newline characters.
5. <code>u</code> (unicode): Treats input string as Unicode, enables correct processes of Unicode surrogate pairs.
6. <code>y</code> (sticky): Mandates regex engine to initiate searching for a match at the exact position specified by the lastIndex property.

### Character Escapes

A character escape, denoted with a backslash <code>\\</code>, suppresses the special meaning of meta characters and represents characters that cannot be directly typed.

>**Example:**
A backslash before a dot <code>\\.</code> allows regex to interpret the literal use of the character instead of a metaphorical wildcard, to accurately match a string.

Meta characters have special meaning in regex, but when placed among character classes lose their special meaning and behave as regular characters. An escape sequence instructs regex to observe a special meaning of a character.

>**Example:**
A backslash before the letter d <code>\\d</code> represents the escape sequence for any digit 0-9 and serves as shorthand for the use of <code>[0-9]</code>. Without the backslash, regex would treat the d as a literal.

While the hex code regex discussed in this guide does not utilize character escapes, it is important to recognize and understand their use. 

## Author

Porsche Herskorn, an aspiring full-stack web developer studying with UC Berkeley Extension.

<b>Follow me on [GitHub](https://github.com/eepitsporsche)</b>