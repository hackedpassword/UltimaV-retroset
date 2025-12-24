# Decorations as a terrain layer

Let's talk about how to add some _real customization_ to an Unciv map. We'll do this by creating some new `terrainFeature`'s that can be layered, then re-layering on top of the `ruleVariants` defined in `jsons/tileSets/[tileset].json`, the usual customizing of multi-layer tile sprites. We'll call this synthetic layer Decorations, or `terrainDecor`.

**Decors** give more control over rendering rules on terrain tiles by mixing in benign entities to terrainFeatures. Another mad modder creation ;)

> "Wow, wow. That's f^k'n .. COOL. Whoa. LOL!!!(more of a HUAHAHAHA)" -me dropping in the first demo decorations

There's several components to successfully implement decorations. 

## Visualized!

A visual step-through should tell you most of what you want to know. I think this technique is probably easier with square-hex tiles due to less sides, but plenty of application to hex tiles. We'll focus on square-hex tiles atm. How-to follows.

|  |  |
| ------- | ------- |
| ![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_1.png) | ![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_2.png) |
| ![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_3.png) | ![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_4.png) |
| ![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_5.png) | ![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_6.png) |

## Tech

Now, we will look closer at certain decor aspects as presented here:

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_7.png)

### POI (1)

In the demo image, you'll find the rivers in this area missing - but they're not. River textures in `TileSets\HexaRealm\Tiles` are all blank and clear. Why? Decors will replace river textures, which cannot be re-ordered in rendering, causing overlay artifacts.

Rendering order artifacts lead to slop like this:

|  |  |
| ------- | ------- |
| ![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/river_layers_fail.png) | ![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/river_layers_fail2.png) 

See, not only do rivers render in an order that is uncontrollable, sometimes right sometimes not, rivers are unaffected by out-of-sight tile dimming. To compensate, I muted the river color contrast as to be a transitional color that might be dimmed, might be seen. It's not awful but also not the intended artistic output. Decor layers aim to fix this.

Let's take a quick look at the sprite sheet rip, and the mod sprites involved:

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor_sprites.png)

Original terrain sprites are highlighted. We then have Grassland decors as 4-channel overlay sprites, river-decor, river-dev, and a regular Coast that's only used to be a terrain attribute modifier called Coast-edgeless, more on this soon.

### POI (2)

This swamp area is interesting for its use of interconnecting river textures. Recall Ultima V mod scales Brittania 1:4, squares vs hexes, making river placement an interpretive artistic task. Perfect for demo'ing!

The way we lay down the decor, with all other layers, is first we must decide what order to present. A Forest then Jungle results in a different sprite than Jungle then Forest. With Grassland as the base, we could place the grasslandXX water corner decor first, then Marsh, to represent marshy water in addition to marshy land. Or, placing Marsh first then decor results in marshy land, normal water. Stacking other terrainFeatures like Forest and Jungle, or Hill, anything, all get the same treatment.

Because the decor here has an opaque area and mostly alpha clear area, when it's applied over most any tile, the water edge appears and land portion appears to recess - automagic. Using these for rivers was actually accidental.

### POI (3)

You'll notice the swamp entrance has a much more natural appearance. Just a few decors did it. The result? _**Wow.**_ For fun, I threw in a couple extra water features that would usually have a river stub to affect movement and whatnot correctly. The overlay effect was too amazing to remove.

**Rivers are _invisible_ textures in-game!** Look again at POI (1), the rivers are there, but some mapper needs to place decor rivers. Well, how do handle map placement? We have a set of river-editor textures (the pink ones). These are specifically designed to be brightly edged, dim transparent core, to clearly see where we are placing rivers, and, clearly see that rivers _are_ placed. This is not a guessing game, we get it right. Decor rivers are placed, and we're certain they're right because the resulting blends look like what we're expecting.

Oh, forgot to add, as seen on the sprite map above, original river sprites are available as decors too. This requires some additional work in `Terrains.json`. I can add new river sets at will. This area has this type, that area has that type, maybe some special alternative mid-river, whatever, control over artistic variety is ours!

```
	{
		"name": "River-Bottom decor",
		"type": "TerrainFeature",
		"unbuildable": true,
		"occursOn": ["Land","Grassland","Mountain","Plains","Desert"],
		"uniques": ["TerrainDecor","River",
		],
	},
```

The `occursOn` array needs each terrain to be used on. For some reason 'Land' is not an acceptable wildcard. We add a label 'TerrainDecor' to be used later, and 'River' to take on river attributes - a special entity in Unciv that we must mind is treated differently than other entities.

### POI (4) and (5)

An interesting problem arose with edges. Applying the water corners at Coast edges doesn't draw over edges. This iirc was due to that hexes are drawn tile by tile in reading order. Whatever the reason the solution was creating a new terrain clone of Coast. There is no edge texture set for this terrain tile so edges are poof gone. As you see by the missing right edge, this needs more work, superficially simple just adding specific edge assets.

Coast-edgeless is applied as a replacement Coast in Terrains.json:
```
	{
		"name": "Coast edgeless",
		"type": "Water",
		"food": 1,
        	"gold": 1,
		"movementCost": 1,
		"RGB": [70, 138, 216],
		"uniques": ["Coast","[+2] to Fertility for Map Generation",
...
```

The only modification to Coast is adding the unique label 'Coast'. What this does is causes assets involved with Coast-edgeless to inherit Coast attributes. Through this inheritence, we don't have to update every single unique that has some connection to Coast. Easy!

Resources are the next challenge, they're not as drop-in as I'd like. In `TileResources.json` we add:
```
	{
		"name": "Fish",
		"resourceType": "Bonus",
		"terrainsCanBeFoundOn": ["Coast","Coast edgeless"],
		"food": 1,
		"improvement": "Fishing Boats",
		"uniques": ["Generated on every [10] tiles <in [{Featureless} {Coast}] tiles>"]
	},
```

We see here the addendum to where Fish can be found, because inheritence doesn't work on that attribute. However, the unique references 'Coast', which should work for map gen. Map placement for Fish won't work on Coast-edgeless unless that update is applied to Fish.
