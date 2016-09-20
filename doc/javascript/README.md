[Front-end styleguide](/README.md) > [1. Working with JavaScript](/doc/javascript)

## Index
1. Javacript
  1. [Guidelines Générales](#12-guidelines-générales)
  2. [Conventions de nommage](#11-conventions-de-nommage)
  3. [TODO] Linters
  4. [TODO] Code style
  5. [TODO] Tooling
  6. [TODO] Librairies

## 1.1 Guidelines générales

#### Version de JavaScript**
Veiller à toujours écrire en JavaScript ES2015+, compilé via [Babel](https://babeljs.io/).

Un peu perdu avec les derniers ajouts au langages ? Commencer par comprendre et apprendre:

- les Modules (ES2015)
- les Arrow Functions (ES2015)
- les String Literals (ES2015)
- Const / Let (ES2015)

puis, graduellement, les autres nouveautés.

#### Séparer son code en modules
Vu que nous avons sous la main une version moderne du language, il est possible d'utiliser les modules ES2015 pour organiser son code.
:white_check_mark: Séparer son code en un ou plusieurs modules, par "concern". 

Par exemple, imaginons la création d'un composant de Tooltip custom.
On pourrait l'organiser de cette manière :

```
components
└─  tooltip
    │  index.js // Le module principal, exporte le constructeur ou la fonction d'init du composant
    │  tooltip_positionner.js // Le module contenant toute la logique pour le positionnement des tooltip
    │  tooltip_display.js // Le module gérant le DOM et les styles des tooltip
    |  defaults.const.js //  Le module contenant les options par défaut des tooltip (constantes)
```

:white_check_mark: Rester libre d'organiser son code comme on le souhaite, mais le séparer en modules quand c'est nécessaire,
ou pour éviter d'avoir trop de lignes par fichier.

#### Séparer sa logique en petites fonctions, correctement nommées
  Les fonctions sont à nommer en lowerCamelCase. Essayer de trouver un nom court, et descriptif.
  
  :white_check_mark: Des fonctions bien nommées font presque office de documentation.
  Leur nom doit être assez clair pour donner au lecteur des informations sur ce qu'il se passe :
  
  ```js
    calcElementsOffset = (element1, element2) => {
      // Calcule l'offset entre deux éléments
    }
  ```
  
  :x: Eviter les fonctions trop longues, complexes, avec des noms obscures
  ```js
    show = (el, e, x, y) => { // Le nom des arguments est confus
      // 200 lignes de code imbitable
    }
  ```

#### Extraire son code en fonctions génériques
  :white_check_mark: Essayer d'extraire la logique qui paraît générique dans des modules "utilitaires" :
  ```
  Une fonction générique, (fonction "capitalize" par ex.), devrait être extraite
  dans un fichier `utils/string.js`, qui pourrait contenir toutes les fonctions de manipulation
  de chaînes de caractère nécessaires au projet.
  ```
  
  (:bulb: Note - Il serait intéressant de faire un repository pour toutes les fonctions utilitaires
   qu'on utilise d'un projet à l'autre )
  

#### Essayer d'utiliser des fonctions pures
Sans vouloir imposer un style de code trop fonctionnel, essayer de créer des fonctions "pures" quand c'est possible.

Une fonction pure :
    - :white_check_mark: doit toujours retourner le même résultat quand appellée avec les mêmes arguments.
    - :white_check_mark: Ne doit avoir aucun effet de bord (side-effect): changement de state, mutation d'objets externes, etc.

Vu que les side effects sont très communs en front (Manipulation du DOM, requêtes HTTP utilisation de localStorage, etc.),
il est inévitable d'avoir des fonctions stateful ou causant des effets de bord.

Mais essayons de les garder sous contrôle, en :
    - :x: Evitant de référencer des variables externes. Préférer les passer en arguments.
    - :x: Evitant de répendre du state à travers son code. Si un composant a besoin de state, garder le contenu
      en le déclarant en haut du fichier (généralement sous la forme d'un object), et indiquer explicitement les fonctions qui le mutent.
    - :white_check_mark: Extraire ce qui peut être extrait en une fonction pure, et garder tout ce qui est impure séparé.

## 1.2 Conventions de nommage

#### Fichiers
Les fichiers JavaScript sont nommés en snake_case, pour :
- :white_check_mark: Eviter les problèmes entre OSX et Unix
- :white_check_mark: Suivre la convention Rails

Dans certains cas, il peut être utile d'ajouter un suffixe à un nom de fichier pour exprimer à quel genre de code on à affaire :
- `endpoints.const.js` Indique que c'est un fichier contenant uniquement des constantes.
- `users.loader.js` Indique que c'est du code utilisé pour récupérer de la donnée via une requête HTTP

#### Fonctions, Variables
Les fonctions JavaScript doivent être en lowerCamelCase, pour respecter la convention générale.
Les noms de variable aussi, **même les constantes** (vu qu'elles seront déclarées via `const` [TODO: Link to const])
Les noms de Constructeurs, ou toute fonction servant à instancier quelque chose, doivent être en UpperCamelCase.

#### Composants React
Les fichiers de composant React sont également à nommer en `.js`. Pas besoin d'introduire un nouveau format, même avec l'utilisation du JSX.


