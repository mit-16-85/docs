# Markdown to PDF

## Command Line Parameters
```
pandoc input.md -o output.pdf \
  -V fontsize=11pt \
  -V geometry:top=10mm,bottom=10mm,left=10mm,right=10mm 
```

```
pandoc input.md -o output.pdf \
  -V fontsize=11pt \
  -V geometry:margin=10mm  
```

## Yaml Header in `.md`
```
---
fontsize: 11pt
geometry: top=10mm,bottom=10mm,left=10mm,right=10mm
---
```

```
---
fontsize: 11pt
geometry: margin=10mm
---
```

```
pandoc input.md -o output.pdf
```