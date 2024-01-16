# Regex for a HTML Tag - Let's break it down!
Deciphering regex expressions can be done one piece at a time. This gist takes you on a journey decomposing the regex for a HTML tag to its smallest parts then building them back together in order to make sense of the whole.

## Summary

This gist will help you to understand regex for matching HTML Tags by decomposing the expression and explaining how each part is represented in the regex. <br>
The regex to match a HTML Tag is: 

    /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/ <br>

Regular expressions (regex) represent the patterns of characters in text. HTML Tags are strings used in code to identify HTML elements and their attributes which provde the structure to a webpage or app. We can create a regex that matches HTML tag because HTML tags consistently hold a certain pattern that can be represented in a series of components.<br>

The decomposition of a HTML Tag is seen in this image:

![Decomposed HTML Tag](./images/Decomposed%20HTML%20Tag%20.png)

There are several reasons for wanting to match HTML tags including: 
- Before accepting the code from other users into the development of our apps, regex can be used to check for HTML tags that may import unwanted files into our app by efficiently finding `<script>` tags. 
- Regex can also be used when a developer wants to refactor code and make it better for screen readers by replacing `<div>` tags with more descriptive tags and adding alt text to all `<img>` elements found in the code. 
- Regex is also a solution for those who want to adjust the content in their HTML to other formats. Regex matches all HTML tags and attributes and then the developer removes them from the file before replication in another file. `<br>`


## Table of Contents

- [Anchors](#anchors)
- [Grouping Constructs](#grouping-constructs)
- [Quantifiers](#quantifiers)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Wildcard](#the-wildcard)
- [Character Escapes](#character-escapes)
- [Back Reference](#back-reference)
- [Putting it all back together](#putting-it-all-back-together)
- [Author](#author)
- [References](#references)


## Regex Components

<span style="background-color: grey">/</span>^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$<span style="background-color: grey">/</span>
A backslash at the start and end of the string identify that this string is a regex. 

### Anchors
    /<span style="background-color: grey">^</span><([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)<span style="background-color: grey">$</span>/

^ is used to indicate the beginning of the expression.<br>
$ is used to show the end of the expression.

### Grouping Constructs
Parentheses () group each pattern. 
/^< <span style="background-color: yellow"> ([a-z]+) </span> <span style="background-color: blue"> ([^<]+)</span> * <span style="background-color: purple"> (?:>(.*)<\/\1>|\s+\/>) </span> $/
<br>
The capturing groups are indicated in yellow and blue. Capturing groups (x) match this group and remember the match for future reference.
<br>
The purple group is a non-capturing group (?:x). It matches but won't be remembered for referencing.<br>

### Quantifiers
/^<([a-z] <span style="background-color: blue"> + </span>) ([^<] <span style="background-color: blue"> + </span> )<span style="background-color: purple"> * </span> (?:>(. <span style="background-color: purple"> * </span> )<\/\1>|\s<span style="background-color: blue"> + </span> \/>)$/ <br>
Quantifiers indicate the number of characters or expressions to match.

- '*' is a quantifier that means: match the preceding item 0 or more times. 
So, ([^<]+)* and .* means match 0 or more times.

- '+' is a quantifier that means: match the preceding item 1 or more times.
So, [a-z]+ means match any letter in the range a-z, 1 or more times and \s+\ means \s 1 or more times

### Bracket Expressions
Bracket are used around characters to create bracket expressions which are either match all in the list expressions or match all except what is in the list expressions. 

### Character Classes

/^<(<span style="background-color: purple"> [a-z] </span> +)(<span style="background-color: purple"> [^<] </span> +)*(?:>(.*)<\/\1>|<span style="background-color: purple">\s </span> +\/>)$/ <br>

Character classes distinguish kinds of characters, for example, distinguishing between letters and digits.
A hyphen can be used in the middle to show a range of characters to look for.

[a-z] means any alphabetic characters in this range 
[^xyz] is a negated or complimented class. This means it matches anything that is not enclosed in the square brackets.
So, [^<] means any character except '<'
And, [^<]+ means any character except '<' 1 or more times.

\s is a Character Class Escape that matches a single whitespace

### The OR Operator

 /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1> <span style="background-color: purple"> | </span> \s+\/>)$/ 
 
Disjunction | shows alternatives separated by a pipe. 
\/\1>|\s+\/ means match either \/\1> OR \s+\/

## Wildcard
. is a wildcard that matches all characters except line terminators
So, .* means wildcard 0 or more times

### Character Escapes
\ means that a character should be treated specially; if special, it is treated as literal and if literal, it is  treated as special.
\/ means a literal /

## Back reference 
A backreference refers to the submatch of a previous capturing group and matches the same text as that group. Capturing groups count by 1 so the first capturing group in the regex will be 1. 
So, \1 refers to ([a-z]+)

## Putting it all back together
After decomposing the regex for HTML Tags, we can now build the pieces and read through the components to make sense of it. 
    /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/

/ Read the follow as a regex
^ Start here
< Arrow bracket
([a-z]+) 1 or more lowercase alphabetic characters in the range a-z

([^<]+)* 1 or more characters including whitespaces EXCEPT '<', 0 or more times

(?: match the pattern inside the brackets but don't remember it, as we won't reference it
> Arrow bracket

(.*) Any character (not line terminators) 0 or more times
< Arrow bracket
\/ Literal forward slash
\1 Repeats the exact text captured by the first capturing group
>
| OR

\s+ single white space 1 or more times
\/ Literal forward slash
> Arrow bracket
) End of the captured group to match, but not remember
$ Finish reading here
/ That is the end of the regex

I hope this has helped you make sense of regex!

## Author

This author enjoys learning new languages and regex was no exception! See more about the author and her work at https://github.com/AmyLloyd.

## References

Mozilla(n.d.) "mdn web docs_" https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Regular_expressions/Character_class_escape <br>
Asay, Gavin(2023) https://gist.github.com/gavin-asay/6cd089ca72b9810957254ec6a0cfced7


