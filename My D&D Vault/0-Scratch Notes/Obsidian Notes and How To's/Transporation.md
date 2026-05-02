---
title: "movement"
transportation: "rhinoceros"
movement:
    walking: {name: "Walking", base: 30, slow: 30, normal: 20, fast: 15}
    camel: {name: "Camel", base: 50, slow: 18, normal: 12, fast: 9}
    donkey: {name: "Donkey", base: 40, slow: 22, normal: 15, fast: 11}
    rhinoceros: {name: "Rhinoceros", base: 40, slow: 22, normal: 15, fast: 11}
tags: "Reference/Movement"
---

>[!alert] There were more types of transportation in his original file. I just didn't want to copy it all from the TV to this note. I think I have a copy of a similar code that does the same thing in my [[0-Scratch Notes|Scratch Notes]] folder.

## Example table:
Here's what a dataview js table based on the info in the front matter would look like.
```dataviewjs
let pg = dv.current(); 
let table = "| Name          | base | slow | normal | fast |\n" +
			"|------------ | ---------: | ---: | -----: | ---: |\n";
dv.header(3, pg.title);
for (let move of Object.entries(pg.movement)) {
	// dv.paragraph(Object.keys(move));
	// dv.paragraph(Object.keys(move[1]));
	table += "| " + move[1].name +
			" | " + move[1].base +
			" | " + move[1].slow +
			" | " + move[1].normal +
			" | " + move[1].fast +
			" |\n"

}
dv.paragraph(table);
```

## Example of calling the data:
*View in source code mode to see how these are working inline.*

The Camel has a base speed of `=this.movement.camel.base` and takes `=this.movement.camel.normal` minutes to go 1 mile.

The Donkey has a base speed of `=this.movement["donkey"].base` and takes `=this.movement["donkey"].normal` minutes to go 1 mile.

>[!alert] You can also use front matter to add a mode of transport to the top of your note that you can pull into code for ALL inline code going forward. In this example, rhinoceros was used as the transport type. 

The Rhino has a base speed of `= this.movement[this.transportation].base` and takes `= this.movement[this.transportation].normal` minute to go 1 mile.

