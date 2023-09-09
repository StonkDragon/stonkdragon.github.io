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

#### Pass-by-Value
By default, structs in scale are passed by reference. This means that when you pass a struct to a function, the function will receive a pointer to the struct, and any changes made to the struct will be reflected in the original struct. If you want to pass a struct by value, you have to put `*` before the type. For example:
```
function increment(p: *Point): Point
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

### Examples
For more detailed examples of the language, see the examples folder at [The Repository](https://github.com/StonkDragon/Scale)
