

---

# Alternation

The vertical bar | matches either the characters that precede it or the characters that follow it. For example, specifying however|but matches either word. You can group the alternative terms within parentheses and then refine the search as explained in the next section.



---

# Anchors_and_Word_Boundaries

The following characters match a position in the string or paragraph instead of one or more characters:

- • Placing the circumflex ^ before the search characters matches characters occurring at the beginning of a string or paragraph. For example, /^Java/ matches strings that begin with “Java” but not ones that contain “Java” after the first character.

- • Placing the dollar sign $ after the search characters matches characters occurring at the end of a string or paragraph. For example, /y$/ matches anything that ends in “y”, and /9$/ matches anything that ends in “9”.

- • The combination \b matches a word boundary. For example, specifying /\bJava\b/ finds the standalone word “Java” but not “JavaScript”.

Because line breaks are not normally relevant or maintained when editing XML document content, the ^ and $ anchor characters in a regular expression match paragraph instead of line boundaries when matching document content (for example, when using the find command). Paragraph elements are defined in the document type configuration file ( .dcf ) for the document type.



---

# Character_Classes

A character class is a regular expression constructed of characters enclosed in square brackets [] that matches any one character contained within it. For example, [aeiou] matches any one of the vowels listed between the brackets. Most special characters lose their special meanings within character classes. For example, find /[.,]/ -e would search for a literal period, a comma, or a space. To match a ] character in a character class, place it as the first character inside the square brackets.

Some special characters used in other regular expression implementations are not supported: \d , \D , \w , \W , \s , and \S . Instead of these, you can use character classes such as [0-9] , [^0-9] , [a-zA-Z0–9_] , [^a-zA-Z0–9_] , and so on.



---

# Grouping

You can use parentheses ( ) to group search criteria, such as s(a|e)t . The alternate specification (a|e) is a grouped term, producing matches for “sat” and “set”.

You can group an expression into a unit within a larger expression and then apply one of the repetition characters to the group, such as ? , + , * , or the alternation character | . For example, /java(script)?/ matches “java” as well as “javascript”. The regular expression "(0|1)+" matches a string of one or more 0 characters or one or more 1 characters.

For the replacement string to the substitute command or the sub or gsub functions, the \ n combination can be specified to reference a specific group within parentheses in the matched result. The n represents the group number by counting groups from left to right. For example, substitute '(John)(Smith)'\2,\1' -e reverses the two groups as Smith, John .

The combination \0 represents the entire matched result. For example:

```
substitute -e -nom 'tag'<\0>'
```

would surround the next occurrence of “tag” with angle brackets. The -nom option prevents the angle brackets in the replacement string from being interpreted as markup.

The \ n combination can not be used in the regular expression itself.



---

# Negation

The circumflex character ^ , when used as the first character of a character class, searches for any matches other than the specification that follows it; that is, it matches any character not in the set. For example, the command find /[^.,]/ -e would match the next occurrence of any character other than a period, comma, or space.



---

# Ranges

The hyphen ( - ) specifies a range when it appears as part of a character class. Use a hyphen to separate the first and last character of a range, such as [a-z] or [0–9] . For example, the command substitute /[0–9]/#/ -e replaces the next occurrence of any digit from 0 through 9 with the pound or hash sign ( # ).

To specify multiple digits, you would need to enter a numeric specification for each digit, such as [0–9][0-9][0-9] to find any three digit number. The command find /1[0–9][0–9]\.5/ -e would find numbers such as “123.5” and “154.5” but it would not match the string “1ab.5”.

To match a literal - as part of a character class, include it as the first or last character, for example, find -e /[-0-9]/ would match a digit or negative sign.



---

# Repetition

Search expressions can be expanded using the repetition characters ? , + and * . These characters can appear after the specification to extend its match. A repetition character cannot appear as the first character of a regular expression.

- • ?

- • +

- • *

The repetition characters can also be applied to groups as explained in the following sections.



---

# Searching_for_Tags_or_Entities

The find , set , caret , and window commands include options that scan markup. To search for markup, you must enable markup scanning either by specifying the -m option for the command, or by entering set markupscan = on on the command line.

Arbortext Editor can recognize a start tag as < element-name > , an end tag as </ element-name > , or an entity reference as & entity-name ; . For example, the command find -m '</para>' would search for the next end paragraph tag, and find -m '&prodname;' would search for the next reference to the text entity named prodname .

Regular expressions can be used in the tag or entity name if you specify either the -e option as part of the command or if set expressions=on option is in effect. For example, you could use the command find -m -e '</.*>' to search for the next occurrence of any end tag.

To search for missing punctuation before certain end tags you could use:

```
find -e -t '[^.?!]</(para|item)>'
```

## Related Topics

- • find command

- • substitute command

- • Searching for patterns



---

# Special_Characters

Most characters in regular expressions, such as alphanumeric characters, match the literal characters. For example, the find -e /search/ command matches any occurrence containing “search”, such as “searching”, “searched”, and “research”. Special characters allow a regular expression to match more than one string. For example, a period ( . ) matches any single character. The command find /s.t/ -e finds “sat”, “set”, “sit” and any other three characters beginning with “s” and ending in “t”.

Other special characters include ^ , $ , ? , + , * , | , [] , and ( ) . These characters are discussed in the following sections.

Special characters can be preceded by a back slash ( \ ) when you do not want them to be interpreted as special. For example, to interpret the period literally, place it after a \ . For example, to search your document for numbers between 100 and 199 ending in “.5”, you would issue the command find /1..\.5/ -e . The first two periods act as wildcards for any character, but the third period following the backslash is interpreted as a literal period. This command would also match strings with letters in them, such as 1ab.5 .