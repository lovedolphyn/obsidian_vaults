This is the template I use for a new NPC. Each section of the template is broken down below for your understanding.

Example

````
---
AssociatedGroup: 
Gender: 
Race: 
Age: 
Class: 
Alignment: 
Character-Role: 
Location: 
NoteIcon: npc
---

<% tp.file.title %>
<% await tp.file.move("/2. Mechanics/Non-Player Characters/" + tp.file.title) %>

<%*
const hasTitle = !tp.file.title.startsWith("NewNPC");
let title;
if (!hasTitle) {
    title = await tp.system.prompt("Enter NPC Name");
    await tp.file.rename(title);
} else {
    title = tp.file.title;
}
_%>

> [!infobox]
> # `=this.file.name`
> ![[z_Assets/Misc/ImagePlaceholder.png|cover hsmall]]
> [[z_Assets/Misc/ImagePlaceholder.png|Show To Players]]
> ###### Basic Information
> Type |  Stat |
> ---|---|
> Home | `=this.Location` |
> Group | `=this.AssociatedGroup` |
> Sex | `=this.gender` |
> Race | `=this.race` |
> Age | `=this.age` |
> Condition | Healthy |
> ###### Rules Info
> Type |  Stat |
> ---|---|
> Alignment | `=this.alignment` |
> Class | `=this.class` |
> Character Role | `=this.character-role` |

# `=this.file.name`
## Profile

<% tp.file.cursor() %>
**<Add description here, extend it with AI Text Generator using Ctrl J>**

> [!info] Statblock
> ```statblock
> name: Individual
> monster: Commoner
> columns: 1
> ```

```encounter-table
name: Individual
creatures:
 - 1: Commoner
```
````

### Front Matter

```
---
AssociatedGroup: Name of Guild or Group they belong to
Gender: Male or Female or... 
Race: Human, Dwarf, Elf, etc
Age: How old are they?
Class: Warrior or Wizard or ... 
Alignment: Are they Chaotic Neutral or Lawful Neutral
Character-Role: Are they a friend or foe?
Location: What is the name of the place they live?
NoteIcon: npc
---
```

For the most part this is just generic information that I like to associate with each npc. There are a few options here that are more useful than others.

