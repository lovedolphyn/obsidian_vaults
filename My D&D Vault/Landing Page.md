Setup for a landing page:  

| Linked world map                                              | Current Campaign      | Current Adventure     | DM Tools       |
| ------------------------------------------------------------- | --------------------- | --------------------- | -------------- |
| ![[Entire-Sword-Coast-Map_HighRes.jpg\|hsmall+wsmall+center]] | (add pic here)        | (add pic here)        | (add pic here) |
| [[World Map - Northwest Faerun]]                              | (add sheet link here) | (add sheet link here) | [[DM Tools (test)]]   |

>[!infobox]
># Session Journals
>#### Insert Button Link Here `BUTTON[example-id]`
>```dataview 
>table without id link(file.name) as "Session", Status, players, OneLiner
>from ""
>where (type = "Session Journal")
>SORT file.name DESC 
>```

# Players 
```dataview
TABLE WITHOUT ID link(file.name) AS "character name", player, class, race, level, status  
from "3-The Party"
where (role = "player")
```

# Recently Modified Notes 
```dataview
table without id 
	link(file.path, file.folder + "/" + file.name) as "Note", 
	file.mtime as "Last Modified"
from ""
where file.mtime >= date(today) - dur(30 days)
and file.name != this.file.name
	and !contains(file.path, "zz_asset-files")
	and !contains(file.path, "z. Templates")
	and !contains(file.path, "daily notes")
sort file.mtime desc 
limit 10
```

A button test 
```meta-bind-button
label: +New
icon: ""
style: default
class: ""
cssStyle: ""
backgroundImage: ""
tooltip: Create new page
id: newpg
hidden: false
actions:
  - type: command
    command: workspace:new-tab
  - type: command
    command: file-explorer:new-file

```

Button test - create new daily note (aka Session Notes - saved in session folder). This button works, but I need to figure out how to get it loaded into a table.

```meta-bind-button
label: New Session Note
icon: ""
style: primary 
class: ""
cssStyle: ""
backgroundImage: ""
tooltip: Create new session note.
id: new-session
hidden: false
actions:
  - type: command
    command: workspace:new-tab
  - type: templaterCreateNote
    templateFile: "z. Templates/Session Template.md"
    folderPath: "0-Scratch Notes/Session Notes"
    fileName: "Session - "
    openNote: true
```



