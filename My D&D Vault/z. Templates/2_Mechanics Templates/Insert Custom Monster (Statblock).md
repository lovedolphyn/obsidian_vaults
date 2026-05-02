This one is from Fantasy Statblocks:
```statblock
layout: Basic 5e Layout
image: 
name: 
size: 
type: 
subtype: 
alignment: 
ac: Number
hp: Number
hit_dice: 
speed: 
stats: 
fage_stats: 
saves:
  - dash: 
  - potato: 
  - stew: 
skillsaves:
  - fake-skill: 
  - turtle: 
damage_vulnerabilities: 
damage_resistances: 
damage_immunities: 
condition_immunities: 
senses: string
languages: string
cr: number
spells:
  - 
  - 
  -  
traits:
  - name: 
    desc: 
  - name: 
    desc: 
actions:
  - name: 
    desc: 
  - name: 
    desc: 
legendary_actions:
  - name: 
    desc: 
  - name: 
    desc: 
bonus_actions:
  - name: 
    desc: 
  - name: 
    desc: 
reactions:
  - name: 
    desc: 
  - name: 
    desc: 
```


This one is from a video by Josh Plunkett 2024:
```statblock
name: string
size: string
type: string
subtype: string
alignment: string
ac: number
hp: number
hit_dice: string
speed: string
stats: [number, number, number, number, number, number]
fage_stats: [number, number, number,number, number, number, number, number, number]
saves:
  - <ability-score>: number
skillsaves:
  - <skill-name>: number
damage_vulnerabilities: string
damage_resistances: string
damage_immunities: string
condition_immunities: string
senses: string
languages: string
cr: number
spells:
  - <description>
    <spell level>; <spell-list>
traits:
  - [<trait-name>, <trait-description>]
  - ...
actions:
  - [<actions-name>, <actions-description>] 
  - ...
legendary_actions:
  - [<legendary_actions-name>, <legendary_actions-description>] 
  - ...
reactions:
  - [<reaction-name>, <reaction-description>] 
  - ...
```
