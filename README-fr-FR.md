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

## Commencer avec TypeScript

### Installation

Visual Studio Code offre une excellente intégration du langage TypeScript, en revanche, il n'intègre pas le compilateur TypeScript.
Pour installer le compilateur TypeScript, vous pouvez utiliser un gestionnaire de paquets tel que npm ou yarn :

```shell
npm install typescript --save-dev
```

ou

```shell
yarn add typescript --dev
```

Assurez-vous de commiter le fichier de configuration généré afin que tout membre de l'équipe utilise la même version de TypeScript.

Pour exécuter le compilateur TypeScript, vous pouvez utiliser les commandes suivantes :

```shell
npx tsc
```
ou

```shell
yarn tsc
```

Il est recommandé d'installer TypeScript avec chaque projet plutôt que globalement, afin de gérer les versions de manière plus précise. 
Cependant, vous pouvez utiliser la commande suivante :

```shell
npm install -g typescript
```

Si vous utilisez Microsoft Visual Studio, vous pouvez obtenir TypeScript en tant que package dans NuGet pour vos projets MSBuild. Dans la console de gestion des packages NuGet, exécutez la commande suivante :

```shell
Install-Package Microsoft.TypeScript.MSBuild
```

Lors de l'installation de TypeScript, deux exécutables sont installés : "tsc" en tant que compilateur TypeScript et "tsserver" en tant que serveur TypeScript autonome. Le serveur autonome contient le compilateur et les services de langage qui peuvent être utilisés par les éditeurs et les IDE pour fournir une complétion de code intelligente.

Il existe également plusieurs transpileurs compatibles avec TypeScript, tels que Babel (via un plugin) ou swc. 
Ces transpileurs peuvent être utilisés pour convertir du code TypeScript en d'autres langages ou versions cibles.


### Configuration


TypeScript peut être configuré en utilisant les options de la commande `tsc` ou en utilisant un fichier de configuration dédié appelé `tsconfig.json`, placé à la racine du projet.

Pour générer un fichier `tsconfig.json` prérempli avec les paramètres recommandés, vous pouvez utiliser la commande suivante :

```shell
tsc --init
```
La commande `tsc` compilera le code en utilisant la configuration spécifiée dans le fichier `tsconfig.json` le plus proche.

Voici quelques exemples de commandes CLI qui s'exécutent avec les paramètres par défaut :

```shell
tsc main.ts // Compile un fichier TypeScript en JavaScript
tsc src/*.ts // Compile tous les fichiers TypeScript dans le répertoire src en JavaScript
tsc app.ts util.ts --outfile index.js // Compile plusieurs fichiers TypeScript en un seul fichier JavaScript
```

### Fichier de configuration TypeScript


Un fichier `tsconfig.json` est utilisé pour configurer le compilateur TypeScript (tsc). Il est généralement ajouté à la racine du projet, avec le fichier `package.json`.

Notes:

* le fichier tsconfig.json accepte les commentaires même s'il est au format json.
* Il est conseillé d'utiliser ce fichier de configuration plutôt que les options en ligne de commande.

Le lien suivant vous permet de trouver la documentation complète et son schéma :

