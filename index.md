[Scale](https://github.com/StonkDragon/Scale) is a [procedual](https://en.wikipedia.org/wiki/Procedural_programming) and [object oriented](https://en.wikipedia.org/wiki/Object-oriented_programming) [concatenative](https://en.wikipedia.org/wiki/Concatenative_programming) [stack oriented](https://en.wikipedia.org/wiki/Stack-oriented_programming) [compiled](https://en.wikipedia.org/wiki/Compiler) programming language inspired by [Lua](https://www.lua.org/) and [Porth](https://gitlab.com/tsoding/porth).

Scale and [C](https://en.wikipedia.org/wiki/C_(programming_language)) can interoperate using a header file named `scale_support.h`, which will be generated when compiling a scale file with the `-t` option. If you have any scale functions marked with the `export` modifier, C-declarations for those functions will appear in the file. Functions marked with the `expect` keyword are expected to be implemented in a different translation unit, i.e. your C-code.

The Compiler is a [source-to-source compiler](https://en.wikipedia.org/wiki/Source-to-source_compiler), as it converts your source code to valid C code, that is then compiled by [Clang](https://en.wikipedia.org/wiki/Clang).

Language features can be found [here](./features.md).
