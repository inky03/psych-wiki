# Psych Engine Lua API - Global Variables

## Debug variables

These are the only global variables you are able to change the value of!
- `luaDebugMode`: Setting this to `true` will enable ["debug mode"]() on the Lua script.
- `luaDeprecatedWarnings`: Only works when "debug mode" is enabled, and is enabled by default.<br>
When enabled, using [deprecated API callbacks]() will print a warning on screen.

## Return values

> [!NOTE]
> - These return values only work in [API callbacks]() by default.

- `Function_Continue`: Stops the callback this is returned on, and resumes calling in other scripts.<br>
Note you can just use `return` alone to stop the callback, and will behave identically.
- `Function_StopLua`: Stops the returned callback from being called in subsequent Lua scripts.
- `Function_StopHScript`: Stops the returned callback from being called in subsequent [HScript]() scripts.
- `Function_StopAll`: Stops the returned callback from being called in subsequent scripts of any kind.
- `Function_Stop`: Stops the returned callback fron continuing.

Example:
```lua
function onUpdateScore() --this function is called when the score text is updated!
	setTextString('scoreTxt', 'Hello!') --sets the score text to the string "Hello!"
	return Function_Stop -- Returns Function_Stop, which will stop other scripts from running this callback
end
```

> [!IMPORTANT]
> Changes to the values of these global variables below will NOT be reflected in game!
> If you need to change these, use `setProperty`, `setPropertyFromGroup` and/or `setPropertyFromClass`

## Chart / Song variables

- `scrollSpeed`: Returns the chart's initial note scroll speed.
- `songLength`: Returns the length of the chart's song, in milliseconds.
- `songName`: Returns the chart's song name.
- `songPath`: Returns the chart's song name, formatted as a song path.
- `startedCountdown`: Boolean that returns if the countdown has started.
- `curStage`: Returns the name of the stage in the current chart.
- `isStoryMode`: Boolean that returns if you're playing in Story Mode.
- `difficulty`: Returns the ID **number** of the selected difficulty.
- `difficultyName`: Returns the **name** of the selected difficulty.
- `difficultyPath`: Same as **difficultyName**, but formatted for the song path.
- `weekRaw`: Returns the number of the selected week.
- `week`: Returns the name of the selected week, from the week JSON in the weeks folder.
- `seenCutscene`: Boolean that returns if a cutscene has been seen.
- `hasVocals`: Boolean that returns if the chart allows vocals.

## Metronome variables

- `bpm`: Returns the chart's initial BPM[^1].
- `curBpm`: Returns the current BPM in the chart.
- `crochet`: Returns the time between beats in the chart, in milliseconds.
- `stepCrochet`: Returns the time between steps[^2] in the chart, in milliseconds.
- `curSection`: Returns the current section in the song.
- `curBeat`: Returns the current beat in the song.
- `curStep`: Returns the current step in the song.
- `curDecBeat`: Same as **curBeat**, with decimal precision.
- `curDecStep`: Same as **curStep**, with decimal precision.

## Gameplay variables

- `inGameOver`: Boolean that returns if the player is in the game over screen.
- `mustHitSection`: Boolean that returns whether the current section is focused on the player side (`true`) or the opponent side (`false`).<br>
- `altAnim`: Boolean that returns if the current section is an alt. animation section.
- `gfSection` Boolean that returns if the current section is focused on speaker side (Girlfriend).

### Gameplay Modifiers

- `playbackRate`: Returns the **Playback Rate** modifier. 1 is 1x speed.
- `instakillOnMiss`: Boolean that returns if the **Instakill on Miss** modifier is enabled.
- `botPlay`: Boolean that returns if the **Botplay** modifier is enabled.
- `practice`: Boolean that returns if the **Practice Mode** modifier is enabled.
- `healthGainMult`: Returns the **Health Gain** multiplier.
- `healthLossMult`: Returns the **Health Loss** multiplier.

## Scoring variables

- `score`: Returns the player's score.
- `misses`: Returns the player's miss count.
- `hits`: Returns the player's total note hits.
- `combo`: Returns the player's current note combo.
- `rating`: Returns the player's rating, from 0 (0%) to 1 (100%).
- `ratingName`: Returns the description of the player's rating in-engine (ex. "Perfect!!", "Sick!", "You Suck!").
- `ratingFC`: Returns the player's FC status in-engine (ex. "SFC", "GFC", "FC", "SDCB", "Clear").

## Position / Scale variables

