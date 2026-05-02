This is the template I use for a new Settlement. Each section of the template is broken down below for your understanding.

```
---
NoteIcon: Settlement
Tags: Category/Settlement
Community-Size: Outpost
Alignment: Chaotic Evil
Government: Autocracy
type: Settlement
politics: Lordship
leader: 
guildsgroups:
 - Thieves Guild 1
 - Cult 1
 - Guiled 1
region: 
 - This area
 - Of this area
size: Small city
population: 0
commonraces:
 - Humans
 - Elves
 - Dwarves
religion:
 - Lathander
exports: 
 - Something
imports: 
 - Something Else
---

<% tp.file.title %>
<% await tp.file.move("/1. World/FR/Faerun/" + tp.file.title) %>

<%*
const hasTitle = !tp.file.title.startsWith("NewLocation");
let title;
if (!hasTitle) {
    title = await tp.system.prompt("Enter Settlement Name");
    await tp.file.rename(title);
} else {
    title = tp.file.title;
}
_%>


> [!infobox]
> # `=this.file.name`
> ![[z_Assets/Misc/MapPlaceholder.png|cover hsmall]]
> [[z_Assets/Misc/MapPlaceholder.png|Show To Players]]
> ###### Geography
> Type |  Stat |
> ---|---|
> Type | `=this.type` |
> Size | `=this.size` |
> Region | `=this.region` |
> ###### Travel (`=[[Party Configuration]].TravelMethod` / `=[[Party Configuration]].HoursPerDay` hrs per day)
> ###### [[Party Configuration]]  / [[Exhaustion]]:  `=[[Party Configuration]].ExhaustionLevel`
> Destination |  Travel Days  |
> ---|---|
> [[Voonlar]] | 🕓`= round(90 * ([[Party Configuration]].MinutesPerMile * choice([[Party Configuration]].ExhaustionLevel > 1, 2, 1)) / 60 / [[Party Configuration]].HoursPerDay, 1)` |
> ###### Politics
> Type |  Stat |
> ---|---|
> Govt Type | `=this.politics` |
> Ruler | `=this.leader` |
> Defense | `=this.defences` |
> ###### Organizations
> Type |  Stat |
> ---|---|
> Guilds & Groups | `=this.guildsgroups` |
> ###### Society
> Type |  Stat |
> ---|---|
> Population | `=this.population` |
> Races | `=this.commonraces` |
> Temples | `=this.religion`  |
> ###### Commerce
> Type |  Stat |
> ---|---|
> Exports | `=this.exports` |
> Imports | `=this.imports` |


# `=this.file.name`
## Overview
Placeholder

### Placeholder Map
![[z_Assets/Misc/MapPlaceholder.png|Placeholder Map]]
[[z_Assets/Misc/MapPlaceholder.png|open outside]]

### Placeholder Picture
![[z_Assets/Misc/ImagePlaceholder.png|Placeholder Picture]]
[[z_Assets/Misc/ImagePlaceholder.png|open outside]]

Placeholder

## Notable NPCs
Placeholder

## Profile
Placeholder

## Story
Placeholder

## Points of Interest
Placeholder

## Valuables
Placeholder

## Internal Relationships
Placeholder

## Outward Relationships
Placeholder

## Background
Placeholder

## Additional Details
Placeholder

`=this.region`


`=link(this.region)`
```

### Front Matter

```
---
NoteIcon: Settlement
Tags: Category/Settlement
Community-Size: Outpost
Alignment: Chaotic Evil
Government: Autocracy
type: Settlement
politics: Lordship
leader: 
guildsgroups:
 - Thieves Guild 1
 - Cult 1
 - Guiled 1
region: 
 - This area
 - Of this area
size: Small city
population: 0
commonraces:
 - Humans
 - Elves
 - Dwarves
religion:
 - Lathander
exports: 
 - Something
imports: 
 - Something Else
---
```

For the most part this is just generic information that I like to associate with each Settlement. There are a few options here that are more useful than others.

