>[!tip] + This is using the "tip" markup and the pic is set to "right lp". 
>![[Redbrand-Hideout_DM_Map.jpg|right lp|400]]But make sure to add it next to some lines of text so it's easily edited from the live preview. Otherwise, you will need to go into source code to view it.


This is a data table that uses dataview. I don't know if I have these terms in my pages yet, so this will not display properly...just an example of a template.
```dataview
table key, key2, key3, key4
from #Tag3
```


This is an infobox table that will sit to the right of text once displayed in "reading mode". I don't  know if I have any of this in my pages yet, so this will not display properly...just an example of a template. "this.file.name" will only work if you have front matter stored at the beginning of the document. Not sure if I'm going to do this, so can be replaced with text instead when I create this template.

>[!infobox]
># `=this.file.name`
>![[Central Shadowdale.png|cover hsmall]]
>[[Central Shadowdale.pgn|Show To Players]]
>###### Geography
>Type | Stat |
>---|---|
>Location | `=this.location`
>Size | `=this.size` |
>Region | `=this.region` |
>###### Travel (`=[[Party Configuration]].TravelMethod`/`=[[Party Configuration]].HoursPerDay` hrs per day)
>###### [[Party Configuration]] / [[Exhaustion]]: `=[[Party Configuration]].ExhaustionLevel`
>Destination | Travel Days |
>---|---|
>[[Voonlar]] | Clock icon `=round(90 * ([[Party Configuration]].MinutesPerMile * choice([[Party Configuration]].ExhaustionLevel > 1, 2, 1)) / 60 / [[Party Configuration]].HoursPerDay, 1)`|
>[[TilvertonScar]] | Clock Icon `=round(160 * ([[Party Configuration]].MinutesPerMile * choice([[Party Configuration]].ExhaustionLevel > 1, 2, 1)) / 60 / [[Party Configuration]].HoursPerDay, 1)`|
>###### Politics 
>Type | Stat | 
>---|---|
>Government | `=this.politics` |
>Ruler | `=this.leader` |
>Alignment | `=this.alignment` |
>###### Society 
>Type | Stat |
>---|---|
>Races | `=this.races` |
>Population | `=this.population` |
>Religion | `=this.religion`
>###### Commerce 
>Type | Stat | 
>---|---|
>Exports | `=this.exports` |
>Imports | `=this.imports` |

Front Matter template to use the "this.file.name" or "this.time", etc. I've added quotations around this block so it doesn't become front matter on this page. I've also added text and numbers as examples. Remove these when creating the template.

"---
NoteType: (use your note type here)
tags: (use your tags here)
alias: (use other known aliases here)
location: Castle 
region:
size: Small city 
politics: Lordship 
leader: 
alignment: Chaotic Evil 
guildsgroups: (if you have multiple, just use a list)
 - Thieves Guild 1
 - Cult 1
 - Guiled 1
 population: 0
 races: 
  - Humans 
  - Elves 
  - Dwarves 
religion: Lathander 
exports: 
 - Something 
 - Another something 
imports: 
 - Something else 
 - Another something else 
---"

The following is front matter for an attack (spell). Remove quotes when creating the template.

"---
Name:
Level: 
CastingTime: 
Ritual: (true/false)
Range: 
Area: 
Components: 
Duration: 
School: 
AttackSave: 
DamageEffect: 
Classes: 
SpellSource: PHB 
Page: 0
---"

And here's the table:

>[!infobox|right]
># `=this.Name` 
>![[Conjuration.png|cover hsmall]]
>###### Stats 
>Type | Stat |
>---|---|
>Level | `=this.Level` |
>CastingTime | `=this.CastingTime` |
>Ritual? | `=this.Ritual` |
>Range |`=this.Range` |
>Area |`=this.Area` |
>Components |`=this.Components` |
>Duration | `=this.Duration` |
>School | `=this.School` |
>Attack/Save | `=this.AttackSave` |
>Damage/Effect | `=this.DamageEffect` |
>Classes | `=this.Classes` |

Example data table using dataview. I don't have this set up yet, so it won't display properly...just for reference.

```dataview
table, Name, Level, CastingTime, Range
where School = "Conjuration"
```







