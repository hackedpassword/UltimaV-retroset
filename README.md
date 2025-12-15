# UltimaV retroset

Tileset graphics mod for Ultima V series. A unicorn of Unciv graphics - square tile gameplay based on the OG RPG, Ultima V.

Not _entirely_ complete yet - things like pillaged improvements and nuance tile conditions still fall back on built-in tilesets. Current progress is more than satisfactory to minimize distraction by the few remaining fallback non-Ultima sprites.

Square tiles are cool, with edges even better. But one of the attractions to the original U5 was its sprite palette of angled terrain edges. Replicating this in Unciv is not trivial, though it seems to be possible as seen in the demo image.

# Updates

New Unciv modding invention: Terrain decorations (decor)

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/Decor%20intro.png)

## What am I looking at?

Let's go step by step to appreciate the direction this is heading.
- Number 1, everything you see above is all graphics modded, meaning vanilla unciv works (almost!) without any updates.
- Second, you'll notice many square textures are now represented with fancy decors that make tetris-looking land into far more natural landscapes.
- This is a basic land set just to show off what decor can do. Wow.

Again, all the above is _absolutely legit hex grid usual gameplay_. The decor renders such that TF's are knocked out (per TF order laid down) allowing careful sprite alignments on the backend (building the decor sprites) to appear like a non-symmetrical shape. Various combinations create entirely new appearances, or extend others. It's so cool. I'm super impressed at how this is turning out.

## Well that is cool but what about us hexgrid'rs?

Been thinking about that (hey I am too!). Decors like the above don't have the tile alignments needed in random map gen to make sense - they'd be a muddled mess. I've already accepted awesome Unciv graphics are not a community selling point, that's fine, unfortunately I can't see how to integrate coherent decor into random gen, without some serious advancements. Personally I find random gen spammy in resources even at minimal settings, or a weird diffusion of terrain. Not complaining my pref. Hand-built has some real advantages like true biomes and route control. I love map-modding.



## Features

- **Square tile** graphics as mentioned (concealing the underlying hex grid)
- Movement remains 6-directional, mandatory being built on top of Unciv
- Original tiles and sprites from fan-dev tilesheet sprite rips
- Maximum preservation of orginal sprites, augmented where needed
- 1:4 scale Britannia map (128^2) is vast despite being quarter-sized
- Terrain sprites overlap with more natural graphical transition
- Feature sprites (like forests) are layered for Unciv gameplay, looking completely original at game start
- Treasures hidden throughout the world, inclusive of expected reagents
- Exploration "feel" *closely* retained in a world of adventure

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/adventure01.png)
  
- Custom [Shadowlord realm themed borders](https://github.com/hackedpassword/Ethereal-borders) look like wild energy barriers (probably the coolest Unciv edge mod to date!)
- Towns, shrines, abbeys, moongates and dungeons are re-themed buildings, improvements, and wonders
- Road Improvements for paths
- Carefully hand-placed resources across the land for an **amazingly balanced** game as civs scale, from start to end
- **Meaningful economics** and trading due to smart resource placement (eliminated resource spam)
- Layered sprites partially conceal items to be discovered making exploration actually rewarding to the player
- Intense attention to crafting the map as accurately as possible factoring both hex->square and quarter-scale design challenges
- **Split-resource tiles**. The lighthouse Fogsbane for example is Landmark + Stone, so one could erect a Quarry, in place of the Landmark. You choose!

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/main/Images/Ethereal%20borders/Screenie1.png)

## Not present, yet
- More re-themed units
- Re-themed nations to become pre-placed towns (ex. Paws or Moonglow, etc)
- Re-theming game entity names, see [Ultima V base](https://github.com/hackedpassword/UltimaV-base/blob/main/jsons/translations/English.properties)
- Re-themed icons
- Granting promotions that act like items or spells
- Better use of wonders
- Conversion into a true tileset vs modding over HexaRealm

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/u5map01.png)

## How do I get this because it sounds awesome!

The mod is modularized atm, so you'll need complimentary mods:

1. Download Unciv
2. IMPORTANT: Enable HexaRealm tileset and FantasyHex unitset in Options > Display (until the mod converts fully we fill in missing assets from default tilesets)
3. Within Unciv, in the Mods menu download: 1. `Ultima retroset` mod, 2. `Ethereal borders` mod, and 3. [Nextgen Maps](https://github.com/hackedpassword/Nextgen-Maps) mod (that's 3 mods total)
4. In the New Game screen, select G&K base ruleset, set Map Type to "Custom", set Map Mod to "Nextgen Maps", select map Britannia
5. Enable the mods `Ultima retroset` and `Ethereal borders`
6. Add some civs and nations. 12 civs and 20 nations should provide plenty of unrushed exploration and casual gameplay. Start your new game!

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/adventure02a.png)

# Previous updates

>>> Updated the installation section below, now accurate and easy to follow! 👍

Nov 2025 in-game look. New forts - fun concept here, using the shadowlord realm as a meta fortress barrier. Forever now, Academy and Fort have shared sprites. The darkened fort color based on [Stonegate's layout/colors](https://geocities.bootstrike.com/Ultima%20V%20Detailed%20Maps/u5/stonegte.gif), contrasted by surrounding realm field neon magenta at a low perspective (and some alpha blend).

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/Serpents%20hold%20island.png)

The present map release looks like the below. That should help you see how decors can really improve map visuals.

![](preview.png)

Primary mod use is theming the Ultima V overworld map [Britannia](https://github.com/hackedpassword/Nextgen-Maps#britannia-overworld). Map generation isn't recommended due to map-modding specificity.

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/Award%20winning%20screenshot.png)

For a comparison, here's the original graphics:
![](https://github.com/hackedpassword/Unciv-Assets/blob/main/Images/Ultima%20V/original_map-at-cove.png)
I love this map! Credit to the author @drrak. The whole map is [here](https://drrak.github.io/ultima5/).

What should stand out the most is that you don't see hex tiles, only "square" tiles. This is an intended and tricky effect to mimic the original looks of the 1988 game.

There's a slight intermix of sprite tilesets, mostly PC version. I wanted to use the Apple ][e version but those sprites are far too low quality so I believe the PC version is my goto.

This mod could use a star :star: to show support of the unique retro concept!
