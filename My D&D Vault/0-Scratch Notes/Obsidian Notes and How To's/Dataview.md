Just an example of an OR statement and an AND statement.

````
```dataview
TABLE WITHOUT ID link(file.name) as "Monster Name"
	WHERE contains(file.name,"lizardfolk") 
	OR contains(file.name,"blackscale") 
	AND (SourceType = "Bestiary")
```
````

# List Bookmarks

````
```dataview
LIST
WHERE file.starred = true
```
````

# List everything with a specific tag

````
```dataview
LIST
FROM #tag 
```
````

# List everything that has a specific field property (eg campaign, npc, location)

````
```dataview
LIST
WHERE <field_name>
```
````

# List everything from a specific folder (including sub-folders)

````
```dataview
LIST
FROM "folder"
```
````

# List everything from a specific folder, grouped by sub-folders

````
```dataview
LIST rows.file.link
FROM "folder"
SORT file.name asc
GROUP by file.folder
SORT file.name asc 
```
````

# List everything with a specific property, grouped by property value

````
```dataview
LIST rows.file.link
WHERE campaign
SORT file.name asc
GROUP by campaign
SORT file.name asc 
```
````

# List everything excluding CLI content

````
```dataview
LIST
FROM "" AND !"3-Mechanics/CLI"
```
````

# Incoming Links

````
```dataview
LIST
FROM [[]]
```
````

# Outgoing Links

````
```dataview
LIST
FROM outgoing([[]])
```
````

# List Files that link to this file, but have no links going to that file

````
```dataview
list from [[]] and !outgoing([[]])
```
````

# List Orphan Files that have no ingoing or outgoing links, not including CLI, asset files or templates.

````
```dataview
LIST 
FROM "" AND !"3-Mechanics/CLI"
WHERE !contains(file.path, "zz_") AND (length(file.inlinks) = 0 AND length(file.outlinks) = 0) 
SORT file.name ASC
```
````

## List Content from Current Folder Only

This might be handy for limiting your queries to only return results from the current folder.

`WHERE contains(file.folder, this.file.folder)`

### Example

````
```dataview  
TABLE WITHOUT ID link(file.name) AS "NPC Name", Gender, Race, Age, Location, AssociatedGroup  
FROM "2. Mechanics/Non-Player Characters"
WHERE contains(file.folder, this.file.folder)
SORT file.mtime DESC
LIMIT 10
```
````

## List The Monsters From Fantasy Statblocks

This example can be placed in a note and will automatically generate a list of monsters from the Fantasy Statblocks plugin.  
The monsters are stored in: `YourVaultFolder\.obsidian\plugins\obsidian-5e-statblocks\data.json`

````
```dataviewjs
// change this to your desired substring (case-insensitive)
const nameFilter = "Goblin";

const monstersAsDvArray = dv
  .array(Array.from(FantasyStatblocks.getBestiary().values()))
  // only those with a CR
  .filter(m => m.cr)
  // only CR = '1'
  .where(m => m.cr == '1')
  // only names containing our filter term
  .filter(m => 
    m.name && 
    m.name.toLowerCase().includes(nameFilter.toLowerCase())
  );

// cap at 20 entries
const limitedMonsters = monstersAsDvArray.slice(0, 20);

dv.table(
  ["Name", "HP", "AC", "CR", "Source"],
  limitedMonsters.map(monster => [
    dv.fileLink(monster.name),
    monster.hp,
    monster.ac,
    monster.cr,
    monster.source
  ])
);
```
````

The returned table should look something like this.

![Pasted image 20230807170134.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230807170134.png)

This requires the installation of the TTRPG Statblocks plugin, the Dataview plugin and you need to enable the javascript option within the Dataview settings.

## List The Monsters Used In The Active Note

This example can be placed in a note and will automatically generate a list of monsters that have been linked from the current note. This is a fantastic tool if you are working with a large adventure of module. I use it to create a nice list at the top of the note that tells me instantly which miniatures I need to go get off my shelf for the current chapter.

For this example you would have 1x note per monster.

