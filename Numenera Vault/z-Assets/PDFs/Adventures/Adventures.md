# Adventures Overview
 
```dataviewjs
const pdfFiles = app.vault.getFiles().filter(file => file.extension === 'pdf' && file.path.includes('Adventures'))
dv.list(pdfFiles.map(file => dv.fileLink(file.path)))
```
 
