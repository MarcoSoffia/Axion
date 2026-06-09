
Ruolo:: 
Area:: 

## Task assegnati

```dataview
TASK
FROM "CYBESECURITY/Learn-By-Project"
WHERE !completed
WHERE assignee = this.file.link OR contains(assignee, this.file.link)
SORT file.name ASC
```

## Task completati

```dataview
TASK
FROM "CYBESECURITY/Learn-By-Project"
WHERE completed
WHERE assignee = this.file.link OR contains(assignee, this.file.link)
SORT file.name ASC
```