- The notes are stored in a `2. Mechanics\Beastiary\<book name>` folder but note that I do not use the folder in this query. I could, and probably should as it will make the query more efficient by reducing the number of folders it needs to index/scan in order to return the result.
    
- Each note has the following [Frontmatter](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Tutorials/YouTube+Series/Front+Matter+\(YAML\)+and+Tags/Front+Matter+\(YAML\)+and+Tags). Frontmatter is listed at the top of a note between the --- and ---.
    

```
---
SourceType: Bestiary
---
```

Here is the Dataview code that can be copied into the active note.  
The second line defines the Table. In this case all I do is rename the first column to `Monster` as the default is `File` which doesn't really fit the theme of my campaign.  
The third line is the WHERE clause that says show me any notes that have an Inbound Link to this file AND they must also have the Frontmatter `SourceType: Bestiary`.

````
```dataview
TABLE WITHOUT ID link(file.name) AS Monster
WHERE contains(file.inlinks, this.file.link) AND SourceType = "Bestiary"
```
````

The returned table should look something like this.

![Pasted image 20230529221432.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230529221432.png)

You can also modify this concept. In this example I bring all the `Magic Items` that are linked from the active note. Note that I use the Frontmatter `Type` here instead of `SourceType`. This is simply because I have imported content in multiple ways and the result is I have sloppy Frontmatter. Ideally I should update all my notes to use the same names for Frontmatter across all my notes. I have thousands of notes though... so do as I say, not as I do. 🫤😁

````
```dataview
TABLE WITHOUT ID link(file.name) AS "Magic Items"
WHERE contains(file.inlinks, this.file.link) AND Type = "Magic Item"
```
````

The returned table should look something like this.

![Pasted image 20230529221538.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230529221538.png)

## List the Party Members

This example can be placed in a note and will automatically generate a list of party members.

For this example you would have 1x note per player.

- The notes are stored in the folder: `1. The Party/Deadly Depth Inn`
- Each note has the following [Frontmatter](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Tutorials/YouTube+Series/Front+Matter+\(YAML\)+and+Tags/Front+Matter+\(YAML\)+and+Tags). Frontmatter is listed at the top of a note between the --- and ---.

```
---
Player: [Player Name]
Class: [Class Name]
Race: [Race Name]
Level: [Level]
hp: [health points]
ac: [armor class]
modifier: [Initiative Modifier]
pasperc: [Passive Perception]
Role: Player
Status: Active
---
```

This is an example of the Frontmatter from one of the player notes.  
![Pasted image 20230529210632.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230529210632.png)

In another note this can now be typed.  
  
