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


# Introduction

Nous savons tous la liaison entre une classe et un objet

```Python

class Cercle():  # definition de ma classe Cercle

    PI = 3.14
    def __init__(self,rayon) :
        self.rayon = rayon

mycercle=Cercle(2) # j'instancie un object de la classe Cercle
print(mon_cercle.rayon) # Affiche le rayon du cercle
print(mon_cercle.PI) # Affiche la constante PI=3,14

```
Quand est-il de la liasion entre l'attribues d'un object et celui d'une classe

## Comment acceder à l'attribut d'un OBJECT

Quand on voulait afficher le rayon de l'object "mon_cercle" on a juste écrit mon_cercle.rayon. ceci ne fait que
renvoyer une valeur stocké dans un dictionnaire de l'object.

Comme on peut le vérifier à traver le code suivant

```Python

print(mon_cercle.__dict__)

```

## Class attribute access

Cependant, de la même manière on pouvait accéder à l'attribut directement au niveau de la class.
Cet attribut est enregistré dans un dictionnaire cet fois ci de la classe.

```Python
print(Cercle.PI)
print(Cercle.__dict__)
print(mon_cercle.PI)

```

Parfois les attributs ne sont pas suffisants. Nous avons besoin de procédés plus puissant. Regardons ensemble 
une des limites des attributs.

```Python
class Circle():
    PI = 3.14
    def __init__(self,radius):
        self.radius = radius
        self.circumference = 2*radius*self.PI

mycircle = Circle(2)
# Affichons la circonférence du cercle 
print(mycircle.circumference)
# Changeons le rayon à 3 au lieu de 2

mycircle.radius = 3
# Affichons encore la circonférence du cercle
print(mycircle.circumference) # Oops la circonférence ne change pas 

```
### Heureusement la magie des @property peut nous sauver
A l'aide de la magie des décorateurs on sait comment contourner le problème.

```Python
class Circle():
    PI = 3.14
    def __init__(self,radius):
        self.radius = radius
 #Super @property nous sauve la vuie
    @property
    def circumference(self):
        return 2*self.radius*self.PI

mycircle = Circle(2)
print(mycircle.circumference)
mycircle.radius = 3
print(mycircle.circumference) # Fixed!
```
Ainsi, On peut ajouter des getters et des setters dans notre classe pour garder nos attributs aussi simple que possibles
tout en intégrant des propriétés super puissantes.
Cependant, savez vous comment ça fonctionne réellement
Aussi, est-ce toujour suffisant pour faire le travail proprement ?


# C'est quoi un "descriptor"

Un "descriptor" est tout object dans lequel est implémenté au moins une de ces méthodes à savoir __get__, __set__ ou __delete__.
On appelle "data-descriptor"  un object qui implémente à la fois __get__ et __set__.

## C'est quoi un desciptor protocol ?

Ce qu'il faut retenir est quand vous appelez un attribut "foo" de votre object "obj" à travers la méthode obj.foo, python suit un protocole bien 
defini et bien hierarchisé pour retrouvé l'attribut en question. En effet, il commence par 

    1. chercher Le résultat de la propriété du même nom si elle est définie
    2. ou voir si la valeur correspondante existe dans obj.__dict__
    3. ou bien il va remonter dans la hierarchie pour chercher dans le type(obj).__dict__
    4. répéter ces étapes pour chaque type dans le mro (methode resolution order : montre la chaine d'héritage ) si votre class a héritée d'autre classes jusqu'à ce qu'il trouve une correspondance
    5. Si c'est une affectationn, ça crée toujours une entrée dans obj.__dict__
    6. Sauf s'il y avait une propriété setter auquel cas vous appelez une fonction.



Pour résumé ici lorsque nous  accédons aux attributs dans de cette façon, ce qui se passe, c'est que python recherche les valeurs de ceux-ci dans le dictionnaire d'instances, en fait, nous pouvons jeter un œil à l'instance dictionnaire si nous devions taper obj.__dict__". 

## Comment écrire un descriptors

De manière simple le "descriptor" s'écrive comme suit :

```Python
descr.__get__(self,obj,type=None)-->value
descr.__set__(self,obj,value)-->None
descr.__delete__(self,obj)-->None

```

Ecrivons notre premier descriptor :

```Python

class MyDescriptor():
    def __get__(self,obj,type):
        print(self, obj, type)
    def __set__(self,obj,val):
        print("Got %s" %val)

class Myclass():
    x = MyDescriptor() # On vient d'instancier notre premier descriptor ): ,

```
Le desripteur est très pratique ça nous permet d'interagir avec notre attribut à l'aide de fonctions pratiques.

```Python

obj= Myclass()

print(obj.x) # un appel de fonction se cache ici

print(Myclass.x) # et ici!

obj.x=4  # ici aussi

```


## Plus de détails sur la signatures des descriptors :

  - self est l'instance du descriptor
  - obj est l'instance de l'object pour qui le descripteur est attaché
  - type est le class avec qui le descriptor est attaché
  - __get__ peut être appelé à travers la class ou  l'objet, __set__  peut être appelé seulement à travers l'objet


# Pourquoi l'utilise t-on ?
# Comment l'utiliser ?
# Pour aller plus loin ....


