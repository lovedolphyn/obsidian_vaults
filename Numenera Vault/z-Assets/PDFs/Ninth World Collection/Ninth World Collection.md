# Ninth World Collection Overview
 
```dataviewjs
const pdfFiles = app.vault.getFiles().filter(file => file.extension === 'pdf' && file.path.includes('Ninth World Collection'))
dv.list(pdfFiles.map(file => dv.fileLink(file.path)))
```
 
