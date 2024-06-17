# Lua Code Introduction

> [!IMPORTANT]
> Lua Scripts in Psych Engine......i forgot what i was going to type here...

> [!NOTE]
> LuaJIT, used in Psych Engine, only supports up to Lua version **5.1**.

## Variables

Variables hold values or data, and can be accessed and have their data reassigned (hence the name **variables**).
```lua
local someNumber = 0 --this declares a local variable with the name of "someNumber", with a value of 0
local someVariable --this declares a local variable with the name of "someVariable", without a declared value
local varA, varB, varC = 2, false --declares two local vars with the name of "varA" and "varB" with a value of 2 and false, respectively. As "varC" is missing a value assignment, it will have a value of nil.
someGlobal = true --this assigns the value of true to a GLOBAL variable with the name of "someGlobal"

someVariable = 32 --assigns the previously declared local variable "someVariable" a value of 32
```

### Local Variables
> [!TIP]
> Prefer using *local* variables over *global* whenever possbile, as local variables are faster to access and avoid clutter.

Local variables are kinds of variables which have their scope limited to the block they're declared on. This may be the body of a function or a chunk, which refers to the whole code run by the script.<br>
These variables must be declared with the keyword `local`, preceding the variable name.
```lua
local var = 10 --declares a variable local to the chunk

function something() --this function is pretty useless, by the way
	local varB = 5 --declares a variable local to the function
	return varB
end

debugPrint(something()) --prints 5, as the function returns the value of "varB" inside the function
debugPrint(var) --prints 10, as this function is part of the chunk "var" was declared in
debugPrint(varB) --will fail, as varB was declared LOCAL to the function body
```

### Global Variables
> [!WARNING]
> All variables are considered *global* unless they're explicitly declared as *local*.

Global variables are variables which can be referenced anywhere throughout the code.<br>
These variables do not need to be declarated, and you can just assign a value to create a global variable.
```lua
var = 10 --assigns the value 10 to a global variable with the name "var"
debugPrint(var) --prints 10
```

## Data Types

Lua is dynamically typed, so variables don't have data types, but values do.<br>
There are 8 data types in Lua, but we will only work with 6 for the time being:

### Nil
It's main purpose is to represent the lack of an useful value. This is similar to **undefined** or **null** in other languages.

