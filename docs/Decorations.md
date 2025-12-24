# Decorations as a terrain layer

Let's talk about how to add some _real customization_ to an Unciv map. We'll do this by creating some new `terrainFeature`'s that can be layered, then re-layering on top of the `ruleVariants` defined in `jsons/tileSets/[tileset].json`
for usual customizing of multi-layer tile sprites. Basically, bending Unciv rendering rules on terrain tile layer mechanics by synthetically mixing in our own layer-ish.

> "Wow, wow. That's f^k'n .. COOL. Whoa. LOL!!!(more of a HUAHAHAHA)" -me dropping in the first demo decorations

I think this technique is probably easier with square-hex tiles due to less sides, but plenty of application to hex tiles. We'll focus on square-hex tiles atm.

A visual step-through should tell you most of what you want to know. How-to follows.





