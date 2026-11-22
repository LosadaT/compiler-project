# Pascal-like Compiler

Project developed for the Compilers course, implementing a compiler for a Pascal-like language. Built in C, it covers lexical analysis, syntactic analysis, and intermediate code generation in MEPA.

## Features

- Lexical analyzer supporting identifiers, numbers (decimal and exponential notation), comments, and all language operators
- Recursive descent parser (RDP) based on the language grammar
- Hash-based symbol table for managing declared variables
- Intermediate code generation in MEPA
- Lexical, syntactic, and semantic error detection with line numbers

## Project Structure

```
.
├── compilador.c       # Main source code
├── codigo.txt         # Input file (source code to compile)
└── README.md
```

## How to Compile

```bash
gcc -Wall -Wno-unused-result -g -Og compilador.c -o compilador
```

## How to Run

The compiler reads `codigo.txt` by default. Place your Pascal-like source code in that file and run:

```bash
./compilador
```

To change the input file, edit line 138 of `compilador.c`:

```c
FILE *f = fopen("yourfile.txt", "r");
```

The output is the generated MEPA code printed to the terminal, followed by the symbol table at the end of execution.

## Example Input

```pascal
(*
program computes the factorial of a read number
*)
program fatorial;
var
  fat, num, cont : integer;
begin
  read(num);
  fat := 1;
  cont := 2;
  while cont <= num do
  begin
    fat := fat * cont;
    cont := cont + 1
  end;
  write(fat) (*prints the computed factorial*)
end.
```

## Example Output (MEPA)

```
    INPP
    AMEM 3
    LEIT
    ARMZ 1
    CRCT 1
    ARMZ 0
    CRCT 2
    ARMZ 2
L1: NADA
    CRVL 2
    CRVL 1
    CMEG
    DSVF L2
    CRVL 0
    CRVL 2
    MULT
    ARMZ 0
    CRVL 2
    CRCT 1
    SOMA
    ARMZ 2
    DSVS L1
L2: NADA
    CRVL 0
    IMPR
    PARA

TABELA DE SIMBOLOS
Entrada Tabela Simbolos: [...] => fat | Endereco: 0
Entrada Tabela Simbolos: [...] => num | Endereco: 1
Entrada Tabela Simbolos: [...] => cont | Endereco: 2
```

## Supported Language

The grammar is similar to Pascal, supporting:

- Types: `integer`, `boolean`, `char` (`char` is ignored during code generation in this version)
- Statements: assignment, `read`, `write`, `if/then/else`, `while/do`, `begin/end` blocks
- Relational operators: `<`, `<=`, `>`, `>=`, `=`, `<>`
- Logical operators: `or`, `and`, `not`
- Arithmetic operators: `+`, `-`, `*`, `div`
- Comments: `(* ... *)`

## Known Limitations

- The `char` type is recognized by the lexer but ignored during code generation
- Mixed-type expressions (e.g., `25 + (x > y)`) do not trigger a proper semantic error
- Unclosed comments report an `[END]` error instead of pointing to the unclosed comment

## Technologies

- **C**
- **GCC**
- **MEPA** (*Máquina de Execução Para Algoritmos* — Algorithm Execution Machine) — intermediate code language
