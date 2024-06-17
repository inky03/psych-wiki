# Introduction

## What is Lua?

"Lua is a powerful, efficient, lightweight, embeddable scripting language. It supports procedural programming, object-oriented programming, functional programming, data-driven programming, and data description." (*[Lua: What is Lua?](https://www.lua.org/about.html)*)<br>
As such, this scripting language is widely used in a large number of applications; and such is the case of Psych Engine!

Lua scripts in Psych Engine allow you to run custom code without having to compile the game, which makes the process of modding the game super easy with just the right amount of knowledge!

## Where do I use Lua scripts?

> [!IMPORTANT]
> Lua scripts can be pretty powerful, but they can only run inside **songs**. This means you can't edit menus or states outside of the play state; this must be done by modding the source code.

> [!IMPORTANT]
> Note that while the condition these scripts run in can vary, they behave identically to each other and have the same [callbacks]()!

Different kinds of Lua scripts can run in a mod:

### Global Scripts

**Global scripts** are saved in the `scripts` folder.<br>
This kind of scripts will run inside **every** song in your mod (or ALL songs if the mod is [global]()), regardless of anything.
You can have various global scripts running at the same time, and they can have any name.

### Song Scripts

**Song scripts** are saved in the same folder the song chart is located (which must be inside the `data` folder).<br>
This kind of scripts will only run while playing that song, independently of the stage or the difficulty.<br>
You can have various song scripts in the same folder, and they can have any name.

### Event Scripts

**Event scripts** are saved in the `custom_events` folder.<br>
This kind of scripts will only run if the event is present in the song currently being played.<br>
The name of the script must match that of the name of the event inside the folder.

[Creating a custom event]()

### Note Type Scripts

**Note type scripts** are saved in the `custom_notetypes` folder.<br>
This kind of scripts will only run if the notetype is present in the song currently being played.<br>
Only one script can run per notetype, as the presence of a script in the custom notetypes folder tells the game to add it to the list of notetypes in the [Chart Editor]().

[Creating a custom notetype]()

### Character Scripts

**Character scripts** are saved in the `characters` folder.<br>
This kind of scripts will only run if the character is present in the song currently being played.<br>
The name of the script must match that of the name of your character inside the folder.

### Stage Scripts

**Stage scripts** are saved in the `stages` folder.<br>
This kind of scripts will only run if the current song is set in the stage.<br>
The name of the script must match that of the name of your stage inside the folder.

[Creating a custom stage]()