[https://www.typescriptlang.org/tsconfig](https://www.typescriptlang.org/tsconfig)

[http://json.schemastore.org/tsconfig](http://json.schemastore.org/tsconfig)

Voici une liste des configurations courantes et utiles :

#### target

La propriété "target" est utilisée pour spécifier la version d'ECMAScript en JavaScript que TypeScript doit émettre/compiler. Pour les navigateurs modernes, ES6 est une bonne option, pour les navigateurs plus anciens, ES5 est recommandé.

#### lib

La propriété "lib" est utilisée pour spécifier les APIS à inclure au moment de la compilation. TypeScript inclut automatiquement les API pour les fonctionnalités spécifiées dans la propriété "target", mais il est possible d'omettre ou de choisir des API spécifiques pour des besoins particuliers. Par exemple, si vous travaillez sur un projet serveur, vous pouvez exclure l'API "DOM", qui est utile uniquement dans un environnement de navigateur.

#### strict

La propriété "strict" ajoute des vérifications plus strictes et améliore la sécurité des types. Il est conseillé d'inclure cette propriété dans le fichier tsconfig.json de votre projet. L'activation de la propriété "strict" permet à TypeScript de :

* Compiler les fichiers TypeScript en mode strict.
* Détecter "null" et "undefined" dans le processus de vérification des types.
* Désactiver l'usage duu type "any" lorsqu'aucune annotation de type n'est présente.
* Déclencher une erreur lors de l'utilisation de l'expression "this", qui impliquerait autrement le type "any".

#### module

La propriété "module" définit le système de modules pris en charge pour le programme compilé. Pendant l'exécution, un chargeur de modules est utilisé pour localiser et exécuter les dépendances en fonction du système de modules spécifié.

Les systèmes de modules les plus couramment utilisés en JavaScript sont Node.js CommonJS pour les applications serveur et RequireJS pour les modules AMD dans les applications web basées sur le navigateur. TypeScript peut transpiler du code pour différents systèmes de modules, y compris UMD, System, ESNext, ES2015/ES6 et ES2020.

Note : Le système de modules doit être choisi en fonction de l'environnement cible et du système de chargement de modules disponible dans cet environnement.

#### moduleResolution

La propriété "moduleResolution" spécifie la stratégie de résolution des modules. Utilisez "node" pour du code TypeScript moderne, la stratégie "classic" est utilisée uniquement pour les anciennes versions de TypeScript (avant 1.6).

#### esModuleInterop

La propriété "esModuleInterop" permet d'importer par défaut des modules CommonJS qui n'ont pas exporté en utilisant la propriété "default". Cette propriété fournit un shim pour assurer la compatibilité dans le JavaScript émis. Après avoir activé cette option, nous pouvons utiliser `import MyLibrary from "my-library"` au lieu de `import * as MyLibrary from "my-library"`.

#### jsx

La propriété "jsx" s'applique uniquement aux fichiers .tsx utilisés dans ReactJS et contrôle la manière dont les constructions JSX sont compilées en JavaScript. Une option courante est "preserve", qui compilera un fichier .jsx en conservant inchangé le JSX afin de pouvoir être transmis à différents outils comme Babel pour d'autres transformations.

#### skipLibCheck

La propriété "skipLibCheck" empêchera TypeScript de vérifier les types de l'ensemble des packages tiers importés. Cette propriété réduira le temps de compilation d'un projet. TypeScript vérifiera toujours votre code par rapport aux définitions de types fournies par ces packages.

#### files

La propriété "files" indique au compilateur une liste de fichiers qui doivent toujours être inclus dans le programme.

#### include

La propriété "include" indique au compilateur une liste de fichiers que nous souhaitons inclure. Cette propriété permet d'utiliser des motifs de type glob, tels que "\*_" pour n'importe quel sous-répertoire, "_" pour n'importe quel nom de fichier, et "?" pour des caractères optionnels.

#### exclude

La propriété "exclude" indique au compilateur une liste de fichiers qui ne doivent pas être inclus dans la compilation. Cela peut inclure des fichiers tels que "node_modules" ou des fichiers de test.
Note : tsconfig.json accepte les commentaires.

### importHelpers

TypeScript utilise du code lors de la génération de code pour certaines fonctionnalités JavaScript avancées ou down-level. Par défaut, ces assistants sont dupliqués dans les fichiers qui les utilisent. L'option `importHelpers` importe ces assistants depuis le module `tslib`, rendant la sortie JavaScript plus efficace.

### Migration to TypeScript Advice
### Conseils pour la migration vers TypeScript

Pour les grands projets, il est recommandé d'adopter une transition progressive où le code TypeScript et JavaScript coexisteront initialement. Seuls les petits projets peuvent être migrés vers TypeScript en une seule fois.

La première étape de cette transition consiste à introduire TypeScript dans le processus de chaîne de construction. Cela peut être fait en utilisant l'option du compilateur "allowJs", qui permet aux fichiers .ts et .tsx de coexister avec les fichiers JavaScript existants. Comme TypeScript reviendra à un type "any" pour une variable lorsqu'il ne peut pas inférer le type à partir des fichiers JavaScript, il est recommandé de désactiver "noImplicitAny" dans vos options de compilateur au début de la migration.

La deuxième étape consiste à s'assurer que vos tests JavaScript fonctionnent aux côtés des fichiers TypeScript afin de pouvoir exécuter les tests à mesure que vous convertissez chaque module. Si vous utilisez Jest, envisagez d'utiliser `ts-jest`, qui vous permet de tester des projets TypeScript avec Jest.

La troisième étape consiste à inclure les déclarations de type pour les bibliothèques tierces dans votre projet. Ces déclarations peuvent être trouvées soit regroupées, soit sur DefinitelyTyped. Vous pouvez les rechercher en utilisant [https://www.typescriptlang.org/dt/search](https://www.typescriptlang.org/dt/search) et les installer en utilisant :

```shell
npm install --save-dev @types/package-name ou yarn add --dev @types/package-name.
```

La quatrième étape consiste à migrer module par module avec une approche ascendante, en suivant votre graphe de dépendances en commençant par les feuilles. L'idée est de commencer à convertir les modules qui ne dépendent pas d'autres modules. Pour visualiser les graphes de dépendances, vous pouvez utiliser l'outil "madge".

Les modules candidats pour ces conversions initiales sont les fonctions utilitaires et le code lié aux API externes ou aux spécifications. Il est possible de générer automatiquement des définitions de types TypeScript à partir de contrats Swagger, de schémas GraphQL ou JSON à inclure dans votre projet.

Dans le cas où il n'y a pas de spécifications ou de schémas officiels disponibles, vous pouvez générer des types à partir de données brutes, telles que du JSON renvoyé par un serveur. Cependant, il est recommandé de générer des types à partir de spécifications plutôt que de données pour éviter de manquer des cas particuliers.

Lors de la migration, évitez de refactoriser le code et concentrez-vous uniquement sur l'ajout de types à vos modules.

La cinquième étape consiste à activer "noImplicitAny", qui garantira que tous les types sont connus et définis, offrant une meilleure expérience TypeScript pour votre projet.

Durant la migration, vous pouvez utiliser la directive `@ts-check`, qui active la vérification des types TypeScript dans un fichier JavaScript. Cette directive fournit une version lâche de la vérification des types et peut être utilisée initialement pour identifier les problèmes dans les fichiers JavaScript. Lorsque `@ts-check` est inclus dans un fichier, TypeScript tentera de déduire les définitions en utilisant des commentaires de style JSDoc. Cependant, considérez l'utilisation des annotations JSDoc uniquement à un stade très précoce de la migration.

Pensez à conserver la valeur par défaut de `noEmitOnError` dans votre fichier tsconfig.json à false. Cela vous permettra de générer du code source JavaScript même si des erreurs sont signalées.