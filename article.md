---
title: |
  "Introduction to Python modules."
date: May, 2022
lang: en-EN
urlcolor: blue
geometry: "left=2.5cm,right=2.5cm,top=3cm,bottom=3cm"
documentclass: article
fontfamily: Alegreya
header-includes: |
    \usepackage{fancyhdr}
    \pagestyle{fancy}
    \fancyhf{}
    \rhead{Dakar Institute of Technology}
    \lhead{Patrick Nsukami}
    \rfoot{Page \thepage}
    \hypersetup{pdftex,
            pdfauthor={Patrick Nsukami},
            pdftitle={Introduction to Python programming},
            pdfsubject={Introduction to Python programming},
            pdfkeywords={Python, Programming},
            pdfproducer={Emacs, Pandoc, Latex, Markdown},
            pdfcreator={Emacs, Pandoc, Latex, Markdown}}
    
---

# C'est quoi un "descriptors"
# Pourquoi l'utilise t-on ?
# Comment l'utiliser ?
# Pour aller plus loin ....

foo bar baz

```python
# module foo.py

a = 42

def bar(x):
    print(x)
  
class Ten :
    def __get__(self,obj,objtype=None):
        return 10
class A :
    x = 5
    y = Ten()

a=A()
print(a.x)
print(a.y)
```
