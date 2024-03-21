# Yara-Rule-for-Dark-Comet-Strain
**Introduction**

Since I want to learn reverse engineering, a friend recommended I learn how to use YARA. 
YARA is  known to be the pattern matching swiss army knife created by VirusTotal. In essence it is a rule enginer that supports a human readable language. It's main objective is detection, but its subobjectives can be used for identification, classification, hunting, or triaging. In a comparative sense, YARA is grep on steroids. 


**Rule Syntax**

<img width="564" alt="Screenshot 2024-03-21 at 15 44 42" src="https://github.com/CaptainIndy/Yara-Rule-for-Dark-Comet-Strain/assets/142528700/dc7a0c20-01bb-49b7-873f-9e9abbb26355">

In the following example above, there is an example rule showing rule syntax. Every rule starts with a rule name enclosed by a pair of curly brackets. Inside you have three different sections:
- meta: your description section where you would put the following:
    - your name as the author
    - the description of the rule
    - a hash so that others can validate your work
    - a date since it is important to know how old a YARA rule is.
- strings: the section  where the rule engine is going to search for the strings we specify and want to match upon.
  Types of strings
    - Ascii strings
    - Wide unicode strings specified by the "wide" variable
    - Regex (which start with a forward slash and end with a forward slash) contains regular expression pattern that that defines the string to match
    - hex or bytes: enclosed by curles braces and consist of hexadecimal values representing bytes of the string
- Condition: the section that specifies the Boolean expression that determines whether the rule should be considered a match. This section allows you to combine the strings from the "strings" section using logical operators to create a complex criteria. In this section we use various logical operators to create complex conditions.
  - Some common operators include:
      - and: Both operands must be true for the condition to be true.
      - or: At least one of the operands must be true for the condition to be true.
      - not: Negates the result of the operand.
      - all of: synonym for 'and'
      - any of: synonym for 'or'
      - for all: Quantifier that specifies that a condition must be true for all elements in a set.
