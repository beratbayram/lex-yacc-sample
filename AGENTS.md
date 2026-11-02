# AGENTS.md

This file provides guidance to coding agents when working with code in this repository.

A toy-language interpreter built with lex and yacc (2019 course project). Source is two files in
`Source Code/` (folder name has a space). No tests beyond the sample programs. Archived on GitHub.

## Build and run

```bash
cd "Source Code"
yacc -d scanner.y && lex scanner.l && gcc lex.yy.c y.tab.c -o interpreter
./interpreter < ../test1.txt
```

Generated files (`y.tab.c`, `y.tab.h`, `lex.yy.c`, `a.out`) are not committed; keep it that way.
The root `interpreter` file is a prebuilt Linux x86-64 binary.

## Code

- `scanner.l`: tokens. Keywords `int`, `str`, `if`, `while`, `else`, `output`, `outputc`,
  `input`, `inputc`, `exit`; identifiers `[a-zA-Z][a-zA-Z0-9_]*`; strings are double-quoted and
  only allow letters, digits and spaces. `//` comments are returned as a `COMMENT` token and
  handled in the grammar.
- `scanner.y`: grammar and semantic actions, evaluated during parsing (no AST). Variables live in
  `mem[100]` with `findIdent`, `saveInt`, `saveStr`, `modifyInt`, `modifyStr`,
  `getIntValue`, `getStrValue`. `main` reads stdin via `yyparse()`; `yyerror` prints the line
  and exits with status 1.
- `IF` and `WHILE` rules have empty actions and `condt` has no value, so blocks always execute
  exactly once. Real control flow would need an AST or deferred execution.

## Docs

`Diagrams/` (BNF PNGs and a parse tree) and `documentation.docx` describe the grammar. If the
grammar changes, note that they are out of date rather than editing the images.
