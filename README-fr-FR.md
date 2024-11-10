# Typescript: Le guide essentiel

Ce guide fournit une vue d'ensemble de TypeScript à travers des explications claires et concises. L'ensemble des fonctionnalités de la dernière version du langage y est abordé, que ce soit son système de types ou ses fonctionnalités avancées. Si vous débutez ou si vous êtes un développeur expérimenté, ce livre est une ressource inestimable pour améliorer votre compréhension et votre maîtrise de TypeScript.

Ce livre est entièrement gratuit et open source.

Si ce projet vous a été utile et que vous souhaitez contribuer, vous pouvez soutenir mes efforts via PayPal. Merci !

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/donate/?business=QW82ZS956XLFY&no_recurring=0&currency_code=EUR)

## Traductions

Ce livre a été traduit en plusieurs langues, dont :

- [Chinois](https://github.com/gibbok/typescript-book/blob/main/README-zh_CN.md)
- [Français](https://github.com/gibbok/typescript-book/blob/main/README-fr-FR.md)


## Téléchargement

Vous pouvez télécharger la version Epub :

[https://github.com/gibbok/typescript-book/tree/main/downloads](https://github.com/gibbok/typescript-book/tree/main/downloads)

Une version en ligne est disponible:

[https://gibbok.github.io/typescript-book](https://gibbok.github.io/typescript-book)

## Table des matières:


## Introduction

Bienvenue dans Le guide essentiel de TypeScript ! Ce guide explique les connaissances essentielles et les compétences pratiques pour un développement TypeScript efficace. Découvrez les concepts et les techniques clés pour écrire un code propre et robuste. Que vous soyez débutant ou développeur expérimenté, ce livre est à la fois un guide complet et une référence pratique pour tirer parti de la puissance de TypeScript dans vos projets.

Ce livre documente TypeScript 5.2.

### À propos de l'auteur

Simone Poggiali est un développeur Front-end Senior expérimenté avec une passion pour  le coding depuis les années 90. 
Tout au long de sa carrière, il a contribué à de nombreux projets pour une large gamme de clients, des startups aux grandes organisations,
telles que HelloFresh, Siemens, O2 et Leroy Merlin.

Pour contacter Simone Poggiali, vous pouvez utiliser les liens suivants :


* LinkedIn: [https://www.linkedin.com/in/simone-poggiali](https://www.linkedin.com/in/simone-poggiali)
* GitHub: [https://github.com/gibbok](https://github.com/gibbok)
* X.com: [https://x.com/gibbok_coding](https://x.com/gibbok_coding)
* Email: gibbok.coding📧gmail.com


## Introduction à TypeScript

### Qu'est-ce que TypeScript ?

TypeScript est un langage de programmation à typage fort, basé sur JavaScript. 
Il a été initialement conçu par Anders Hejlsberg en 2012 et est actuellement développé et maintenu par Microsoft

Typescript compile en JavaScript et peut être exécuté dans n'importe quel environnement JavaScript (par exemple, un navigateur ou un serveur Node.js).

TypeScript prend en charge plusieurs paradigmes de programmation, fonctionnel, générique, impératif et orienté objet. 
TypeScript n'est ni un langage interprété ni un langage compilé.

### Pourquoi TypeScript ?

TypeScript est un langage à typage fort qui permet d'anticiper les erreurs de programmation courantes et d'éviter certains types d'erreurs lors de l'exécution

Un langage à typage fort permet au développeur de spécifier des contraintes et comportements dans les définitions de types de données, 
facilitant la correction automatique et la correction des défauts du code. 
Ceci est très utile avec les applications de grande taille.

Voici quelques-uns des avantages de TypeScript :

* Typage statique, à typage fort optionnel
* Inférence de type
* Accès aux fonctionnalités ES6 et ES7
* Compatibilité avec plusieurs plateformes et navigateurs
* Support des outils comme l'IntelliSense

### TypeScript et JavaScript

TypeScript est écrit dans des fichiers `.ts` ou `.tsx`, tandis que les fichiers JavaScript sont écrits dans des fichiers `.js` ou `.jsx`.

Les fichiers avec l'extension `.tsx` ou `.jsx` peuvent contenir la syntaxe JavaScript JSX, utilisée notamment avec React.

TypeScript est une sur-couche (superset) typée de JavaScript (ECMAScript 2015) en termes de syntaxe. 

L'ensemble du code JavaScript est valide en TypeScript, l'inverse n'est pas toujours vrai.

Par exemple, considérons une fonction dans un fichier JavaScript avec l'extension `.js` :
<!-- skip -->
```typescript
const sum = (a, b) => a + b;
```

Cette fonction peut être convertie et utilisée dans un fichier TypeScript en changeant l'extension du fichier en `.ts`. 
Cependant, si la même fonction est annotée avec des types TypeScript, elle ne peut pas être exécutée dans un environnement JavaScript sans compilation. 
Le code TypeScript suivant produira une erreur de syntaxe s'il n'est pas compilé :

<!-- skip -->
```typescript
const sum = (a: number, b: number): number => a + b;
```

TypeScript a été conçu pour détecter les potentielles exceptions qui peuvent survenir lors de l'éxécution, en demandant au développeur de définir des annotations de type. 
De plus, TypeScript peut détecter des problèmes si aucune annotation de type n'est fournie. 
Par exemple, le code suivant ne spécifie aucun type TypeScript :
<!-- skip -->
```typescript
const items = [{ x: 1 }, { x: 2 }];
const result = items.filter(item => item.y);
```

Dans ce cas, TypeScript détecte une erreur et signale :
```text
Property 'y' does not exist on type '{ x: number; }'.
```

TypeScript est fortement influencé par le comportement d'exécution de JavaScript. 

Par exemple, l'opérateur d'addition (+), qui en JavaScript peut soit effectuer une concaténation de chaînes, soit une addition numérique, est modélisé de la même manière en TypeScript :

```typescript
const result = '1' + 1; // En JavaScript, le résultat est égal à '11'
```

Les développeurs de TypeScript ont choisi de signaler les comportements inhabituels de JavaScript comme des erreurs. 

Par exemple, considérons le code JavaScript suivant :
<!-- skip -->
```typescript
const result = 1 + true; // En JavaScript, le résultat est égal à 2
```

TypeScript, cependant, signale une erreur :

```text
Operator '+' cannot be applied to types 'number' and 'boolean'.
```

Cette erreur se produit car TypeScript impose la compatibilité des types de manière stricte, et dans ce cas, identifie une opération invalide entre un nombre et un booléen.

### Génération de code TypeScript

Le compilateur TypeScript a deux roles : vérifier les erreurs de type et compiler en JavaScript. Ces deux processus sont indépendants l'un de l'autre. 
Les types n'affectent pas l'exécution du code dans un environnement d'exécution JavaScript, car ils sont complètement effacés lors de la compilation.
Le compilateur TypeScript est capable de générer du JavaScript même en présence d'erreurs de type.

Voici un exemple de code TypeScript avec une erreur de type :

<!-- skip -->
```typescript
const add = (a: number, b: number): number => a + b;
const result = add('x', 'y'); // Les paramètres de type 'string' ne peuvent pas être assignés à des paramètres de type 'number'.
```

Cependant, il va produire un code JavaScript exécutable :

<!-- skip -->
```typescript
'use strict';
const add = (a, b) => a + b;
const result = add('x', 'y'); // xy
```

Il est impossible de vérifier les types TypeScript lors de l'exécution. Par exemple :

<!-- skip -->
```typescript
interface Animal {
    name: string;
}
interface Dog extends Animal {
    bark: () => void;
}
interface Cat extends Animal {
    meow: () => void;
}
const makeNoise = (animal: Animal) => {
    if (animal instanceof Dog) {
        // 'Dog' fait référence uniquement à un type, mais est utilisé comme une valeur ici.
        // ...
    }
};
```

Étant donné que les types sont effacés après la compilation, il est impossible d'exécuter ce code en JavaScript. 
Pour reconnaître les types lors de l'exécution, il est nécessaire d'utiliser une logique différente.

TypeScript propose plusieurs options, la plus courante étant la liaison de types("tagged union"). Par exemple :

```typescript
interface Dog {
    kind: 'dog'; // Tagged union
    bark: () => void;
}
interface Cat {
    kind: 'cat'; // Tagged union
    meow: () => void;
}
type Animal = Dog | Cat;

const makeNoise = (animal: Animal) => {
    if (animal.kind === 'dog') {
        animal.bark();
    } else {
        animal.meow();
    }
};

const dog: Dog = {
    kind: 'dog',
    bark: () => console.log('bark'),
};
makeNoise(dog);
```
La propriété "kind" est une valeur qui peut être utilisée à l'exécution pour distinguer les objets en JavaScript.

Il est également possible qu'une valeur lors de l'exécution ait un type différent de celui déclaré dans la déclaration de type. Par exemple, si une valeur a été mal interprétée par un développeur et annotée de manière incorrecte.

TypeScript est une sur-couche (superset) de JavaScript, le mot-clé "class" peut donc être utilisé comme un type et une valeur lors de l'exécution.

```typescript
class Animal {
    constructor(public name: string) {}
}
class Dog extends Animal {
    constructor(
        public name: string,
        public bark: () => void
    ) {
        super(name);
    }
}
class Cat extends Animal {
    constructor(
        public name: string,
        public meow: () => void
    ) {
        super(name);
    }
}
type Mammal = Dog | Cat;

const makeNoise = (mammal: Mammal) => {
    if (mammal instanceof Dog) {
        mammal.bark();
    } else {
        mammal.meow();
    }
};

const dog = new Dog('Fido', () => console.log('bark'));
makeNoise(dog);
```

En JavaScript, une classe (`class`) a une propriété "prototype", l'opérateur "instanceof" peut donc être utilisé pour vérifier si la propriété prototype d'un constructeur apparaît dans la chaîne de prototype d'un objet.

TypeScript has no effect on runtime performance, as all types will be erased. However, TypeScript does introduce some build time overhead.
TypeScript n'a aucun effet sur les performances d'exécution, puisque tous les types seront effacés. 
En revanche, TypeScript ralentit la compilation.

### Avec du JavaScript "moderne" (Downleveling)

TypeScript peut compiler du code vers n'importe quelle version de JavaScript publiée depuis ECMAScript 3 (1999).
TypeScript peut donc transpiler du code contenant les dernières fonctionnalités JavaScript vers des versions plus anciennes, cette opération est appelée "Downleveling".
Cela permet d'utiliser du JavaScript moderne tout en maintenant une compatibilité avec les anciens environnements.

Il faut néanmoins garder à l'esprit que lors de la transpilation vers une version plus ancienne de JavaScript, 
TypeScript peut générer du code avec des performances inférieures en comparaison avec des implémentations natives.

Voici quelques-unes des fonctionnalités JavaScript modernes qui peuvent être utilisées en TypeScript :

* Utilisation de modules ECMAScript au lieu de callbacks "define" de style AMD ou de déclarations "require" de style CommonJS.
* Classes au lieu de prototypes.
* Variables déclarées avec "let" ou "const" au lieu de "var".
* "for-of" loop ou ".forEach" au lieu de la boucle "for".
* Fonctions fléchées au lieu de fonctions anonymes.
* Affectation par décomposition (destructuring assignment).
* Proprités et méthodes raccourcies et noms de propriétés calculés. (Shorthand properties).
* Arguments par défaut dans les fonctions.

En utilisant ces fonctionnalités JavaScript "modernes", les développeurs peuvent écrire un code plus concis grâce à TypeScript.
