Just change folder name:
```dataviewjs
const pdfFiles = app.vault.getFiles().filter(file => file.extension === 'pdf' && file.path.includes('World Source Books'))
dv.list(pdfFiles.map(file => dv.fileLink(file.path)))
```
