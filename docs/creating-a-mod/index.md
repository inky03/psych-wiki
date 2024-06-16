# Creating a mod

> [!IMPORTANT]
> Please note this guide will be primarily focusing on the **latest version of Psych Engine** (as of writing this the latest version is **0.7.3**!!), and will only be covering the creation of **softcoded mods**. If you wanna make a mod with source code, please refer to the [build instructions](https://github.com/ShadowMario/FNF-PsychEngine/blob/main/BUILDING.md) for the engine.

> [!WARNING]
> While softcoded mods are the easiest to create, please keep in mind they're only limited to **songs**!! This means you can't edit menus or other states outside of the play state purely with softcoding.

Start by getting a clean version of Psych Engine in [GameBanana](https://gamebanana.com/mods/309789) or the [Releases tab on Github](https://github.com/ShadowMario/FNF-PsychEngine/releases).<br>
When you've downloaded the engine, in the same directory for the executable you will be able to see a folder named **mods**; this folder is where you will be able to install or create mods.
To create a new mod, create a new folder inside your **mods** folder.

## File structure
> [!TIP]
> Also check **modTemplate.zip** inside your mods folder! Inside you will also find the file structure your mod may require.<br>
The structure of a mod folder is as follows:
- Mod Name
  - characters
  - custom_events
  - custom_notetypes
  - data
    - `options.json`
  - images
  - music
  - scripts
  - shaders
  - songs
  - stages
  - videos
  - weeks
  - `pack.json`
  - `pack.png`