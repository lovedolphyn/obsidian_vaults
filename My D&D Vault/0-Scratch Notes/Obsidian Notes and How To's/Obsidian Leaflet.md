You can add your own maps into [Obsidian Leaflet](obsidian://show-plugin?id=obsidian-leaflet-plugin). From there you can:

- Add pins to your maps.
- Link those pins to notes.
- Measure distance.
- Draw shapes and lines on your map.
- It supports layered maps.
- It supports custom pins.
- Pins can be made visible/invisible at specific zoom levels.

![Obsidian_Leaflet.gif](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Obsidian_Leaflet.gif)

## Tutorials

Official Plugin Documentation

## Obsidian Leaflet Template

Patreon supporters using the Vault. Just press Alt + E and search for map. The template is already in the vault.

**Pre-Requirement:** [Plugin: Leaflet](obsidian://show-plugin?id=obsidian-leaflet-plugin)  
**Pre-Requirement:** [Plugin: Meta Bind](obsidian://show-plugin?id=obsidian-meta-bind-plugin)  
Copy this into a new template.

````
---
map_height_y: 2048  
map_width_x: 1642  
scale_pixels: 268  
scale_pixels_range: 25  
mapCalc1: 0  
---

> [!NOTE]- Quick Calculator  
> Map Height in Pixels: `INPUT[number:map_height_y]`  
> Map Width in Pixels: `INPUT[number:map_width_x]`  
> lat: `VIEW[{map_height_y} / 2][math]`  
> long: `VIEW[{map_width_x} / 2][math]`  
> How Many Pixels In Scale: `INPUT[number:scale_pixels]`  
> How Many Units in Scale: `INPUT[number:scale_pixels_range]`  
> Scale: `VIEW[1/({scale_pixels}/{scale_pixels_range})][math:mapCalc1]`



```leaflet  
id: MapCalcExample ### Must be unique with no spaces  
image: [[Map - Regional map of Lampoteuo.png]] ### Link to the map image file. Do not add a ! in front of the image  
bounds: [[0,0], [2048, 1642]] ### Size of the map in px Height_y, Width_x. Ignore 0,0  
height: 850px ### Size of the leaflet embed in px on your screen  
width: 95% ### Size of the leaflet embed in your note  
lat: 1024 ### To center the map, make this half of the map height.  
long: 821 ### To center the map, make this half of the map width.  
minZoom: -1.5 ### Controls how far away from the map you can zoom out. Hover over the target icon to see the current level.  
maxZoom: 1 ### Controls how far towards the map you can zoom in. Hover over the target icon to see the current level.  
defaultZoom: -1 ### Sets the default zoom level when the map loads. Hover over the target icon to see the current level.  
zoomDelta: 0.5 ### Adjust how much the zoom changes when you zoom in or out.  
unit: mi ### The value displayed when measuring so you know what type of unit is being measure.  
scale: 0.09328358208955223 ### Real units/px (resolution) of your map  
recenter: false  
darkmode: false ### marker
```

````

## How To Use The Template

1. Press your hotkey to insert a template (Alt+T).
2. Type `map` and select `Insert Map (Simplified Template)`
3. Copy the name of your map into the **image** field per the example.
4. Change the **id** of the id. Pick something unique. Maps that share the same ID will share pins also!
5. External to Obsidian, check the properties of the map file to determine its pixel size.
6. Enter the map **height** and **width** in pixels into the calculator.
7. Copy the same details into the **bounds** section of the leaflet template.
8. Now copy the **lat** and **long** from the calculator into the **lat** and **long** sections of the leaflet template.
9. Play with the **height** and **width** now. This determines the size of the Leaflet object when displayed in the note.
10. You map should now be usable but you will want to tweak the zoom settings.
11. I usually get the map into the zoom I'm happiest with and set that to the **defaultZoom**.
12. Adjust the **minZoom** and **maxZoom** based on your personal preference.
13. You can hover your mouse over the little target icon to see the current zoom level which is useful for filling these in.
14. This is as far as you need to go if you don't need to measure within the map.
15. To enable measurement you need to open the map in some software that has a measurement tool. I use Gimp for this which is free.
16. You need to measure the scale of the map to determine how many pixels exist within the units of the scale.
17. In this example, I measure the pixels from 0-25 which is 268 pixels. I enter that in the calculator.
18. Then I update the how many unit in scale to match the scale of the map. So there are 25 units.
19. ![Pasted image 20250129203906.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020250129203906.png)
20. The **scale** is now calculated and I copy the result into the leaflet template.
21. Example: scale: 0.09328358208955223
22. You can now: Alt + Click to set a measurement point and then measure. You can press Alt + Click again to see a additional measurement point.