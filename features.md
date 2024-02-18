## Features
### Stack
In Scale, every operation uses the Stack. For example, adding two numbers would look like this:
```
1 2 +
```
This pushes the numbers `1` and `2` onto the stack, and then adds them together, leaving the result `3` on the stack.

### Variables
Variables are declared using the `decl` keyword. For example:
```
decl x: int
```
This declares a variable named `x` of type `int`. Variables can be assigned to using the `=>` operator:
```
1 => x
```
This pops the number `1` off the stack, and assigns it to the variable `x`.
These two operations can be combined into one:
```
1 => decl x: int
```
This pushes the number `1` onto the stack, and then assigns it to a new variable named `x`.

### Functions
Functions are declared using the `function` keyword. For example:
```
function add(a: int, b: int): int
    a b + return
end
```
This declares a function named `add` that takes two `int`s and returns an `int`. The function adds the two arguments together, and returns the result.

Calling a function is as simple as putting the arguments on the stack, and then writing the function name:
```
1 2 add
```

### Control Flow
Scale has a few control flow statements, such as `if`, `while`, and `for`. For example:
```
1 => decl x: int
while x 10 < do
    x 1 + => x
done
```
This declares a variable named `x` and sets it to `1`. Then, while `x` is less than `10`, it adds `1` to `x`.

```
for i in 1 to 10 do
    i puts
done
```
This prints the numbers `1` through `9`. The `for` loop is inclusive of the start, but exclusive of the end.

```
if 1 2 == then
    "1 is equal to 2" puts
else
    "1 is not equal to 2" puts
fi
```
This prints `1 is not equal to 2` (as expected).

### Comments
Line Comments are started with `#` and end at the end of the line.
Block Comments are started with `` ` `` and end with `` ` ``.

### Types
Scale has a few built-in types, such as `int`, `float` and `any`.
`int` is a 64-bit signed integer.
`float` is a 64-bit floating point number.
`any` is a type that can hold any value.

Primitive Arrays are also supported. They are declared by enclosing the type in square brackets. For example:
```
decl x: [int]
```
This declares a variable named `x` as an array of `int`s.

### Strings
Strings are declared like many other languages, with double quotes. For example:
```
"Hello, World!" puts
```
This prints `Hello, World!` to the console.

Strings have a type of `str`, which is the only type that is not directly compatible with C. 
To create a C-compatible string, prefix the string with `c`. For example:
```
c"Hello, World!"
```

### Structs
Structs in Scale are similar to structs in C++. For example:
```
struct Point
    decl x: int
    decl y: int
end
```
This declares a struct named `Point` with two fields, `x` and `y`, both of type `int`.

Structs can be instantiated using the `new` keyword. For example:
```
Point::new => decl p: Point
```
This creates a new `Point` and assigns it to the variable `p`.

Struct members can be accessed using `.`. For example:
```
34 => p.x
```
This assigns `34` to the `x` field of `p`.

Structs can also have methods. For example:
```
struct Point
    decl x: int
    decl y: int

    function add(other: Point): Point
        x other.x + => x
        y other.y + => y
        self return
    end
end
```
This adds a method named `add` to the `Point` struct. The method takes another `Point` as an argument, and adds the `x` and `y` fields of the argument to the `x` and `y` fields of the struct, respectively. It then returns the struct.

Struct methods can be called using `:` on an instance of the struct. For example:
```
Point::new => decl p: Point
Point::new => decl p2: Point
p p2:add => p
```
This creates two new `Point`s, and then calls the `add` method on `p2` with `p` as an argument. It then assigns the result to `p`.

#### Struct Initialization
There are two ways to initialize a struct in Scale. The first is to use the `new` static function. For example:
```
Point::new => decl p: Point
```
This creates a new `Point` and assigns it to the variable `p`.

