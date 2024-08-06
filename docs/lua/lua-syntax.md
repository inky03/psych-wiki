# Lua Syntax

> [!IMPORTANT]
> Lua Scripts in Psych Engine......i forgot what i was going to type here...and i still havent remembered...

> [!NOTE]
> LuaJIT, used in Psych Engine, only supports up to Lua version **5.1**.

## Comments

```lua
local useless = 'code' -- you can add comments by adding two dashes before text!
--[[
	you can use brackets to add multi-line comments.
	yay!
]]
--[=[
	this is a multi line comment with [[ nested ]] brackets.
	you can add more = equal signs at the middle of start and end brackets to nest more levels!
	the same syntax is used for multi-line nested strings which you will see below, without the dashes.
]=]
```

## Variables

Variables hold values or data, and can be accessed and have their data reassigned (hence the name **variables**).
```lua
local someNumber = 0 -- this declares a local variable with the name of "someNumber", with a value of 0
local someVariable -- this declares a local variable with the name of "someVariable", without a declared value
local varA, varB, varC = 2, false -- declares two local vars with the name of "varA" and "varB" with a value of 2 and false, respectively. As "varC" is missing a value assignment, it will have a value of nil.
someGlobal = true -- this assigns the value of true to a GLOBAL variable with the name of "someGlobal"

someVariable = 32 -- assigns the previously declared local variable "someVariable" a value of 32
```

### Local Variables
> [!TIP]
> Prefer using *local* variables over *global* whenever possible, as local variables are faster to access and avoid clutter.

Local variables are kinds of variables which have their scope limited to the block they're declared on. This may be the body of a function or a chunk, which refers to the whole code run by the script.<br>
These variables must be declared with the keyword `local`, preceding the variable name.
```lua
local var = 10 -- declares a variable local to the chunk

function something() -- this function is pretty useless, by the way
	local varB = 5 -- declares a variable local to the function
	return varB
end

debugPrint(something()) -- prints 5, as the function returns the value of "varB" inside the function
debugPrint(var) -- prints 10, as this function is part of the chunk "var" was declared in
debugPrint(varB) -- will fail, as varB was declared LOCAL to the function body
```

### Global Variables
> [!WARNING]
> All variables are considered *global* unless they're explicitly declared as *local*.

Global variables are variables which can be referenced anywhere throughout the code.<br>
These variables do not need to be declarated, and you can just assign a value to create a global variable.
```lua
var = 10 -- assigns the value 10 to a global variable with the name "var"
debugPrint(var) -- prints 10
```

## Data Types

Lua is dynamically typed, so variables don't have data types, but values do!<br>
There are 8 data types in Lua, but we will only work with 6 for the time being:

### `nil`
It's main purpose is to represent the lack of an useful value. This is similar to `undefined` or `null` in other programming languages.

