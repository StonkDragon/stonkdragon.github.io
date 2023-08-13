
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


For more detailed examples of the language, see the examples folder at [The Repository](https://github.com/StonkDragon/Scale)
