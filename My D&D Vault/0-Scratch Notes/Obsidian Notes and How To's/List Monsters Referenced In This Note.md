Personally this is a Dataview query that I used a lot. It displays a list of monsters that are mentioned within the current note. I like to stick it in my module/chapter notes at the very top of the note. It let's my quickly see what monsters are involved in the chapter which helps me know what miniatures to prepare for my game.

In the example below you can see the Bases highlighted. It's specifically a Cards view so you get to see an image of the monsters as well. If you click them, it takes you to the monsters note.

Example

![Pasted image 20250817221033.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020250817221033.png)

Copy the code below into a note.

````
```base
views:
  - type: cards
    name: Mentioned Monsters
    filters:
      and:
        - this.hasLink(file)
        - noteType == "pf2eMonster"
    image: note.image
    cardSize: 200
    imageFit: contain
    imageAspectRatio: 1

```
````

### Instructions For Use

For this to work you need a few things in place.

- Your monster notes need to contain a property called **image**.
    - The value of image should be the image name.
    - Example: image: monstername.png
- Your monster notes need to contain a Property or Tag that can uniquely identify this note as being a monster. In my example, each monster note contains the noteType property with the value 'pf2eMonster'.
- You then simply insert this code into your note.
- Any mentions of monsters within the note '[monster name](https://obsidianttrpgtutorials.com/monster+name)' with display in the Cards view.