### Number
Represents a real (floating point) number. This data type may be used with [arithmetic operators](#arithmetic-operators).<br>
Really big / small numbers may also be represented with **hexadecimal** (ex. `0xff0000`) or **scientific** notation.

### Boolean
Mainly used for condition checking, this data type only admits `true` and `false` values to represent truth values.

### String
This data type is used to represent readable text.

You can define string values by enclosing text between single/double quotes like 'this' or "this".<br>
You can define multi-line string values by enclosing text between brackets like \[\[this\]\] (which can also be nested!)
**Escape characters** are special characters that allow you to insert "illegal" characters inside a string, which can be done by putting a **back slash** `\`, followed after the character you want to escape.
```lua
local stringA = 'im a string!'
local stringB = "im also a string!"
local stringC = [[ -- allows multiline strings
	im also a string!
	isn't that great?
]]
local stringD = [=[ -- allows multiline strings with nesting brackets
	im [[also]] also a string!
	[[yay]]!
]=]
local stringE = "cool \"quotes\"" --> cool "quotes"  (escape characters example)
```

### Function
This data type represents methods which can be called and may have a return value.
```lua
local function addition(A, B) -- declares a local function with two arguments: A and B
	return A + B -- returns the sum of A and B
end
debugPrint(addition(3, 6)) -- calls the "addition" function with the arguments 3 and 6. Prints 9
```

### Table
Tables are the only type of data structure in Lua, but are powerful and can be used to represent arrays or dictionaries.

Array tables:
```lua
local arrayTable = {'apple', 'orange', 4, false, 'banana', {'hello', 'world'}} -- tables can hold different data types, including other tables!
--[[
	Array tables can be accessed with table[index]; the index starts at 1, which is the first element in the array.
	Do note arrays have numbered indexes, and as such the "index" must be a number.
]]
debugPrint(arrayTable[2]) -- prints the second element in the table; "orange".
```
Dictionary/object tables:
```lua
local dictTable = {
	banana = 1, -- dictionary entries can be defined like this...
	['apple'] = 2, -- or like this!
	[8] = true, -- dictionary entries can also be defined using types other than strings.
	foo = { -- you can also put dictionaries inside of dictionaries!
		bar = 'baz'
	}
}
-- Dictionary tables may be accessed like table.entry, or table[entry] (where "entry" may be of any data type as well)
debugPrint(dictTable.banana) -- prints 1, as this is the definition of the "banana" entry.
debugPrint(dictTable['banana']) -- prints 1; ditto, just different syntax!
debugPrint(dictTable['apple']) -- prints 2, the definition of the "apple" entry.
debugPrint(dictTable.foo.bar) -- prints "baz"; this is the value of "bar" from the entry "foo".
debugPrint(dictTable['what']) -- prints nil, as this value is not an entry in the table.
debugPrint(dictTable[8]) -- prints true.
debugPrint(dictTable.8) --this will fail, as you cant use just numbers with identifiers!
```

**ADVANCED**: [Metatables]() can be used to give tables useful, special behaviors!

## Operators

### Arithmetic Operators
Arithmetic operators are used perform operations on [number type](#number) values.
| Operator | Behavior | Example |
| :------: | -------- | ------- |
| +        | **Addition**: Adds two numbers. | `5 + 2` -> `7` |
| -        | **Subtraction**: Subtracts two numbers. | `5 - 2` -> `3` |
| *        | **Multiplication**: Multiplies two numbers. | `5 * 2` -> `10` |
| /        | **Division**: Divides two numbers. | `5 / 2` -> `2.5` |
| %        | **Modulus**: It's result is the remainder of the division of two numbers. | `5 % 2` -> `1` |
| ^        | **Exponentiation**: Performs exponentiation on two numbers:<br>Raises number A to the power of number B. | `5 ^ 2` -> `25` |

**ADVANCED**: You can also give tables custom behaviors on arithmetic operators with [metatables]()!

### Concatenation
> [!WARNING]
> Concatenating values with data types other than [string](#string) and [number](#number) will fail!<br>
> If you want to concatenate boolean, nil, etc. data types, use `tostring(value)`.

You can use `..` to concatenate two or more values together.
- `'hello_' .. 'world'` returns `hello_world`
- `'i have ' .. 2 .. ' apples'` returns `i have 2 apples`[^1]

### Binary Operators
> [!IMPORTANT]
> Due to the way binary operators work in Lua, they may **not** return a boolean value.<br>
> For the sake of simplicity, we only work with boolean inputs here.

Logical operators perform logical operations with [boolean types]().<br>
These keywords are reserved for Lua and may not be used as variable names or identifiers.
| Operator | Behavior | Example |
| :------: | -------- | ------- |
| and      | Returns `true` if both operands A and B are `true`; if either A or B is `false`, returns `false`. | `A and B` |
| or       | Returns `true` if either operand A or B is `true`; if both A and B are `false`, returns `false`. | `A or B` |
| not      | Negates an expression:<br>Returns `false` if the expression is `true`, and viceversa. | `not (A and B)` negates the AND expression. |

### Relational Operators
> [!WARNING]
> Always do `a ~= b` instead of `not a == b` for inequality!! Lua interprets the latter as `(not a) == b`, which very often causes unexpected results.

> [!IMPORTANT]
> Be careful when comparing values of different types! Strings act different to numbers, and so on.

Relational operators compare two values and always return either `true` or `false`.
| Operator | Behavior | Example |
| :------: | -------- | ------- |
| ==       | **Equality**: returns `true` if two values are equal, or `false` otherwise | `2 == 3` -> `false`
| ~=       | **Inequality**: returns `true` if two values are inequal / different, or `false` otherwise | `2 ~= 3` -> `true`
| <        | **Lower than**: returns `true` if the first operand is lower than the second, or `false` otherwise | `2 < 3` -> `true`
| >        | **Greater than**: returns `true` if the first operand is greater than the second, or `false` otherwise | `2 > 3` -> `false`
| <=       | **Equal or lower than**: returns `true` if the first operand is equal or lower than the second, or `false` otherwise | `3.01 <= 3` -> `false`
| >=       | **Equal or greater than**: returns `true` if the first operand is equal or greater than the second, or `false` otherwise | `2.99 >= 3` -> `false`

> [!WARNING]
> Lua does not support assignment operators like +=, -=, \*=, etc. as is the case in other languages!

### Ternary Conditional Operator
> [!IMPORTANT]
> While this operator is really useful to write short code, avoid nesting them as this can hinder the readability of your code.<br>
> (ex. `ConditionA and expressionA or (ConditionB and expressionB or expressionC)` -> notice how it becomes much harder to follow)

In other programming languages, the ternary[^2] conditional operator is a conditional expression.<br>
The ternary conditional operator has the following syntax in C:
```c
Condition ? expressionA : expressionB
```
If `Condition` is `true`, then `expressionA`, else `expressionB`.<br>
You may have noticed this is identical to an if-else statement! This operator is really useful as it's much shorter to write than an if-else, while keeping it concise.

Let's see an if-else statement in Lua:
```lua
if Condition then
	--expressionA
else
	--expressionB
end
```
We can *partially* replicate the ternary conditional operator in Lua with the following syntax:<br>
```lua
Condition and A or B
```
> [!WARNING]
> Expression **A** should not be `false` or **nil**; this causes unexpected results.

# Extra Resources

[Basics of Coding in Meme1079's Unofficial Psych Wiki](https://github.com/Meme1079/PsychWiki/wiki/Lua-Coding-Docs:-Basics-of-Coding)


[^1]: by the way, i don't actually have 2 apples.
[^2]: **Ternary**: consisting of three parts (From the [Cambridge English Corpus](https://dictionary.cambridge.org/dictionary/english/ternary)). This refers to the three operands of the operator; the condition and the two expressions.