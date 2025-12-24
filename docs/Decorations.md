# Decorations as a terrain layer

Let's talk about how to add some _real customization_ to an Unciv map. We'll do this by creating some new `terrainFeature`'s that can be layered, then re-layering on top of the `ruleVariants` defined [...]

**Decors** give more control over rendering rules on terrain tiles by mixing in benign entities to terrainFeatures. Another mad modder creation ;)

> "Wow, wow. That's f^k'n .. COOL. Whoa. LOL!!!(more of a HUAHAHAHA)" -me dropping in the first demo decorations

There's several components to successfully implement decorations. 

## Visualized!

A visual step-through should tell you most of what you want to know. I think this technique is probably easier with square-hex tiles due to less sides, but plenty of application to hex tiles. We'll fo[...]

| Swamp demo |  |
| ------- | ------- |
| [![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_1.png)](./decor-demo-1.md) | image 2 - [credit](https://drrak.github.io/ultima5/)![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_3.png)
| image 3![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_2.png) | image 4![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_4.png)
| image 5![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_5.png) | image 6![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_6.png)
| image 7![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_8.png) | image 8![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor-demo_7.png)

## Tech

Now, we will look closer at certain decor aspects of the swamp area as presented above in image 8.

### POI (1)

In the demo image, you'll find the rivers in this area missing - but they're not. River textures in `TileSets\HexaRealm\Tiles` are all blank and clear. Why? Decors will replace river textures, whi[...]

Rendering order artifacts lead to slop like this:

|  |  |
| ------- | ------- |
| ![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/river_layers_fail.png) | ![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/river_layers_fail.png) |

See, not only do rivers render in an order that is uncontrollable, sometimes right sometimes not, rivers are unaffected by out-of-sight tile dimming. To compensate, I muted the river color contras[...]

Let's take a quick look at the sprite sheet rip, and the mod sprites involved:

![](https://raw.githubusercontent.com/hackedpassword/Unciv-Assets/refs/heads/main/Images/Ultima%20V/decor_demo/decor_sprites.png)

Original terrain sprites are highlighted. We then have Grassland decors as 4-channel overlay sprites, river-decor, river-dev, and a regular Coast that's only used to be a terrain attribute modifie[...]

### POI (2)

This swamp area is very interesting for its use of interconnecting river textures, where we can use land-specific corner decors instead of river-specific decors. 

Recall Ultima V mod scales Brittania 1:4, squares vs hexes, making river placement an interpretive artistic task. Perfect for demo'ing! Let's look at a GrasslandXX terrainDecor asset:

```
	{
		"name": "GrasslandSE",
		"type": "TerrainFeature",
		"unbuildable": true,
		"occursOn": ["Grassland","Plains","Desert"],
		"uniques": ["TerrainDecor","Grassland","Land",
		],
	},
```

Building a terrainDecor is quite simple. I'm still torn on caps TerrainDecor or terrainDecor, for our purposes either is fine but for json's the above is the current use. Now, how do we do it?

The way we lay down the decor, with all other layers, is first we must decide what order to present. Normally, a Forest then Jungle results in a different sprite than Jungle then Forest. With Gras[...]
... (rest of file unchanged)
