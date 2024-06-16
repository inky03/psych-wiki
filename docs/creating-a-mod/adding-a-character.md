# Adding a character
You can access the Character Editor in 2 ways:
1. Press **Debug Key 1** in the main menu. This will open the Debug Menu, where you may then select the Character Editor.
2. Press **Debug Key 2** in a song. This will immediately load the Character Editor on the opponent side's character.

> [!NOTE]
> The debug keys are binded to **7** and **8** in your keypad by default, for Debug Key 1 and Debug Key 2 respectively.<br>
> You may change this in the Options menu if necessary, under Controls.

(image of the debug menu)

# The Character Editor

(image of the character editor)

Welcome to the Character Editor! Pay attention to the interface:
- The list of animations of the character, with their respective [offsets](#animation-offsets) are listed at the top left.
- The bottom left has a display with your character's icon and healthbar color.
- Finally, you will see two panes at the right.

These panes will be used to set up your character! They are as follows:

## Settings tab
> [!CAUTION]
> Changing or reloading the current character, or clicking Load Template will REPLACE the current character you're editing!<br>Make sure you've saved your changes before using any of these!

### Character
This is a dropdown where you can change the currently selected character.
### Reload Char.
Reloads the currently selected character file.
### Load Template
Loads a simple character template with only the idle and note pose animations.
### Playable Character
Use this tickbox to preview the character in each side. If unticked, the character will be previewed from the opponent side, otherwise it will be previewed from the player side.

## Ghost tab
An animation ghost is a copy of your character that you may use as a position reference when [offsetting animations](#animation-offsets).
### Make Ghost
> [!NOTE]
> You can only have one animation ghost at a time.
Makes an animation ghost of the current character animation.
### Highlight Ghost
Ticking this will make the animation ghost appear brighter / more white.
### Opacity
Use this slider to change the opacity of the animation ghost, where 0 is invisible and 1 is opaque.

## Character tab
This tab contains most of the important information for your character.
### Image file name
This will be the path to your character spritesheet, beginning from the images folder, excluding filetype.<br>
[Supported spritesheet formats](#supported-spritesheet-formats)

- **For XML/JSON spritesheets**<br>
  For example, if your image is located in `images/characters/BOYFRIEND.png` (and .xml or .json), you would input `characters/BOYFRIEND`.

- **For texture atlases**<br>
  Input the directory the texture atlas is located in.<br>
  For example, if your spritesheet data is in the following directories:
  - `images/characters/textureAtlas/Animation.json`
  - `images/characters/textureAtlas/spritemap1.json`
  - `images/characters/textureAtlas/spritemap1.png`
  then you would input `characters/textureAtlas` .

### Reload Image
After setting the **image file name**, press this button to load the spritesheet. If your character hasn't appeared after pressing the button, your path may be set up incorrectly.
### Health icon name
Changes the current icon of your character. Your icon must be located in **"images/icons/icon-ICONNAME.png"**, where **ICONNAME** is what must be input in the box.
### Get Icon Color
Gets the dominant color of the current icon and sets the healthbar color to match.
### Vocals File Postfix
Allows to load a vocals file for this character with a postfix[^1] when inside a song (**"Vocals.ogg"** > **"Vocals-postfix.ogg"**).<br>
### Character X/Y
> [!TIP]
> Make sure your character is aligned with the silhouette of the side you're previewing!
Here are two inputs to change the default position of a character.
### Camera X/Y
Offsets the camera position when it's focused on your character (note the crosshair!).
### Flip X
If ticked, the character will be flipped horizontally (make sure it's facing left when playable and right when not!).
### No Antialiasing
If unticked, the character will have a rough, more "pixelled" appearance. It's recommended to use this if you're working with pixel sprites.
### Scale
Changes the scale of your character. 1 is the default size (100%).
### Health bar R/G/B
Here are three inputs to change the healthbar color by its red, green and blue color values.
### Sing Animation length
Change the time the sing animations of your character will play for, measured in **steps** (steps are a quarter of a beat).
### Save Character
Saves the character to a file.

## Animations tab
> [!TIP]
> All default animation names used in Psych Engine are listed in [Default Animation List](#default-animation-list).<br>
> You're free to add more animations, but keep in mind they must be [scripted]().

In this tab you can add or edit the animations that will be played on your character in-game.<br>
Start by opening the data file used on your character's spritesheet (this must be a XML or JSON file).

1. Input the name of your animation in the **Animation name** input field.
2. Check your spritesheet data file.<br>
  In the case of .xml files, the animation prefix is located after `<SubTexture name...`<br>
  Input this animation prefix to the **Animation Symbol Name/Tag** input field, excluding the last 4 numbers.
3. You may change the animation framerate or tick the **Should It Loop?** box if required.<br>
  The default framerate is 24 FPS, which is the standard in Friday Night Funkin' character sprites.
4. Press the **Add/Update** button to add or update the currently selected animation.<br>
  If you want to remove the animation instead, press the **Remove** button. (shocker isn't it?)

Repeat this process for each animation you want to add to your character file!

### Animation Indices
> [!NOTE]
> The frame numbers start at **0**. This means frame 0 is the first frame of your animation.

This is an advanced feature in animations that allows them to be played in a certain sequence.<br>
You can do this by inputting the frame numbers of your animation separated by a comma; for example, putting **0,2,4** in this field will only play frames 1, 3 and 5 in your animation.

### Animation Offsets
> [!TIP]
> - Press F1 to see the full list of controls in the Character Editor.<br>
> - You can use the [animation ghost]() on your idle animation as a position reference!

> [!WARNING]
> Keep in mind that due to quirks with Flip X, your animation offsets may look wrong on one side.<br>
> Make sure you're previewing the character in the desired side when changing these offsets.

Once you've added all of your animations, try pressing W or S to cycle through them.

(image of bad offsets here)

You may immediately notice the animations aren't aligned with each other!<br>
That's what animation offsets are for; this will allow you to align your animations so they are in the correct positions.

1. Press W or S again to cycle and select the animation you want to change.
2. Press the arrow keys to move the offsets by 1 pixel. Hold the **Shift** key to move it by 10 pixels instead.
3. Keep playing around with the offsets until your character is correctly aligned.

Repeat this process for every animation you have. 

## What next?
Done setting up your character?

1. Go back to the **Character tab**.
2. Press the **Save Character** button to open the save prompt.
3. Your character file must be saved in your mod folder, inside **characters**! Give your character a filename and save it as **.json**.

🎉 **All set!!** If everyone is done correctly, your character should now show up in the character list in the **Character Editor** and the **[Chart Editor]()**.

# Other Resources

## Supported Spritesheet Formats
Characters can load the following formats:
- **Sparrow texture atlas**: This is the kind most Friday Night Funkin' sprites use! The data is contained in a .xml file.<br>
  You can export spritesheets to this format in Adobe Flash[^2] and Adobe Animate.
- **Texture Packer JSON**: This is a JSON format exported by [TexturePacker](https://www.codeandweb.com/texturepacker).<br>
- **Adobe Animate Texture Atlas**: This is a format exported by Adobe Animate which exports symbols instead of whole frames. This is very useful to avoid huge spritesheets sizes, but support is currently limited[^3].

## Default Animation List
The default animation names for a character are as follows:
> [!NOTE]
> The "danceLeft" and "danceRight" animations are used for Girlfriend and the Spooky Kids' sprites.
- **idle**: Idle pose
- **danceLeft**: Idle pose (swaying left)
- **danceRight**: Idle pose (swaying right)
- **singLEFT**: Left note pose
- **singDOWN**: Down note pose
- **singUP**: Up note pose
- **singRIGHT**: Right note pose
- **singLEFTmiss**: Left note pose (note missed)
- **singDOWNmiss**: Down note pose (note missed)
- **singUPmiss**: Up note pose (note missed)
- **singRIGHTmiss**: Right note pose (note missed)
- **hey**: Used on the Hey! event (ex. as seen in Bopeebo)
- **cheer**: Used on the Hey! event (Speaker only)
- **scared**: Used when lightning strikes (ex. as seen in Week 2)

The default animation names for a Game Over character are as follows:
- **firstDeath**: This animation plays at the start of the Game Over screen
- **deathLoop**: This animation plays during the music loop in the Game Over screen.<br>
  The animation must loop to display correctly.
- **deathConfirm**: This animation plays when you retry in the Game Over screen

[^1]: **Postfix**: to add or append at the end of something: suffix. (Definition from the [Collins English Dictionary](https://www.collinsdictionary.com/dictionary/english/postfix))
[^2]: Adobe Flash exports the Sparrow format encoded in UTF-16; this is unsupported and will cause the game to crash. Change the XML encoding to UTF-8 first.
[^3]: [TODO in Dot-Stuff/FlxAnimate](https://github.com/Dot-Stuff/flxanimate?tab=readme-ov-file#todo)