### Number
Represents a real (floating point) number. This data type may be used with [arithmetic operators](#arithmetic-operators).<br>
Really big / small numbers may also be represented with **hexadecimal** (ex. `0xff0000`) or **scientific** notation.

### Boolean
Mainly used for condition checking, this data type only admits **true** and **false** values to represent truth values.

### String
This data type is used to represent readable text.

You can define string values by enclosing text between single/double quotes like 'this' or "this".<br>
You can define multi-line string values by enclosing text between brackets like \[\[this\]\] (which can also be nested!)
**Escape characters** are special characters that allow you to insert "illegal" characters inside a string, which can be done by putting a **back slash** `\`, followed after the character you want to escape.
```lua
local stringA = 'im a string!'
local stringB = "im also a string!"
local stringC = [[ --allows multiline strings
	im also a string!
	isn't that great?
]]
local stringD = [=[ --allows multiline strings with nesting brackets
	im [[also]] also a string!
	[[yay]]!
]=]
local stringE = "cool \"quotes\"" --> cool "quotes"  (escape characters example)
```

### Function
This data type represents methods which can be called and may have a return value.
```lua
local function addition(A, B) --declares a local function with two arguments: A and B
	return A + B --returns the sum of A and B
end
debugPrint(addition(3, 6)) --calls the "addition" function with the arguments 3 and 6. Prints 9
```

### Table
todo...

## Operators

### Arithmetic Operators
Arithmetic operators are used perform operations on [number type](#number) values.
- **+ (addition)**: Adds two numbers.<br>
  (ex. `5 + 2` returns `7`)
- **- (subtraction)**: Subtracts two numbers.<br>
  (ex. `5 - 2` returns `3`)
- **\* (multiplication)**: Multiplies two numbers.<br>
  (ex. `5 * 2` returns `10`)
- **/ (division)**: Divides two numbers.<br>
  (ex. `5 / 2` returns `2.5`)
- **% (modulus)**: Returns the remainder of a division between two numbers.<br>
  (ex. `5 % 2` returns `1`)
- **^ (exponentiation)**: Performs exponentiation on two numbers.<br>
  (ex. `5 ^ 2` > 5 to the power of 2 > returns `25`)

### Concatenation
> [!WARNING]
> The concatenation operator only works with [string](#string) and [number](#number) data types!<br>
> If you want to concatenate boolean, nil, etc. data types, use `tostring(value)`.

**..** is an operator that concatenates values together. Numbers can also be concatenated!<br>
Examples:
- `'hello_' .. 'world'` returns `hello_world`
- `'i have ' .. 2 .. ' apples'` returns `i have 2 apples`[^1]

### Binary Operators
> [!IMPORTANT]
> Due to the way binary operators work in Lua, they may **not** return a boolean value.<br>
> For the sake of simplicity, we only work with boolean inputs here.

Logical operators perform operations with [boolean types]().<br>
These keywords are reserved for Lua and may not be used as variable names or identifiers.
- **and**: Returns **true** if both statements A and B are **true**, or **false** otherwise.<br>
  (ex. `A and B`)
- **or**: Returns **true** if either statement A or B is **true**, or **false** otherwise.<br>
  (ex. `A or B`)
- **not**: Negates an expression, making `false`, `true` instead, and viceversa.<br>
  (ex. `not (A and B)`: this negates the AND operator and will return **false** if A and B are true, or **true** otherwise)

### Relational Operators
> [!WARNING]
> Always do `a ~= b` instead of `not a == b` for inequality!! Lua interprets the latter as `(not a) == b`, which very often causes unexpected results.

> [!NOTE]
> Be careful when comparing values of different types! Strings act different to numbers, and so on.

> [!TIP]
> TODO: put these in a table instead?? i dont know im stupid..

Relational operators compare two values and always return either **true** or **false**.
- **== (equality)**: If two values are equal, this will return **true**, or **false** otherwise.<br>
  (ex. `2 == 3` returns `false`)
- **~= (inequality)**: If two values are inequal (different), this will return **true**, or **false** otherwise.<br>
  (ex. `2 == 3` returns `true`)
- **< (lower)**: If A is lower than B, this will return **true**, or **false** otherwise.<br>
  (ex. `2 < 3` returns `true`, as 2 is lower than 3)
- **> (greater)**: If A is greater/bigger than B, this will return **true**, or **false** otherwise.<br>
  (ex. `2 > 3` returns `false`, as 2 is not greater than 3)
- **<= (equal or lower)**: If A is equal or lower than B, this will return **true**, or **false** otherwise.<br>
  (ex. `3.01 <= 3` returns `false`, as 3.01 is not 3 or lower)
- **>= (equal or higher)**: If B is equal or greater/bigger than B, this will return **true**, or **false** otherwise.<br>
  (ex. `2.99 >= 3` returns `false`, as 2.99 is not 3 or greater)

> [!WARNING]
> Lua does not support assignment operators like +=, -=, \*=, etc. as is the case in other languages!

### Ternary Conditional Operator
In other programming languages, the ternary conditional operator is a conditional expression.<br>
The ternary conditional operator in C, for example, is written as `Condition ? A : B`.<br>
This is very useful as it follows the same rules as an if-else statement, but is also written in a much shorter way.

We can *partially* replicate the ternary conditional operator in Lua with the following syntax:<br>
```lua
Condition and A or B
```
> [!WARNING]
> Expression **A** should not be **false** or **nil**; this may cause unexpected results.

[^1]: by the way, i don't actually have 2 apples :(