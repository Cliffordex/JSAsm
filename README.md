# JSAsm
Javascript in-browser assembler

This was a project I used to teach myself how to use JQuery. I have since eliminated the requirement for the JQuery library, but left the old code in 'jqcmp_oldjquery.html' and 'jqtest_oldjquery.html'. 

## Notes

The jsAssembler will contain information on each available opcode. -TODO

Numbers are considered binary unless prepended with "d" for decimal.

# jsCompiler
Javascript compiler, stores output in localStorage, which is automatically loaded by the interpreter.

## Commands

## `~`
Literal command.
Anything prepended with `~` will be output inline as typed.

## Macros
Macro command `macro` tells the compiler what to replace, and has several special options.

### Macro structure types
* `unk` : Argument does not match any known types.
* `num` : Argument is a number.
* `mem` : Argument corresponds to a memory location. (either named or literal)

#### `%n%`
Replaces literally with the zero-based nth argument.

Example: `macro mem-"="-nummem { "mov %0% %2%" }`


# jsAssembler
Assembler interpreter, loads from localStorage.