- **NoteIcon:** This is used with the [Supercharged Links](obsidian://show-plugin?id=supercharged-links-obsidian) plugin which basically changes links within notes to a specified format. I often use it to add little emojis before the links. A Location note will have a little 🏠in front of it and a character will have a 🧙🏽‍♂️. NoteIcon is the property that I use within the plugin and thus I have a setting that says where NoteIcon = npc then the link should have the 🧙🏽‍♂️ in front of it. It helps make links pop within my notes.
    
- **Tags:** I don't actually use Tags. It's shown here so that you know they can be used.
    

### Templater Code

This is scary looking code!

```
<% tp.file.title %>
<% await tp.file.move("/1. World/FR/Faerun/" + tp.file.title) %>

<%*
const hasTitle = !tp.file.title.startsWith("NewLocation");
let title;
if (!hasTitle) {
    title = await tp.system.prompt("Enter Settlement Name");
    await tp.file.rename(title);
} else {
    title = tp.file.title;
}
_%>
```

Basically this code is achieving two important things.

1. It moves the Note to the specified folder: `"/1. World/FR/Faerun/"` You should update this folder path to match your own Vault and specify where you would like your Settlement notes to go.
2. The second section prompts the user to name the Settlement. It creates a little popup window titled `Enter Settlement Name` and the user can enter a name. You should update the `"NewLocation"` to match the original name of your Template Note and also the `"Enter Settlement Name"` if you wish to change the text.

Note

This code only works when triggered using a button which is documented at the bottom of this page.

### Infobox (Right Hand Wiki Style Table)

This section of text will create a table that is aligned to the right of the note. This is commonly seen used in Wiki sites. For this to work you need to have the [ITS Theme](https://publish.obsidian.md/slrvb-docs/ITS+Theme/ITS+Theme) installed or be using the ITS Callout *.css. You can find the *.css [here](https://publish.obsidian.md/slrvb-docs/ITS+Theme/Callout+Adjustments) and check here for install instructions: [How To - Install Custom CSS](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Tutorials/Basic+Tool+Usage/How+To+-+Install+Custom+CSS)

There are quite a few references in this code that look like this: `=this.file.name`  
This is Dataview code that references front matter within the note. This line will pull in the Note Name and turn it into a title.

I like to do this so that I only need to document something within the note once. For example, I add it to the frontmatter and it auto-populates through the rest of my note without the need to copy and paste the data.

You can learn more about Dataview and this type of use here: [Dataview - Reference Frontmatter Within Note](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Plugin+Tutorials/Community+Plugins/Dataview/Dataview+-+Reference+Frontmatter+Within+Note)

Example

```
[[z_Assets/Misc/ImagePlaceholder.png|Show To Players]]
```

Where you see `|Show To Players` in an image link that does not have a ! at the start. This is where I use the [Second Window](obsidian://show-plugin?id=image-window) plugin. It lets me right click on an image link that is not rendered (that's why there is no ! at the start) and select `Open In New Window`. I use the [Second Window](obsidian://show-plugin?id=image-window) in place of the native multi-window support because it automatically maximises the images to the size of the window which is much better for showing the players.

```
> [!infobox]
> # `=this.file.name`
> ![[z_Assets/Misc/MapPlaceholder.png|cover hsmall]]
> [[z_Assets/Misc/MapPlaceholder.png|Show To Players]]
> ###### Geography
> Type |  Stat |
> ---|---|
> Type | `=this.type` |
> Size | `=this.size` |
> Region | `=this.region` |
> ###### Travel (`=[[Party Configuration]].TravelMethod` / `=[[Party Configuration]].HoursPerDay` hrs per day)
> ###### [[Party Configuration]]  / [[Exhaustion]]:  `=[[Party Configuration]].ExhaustionLevel`
> Destination |  Travel Days  |
> ---|---|
> [[Voonlar]] | 🕓`= round(90 * ([[Party Configuration]].MinutesPerMile * choice([[Party Configuration]].ExhaustionLevel > 1, 2, 1)) / 60 / [[Party Configuration]].HoursPerDay, 1)` |
> ###### Politics
> Type |  Stat |
> ---|---|
> Govt Type | `=this.politics` |
> Ruler | `=this.leader` |
> Defense | `=this.defences` |
> ###### Organizations
> Type |  Stat |
> ---|---|
> Guilds & Groups | `=this.guildsgroups` |
> ###### Society
> Type |  Stat |
> ---|---|
> Population | `=this.population` |
> Races | `=this.commonraces` |
> Temples | `=this.religion`  |
> ###### Commerce
> Type |  Stat |
> ---|---|
> Exports | `=this.exports` |
> Imports | `=this.imports` |
```

### Note Body

My note body consists of a few elements.

# `=this.file.name` - This will create a heading within my note that matches the name of the Note. Because my note is named after the NPC I end up with `# Settlement Name`.

`<% tp.file.cursor() %>` - This is Templater code and should place the mouse cursor on this line once the template is created.

### Button To Trigger Template

![left](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Obsidian_p7HuWliDzL.gif)  
Instead of using the Templater hotkey to trigger this template I use a button on my DM Board note. The DM Board note is dragged into the left hand pane so that it's always available as a tab should I need it.

You will need the [Buttons](obsidian://show-plugin?id=buttons) plugin and [Templater](obsidian://show-plugin?id=templater-obsidian) plugin.

Then copy this code into your note.

````
```button
name New Location
type note(NewLocation, split) template
action TemplateSettlement
templater true
```
^button-NewLocationID
````

`name New Location` This is the name that displays on the button. You can change `New Location` to meet your own needs.  
`action TemplateSettlement` This is the action occurs when the button is clicked. `NewLocation` needs to match the name of your template.

Within the Templater plugin I have Folder Templates setup like this.

![Pasted image 20230811000355.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230811000355.png)