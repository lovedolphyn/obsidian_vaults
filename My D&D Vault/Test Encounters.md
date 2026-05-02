![[phandalin.webp|497]]
Brief overview of adventure from [[lost-mine-of-phandelver|Lost Mine of Phandelver]] with fake encounters below.

standard encounter 
```encounter
name: Example
creatures:
- 1: Goblin 
```

encounter table 
```encounter-table
name: Example 2
creatures: 
- Hobgoblin 

---

name: Example 3
creatures: 
- 3: Goblin 
```

inline encounter! This will be awesome to add into an adventure.
`encounter: 1d6: Goblin`

| 1d2 | Encounter                              |
| --- | -------------------------------------- |
| 5   | `encounter: 3: Hobgoblin, 1d5: Goblin` |
| 6   | `encounter: Dragon`                    |
^test-encounter

They list a way to exclude players from the list below, but "players - false" isn't working for me.
```encounter
name: Example 7
players: false 
creatures:
  - Ghoul 
```

However, you can add specific players by calling them out.
```encounter
players:
 - Lelu - Ginger
 - Alvyn - Christopher
```

You can even revise the stats of a monster using the encounter block: (creature name, hp, ac, initiative modifier, xp)
```encounter
creatures:
  - Goblin, 7, 15, 2
  - Goblin, 5, 10, 2, 25
```

Name your monsters 
```encounter
creatures:
  - [[Hobgoblin, Bob]]                 
  - [[Hobgoblin, Jim], 12, 13, 2, 25]  
```

Set monster as an ally. This doesn't add them to the player team, but does add an icon. To add monster to the player group, you will need to add the monster to the players list in the initiative tracker settings.
```encounter
creatures:
  - 2: Orc, ally
  - 3: Ghoul
```

Multiple encounters, neatly on the page
```encounter
name: Goblin Charge
creatures:
 - Hobgoblin
 - 3: Goblin

---

name: Goblin Camp
creatures:
 - 3: Hobgoblin
 - Goblin

```

Encounter table setup 
```encounter-table
name: Goblin Ambush
creatures:
- Goblin
- 2: Hobgoblin
- Bugbear

---

name: Bandit Attack
creatures:
- Bandit
- Bandit Captain

---

name: Undead Foes
creatures:
- 2: Skeleton
- Zombie
- Ghoul
```

