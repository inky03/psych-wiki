# Psych Engine Lua API - Compatibility

> [!IMPORTANT]
> Use of outdated versions of the engine, specially if you're only creating softcoded mods, is discouraged.

## pre-0.7.x -> 0.7.x

### Class Reorganization

> [!TIP]
> You should be able to see all packages in the [source code](https://github.com/ShadowMario/FNF-PsychEngine/tree/main/source).

As of 0.7.x, all of the classes in the source code have been reorganized and put in packages/folders (except Main)!

### Conversions
- Classes are now organized in packages/folders, as aforementioned. Change the first argument from `setPropertyFromClass` have the package name followed by a dot, preceding the actual class name (ex. `ClientPrefs` -> `backend.ClientPrefs`)
  - This mostly only applies to classes in the engine's source code!
  - In the case of ClientPrefs, add `data.` preceding the property name (the second argument).<br>
Example:
```lua
-- pre-0.7.x
setPropertyFromClass('GameOverSubstate', 'characterName', 'bf-dead')
getPropertyFromClass('ClientPrefs', 'showFPS')
-- 0.7.x
setPropertyFromClass('substates.GameOverSubstate', 'characterName', 'bf-dead')
getPropertyFromClass('backend.ClientPrefs', 'data.showFPS')
```

- The healthbar and timebar use a new class (`objects.Bar`)! `healthBarBG` and `timeBarBG` no longer in use.
  Each side of the bar is now accessed with `Bar.leftBar` and `Bar.rightBar`.<br>
  You can just set the `Bar` instead of `BarBG` to change the property for the whole bar, and `Bar.bg` to change the property for the bar background.<br>
Example:
```lua
-- pre-0.7.x
setProperty('healthBarBG.scale.x', .75)
setProperty('healthBar.scale.x', .75)
-- 0.7.x
setProperty('healthBar.scale.x', .75) -- you can unify the BG and bar properties now by just changing healthBar!
```

- Notes use a RGB system instead of HSB now! (to be expanded)

## 0.7.x -> 0.6.1+

> [!CAUTION]
> As 0.6.1 is the first update to allow running HScript code, none of these functions can be run in versions prior to it.<br>There's no available workarounds.

### Conversions
- `callMethod(method, {argument1, argument2})` can be replaced by `runHaxeCode('game.method(argument1, argument2);')`.<br>
Example:
```lua
callMethod('moveCamera', {false}) -- 0.7.x
-- would change to...
runHaxeCode('game.moveCamera(false);') --dont forget the semicolon at the end of the function call!
```

- `callMethodFromClass(class, method, {argument1, argument2})` can be replaced by `runHaxeCode('class.method(argument1, argument2);')`. <br>Remember to use `addHaxeLibrary('class', 'package')` to import the class first (where 'package' is everything before the last period, and 'class' is everything after)<br>
Example:
```lua
callMethodFromClass('flixel.util.FlxStringUtil', 'formatTime', {25}) -- 0.7.x
-- would change to...
addHaxeLibrary('FlxStringUtil', 'flixel.util')
runHaxeCode('return FlxStringUtil.formatTime(25);') -- we put "return" because the function returns a value we can use here!
```

- `instanceArg(instance)` can be replaced by just the `instance` value, with `game.` beforehand.<br>
In case of Lua sprites, try using `game.getLuaObject('instance')`.<br>
Example:
```lua
callMethod('goodNoteHit', {instanceArg('notes.members[' .. i .. ']')}) -- 0.7.x
-- would change to...
runHaxeCode('game.goodNoteHit(game.notes.members[' .. i .. ']);'); -- pre-0.7.x
```

(shoutouts to LarryFrosty and ghostglowdev)