| Variables | Description |
| :-------: | ----------- |
| `defaultBoyfriendX`<br>`defaultBoyfriendY` | Return the default X and Y positions for the player side character. |
| `defaultOpponentX`<br>`defaultOpponentY` | Return the default X and Y positions for the opponent side character. |
| `defaultGirlfriendX`<br>`defaultGirlfriendY` | Return the default X and Y positions for the speaker side character. |
| `defaultPlayerStrumX0` to `defaultPlayerStrumX3`<br>`defaultPlayerStrumY0` to `defaultPlayerStrumY3` | Return the default player strum[^3] X and Y positions.<br>0 -> left; 1 -> down; 2 -> up; 3 -> right |
| `defaultOpponentStrumX0` to `defaultOpponentStrumX3`<br>`defaultOpponentStrumY0` to `defaultOpponentStrumY3` | Return the default opponent strum[^3] X and Y positions.<br>0 -> left; 1 -> down; 2 -> up; 3 -> right |
| `screenWidth`<br>`screenHeight` | Return the game's full width and height.<br>The default game resolution is 1280x720. |

## Character variables

- `boyfriendName`: The name of the player side character, from the character JSON in the characters folder.
- `dadName`: The name of the opponent side character.
- `gfName`: The name of the speaker side character.

## Options variables

> [!NOTE]
> Some options aren't set in Lua scripts! You may get these settings with getPropertyFromClass.<br>
> ex. `getPropertyFromClass('backend.ClientPrefs', 'data.discordRPC')` checks if **Rich Presence** is enabled.

### Gameplay

- `downscroll`: Boolean that returns if **Downscroll** is enabled.
- `middlescroll`: Boolean that returns if **Middlescroll** is enabled.
- `ghostTapping`: Boolean that returns if **Ghost Tapping** is enabled.
- `noteOffset`: Returns the **Rating Offset**, in milliseconds.
- `guitarHeroSustains`: Boolean that checks if **Sustains as One Note** is enabled.

### Graphics

- `lowQuality`: Boolean that returns if **Low Quality** is enabled.
- `shadersEnabled`: Boolean that returns if **Shaders** are enabled.
- `framerate`: Returns the **Framerate** cap.

### Visuals and UI

- `noteSkin`: Returns the selected note skin in **Note Skins**.
- `noteSkinPostfix`: Returns the postfix of the selected note skin in **Note Skins**.<br>
Ex. if the "Future" note skin is selected, **noteSkinPostfix** will be **"-future"**.
- `splashSkin`: Returns the selected note splash skin in **Note Splashes**.
- `splashSkinPostfix`: Returns the postfix of the selected note splash skin in **Note Splashes**.<br>
Ex. if the "Diamond" note skin is selected, **splashSkinPostfix** will be **"-diamond"**.
- `splashAlpha`: Returns the **Note Splash Opacity**, from 0 (invisible) to 1 (opaque).
- `hideHud`: Boolean that returns if **Hide Hud** is enabled.
- `timeBarType`: Returns the **Time Bar Type**, as a string.<br>
If you want to check if the time bar is disabled, you can check if its equal to "Disabled":
```lua
if timeBarType ~= 'Disabled' then --if the timebar isn't disabled, then...
	-- ...
end
```
- `flashingLights`: Boolean that returns if **Flashing Lights** are enabled.
- `cameraZoomOnBeat`: Boolean that returns if **Camera Zooms** are enabled.
- `scoreZoom`: Boolean that returns if **Score Text Zoom on Hit** is enabled.
- `healthBarAlpha`: Returns the **Health Bar Opacity**, from 0 (invisible) to 1 (opaque).
- ``

## Misc. variables

- `inChartEditor`: Always `false`, as you can't run Lua scripts inside the Chart Editor.
- `scriptName`: Returns the name of the Lua script.
- `version`: Returns the current Psych Engine version.
- `buildTarget`: Returns the build target for your Psych Engine build.
  | Build Target | Description |
  | :----------: | ----------- |
  | "windows"    | If compiled to Windows. |
  | "linux"      | If compiled to Linux. |
  | "mac"        | If compiled to Mac. |
  | "browser"    | If compiled to HTML5. |
  | "android"    | If compiled to Android. |
  | "switch"     | If compiled to Nintendo Switch? (missing documentation) |
  | "unknown"    | Returned if it wasn't compiled to any of the previous targets. |

[^1]: **BPM**: Beats per minute. Indicates the number of beats that occur within a minute. ([LANDR Blog: What is Tempo?](https://blog.landr.com/what-is-tempo/))
[^2]: In Friday Night Funkin' terms, a **step** is a quarter of a beat.
[^3]: **Strums** or **Receptors** refers to the gray notes that are always on screen.