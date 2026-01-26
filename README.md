# Bat 🦇

A Simple programming Language written in Go

## Features

- Arithmetic operations (+, -, *, /)
- Variables and assignments
- If statements
- Functions and return values
- REPL (Read-Eval-Print Loop) for interactive coding

## Running the REPL

```bash
go run main.go
````

You should see the REPL prompt:

```bash
>>
```

Type Bat code directly, for example:

```bash
>> let a = 5;
>> let b = 10;
>> a + b;
15
```

## Grammar

Bat follows a simple, C-like syntax. Here's the core grammar:

```ebnf
<program>        ::= <statement>*

<statement>      ::= "let" <identifier> "=" <expression> ";"
                   | "return" <expression> ";"
                   | <expression> ";"

<expression>     ::= <integer>
                   | <boolean>
                   | <identifier>
                   | <expression> <operator> <expression>
                   | "(" <expression> ")"
                   | "if" "(" <expression> ")" "{" <program> "}" ("else" "{" <program> "}")?
                   | "fn" "(" <parameters> ")" "{" <program> "}"
                   | <expression> "(" <arguments> ")"

<parameters>     ::= <identifier> ("," <identifier>)*
                   | ε

<arguments>      ::= <expression> ("," <expression>)*
                   | ε

<operator>       ::= "+" | "-" | "*" | "/" | "==" | "!=" | "<" | ">" 

<identifier>     ::= [a-zA-Z_][a-zA-Z0-9_]*
<integer>        ::= [0-9]+
<boolean>        ::= "true" | "false"
```

```txt
                      _..-'(                       )'-.._
                   ./'. '||\\.       (\_/)       .//|' .'\.
                ./'.|'.'||||\\|..    )O O(    ..|//|||'.'|.'\.
             ./'..|'.|| |||||\'''''' '"'" ''''''/||||| ||'|..'\.
           ./'.||'.|||| ||||||||||||.     .|||||||||||| |||||'||.'\.
          /'|||'.|||||| ||||||||||||{     }|||||||||||| ||||||'|||'\
         '.|||'.||||||| ||||||||||||{     }|||||||||||| |||||||'|||.'
        '.||| ||||||||| |/'   ''\||''     ''||/''   '\| ||||||||| |||.'
        |/' \./'     '\./         \!|\   /|!/         \./'     '\./ '\|
        V    V         V          }' '\ /' '{          V         V    V
        '    '         '               V               '         '    '
```

Ty Thorsten Ball
