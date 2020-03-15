## Terrainz.js
Terrainz.js is a flexible mini-library built on top of [noisejs](https://github.com/josephg/noisejs). It uses perlin noise to
create somewhat convincing 2d maps. First, include the library in your webpage:
```js
<script src="https://cdn.jsdelivr.net/gh/N8Python/terrainzjs/terrainz.js"></script>
```
Then, you can generate a map (with any width and height) based off perlin noise by calling the `terrain` function (make sure you `await` it inside an async function.
```
const noise = await terrain(width, height);
```
You can configure the noise with options in the third parameter of the `terrain` function, but these variables are already pre-set 
to generate pretty good terrain:
```
const noise = await terrain(width, height, {
    scale = 200,
    octaves = 16,
    persistance = 0.5,
    lacunarity = 1.87
});
```

As you lower the scale, your noise becomes more zoomed out. The higher the octave count, the more small details are inserted into your noise. Lacunarity and persistance determine the quantity and influence of these small details.
Now, the noise is a 2d array with values from 0 to 1. However, you can automatically turn this noise into an array of color values by using a custom method defined
on it: `make`:
```
const islandMap = await noise.make("islands"); // Make an island map
const forestMap = await noise.make("forest"); // You get the idea
```
The following is a list of all prebuilt biomes in `terrainzjs`:
- islands
- plains
- mountains
- forest
- tundra
- desert

You can define new types of terrain by adding them to the terrain object - for example, to define the island biome:
```
terrain.islands = {
    "blue": 0,
    "lightblue": 0.35,
    "rgb(255, 198, 153)": 0.4,
    "green": 0.5,
    "grey": 0.7,
    "white": 0.9
}
```
That means that numbers in the noise array between 0 and 0.35 are colored "blue", numbers between 0.35 and 4 are colored "lightblue",
and so on. Then you can enter the name of your biome into the `noise.make` function and lo and behold: the noise will be replaced by
a custom map.

That's it, becuase this is more of a mini library than a full-fledged project.

Enjoy!
