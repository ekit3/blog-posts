---
layout: default-template
title:  "Abstract Data Types"
date:   2023-03-15 9:00:00 +0200
categories: Common
author: [florian_barbet]
excerpt_separator: <!--END_SUMMARY-->
---

##### Les types abstraits, ou pourquoi vous devez utiliser Optional

En tant que développeur, nous cherchons souvent des moyens d’améliorer nos applications. Les rendre plus robustes, plus normées, ou encore anéantir les potentiels effets de bord. La montée des langages fonctionnels a pu faire réapparaître certains concepts mathématiques pour améliorer tout ça.
C’est le cas des types abstraits (en anglais, abstract data type ou ADT). Au-delà des gains cités, certains ADT permettent d’améliorer la gestion de certains langages.<br/>

![image](henry_1.png)<br/>

L’illustre Henri, qui aime tant les mathématiques, semble être très intéressé par le sujet, mais surtout parce qu’il existe un ADT pour optimiser [son application du plus fort cailloux](https://ekite.tech/articles/front-end/algebraic-structure/). Cela permettra d’illustrer les explications qui suivent.
<!--END_SUMMARY-->

##### Définitions

Pour créer un type de donnée il faut réunir un ensemble de valeurs et des opérations à appliquer sur cet ensemble. On peut prendre exemple sur les nombres entiers (int, integer).
Il est possible d’appliquer une multitude d’opérations sur les entiers : additions, soustractions, multiplications, etc.

Une des analogies les plus reprises en informatique des types de données sont les primitives, comme les entiers, les booléens, ou les float par exemple.
N.B : Les types primitifs sont nativement gérés par le langage, qui stocke directement les valeurs des variables en mémoire, parfois dans une zone mémoire dédiée (la stack).

L’évolution d’un type de donnée, ce sont les types de données définis par utilisateur. Pour vulgariser il s’agit d’une structure nommée et composée de type de données. Il est possible de les représenter par des structures, des énumérations ou encore des unions. Pour illustrer la représentation d’un point est un type de données définies par utilisateur : Point(int x, int y).

Les types de données défini par utilisateur ne sont pas définis par la machine contrairement aux primitives. Les opérations sous-jacentes de ce type de données sont elles aussi définies par l’utilisateur (le développeur).

Un type abstrait peut être représenté comme le moule d’un type de données définis par utilisateur à la différence près que ce type doit amener une certaine robustesse dans l’écriture de types. 
Ce type de données doit répondre à trois contraintes pour subsister dans un système de type. Il doit être capable de définir des types sommes, produits et récursifs.

##### Pré-requis du système de type pour faire des ADT

1 - Le type somme (tagged-union, variant) c’est la capacité de définir un type pouvant se définir par un sous-ensemble fini de types. En Java cela correspond aux sealed-interface, en OCaml ce sont les variants, en Rust les enum.
Exemple en OCaml : 

```
 type month_type = 
  | PLEIN 
  | CREUX 
  | BIS of int
```

2 - Le type produit (record) correspond à la capacité de créer des structures dans un langage. En Java, on peut créer des objets ou des records, en Rust ou en C on peut créer des structures (struct).

3 - Le type récursif correspond à la capacité pour un type de s’appeler lui-même. 
Exemple avec les variants : 

```
 type List = 
  | Item of int * List
  | Empty

Item (1, Item (2, Item ( 3, Empty)))
```

Voici une liste de quelques langages permettant de faire des ADT : 
* Caml
* Rust
* Haskell
* Java 17+
* Typescript
* Python
* Scala
* Kotlin

##### Cas d’utilisations

Les types de données abstraits permettent d’acquérir de la robustesse applicative ET conceptuelle. Cela permet également de pouvoir créer des [design pattern](https://ekite.tech/articles/other/design-pattern/) purs et de simplifier la mise en place de machine à état.
Enfin les ADT permettent de rapprocher les données d’un programme lié aux [structures algébriques](https://ekite.tech/articles/front-end/algebraic-structure/).

Voici une liste de quelques types abstraits connus, liés aux structures algébriques: 
* La présence de valeur (Option)
* La réussite d’un programme (Try)
* La réussite ou l’erreur d’un programme (Result)
* La possibilité d’afficher une donnée (Show)

Henri a préparé quelques cartes que vous pourrez trouver [ici](https://docs.google.com/presentation/u/0/d/1P06bSfyXNix0k740iRl1LyyqNyRibcAOsTWn9lomjUo/edit) !

##### La parole à Henri

Henri nous rappelle que son application a été codée en Java 17.
La gestion d’erreur dans certains langages peut-être très gourmande en termes de ressources. Ce [lien](https://www.infoworld.com/article/2076868/how-the-java-virtual-machine-handles-exceptions.html) explique en détails le bytecode derrière un try-catch. Pour résumer, lorsqu'une exception survient il faut pouvoir dire à la machine de revenir en arrière et exécuter le code dans la partie “catch”.
Plusieurs années se sont écoulées depuis et Henri trouve que son application est obsolète
Il demande à son ami de faire évoluer son application, mais se retrouve depuis quelques temps confronté à une multitude de problème qu’il ne comprend pas :

```
    java.lang.IllegalArgumentException: D20160229 is not a Caillou
```

![image](henry_2.png)

Henri est venu nous voir en nous expliquant qu’il a ce problème à chaque fois qu’il enregistre un de ses cailloux un 29 février. Cela fait déjà 6 ans qu’Henri n’arrive pas à enregistrer son caillou préféré.
Prenons notes de l’existant :
* Les fonctionnalités sont rétro-compatibles avec l’ancien modèle.
* La structure de données d’un caillou a changé comme suit : 
    * Un caractère et 8 chiffres.
Nous décidons de corriger l’ensemble tel qu’il soit constitué d’un caractère et d’une date au format yyyyMMdd. (Cela corrigera en parti les problèmes de la nouvelle application d’Henri)
Nous ne pouvons donc plus nous fier à l’ensemble CPH (Cailloux Potentiels d’Henri), nous sommes sur un ensemble différent que nous nommerons NCPH (Nouveaux Cailloux Potentiels d’Henri) .
Notons que cet ensemble est composé de l’ensemble CPH et de toute chaîne de caractères avec les caractéristiques susmentionnées (nommons cet ensemble CPGH pour Cailloux Potentiels du Grand Henri). On obtient donc CPGH = CPH + NPCH.

![image](henry_3.png) <br/>

Malgré notre précédente correction Henri nous a remonté qu’il subsiste quelques lenteurs et nous fait part de ses besoins :<br/>
1 - Il veut pouvoir basculer sur son ancien modèle à tout moment.<br/>
2 - Faire en sorte que son application ne subisse plus de lenteurs / erreurs incompréhensibles.<br/>
Pour le premier point nous verrons une prochaine fois l’application de la théorie des catégories (plus particulièrement la flèche).
Pour le second ça tombe bien, car nous avons investigué et sommes tombé sur quelques imbrications de try-catch dignes d’une [bonne programmation défensive](https://en.wikipedia.org/wiki/Defensive_programming). Cela s’explique par le fait de devoir convertir les éléments de CPH vers CPGH.
/!\ N’oublions pas qu’Henri procède à des millions d'enregistrements de cailloux par jour. 

La solution au problème ![image](henry_4.png) <br/>

```java
static Result<Caillou, Exception> create(String name){
    var letter = name.charAt(0);
    if(letter < 65 || letter > 90) {
        throw new IllegalArgumentException(format("%s is not a Cailloux", name));
    }

    var dayOfYear = Integer.parseInt(name.substring(1));
    if(dayOfYear < 0 || dayOfYear > 365) {
        throw new IllegalArgumentException(format("%s is not a Cailloux", name));
    }

    return new Caillou(letter, dayOfYear);
}

void handleCreate(String input){
    try {
        var result = create(input);
        doSomethingWithCaillou(result);
    }catch(Exception error){
    log(error);
    }
}
```
(L'ancien code.)

Ces imbrications nous privent de précieuses performances. Une des solutions à ce problème c’est l’ADT Result. 
Malheureusement pour Henri en Java 17 il n’existe pas d’implémentation de Result. Cependant il y a eu une grande avancée permettant de créer ce genre de typage :
* Les interfaces scellées
* Les records
* Le switch-pattern-matching
Voici comment on pourrait représenter le Result en Java 17 

```java
sealed interface Result<T,E> permits Result.Ok, Result.Err {
    record Ok<T,E>(T ok) implements Result<T,E> {
        public Ok {
            java.util.Objects.requireNonNull(ok);
        }
    } 
    record Err<T,E>(E error) implements Result<T,E> {
        public Err {
            java.util.Objects.requireNonNull(error);
        }
    }
    public static<T> Ok ok(T ok){
        return new Ok(ok);
    }
    public static<E> Err err(E error){
        return new Err(error);
    }
}
```
(source: [Thomas Haesslé](https://oteku.github.io/))


Voici comment Henri l’utilise aujourd’hui 
```java
static Result<Caillou, Exception> create(String name){
    var letter = name.charAt(0);
    if(letter < 65 || letter > 90) {
        return Result.err(new IllegalArgumentException(format("%s is not a Cailloux", name)));
    }

    var dayOfYear = Integer.parseInt(name.substring(1));
    if(dayOfYear < 0 || dayOfYear > 365) {
        return Result.err(new IllegalArgumentException(format("%s is not a Cailloux", name)));
    }

    return Result.ok(new Caillou(letter, dayOfYear));
}

void handleCreate(String input){
    switch (create(input)){
        case Result.Err<Caillou, Exception> result -> log(result.error);
        case Result.Ok<Caillou, Exception> result -> doSomethingWithCaillou(result.ok);
    }
}
```
(Le nouveau code)

![image](henry_5.png) <br/>

Maintenant Henri est heureux, il propose pour conclure quelques cartes pour mémoriser certains ADT et leurs particularités.


Sources
* [https://en.wikipedia.org/wiki/Tagged_union](https://en.wikipedia.org/wiki/Tagged_union)
* [https://fr.wikipedia.org/wiki/Structure_de_donn%C3%A9es](https://fr.wikipedia.org/wiki/Structure_de_donn%C3%A9es)
* [https://fr.wikipedia.org/wiki/Type_abstrait](https://fr.wikipedia.org/wiki/Type_abstrait)
* [https://dev.realworldocaml.org/variants.html](https://dev.realworldocaml.org/variants.html)
* [https://jpintelli.com/2020/12/28/adt-with-java-sealed-classes-pattern-matching-records/](https://jpintelli.com/2020/12/28/adt-with-java-sealed-classes-pattern-matching-records/)
* [https://en.wikipedia.org/wiki/Record_(computer_science)](https://en.wikipedia.org/wiki/Record_(computer_science))
* [https://fr.wikipedia.org/wiki/Type_r%C3%A9cursif](https://fr.wikipedia.org/wiki/Type_r%C3%A9cursif)
* [https://blog.shangjiaming.com/vavr-introduction/](https://blog.shangjiaming.com/vavr-introduction/)
* [https://www.vavr.io/](https://www.vavr.io/)
* [https://v2.ocaml.org/manual/gadts-tutorial.html](https://v2.ocaml.org/manual/gadts-tutorial.html)
* [https://cs.wellesley.edu/~cs251/s12/handouts/modules.pdf](https://cs.wellesley.edu/~cs251/s12/handouts/modules.pdf)
* [https://medium.com/@aoturan/commonly-used-abstract-data-types-d9470b14f864](https://medium.com/@aoturan/commonly-used-abstract-data-types-d9470b14f864)
