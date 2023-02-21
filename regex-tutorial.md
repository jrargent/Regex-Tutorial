# Email Regex Tutorial and Explanation

The purpose of this tutorial is to explain what a regex is, how it works, and how it can be useful for JavaScript coding purposes. 

A Regular Expression, or regex, is a way to define a search pattern using text characters. The simplest and easiest to understand example of what regex can be used for is the "find" or "find and replace" function in a program like Microsoft Excel. 

For JavaScript and web development purposes, regex can be used for input validation, among many other things. 

## Summary

The characters in a regex represent specific or special things, including strings of letters and/or numbers to look for in a search as well as specific quantities of search items.  

The regex I will be explaining is used for email validation.
The regex is:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```
I will use the email address "hello@world.com" as an example. 

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Back-references](#back-references)
- [Putting it all together](#Putting-it-all-together)

## Regex Components

### Anchors

```
^
```
This character, called a carrot when used in writing, denotes the beginning of a string.
It can also denote the beginning of a line if multuple lines are being searched.
For example, the regex "^hello" will look for anything that starts with "hello"

```
$
```
This character denotes the end point of a string.
It can also denote the end of a line is multiple lines are being searched. 
For example, the regex "com$" will look for anything that ends with "com"


### Quantifiers
Quantifiers are parts of a regex that denote how often the search for look for a particular character. 

```
+
```
This denotes a search for one or more of the preceding character.
For example "hello+" can find "hello", "hellooooooooooooo" or any number of "o"s after hello. 

```
*
```
This denotes a search for zero or more of the preceding character.
For example, "hello*" can find "hello", "hellooooo" or "hell"

```
?
```
This denotes a search for one or none of the preceding character.
For example, "hello?" can find "hello" or "hell"

```
{}
```
This denotes a search for the preceding character a number of times specified in the curly braces.
For example, "hello{1}" will find "hello". "hello{1,3}" will find "hello", "helloo", or "hellooo". It will find "hell" followed by a number of "o"s between 1 and 3. 

### OR Operator

```
|
```
This denotes a search for the preceding character(s) or subsequent character(s).
For example, "(hello|world)" can find "hello" or "world"

### Character Classes

```
.
```
This denotes a search for any character.

```
\
```
This is an escape character and is used to denote a search for a special character in particular. 
For example, "." will search for any character while "\." will search specifically for "."

```
\w
```
This denotes a search for any alphaneumeric character, called word characters in regex. 

```
\W
```
This denotes a search for any non-alphaneumeric character, called non-word characters. This could include commas, semi-colons, and anything that isn't a letter or number. \W is the opposite of \w. 

```
\d
```
This denotes a search for a digit between 0 and 9. 

```
\D
```
This denotes a search for a character that is not a digit. This is the opposite of \d. 

```
\s
```

### Grouping and Capturing

```
( )
```
Parentheses denote a group. Anything between the parentheses can be searched for, as opposed to just a single character. 

Groups can also be captured and replaced as needed. That is, JavaScript or another programming language can be used to identify and then replace part of the regex that is in the captured group.
 
If you do not want a group to be captured, include ``` ? ``` after the first ``` ( ```. 

For example, ``` (?hello) ``` will not be a captured group. 

### Bracket Expressions
```
[]
```
This denotes a search for the items in the brackets as if there was an ``` | ``` between all characters.
That is, if the expression was [\da-z], the search would look for either a single digit (\d) OR any lowercase letter. 

### Greedy and Lazy Match
A greedy match means an expression will search for as many characters as possible. You can think of a greedy match as having "or more" at the end of it. 

For example, the  ``` * ``` quantifier looks for 0 *or more* of the character(s) that precede it. 

A lazy match means an expression will search for as few characters as possible. You can think of a lazy match as having "and no more" at the end of it. 

For example, the ``` ? ``` quantifier looks for 0 or 1 *and no more* of the character(s) that precede it. 


### Back-references
```
\1
```
A back-reference is a way to repeat a group in a regex without having to write it out in its entirety again.
Each group has its own identifier, starting with the number 1. 
If a group such as (Example|Sample) was the first group in a regex, it could be referenced again later in the regex by using \1.


### Putting it all together

I will now break apart the email validation regex piece by piece to walkthrough how it all works.

As a reminder, this is what the regex looks like all together:
```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

``` ^ ``` is the start of the expression and denotes the beginning of the string that will be searched for.

``` ([a-z0-9_\.-]+) ``` is a bracketed search inside of a group. Inside the brackets, it looks for anything that matches all lowercase letters or all digits between 0 and 9. It also looks for underscores (_), or dots (.), or hyphens (-). The + outside the brackets denotes that the regex will look for any number of the preceding characters (everything that is inside the brackets). Finally, the () denotes that this section is a group. 

In plain english, this means that the regex will look for the first part of an email address, the part that comes before the @ symbol. For our example email, this would be the "hello" part of "hello@world.com"


``` @ ``` will search specifically for the @ symbol, which all email addressess would have. This would be the "@" in "hello@world.com"


``` ([\da-z\.-]+) ``` is a second group, denoted by (). The items in the brackets denote that the search will look for a single digit between 0 and 9 (\d), or a lowercase letter (a-z), or a dot (\.) or a hyphen (-). The + outside the brackets denotes that the regex will look for any number of the preceding characters (everything that is inside the brackets).

For our example email, this would be the "world" part of "hello@world.com"


``` \. ``` will search specifically for the . symbol, which all email addresses would have. This would be the "." in "hello@world.com"

``` ([a-z\.]{2,6}) ``` is a third group, denoted by (). The items in the brackets denote that the search will look for a lowercase letter (a-z) or a dot (\.). The {2,6} means that the search will look for a number of the preceding items between 2 and 6 characters long. 
Since most if not all email address websites will end in something like ".ca", ".net", ".org", etc., the search does not need to search for anything smaller than 2 characters or larger than 6 characters. 

For the example email, this would be the "com" in "hello@world.com".


Lastly, ``` $ ``` denotes the end of the expression and the end of the search criteria. 

## Author

I am a beginning programmer going through a coding bootcamp at the moment. 

I am also an accomplished weaver, spinner, knitter, and textile history recreationist. 

[My GitHub](#https://github.com/jrargent)
