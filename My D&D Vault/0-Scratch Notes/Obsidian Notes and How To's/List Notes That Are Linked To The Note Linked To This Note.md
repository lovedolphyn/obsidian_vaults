Exactly as the title suggests. This is actually really useful.

Lets say you have a note for an NPC. That NPC works in a shop. So the NPC is linked to the shop. But the shop exists in a Town.

This Bases snippet lets you open the Town note and see a list of NPCs that reside in the town even though the NPCs are not directly linked to the town!

Thanks SailKite

Massive thanks to SailKite from the Obsidian TTRPG Community Discord for this one! He thinks this stuff is easy, I have no idea how it works!

Example

In this example:

1. The people each contain a property called MyContainer. The value of MyContainer is the note-name for the place that they reside in.
2. Each place also has a property called MyContainer. The value of MyContainer is the note-name for the hub that they reside in.
3. The hub contains the bases syntax below. It dynamically shows all the NPCs that reside within the hub.  

    ![Pasted image 20250817222701.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020250817222701.png)

Copy the code below into a note.

````
```base
formulas:
  LinkedViaPlace: |
    list(MyContainer)                                          
      .filter( file(value)                                     
               && list(file(value).properties.MyContainer)     
                    .contains(this) )                          
      .length > 0
  PlacesForThis: |
    list(MyContainer)
      .filter( file(value)
               && list(file(value).properties.MyContainer).contains(this) )
      .map( link(value, file(value).name) )
properties:
  file.name:
    displayName: Person
  PlacesForThis:
    displayName: Places (for this note)
views:
  - type: cards
    name: People linked via Places → this note
    filters:
      and:
        - file.inFolder("2-World/People")
        - formula.LinkedViaPlace
    order:
      - file.name
      - char_age
      - char_gender
      - char_race
    image: note.image
  - type: table
    name: View

```
````

### Instructions For Use

- Ensure each note has the MyContainer property.
    - **Tip:** I populate the value of the property with a MetaBind suggestor.
    - `` `INPUT[suggester(optionQuery(#Category/Region)):MyContainer]` ``
- Update the inFolder reference to the folder where you are storing your people. This is the notes that will be returned by the query.
    - Example: my people notes are stored in "2-World/People". Change this to match your folder structure.
- Each note needs to contain an image property that contains the image name that you want to display in the Base.
    - Example: image: notename.png