## gomacro - A Go interpreter with Lisp-like macros

The package `compiler` contains a faster reimplementation of gomacro core interpreter.

To learn about gomacro, download, compile and use it, please refer to the original implementation [README.md](../README.md)

If you want to help with the reimplementation, or you are simply curious, read on :)

## Current Status

ALPHA.

The fast intepreter supports:
* parsing - because it is shared with the original code
* quote and quasiquote - because they are shared with the original code
* binary expressions on bools, integers, floats, complex numbers, and strings
* constant, variable and type declarations
* incomplete: if and for, except for-range

Everything else is still missing. You are welcome to contribute.

Limitations:
* no distinction between named and unnamed types created by interpreted code.
  For the interpreter, `struct { A, B int }` and `type Pair struct { A, B int }`
  are exactly the same type. This has subtle consequences, including the risk
  that two different packages define the same type and overwrite each other's methods.

  The reason for such limitation is simple: the interpreter uses `reflect.StructOf()`
  to define new types, which can only create unnamed types.
  The interpreter then defines named types as aliases for the underlying unnamed types.