# Introduction

## What is HScript?

**HScript** is short for **Haxe Script** and is essentially a parser and interpreter for **Haxe** code, the programming language Friday Night Funkin' uses.<br>
If you're modding source code, HScript is specially useful for prototyping code, and porting code over is almost as simple as a drag-and-drop.<br>
HScript code is also relatively faster and easier to type with the right amount of knowledge; both HScript and Lua have advantages and disadvantages to their usage, however.

As of **0.7.3**, the library Psych Engine uses for HScript is called **SScript**, which has since been discontinued.

## Similarities to Lua scripts

While Haxe syntax is almost entirely different from Lua, they do have their similarities within the mods system from Psych Engine:
- HScript scripts can run in the same [locations and folders](../lua/introduction.md) Lua scripts do by default.
- HScript scripts have the same [callbacks]() as Lua scripts; however, they do not have the same functions.