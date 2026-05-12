# Maps Overview
 
```dataviewjs
const pdfFiles = app.vault.getFiles().filter(file => file.extension === 'pdf' && file.path.includes('Maps'))
dv.list(pdfFiles.map(file => dv.fileLink(file.path)))
```
 