The second way is to use property initialization. For example:
```
Point {
    1 => x
    2 => y
} => decl p: Point
```
This creates a new `Point` with the `x` field set to `1` and the `y` field set to `2`, and assigns it to the variable `p`.
With property initialization it is necessary to initialize all fields.

#### Custom Property getters and setters
Structs can have custom property getters and setters. For example:
```
struct MyStruct
    decl someString: str
        get()
            "someString: " field + return
        end
        set(value)
            value => field
        end
end
```
This declares a struct named `MyStruct` with a field named `someString`. The field has a custom getter and setter. The getter returns the value of the field with `someString: ` prepended to it. The setter sets the value of the field to the value passed to it.
The getter and setter are called automatically when accessing the field. For example:
```
MyStruct {
    "Hello, World!" => someString
} => decl s: MyStruct

s.someString puts
```
This prints `someString: Hello, World!` to the console.

#### Pass-by-Value
By default, structs in scale are passed by reference. This means that when you pass a struct to a function, the function will receive a pointer to the struct, and any changes made to the struct will be reflected in the original struct. If you want to pass a struct by value, you have to put `@` before the type. For example:
```
function increment(p: @Point): Point
    p.x 1 + => p.x
    p.y 1 + => p.y
    p return
end
```
Any changes made to `p` will not be reflected in the original struct.

### Enums
Enums in Scale are similar to enums in C. For example:
```
enum Color
    Red
    Green
    Blue
end
```
This declares an enum named `Color` with three variants, `Red`, `Green`, and `Blue`.
Each variant corresponds to an integer, starting at `0`. For example:
```
Color::Red => decl c: Color
```
This assigns the variant `Red` to the variable `c`. This is equivalent to:
```
0 => decl c: Color
```

#### Variant Values
Each variant can have a value associated with it. For example:
```
enum Color
    [0xFF0000] Red
    [0x00FF00] Green
    [0x0000FF] Blue
end
```
This assigns the value `0xFF0000` to the `Red` variant, `0x00FF00` to the `Green` variant, and `0x0000FF` to the `Blue` variant.

### Unions
Unions in Scale are similar to unions in C. For example:
```
union IntOrFloat
    asInt: int
    asFloat: float
end
```
This declares a union named `IntOrFloat` with two variants, `asInt` and `asFloat`.
Each variant can hold a different type. For example:
```
1 IntOrFloat::asInt => decl x: IntOrFloat
```
This assigns the variant `asInt` to the variable `x`, and sets the value to `1`.
Unions in Scale are tagged, meaning an error will be thrown if you try to access the wrong variant. For example:
```
x.asFloat
```
This will throw an error, as `x` is currently the `asInt` variant.

### C Interop
Scale can interoperate with existing C code. For example:
```
expect foreign function puts(string: [int8]): int
```
This imports the `puts` function from C. The `expect` keyword tells the compiler that the function will be implemented in a different translation unit and the `foreign` keyword tells the compiler to not mangle the function symbol.

```
export foreign function add(a: int, b: int): int
    a b + return
end
```
This exports the `add` function to C. The `export` keyword tells the compiler to generate a function declaration in `scale_interop.h`. The `foreign` keyword tells the compiler to not mangle the function symbol.
Calling Scale functions from C is as simple as including the `scale_interop.h` header file, and calling the function. For example:
```c
#include <stdio.h>
#include "scale_interop.h"

int main() {
    printf("%d\n", add(1, 2));
    return 0;
}
```
This prints `3` to the console.

### Arrays
Arrays in Scale are similar to arrays in C. For example:
```
decl x: [int]
```
This declares a variable named `x` as an array of `int`s.
This, however, does not allocate any memory for the array. To allocate memory, use the `new` keyword. For example:
```
new<int>[10] => x
```
This allocates enough memory for 10 `int`s, and assigns it to the variable `x`.

Arrays can be indexed using `[]`. For example:
```
x[0] => decl y: int
```
This assigns the first element of `x` to the variable `y`.

