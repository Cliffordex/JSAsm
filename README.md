# JSAsm
Javascript in-browser assembler

This was a project I used to teach myself how to use JQuery. I have since eliminated the requirement for the JQuery library, but left the old code in 'jqcmp_oldjquery.html' and 'jqtest_oldjquery.html'. 

## Hello World example
To run the example:
1. Copy the jsCompiler.html and jsAssembler.html to an executable location.
1. Open jsCompiler.html in browser and click `compile`.
1. Open jsAssembler.html in browser and click `run` in the top left.
1. Enjoy watching the stack and base pointers! :D

## Notes

The jsAssembler will contain information on each available opcode. -TODO

Numbers are considered binary unless prepended with "d" for decimal.

# jsCompiler
Javascript compiler, stores output in localStorage, which is automatically loaded by the interpreter.

## Commands

### `~`
Literal command.
Anything prepended with `~` will be output inline, only variable names will be replaced.

### `macro`
The `macro` command tells the compiler what to replace, and has several special options for matching structures and replacing.

### Macro structure types
* `unk` : Argument does not match any known types.
* `"<literal>"` : Argument must match exactly.
* `num` : Argument is a number.
* `mem` : Argument corresponds to a memory location. (either named or literal)
* `nummem` : Argument is either a number or memory location.
* `lab` : Argument is a program label

### Macro Commands

#### `%n%`
Replaces literally with the zero-based nth argument.

Example: `macro mem-"="-nummem { "mov %0% %2%" }`

#### `def` : def [name] [value]
Defines a string as something, then replaces all instances of it.

Example: 
```
macro "define"-unk-num { def %1% %2% }
define pi 3.14
```

#### `?def` | `?!def`
Only executes code block if compiler has defined a term. (or has not defined a term, in the case of `?!def`)

Example:
```
// In this example, the macro uses ?!def to check if ckeys has already appeared in the program.
macro "ckeys" {?!def CKEYS {"or int 10000000", def CKEYS 1} }
```

#### `eachchr` | `reachchr` : eachchr [value] [code block]
Iterates through characters, running the code block once per char.
`reachchr` does the same in reverse order.

Inside the block, `%0%` will represent the character.

Example:
```
macro "pushstr"-unk { "push d0", reachchr %1% { "push CHAR_%0%" } }
```


# jsAssembler
Assembler interpreter, loads from localStorage.