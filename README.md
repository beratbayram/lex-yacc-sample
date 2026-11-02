# Lex & Yacc Sample

A small interpreter for a toy language, written with lex and yacc for a programming languages course in 2019. It reads a program from standard input and runs each statement as soon as it is parsed.

## The language

```c
// comments start with two slashes
int x;
int y = 5;
x = 2;
output x + y * 3;      // prints 17

str s = "ali";
outputc s;             // prints ali

input x;               // reads an integer
inputc s;              // reads a word

exit;
```

- Two types: `int` and `str`. Up to 100 variables, kept in a fixed table.
- Integer arithmetic with `+ - * / %` and the usual precedence.
- `output` prints an integer expression, `outputc` prints a string literal or `str` variable; `input` and `inputc` read into a variable.
- Every statement ends with `;`.
- `if` and `while` with comparisons (`< > == != <= >=`) and `{ }` blocks are parsed, but the interpreter does not evaluate the condition: the block's statements always run once.

The grammar is documented as BNF diagrams in `Diagrams/`, with a parse tree example, and the full write-up is in `documentation.docx`.

## Building and running

Needs `yacc` (or `bison -y`), `lex` (or `flex`) and a C compiler.

```bash
cd "Source Code"
yacc -d scanner.y && lex scanner.l && gcc lex.yy.c y.tab.c -o interpreter
./interpreter < ../test2.txt
```

`test1.txt` and `test2.txt` are sample programs. The committed `interpreter` binary at the root is a Linux x86-64 build.

## License

MIT
