# UltimaV retroset

Tileset graphics mod for Ultima V series. A unicorn of Unciv graphics - **square tile** gameplay, based on the OG GOAT RPG, [Ultima V](https://wiki.ultimacodex.com/wiki/Ultima_V:_Warriors_of_Destiny)!

Skip down to [Features](https://github.com/hackedpassword/UltimaV-retroset/edit/main/README.md#features) section to know what this mod is all about.

# Mod info

The tileset is built specifically for the Brittania map. See installation below to match these up.

This mod is evolving from a tileset into a styled mod! There's a lot of potential to capture Ultima V gameplay in a Civ V world. Anticipated is the use of equipment, items, and spells, along with a re-envisioned Unciv battlefield experience to reflect Ultima V's adventurous and dangerous roaming about. Quests? Objectives? Absolutely. There's an idea of a winning condition that involves visiting shrines, cities of virtue, dungeons, codex, and other landmarks, to progress the narrative, while intersecting with other players also questing. Fight? Collaborate? Lots to consider while working to secure the next goal.

# Updates

## Decor alignment tech
Splitting dev work between gfx and base. On the graphics side, a particularly ugly issue has been plaguing decor sprites - alignments. Cause: render space per `32x32` sprite is actually `24x28` for almost seamless tiling. Ouch, not a proper divisor, compensated. First batch of rebuilt TF's show how immensely powerful only a 4-pack of `terrainDecor` can be. The open island below is 2 tiles thick, symmetrical.

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/Decor_size_correction_demo.png)

Now that I understand the technical rendering requirements for decor seamlessness, the rest of the decors will be updated. Another challenge to this is that in 1:4 there are 4 sudo-tiles to factor per sprite, inclusive to determining what land that decor belongs to. The 4 above are `Grassland` decors so land improvements can be built there. To modify movement where water appears to split the land, rivers should be applied.

## Reverse engineering tiles

Made a per-tile representation mod of [drrak's map](https://drrak.github.io/ultima5/). Clever Lord British and company use both angled and curved grass-water edging all over to create natural visuals. When tiled, the simplicity is exposed:

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/revealed_tiles.png)

This is really cool to look at up close. River used between river-end aside various angled textures, brilliant. Some map areas are challenging to interpret to re-map into 1:4 hex->square, this helps guide that effort.

[Full map is here](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/resource/Ultima%20V%20-%20Overworld%204096%20-%20with%20overlay.png).

## Terrain decor update

New Unciv modding invention: [Terrain decorations](https://github.com/hackedpassword/UltimaV-retroset/blob/main/docs/Decorations.md) that add a new dimension of mapping goodness! This demo shows the basics of decor applications.

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/bordermarch_decor.png)

You'll notice square tiles have overlying fancy decor sprites that make tetris-looking land turn into far more natural landscapes. Much like how the original map was built, though here we build by layers versus single sprites.

It may seem weird, but square tiles in a hex grid is _absolutely legit hex grid gameplay_. The decor renders such that TF's (terrainfeatures) are placed (per TF order laid down) allowing careful sprite alignments on the backend (building the decor sprites) to appear like a non-symmetrical shape. Various combinations create entirely new appearances, or extend others. It's so cool. I'm super impressed at how this is turning out.

# Dev notes

## what about hex grid decor?

Been thinking about that. We'll see, does sound interesting though.

### Random map generation

Decors like the above don't have the auto tile alignments needed in random map gen to make sense - they'd be a muddled mess. I've already accepted awesome Unciv graphics are not a community selling point, that's fine, but dev work towrads this end isn't a priority.

Unfortunately I can't see how to integrate coherent auto gen decor into random gen, without some serious advancements. Personally I find random gen spammy anyway (in resources) even at minimal settings, or a weird diffusion of terrain (biomes could use an overhaul). Not complaining, my pref. Hand-built has some real advantages like true biomes and route control. I love map-modding! Look at the biomes of Britannia, current Unciv map gen can't touch that level of environmental/world design. Would be an interesting side project to try volumetric biome gen. Likely would use two stages - 1st stage map gen lays down env frame tiles, then 2nd stage uses 'this tile becomes' unique to transform the framework tiles at game start into blossomed biome areas.

### PSA, 🍺🥴🤕🤔😁🍺

Nobody follows my tech lol (it's too advanced) so pretty much just noting for myself. Is there anyone out there that can modhack Unciv's potential like I do? Who are the mad modders? :P First mad modders that come to mind are @carriontrooper and @AutumnPizazz for their highly creative mods that push Unciv. I must be shortsighted, but I'm also not on discord atm while r/l pressures/stresses detract from immediate community involvement, so who's doing what currently? Dunno, I'm killin it though that's what matters.

# Features

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
