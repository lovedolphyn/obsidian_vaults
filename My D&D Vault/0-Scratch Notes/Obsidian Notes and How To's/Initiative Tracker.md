**Plugin Link:** [Initiative Tracker](obsidian://show-plugin?id=obsidian-5e-statblocks)  
**Official Documentation:** [Official Documentation](https://plugins.javalent.com/initiative-tracker)

The Initiative Tracker plugin for **[Obsidian](https://obsidian.md/)** allows you to keep track of initiative and turn order during combat encounters in tabletop role-playing games.

With this plugin, you can add creatures and NPCs to the initiative tracker, and track their health, armor class, and other stats. The plugin also calculates experience points for creatures, and supports both custom and SRD creatures from the [Fantasy Statblocks](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Plugin+Tutorials/Community+Plugins/Fantasy+Statblocks) plugin.

![Obsidian_JUm8z9mMTh.gif](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Obsidian_JUm8z9mMTh.gif)

## Tutorials

Official Plugin Documentation

Initiative Tracker

Managing Parties

## Supplementing Plugins

[Fantasy Statblocks](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Plugin+Tutorials/Community+Plugins/Fantasy+Statblocks) and [Dice Roller](obsidian://show-plugin?id=obsidian-dice-roller)

## Character Configuration

You need to set your party members up so that they work in the Initiative Tracker plugin. The plugin requires some basic information for each character in order to work.  
`Settings > Community Plugins > Initiative Tracker > Players > Click + > Complete the form`

![Pasted image 20230713094825.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230713094825.png)

### Setup To Pull From Notes

Instead of manually configuring each player in the plugin settings you can also create a note for each player and then link the player to the note. Each player note should have the following [Front Matter](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Tutorials/YouTube+Series/Front+Matter+\(YAML\)+and+Tags/Front+Matter+\(YAML\)+and+Tags). The player name will default to the notes name.

```
---
level: 7
hp: 65
ac: 20
modifier: 4
---
```

## Party Configuration

Next you need to create a Party (or multiple parties perhaps) for your players to belong to.  
`Settings > Community Plugins > Initiative Tracker > Parties > Click + > Complete the form`  
You need to search for each player and then press the plus (+) button to save them to the party. Exit the form once everyone has been added.  
You should now set a party as the default.  
`Settings > Community Plugins > Initiative Tracker > Parties > Default Party > Select your Default Party`

## Encounters

Encounters can be added to notes by adding in an encounter block.

````yaml
```encounter
name: Encounter Name
creatures:
 - 1: Goblin
```
````

In preview mode this will look like this:

![Pasted image 20230713093207.png](https://publish-01.obsidian.md/access/36b98e212e9d73fe1bd4813f96b0fd71/z_Assets/Pasted%20image%2020230713093207.png)

You can click the Sword icon to begin a new encounter with these creatures or you can click the plus (+) button to add the creatures to the existing encounter.

Party Members

Party members are configured in the [Initiative Tracker](obsidian://show-plugin?id=initiative-tracker) Plugin settings.

I have these saved as Templates so that I can very quickly add the necessary syntax to a note when I want to use the plugin.  
In all cases the name of the monster needs to match the name of the Monster per your [TTRPG Statblocks](https://obsidianttrpgtutorials.com/Obsidian+TTRPG+Tutorials/Tutorials/YouTube+Series/TTRPG+Statblocks/TTRPG+Statblocks) configuration. The name needs to be exact so type `Goblin` not `Goblins` for example.

Insert Encounter

Insert Encounter Table

Insert Multiple Encounters

Insert Multiple Encounters Table

Insert Inline Encounter

Insert Random Encounter Table

### Encounter Builder

There is an encounter builder included with the Initiative Tracker plugin. Check this video out to learn how to use it. https://youtu.be/55kNaduWwVs