#### Map syntax
Scale has a special syntax for creating and modifying arrays. For example:
```
[10 do i fib] => decl fibs: [int]
```
This creates an array of 10 elements, and assigns it to the variable `fibs`. Each element is the result of calling the `fib` function with the index as an argument.

Modifying arrays is also simple. For example:
```
[fibs do val 2 *]
```
This multiplies each element of `fibs` by `2`.

If you just want to loop over the array without modifying it, make sure to not leave any values on the stack. For example:
```
[fibs do val puts]
```
This prints each element of `fibs` to the console.

### Imports
Scale has a simple import system. For example:
```
import <file>
```
This imports the file named `file.scale` relative to the current file.

```
import <dir>.<file>
```
This imports the file named `file.scale` relative to the directory named `dir`.

```
import <module>
```
This imports the module named `module`.

#### Modules
Modules are defined by Scale frameworks. For example the following `index.drg` defines a module named `test`:
```
framework: {
    # ...
    modules: [
        test: [
            "foo.scale";
            "bar.scale";
            "baz.scale";
        ];
    ];
};
```
This defines a module named `test` with the files `foo.scale`, `bar.scale`, and `baz.scale`.
Importing this module will import all of the files in the module.

### Macros
Scale has a simple macro system. For example:
```
macro! MyMacro(str1, str2) {
    $str1 ": " + $str2 +
}
```
This defines a macro named `MyMacro` that takes two arguments, `str1` and `str2`.
For example:
```
MyMacro! "Hello" "World!"
```
This expands to `"Hello" ": " + "World!" +`.

More complex macros can be defined as such:
```
macro! ComplicatedMacro() in "lib"
```
Where `lib` is the name of a dynamic library. The dynamic library must be visible to the compiler.
These function-like macros must be defined like so:
```
foreign function ComplicatedMacro(loc: SourceLocation, parser: Parser): Result
```
Where `loc` is the location of the macro invocation, and `parser` can be used to parse the arguments to the macro.
The return value must be of type `Result`, where the `Ok` variant is `[Token]` and the `Err` variant is `MacroError`.
For example:
```
foreign function ComplicatedMacro(loc: SourceLocation, parser: Parser): Result
    parser:peek => decl token: Token?
    if token nil == then
        MacroError {
            "Expected a token, but got nothing" => msg
            nextTok.location => location
        } Result::Err return
    fi

    new<Token>{
        token!!
    } Result::Ok return
end
```
This macro will expand to the next token in the source file.

### Data Type Literals
A few of Scale's data types have literals. For example:
```
new<int>{1, 2, 3} => decl x: [int]
```
This creates an array of `int`s with the values `1`, `2`, and `3`, and assigns it to the variable `x`.

```
(1, 2) => decl x: Pair
```
This creates a `Pair` with the values `1` and `2`, and assigns it to the variable `x`.
This assumes that the `Pair` struct has been declared.

```
(1, 2, 3) => decl x: Triple
```
This creates a `Triple` with the values `1`, `2`, and `3`, and assigns it to the variable `x`.
This assumes that the `Triple` struct has been declared.

```
(1 to 3) => decl x: Range
```
This creates a `Range` with the values `1` and `3`, and assigns it to the variable `x`.
This assumes that the `Range` struct has been declared.

```
(1 to) => decl x: PartialRange
```
This creates a `PartialRange` with the lower bound `1`, and assigns it to the variable `x`.
This assumes that the `PartialRange` struct has been declared.

```
(to 3) => decl x: PartialRange
```
This creates a `PartialRange` with the upper bound `3`, and assigns it to the variable `x`.
This assumes that the `PartialRange` struct has been declared.

```
(to) => decl x: UnboundRange
```
This creates an `UnboundRange`, and assigns it to the variable `x`.
This assumes that the `UnboundRange` struct has been declared.

### Examples
For more detailed examples of the language, see the examples folder at [The Repository](https://github.com/StonkDragon/Scale)
