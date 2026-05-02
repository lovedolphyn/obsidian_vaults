Exactly as the title suggests. This is actually really useful.

Lets say you have a note for an NPC. That NPC works in a shop. You put this query in the shop and it will dynamically list all NPCs who reside in that shop.

Example

In this example:

1. The people each contain a property called MyContainer. The value of MyContainer is the note-name for the place that they reside in.
2. The place contains the bases syntax below. It dynamically shows all the NPCs that reside within the place.  
    ![Pasted image 20250817223909.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020250817223909.png)

Copy the code below into a note.

````
```base
properties:
  file.name:
    displayName: List of People in Place
views:
  - type: cards
    name: People - Cards
    filters:
      and:
        - file.folder == "2-World/People"
        - list(MyContainer).contains(this)
        - char_status.contains("Alive")
    order:
      - file.name
    image: note.image
  - type: table
    name: People - Table
    filters:
      and:
        - file.folder == "2-World/People"
        - list(MyContainer).contains(this)
        - char_status.contains("Alive")
    order:
      - file.name
    sort:
      - property: file.name
        direction: DESC
    columnSize:
      file.name: 182

```
````

### Instructions For Use

- Ensure each note has the MyContainer property.
    - **Tip:** I populate the value of the property with a MetaBind suggestor.
    - `` `INPUT[suggester(optionQuery(#Category/Places)):MyContainer]` ``
- Update the file.folder reference to the folder where you are storing your people. This is the notes that will be returned by the query.
    - Example: my people notes are stored in "2-World/People". Change this to match your folder structure.
- I have an extra filter on this which checks to see if the person is still alive. If char_status does not contain 'Alive' then the note will not appear.
- Each note needs to contain an image property that contains the image name that you want to display in the Base.
    - Example: image: notename.png