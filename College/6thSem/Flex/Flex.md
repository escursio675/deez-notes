#college
# Flex file boilerplate
```
%{
/* C declarations */
%}

%%
/* Rules section: pattern → action */
%%

/* User code */
```
For example:
```%%
[0-9]+     { printf("NUMBER\n"); }
[a-zA-Z]+  { printf("WORD\n"); }
\n         { /* ignore */ }
%%
```

==When input ends, `yylex()` calls `yywrap()`. If it's not defined, you get a **linker error** like 'undefined reference to yywrap'==

## Breakdown of Components
1. The part `%{ ... %}` is called the **Definitions Section** and contains the C code that is copied directly into the .c file. It is used for `#include` s, global variables and function declarations.
2. `yywrap()` is a function that returns an `int` . It returns 1 to stop scanning(the `yylex()`) and 0 if there is more input. It is generally used when reading input from multiple files.
3. The **Rules Section** is included within `%% .. %%` and it maps patterns to actions where pattern is a regex and action is a C statement. Here, `yytext` is a variable provided by flex which is the lexeme matched to the regex in the form of a string.
4. `.` pattern matches any single character.
==The rule prioritises the longest match. If tie → first rule wins.==
5. The last part is the **User Code Section**. Here `yylex()` is the scanner function provided by Flex that reads input, applies rules and executes actions.

# Compiling and Running
```
flex file.l
gcc lex.yy.c -o scanner
./scanner
```
# Common Regex
```
[a-zA-Z_][a-zA-Z0-9_]*   // identifier
[0-9]+                   // integer
[0-9]+\.[0-9]+           // float
[ \t\n]+                 // whitespace
\n                       // newline
\"[^\"]*\"               // string
\/\/.*                   // single-line comment
==|!=|<=|>=|<|>          // relational operators
\+|\-|\*|/               // arithmetic operators
.
```

# Start Conditions
1. Default flex state is INITIAL
2. Use `%x state_name` to define exlusive and `%s state_name` to define inclusive states
3. Use `BEGIN(stat_name)` to define start condition for state
4. Use `<state1, state2,..., staten>...` to define rules for states 1 through n



# Programs
## Practice
## Level 1: Basics (Understanding Flex Mechanics)

These help you understand **patterns and actions**.

### Q1. Simple Token Recognition

Write a Flex program that:

- Identifynumbers (`[0-9]+`)
- Identify words (`[a-zA-Z]+`)
- prints:
    
    NUMBER: 123  
    WORD: hello
    

---

### Q2. Count Lines and Words

Write a scanner that:

- counts:
    - number of lines
    - number of words
- prints totals at the end

👉 Focus: global variables + `\n` handling

---

### Q3. Ignore Whitespaces

Write a scanner that:

- prints all words
- ignores:
    - spaces
    - tabs
    - newlines

👉 Focus: pattern priority and ignoring tokens

---

## 🟡 Level 2: Token Classification

Now move toward **real lexical analysis concepts**.

### Q4. Classify Basic Tokens

Recognize and print:

- Keywords: `int`, `float`, `if`, `else`
- Identifiers
- Numbers

Output example:

KEYWORD: int  
IDENTIFIER: x  
NUMBER: 100

---

### Q5. Operators Recognition

Write a scanner to detect:

- Arithmetic: `+ - * /`
- Relational: `== != < > <= >=`

Print:

OPERATOR: +  
OPERATOR: ==

---

### Q6. Identifier Validation

Write rules to:

- Accept valid identifiers: `abc`, `a1`, `_temp`
- Reject invalid: `1abc`

Print:

VALID: abc  
INVALID: 1abc

👉 This directly prepares you for lexical error detection.

---

## 🟠 Level 3: State & Context Handling

Now you're entering **real Flex power (states + context)**.

### Q7. String Recognition

Recognize strings:

"hello world"

Handle:

- valid strings
- unterminated strings

---

### Q8. Remove Single-Line Comments

Input:

int x; // this is a comment

Output:

int x;

---

### Q9. Remove Multi-Line Comments

Handle:

/* comment */

👉 Hint: Use **start conditions (`%x`)**

---

## 🔴 Level 4: Tracking & Data Structures

Now move toward your actual test questions.

### Q10. Line Number Tracking

Modify any scanner to:

- print line number with each token

---

### Q11. Column Number Tracking

Extend Q10 to:

- track column position

👉 Hint:

- increment column for each character
- reset on newline

---

### Q12. Token Counter

Count:

- identifiers
- numbers
- keywords

Print totals at end.

---

## 🔵 Level 5: Pre-Symbol Table Concepts

Before full symbol table, do this:

### Q13. Unique Identifier List

Store identifiers:

- print them **only once**

👉 Hint:

- use array + `strcmp`

---

### Q14. Frequency of Identifiers

Track:

x → 3 times  
y → 2 times

---

## ⚫ Level 6: Mini Lab-Level Problems

Now you're ready for near-exam problems.

### Q15. Mixed Token Analyzer

Recognize:

- keywords
- identifiers
- numbers
- operators

Print:

TYPE : LEXEME

---

### Q16. Error Detection Lite

Detect:

- invalid identifiers
- unknown symbols

Continue scanning after error.

## Questions
1. Design a lexical analyzer that identifies tokens and prints token type, lexeme, line number, and column number.
2. Design a scanner that builds a symbol table during lexical analysis.
   Symbol Table Fields:
   Identifier name
   Type (if available)
   Line number
   Scope (optional)
   Constraint: No duplicate identifiers allowed
3. Design a scanner that counts frequency of each token type.
   Sample output:
   Identifiers: 12
   Keywords: 5
   Operators: 8
4. Design a scanner that removes comments and outputs a cleaned source file.
   Supported Comments:
   // single-line
   /* multi-line */
5. Extend a scanner to detect and report lexical errors and continue scanning.
   Errors to Detect:
   Invalid identifiers (2abc)
   Unterminated strings
   Illegal symbols (@, #)
   Output Example:
   line 3: Invalid identifier 2abc