Note that the Dataview query creates a table where the first column is the name of the Note. If you name the note after your player then this will always be the players name. You then define the column in the second line of the code. Each column is created by typing FrontmatterName, FrontmatterName2, FrontmatterName3, etc.  
The third line defines the folder you are looking at. You can replace this with a [#tag](https://publish.obsidian.md/#tag) also.  
The fourth line is a where clause that says only show me the notes where Role = Player.  
The firth line is a where clause that says only show me the notes where Satus = Active.

I do this because I have other notes in this folder and sub-folders that I do not want to display in the table. Dead players for example I change to `Status: Dead` and this way they will not display in the result.

````
```dataview
table Player, Class, Race, level, Role
from "1. The Party/Deadly Depth Inn"
where (Role = "Player") 
where (Status = "Active") 
```
````

![Pasted image 20230529205604.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230529205604.png)

This code is basically the same as the one above except I have brought in different columns.  
Line two does rename a column from `pasperc` to `Passive Perception (WIS)`.

````
```dataview
table Player, hp, ac, modifier, pasperc As "Passive Perception (WIS)"
where (Role = "Player") 
where (Status = "Active") 
```
````

![Pasted image 20230529210315.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230529210315.png)

Here is a slightly more advanced example.

- I did not like that the first column was called File. I wanted it represent the purpose of the column. To do this you start with:
    - `TABLE WITHOUT ID link(file.name) AS "Character Name"`
    - This over-rides the default column header and renames the column as "Character Name".
    - Note that the "Character Name" is in quotation marks. This is because there is a space in the column name and spaces break the code. If the column was just going to be called Character then the quotation marks are not required. You can see the quotation marks are using for the renaming of pasperc also.

````
```dataview
TABLE WITHOUT ID link(file.name) AS "Character Name", Player, hp, ac, modifier, pasperc As "Passive Perception (WIS)"
where (Role = "Player") 
where (Status = "Active") 
```
````

![Pasted image 20230529215920.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230529215920.png)

# New Tab Home Page 

Within my vault I like to have a Home Page. A place I can go to where I keep a handful of links that I commonly use.  
The process for creating the Home Page is covered in this video.

# Required Plugins

Here is a list of the plugins that are mentioned in the video. https://youtu.be/cF2g1N1GrmM

| Plugin                                                               | Usage                                         |
| -------------------------------------------------------------------- | --------------------------------------------- |
| [Advanced Table](obsidian://show-plugin?id=table-editor-obsidian)    | Makes it easier to make Tables.               |
| [Dataview](obsidian://show-plugin?id=dataview)                       | Primary Plugin                                |
| [Various Complements](obsidian://show-plugin?id=various-complements) | Automatic Linking and Front Matter Dropdowns. |

## Top Link Bar

The page has a section of images along the top that server as pretty links to other notes. The images themself serve no function, they are there for visual appeal.  
![Pasted image 20230708144828.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230708144828.png)

This is just a table. The top row has a link to the pictures. It makes use of the [ITS Theme - Image Adjustments](https://publish.obsidian.md/slrvb-docs/ITS+Theme/Image+Adjustments) to resize the images into smaller squares.

The second row is just links to notes.

I make use of `\` before special characters like '|'. This is called escaping and basically means I don't want the tool to use the `|` as part of the table. I am `escaping` the `|` with a `\` to tell the tool that it should ignore the pipe for it's current expectation and instead allow it to be used for it's normal purpose.

```
| ![[Imagename1.png\|hsmall+wsmall+center]] | ![[Imagename2.png\|hsmall+wsmall+center]] | ![[Imagename3.png\|hsmall+wsmall+center]]         | ![[Imagename4.png\|hsmall+wsmall+center]] | 
| ---------------------------------- | --------------------------- | ----------------------------------- | ------------------------ |
| [[Notename1]]                         | [[Notename2]]       | [[Notename3]] | [[Notename4\|Rename Note Name]]                        |
```

## Player Dataview Tables

You can learn how to make this over here: [Dataview - List Party Members](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Plugin+Tutorials/Community+Plugins/Dataview/Dataview+-+List+Party+Members)

## Right Hand Table - Session Journals

You can learn how to make this over here: [Dataview - List Session Journals](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Plugin+Tutorials/Community+Plugins/Dataview/Dataview+-+List+Session+Journals)

## Recently Modified Notes

You can learn how to make this over here: [Dataview - List Recently Modified Notes](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Plugin+Tutorials/Community+Plugins/Dataview/Dataview+-+List+Recently+Modified+Notes)

## Recently Modified NPCs

You can learn how to make this over here: [Dataview - List Recently Modified NPCs](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Plugin+Tutorials/Community+Plugins/Dataview/Dataview+-+List+Recently+Modified+NPCs)

## Recently Modified Locations

You can learn how to make this over here: [Dataview - List Recently Modified Locations](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Plugin+Tutorials/Community+Plugins/Dataview/Dataview+-+List+Recently+Modified+Locations)

# Reference Front Matter 

## Inline Expressions

Frontmatter can also be useful in your notes. You can store values in your Frontmatter and call those values into your notes. These are called Inline Expressions.

```
---
Player: Bob
Class: Warrior
Race: Gnome
Level: 5
---
 
# `=this.Player`
`=this.Player` is a `=this.Race` `=this.Class` who is level `=this.Level`. 
```

If you copy this into a note with Dataview enabled then the text should render like this.

![Pasted image 20230530204652.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230530204652.png)

As you can see it's rather easy to pull data from your current notes frontmatter.

```
`this.FrontMatterName`
```

You can also pull frontmatter from other notes like this:

```
`=NoteName.FrontMatterName`
```

# Faction Reward Tracker 

## Example Output

![Pasted image 20250213210409.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020250213210409.png)

## Faction Note

Add this to the properties of your Faction Notes.

```
---
faction: "Faction Name"
benefits:
  - standing: 1
    reward: "What do they get at level 1?"
  - standing: 2
    reward: "What do they get at level 2?"
  - standing: 3
    reward: "What do they get at level 3?"
---

```

## Player Note or Party Note

Add this to the properties of your Player or Party Note(s).

Update the folder location so that it points to the folder where you keep your Faction notes.  
The Faction Names need to match the names of the Factions used in the Faction Notes.

````
---
name: "Player Name"
faction_standing:
  "Faction Name 1": 1
  "Faction Name 3": 2
  "Faction Name 3": 3
---

```dataviewjs
const player = dv.current();
const factions = dv.pages('"ParentFolder/FactionFolder"');

let tableData = [];

for (let faction of factions) {
    let factionName = faction.faction;
    let playerStanding = player.faction_standing?.[factionName] || 0;

    // Ensure benefits is treated as an array
    let benefitsList = Array.isArray(faction.benefits) ? faction.benefits : [];

    // Filter benefits the player qualifies for
    let qualifiedBenefits = benefitsList
        .filter(b => playerStanding >= b.standing)
        .map(b => b.reward)
        .join(", "); 

    tableData.push([factionName, playerStanding, qualifiedBenefits || "No benefits yet"]);
}

dv.table(["Faction", "Your Standing", "Benefits"], tableData);

```
````

## List Random Notes

This will return random notes from your vault.

Change the WHERE section to contains rules about the notes you want to contain.

````
``` dataview
TABLE 
    file.name, tags, cost, weight
FROM ""
WHERE 
    SourceType = "Magic Item" AND contains(tags, "uncommon")
FLATTEN 
    date(now) as Now 
FLATTEN 
    (file.mtime.year + file.mtime.hour + file.mtime.day + file.mtime.hour + file.mtime.minute + file.mtime.second + file.size + Now.hour + Now.minute + Now.second) * 15485863 as Hash 
FLATTEN 
    ((Hash * Hash * Hash) % 2038074743) / 2038074743 as Rand 
WHERE 
    max(Rand)
SORT 
    Rand
LIMIT 
    10
```
````

![Obsidian_lG27LsudDf.gif](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Obsidian_lG27LsudDf.gif)

# Progress Bar on Tasks 

You can add a status bar to your notes that tracks progress of checkboxes within your current note.

![Obsidian_AaMCSaPjqL.gif](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Obsidian_AaMCSaPjqL.gif)

Copy the code below into a note.  
Update the 2x `"Test"`. Change these to `"YourNoteName"`

````
```dataviewjs
    (await dv.tryQuery('TASK FROM "Test" ')).values.length
    const Tasks = dv.page("Test").file.tasks
    
    let CompletedTasks = Tasks
        .where(t => t.completed)
    
    dv.span(
        "![progress](https://progress-bar.dev/"
        + parseInt((CompletedTasks.length / Tasks.length) * 100)
        + "/)"
    )
```

- [ ] Quest 1
- [ ] Quest 2
- [ ] Quest 3
- [ ] Quest 4
- [ ] Quest 5

````

Here is a variant:

![Obsidian_qRU5Pc9IwV.gif](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Obsidian_qRU5Pc9IwV.gif)

```
`$= const value = Math.round(((dv.current().file.tasks.where(t => t.completed).length) / (dv.current().file.tasks).length || 0) * 100); "<progress value='" + value + "' max='100'></progress>" + " " + value + "%"`

- [ ] Quest 1
- [ ] Quest 2
- [ ] Quest 3
- [ ] Quest 4
- [ ] Quest 5

```