- **AssociatedGroup:** This is where I write the name of the Guild or Group that they belong to. This is used in the Group Template also where I use a Dataview Query to list all NPCs that belong to the specified group. It uses this fields and basically says list all notes where AssociatedGroup = GroupName.
- **Location:** As per above, by having the Location listed, it enables me to use Dataview in the Location notes to list all NPC's who live in the same location.
- **NoteIcon:** This is used with the [Supercharged Links](obsidian://show-plugin?id=supercharged-links-obsidian) plugin which basically changes links within notes to a specified format. I often use it to add little emojis before the links. A Location note will have a little 🏠in front of it and a character will have a 🧙🏽‍♂️. NoteIcon is the property that I use within the plugin and thus I have a setting that says where NoteIcon = npc then the link should have the 🧙🏽‍♂️ in front of it. It helps make links pop within my notes.

### Templater Code

This is scary looking code!

```
<% tp.file.title %>
<% await tp.file.move("/2. Mechanics/Non-Player Characters/" + tp.file.title) %>

<%*
const hasTitle = !tp.file.title.startsWith("NewNPC");
let title;
if (!hasTitle) {
    title = await tp.system.prompt("Enter NPC Name");
    await tp.file.rename(title);
} else {
    title = tp.file.title;
}
_%>
```

Basically this code is achieving two important things.

1. It moves the Note to the specified folder: `"/2. Mechanics/Non-Player Characters/"` You should update this folder path to match your own Vault and specify where you would like your NPC notes to go.
2. The second section prompts the user to name the NPC. It creates a little popup window titled 'Enter NPC Name' and the user can enter a name. You should update the `"NewNPC"` to match the original name of your Template Note and also the `"Enter NPC Name"` if you wish to change the text.

Note

This code only works when triggered using a button which is documented at the bottom of this page.

### Infobox (Right Hand Wiki Style Table)

This section of text will create a table that is aligned to the right of the note. This is commonly seen used in Wiki sites. For this to work you need to have the [ITS Theme](https://publish.obsidian.md/slrvb-docs/ITS+Theme/ITS+Theme) installed or be using the ITS Callout *.css. You can find the *.css [here](https://publish.obsidian.md/slrvb-docs/ITS+Theme/Callout+Adjustments) and check here for install instructions: [How To - Install Custom CSS](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Tutorials/Basic+Tool+Usage/How+To+-+Install+Custom+CSS)

There are quite a few references in this code that look like this: `=this.file.name`  
This is Dataview code that references front matter within the note. This line will pull in the Note Name and turn it into a title.  
This line `=this.AssociatedGroup` will display the value from the AssociatedGroup frontmatter.

I like to do this so that I only need to document something within the note once. For example, I add it to the frontmatter and it auto-populates through the rest of my note without the need to copy and paste the data.

You can learn more about Dataview and this type of use here: [Dataview - Reference Frontmatter Within Note](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Plugin+Tutorials/Community+Plugins/Dataview/Dataview+-+Reference+Frontmatter+Within+Note)

Example

```
[[z_Assets/Misc/ImagePlaceholder.png|Show To Players]]
```

Where you see `|Show To Players` in an image link that does not have a ! at the start. This is where I use the [Second Window](obsidian://show-plugin?id=image-window) plugin. It lets me right click on an image link that is not rendered (that's why there is no ! at the start) and select `Open In New Window`. I use the [Second Window](obsidian://show-plugin?id=image-window) in place of the native multi-window support because it automatically maximises the images to the size of the window which is much better for showing the players.

````
```
> [!infobox]
> # `=this.file.name`
> ![[z_Assets/Misc/ImagePlaceholder.png|cover hsmall]]
> [[z_Assets/Misc/ImagePlaceholder.png|Show To Players]]
> ###### Basic Information
> Type |  Stat |
> ---|---|
> Home | `=this.Location` |
> Group | `=this.AssociatedGroup` |
> Sex | `=this.gender` |
> Race | `=this.race` |
> Age | `=this.age` |
> Condition | Healthy |
> ###### Rules Info
> Type |  Stat |
> ---|---|
> Alignment | `=this.alignment` |
> Class | `=this.class` |
> Character Role | `=this.character-role` |
```
````

### Note Body

My note body consists of a few elements.

````
# `=this.file.name`
## Profile

<% tp.file.cursor() %>
**<Add description here, extend it with AI Text Generator using Ctrl J>**

> [!info] Statblock
> ```statblock
> name: Individual
> monster: Commoner
> columns: 1
> ```

```encounter-table
name: Individual
creatures:
 - 1: Commoner
```
````

# `=this.file.name` - This will create a heading within my note that matches the name of the Note. Because my note is named after the NPC I end up with `# NPC Name`.

`<% tp.file.cursor() %>` - This is Templater code and should place the mouse cursor on this line once the template is created.

The following section adds a basic [Fantasy Statblock](obsidian://show-plugin?id=obsidian-5e-statblocks) into the note. It's for a Commoner but I change this to match the npc if I want something more specific. You can see that I have placed the statblock inside of a Callout. This is to allow the statblock to align next to the ITS Infobox documented above. Without the callout you will find the statblock will render at the bottom of the ITS Infobox leaving a large chunk of blank space on the note.

```
> [!info] Statblock
> ```statblock
> name: Individual
> monster: Commoner
> columns: 1
> ```
```

The final section is a [Initiative Tracker](obsidian://show-plugin?id=initiative-tracker) encounter block. It's also pointing towards the Commoner statblock. I change the Commoner to something else if I want the npc to have a different statblock. This section is here so that I can add the npc to the combat tracker if my players decide combat is the better solution to the current situation.

````
```encounter-table
name: Individual
creatures:
 - 1: Commoner
```
````

### Button To Trigger Template

![left](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Obsidian_p7HuWliDzL.gif)  
Instead of using the Templater hotkey to trigger this template I use a button on my DM Board note. The DM Board note is dragged into the left hand pane so that it's always available as a tab should I need it.

You will need the [Buttons](obsidian://show-plugin?id=buttons) plugin and [Templater](obsidian://show-plugin?id=templater-obsidian) plugin.

Then copy this code into your note.

````
```button
name New NPC
type note(NewNPC, split) template
action TemplateNPC
templater true
```
^button-NewNPCID
````

`name New NPC` This is the name that displays on the button. You can change `New NPC` to meet your own needs.  
`action TemplateNPC` This is the action occurs when the button is clicked. `TemplateNPC` needs to match the name of your template.

Within the Templater plugin I have Folder Templates setup like this.

![Pasted image 20230811000355.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230811000355.png)