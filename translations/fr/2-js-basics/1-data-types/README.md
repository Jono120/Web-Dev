<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "b95fdd8310ef467305015ece1b0f9411",
  "translation_date": "2025-08-29T13:40:05+00:00",
  "source_file": "2-js-basics/1-data-types/README.md",
  "language_code": "fr"
}
-->
# Notions de base en JavaScript : Types de données

![Notions de base en JavaScript - Types de données](../../../../translated_images/webdev101-js-datatypes.4cc470179730702c756480d3ffa46507f746e5975ebf80f99fdaaf1cff09a7f4.fr.png)
> Sketchnote par [Tomomi Imura](https://twitter.com/girlie_mac)

## Quiz avant le cours
[Quiz avant le cours](https://ff-quizzes.netlify.app/web/)

Cette leçon couvre les bases de JavaScript, le langage qui permet d'ajouter de l'interactivité sur le web.

> Vous pouvez suivre cette leçon sur [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-variables/?WT.mc_id=academic-77807-sagibbon)!

[![Variables](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Variables en JavaScript")

[![Types de données en JavaScript](https://img.youtube.com/vi/AWfA95eLdq8/0.jpg)](https://youtube.com/watch?v=AWfA95eLdq8 "Types de données en JavaScript")

> 🎥 Cliquez sur les images ci-dessus pour des vidéos sur les variables et les types de données.

Commençons par les variables et les types de données qui les remplissent !

## Variables

Les variables stockent des valeurs qui peuvent être utilisées et modifiées dans votre code.

Créer et **déclarer** une variable suit la syntaxe suivante : **[mot-clé] [nom]**. Cela se compose de deux parties :

- **Mot-clé**. Les mots-clés peuvent être `let` ou `var`.  

✅ Le mot-clé `let` a été introduit dans ES6 et donne à votre variable une _portée de bloc_. Il est recommandé d'utiliser `let` plutôt que `var`. Nous approfondirons les portées de bloc dans les prochaines parties.
- **Le nom de la variable**, que vous choisissez vous-même.

### Tâche - Travailler avec des variables

1. **Déclarez une variable**. Déclarons une variable en utilisant le mot-clé `let` :

    ```javascript
    let myVariable;
    ```

   `myVariable` a maintenant été déclarée en utilisant le mot-clé `let`. Elle n'a actuellement pas de valeur.

1. **Attribuez une valeur**. Stockez une valeur dans une variable avec l'opérateur `=`, suivi de la valeur attendue.

    ```javascript
    myVariable = 123;
    ```

   > Remarque : l'utilisation de `=` dans cette leçon signifie que nous utilisons un "opérateur d'affectation", utilisé pour attribuer une valeur à une variable. Cela ne signifie pas égalité.

   `myVariable` a maintenant été *initialisée* avec la valeur 123.

1. **Réécrivez**. Remplacez votre code par l'instruction suivante.

    ```javascript
    let myVariable = 123;
    ```

    Ce qui précède est appelé une _initialisation explicite_ lorsqu'une variable est déclarée et qu'une valeur lui est attribuée en même temps.

1. **Changez la valeur de la variable**. Modifiez la valeur de la variable de la manière suivante :

   ```javascript
   myVariable = 321;
   ```

   Une fois qu'une variable est déclarée, vous pouvez changer sa valeur à tout moment dans votre code avec l'opérateur `=` et la nouvelle valeur.

   ✅ Essayez-le ! Vous pouvez écrire du JavaScript directement dans votre navigateur. Ouvrez une fenêtre de navigateur et accédez aux Outils de développement. Dans la console, vous trouverez une invite ; tapez `let myVariable = 123`, appuyez sur Entrée, puis tapez `myVariable`. Que se passe-t-il ? Notez que vous en apprendrez davantage sur ces concepts dans les leçons suivantes.

## Constantes

La déclaration et l'initialisation d'une constante suivent les mêmes concepts qu'une variable, à l'exception du mot-clé `const`. Les constantes sont généralement déclarées avec des lettres majuscules.

```javascript
const MY_VARIABLE = 123;
```

Les constantes sont similaires aux variables, avec deux exceptions :

- **Doivent avoir une valeur**. Les constantes doivent être initialisées, sinon une erreur se produira lors de l'exécution du code.
- **La référence ne peut pas être modifiée**. La référence d'une constante ne peut pas être modifiée une fois initialisée, sinon une erreur se produira lors de l'exécution du code. Examinons deux exemples :
   - **Valeur simple**. Ce qui suit n'est PAS autorisé :
   
      ```javascript
      const PI = 3;
      PI = 4; // not allowed
      ```
 
   - **La référence d'un objet est protégée**. Ce qui suit n'est PAS autorisé.
   
      ```javascript
      const obj = { a: 3 };
      obj = { b: 5 } // not allowed
      ```

    - **La valeur d'un objet n'est pas protégée**. Ce qui suit EST autorisé :
    
      ```javascript
      const obj = { a: 3 };
      obj.a = 5;  // allowed
      ```

      Ci-dessus, vous modifiez la valeur de l'objet mais pas la référence elle-même, ce qui est autorisé.

   > Remarque : un `const` signifie que la référence est protégée contre la réaffectation. Cependant, la valeur n'est pas _immuable_ et peut changer, surtout si c'est une structure complexe comme un objet.

## Types de données

Les variables peuvent stocker différents types de valeurs, comme des nombres et du texte. Ces différents types de valeurs sont appelés **types de données**. Les types de données sont une partie importante du développement logiciel, car ils aident les développeurs à décider comment le code doit être écrit et comment le logiciel doit fonctionner. De plus, certains types de données ont des caractéristiques uniques qui permettent de transformer ou d'extraire des informations supplémentaires d'une valeur.

✅ Les types de données sont également appelés primitives de données en JavaScript, car ce sont les types de données les plus basiques fournis par le langage. Il existe 7 types de données primitifs : string, number, bigint, boolean, undefined, null et symbol. Prenez un moment pour visualiser ce que chacun de ces types primitifs pourrait représenter. Qu'est-ce qu'un `zebra` ? Et `0` ? `true` ?

### Nombres

Dans la section précédente, la valeur de `myVariable` était un type de données nombre.

`let myVariable = 123;`

Les variables peuvent stocker tous types de nombres, y compris les décimaux ou les nombres négatifs. Les nombres peuvent également être utilisés avec des opérateurs arithmétiques, abordés dans la [section suivante](../../../../2-js-basics/1-data-types).

### Opérateurs arithmétiques

Il existe plusieurs types d'opérateurs pour effectuer des fonctions arithmétiques, et certains sont listés ici :

| Symbole | Description                                                              | Exemple                          |
| ------- | ------------------------------------------------------------------------ | -------------------------------- |
| `+`     | **Addition** : Calcule la somme de deux nombres                          | `1 + 2 //réponse attendue : 3`   |
| `-`     | **Soustraction** : Calcule la différence entre deux nombres              | `1 - 2 //réponse attendue : -1`  |
| `*`     | **Multiplication** : Calcule le produit de deux nombres                  | `1 * 2 //réponse attendue : 2`   |
| `/`     | **Division** : Calcule le quotient de deux nombres                       | `1 / 2 //réponse attendue : 0.5` |
| `%`     | **Reste** : Calcule le reste de la division de deux nombres              | `1 % 2 //réponse attendue : 1`   |

✅ Essayez-le ! Essayez une opération arithmétique dans la console de votre navigateur. Les résultats vous surprennent-ils ?

### Chaînes de caractères

Les chaînes de caractères sont des ensembles de caractères placés entre des guillemets simples ou doubles.

- `'Ceci est une chaîne'`
- `"Ceci est aussi une chaîne"`
- `let myString = 'Ceci est une valeur de chaîne stockée dans une variable';`

N'oubliez pas d'utiliser des guillemets lorsque vous écrivez une chaîne, sinon JavaScript supposera qu'il s'agit d'un nom de variable.

### Mise en forme des chaînes

Les chaînes sont textuelles et nécessiteront parfois une mise en forme.

Pour **concaténer** deux chaînes ou plus, ou les joindre, utilisez l'opérateur `+`.

```javascript
let myString1 = "Hello";
let myString2 = "World";

myString1 + myString2 + "!"; //HelloWorld!
myString1 + " " + myString2 + "!"; //Hello World!
myString1 + ", " + myString2 + "!"; //Hello, World!

```

✅ Pourquoi `1 + 1 = 2` en JavaScript, mais `'1' + '1' = 11` ? Réfléchissez-y. Et `'1' + 1` ?

Les **littéraux de gabarit** sont une autre façon de formater des chaînes, sauf qu'au lieu de guillemets, on utilise l'accent grave. Tout ce qui n'est pas du texte brut doit être placé dans des placeholders `${ }`. Cela inclut toutes les variables qui peuvent être des chaînes.

```javascript
let myString1 = "Hello";
let myString2 = "World";

`${myString1} ${myString2}!` //Hello World!
`${myString1}, ${myString2}!` //Hello, World!
```

Vous pouvez atteindre vos objectifs de mise en forme avec l'une ou l'autre méthode, mais les littéraux de gabarit respecteront les espaces et les sauts de ligne.

✅ Quand utiliseriez-vous un littéral de gabarit plutôt qu'une chaîne classique ?

### Booléens

Les booléens ne peuvent avoir que deux valeurs : `true` ou `false`. Les booléens peuvent aider à décider quelles lignes de code doivent s'exécuter lorsque certaines conditions sont remplies. Dans de nombreux cas, les [opérateurs](../../../../2-js-basics/1-data-types) aident à définir la valeur d'un booléen, et vous remarquerez souvent des variables initialisées ou leurs valeurs mises à jour avec un opérateur.

- `let myTrueBool = true`
- `let myFalseBool = false`

✅ Une variable peut être considérée comme 'truthy' si elle évalue à un booléen `true`. Fait intéressant, en JavaScript, [toutes les valeurs sont truthy sauf si elles sont définies comme falsy](https://developer.mozilla.org/docs/Glossary/Truthy).

---

## 🚀 Défi

JavaScript est connu pour ses façons surprenantes de gérer les types de données à l'occasion. Faites quelques recherches sur ces "pièges". Par exemple : la sensibilité à la casse peut poser problème ! Essayez ceci dans votre console : `let age = 1; let Age = 2; age == Age` (résout `false` -- pourquoi ?). Quels autres pièges pouvez-vous trouver ?

## Quiz après le cours
[Quiz après le cours](https://ff-quizzes.netlify.app)

## Révision et auto-apprentissage

Consultez [cette liste d'exercices JavaScript](https://css-tricks.com/snippets/javascript/) et essayez-en un. Qu'avez-vous appris ?

## Devoir

[Exercice sur les types de données](assignment.md)

---

**Avertissement** :  
Ce document a été traduit à l'aide du service de traduction automatique [Co-op Translator](https://github.com/Azure/co-op-translator). Bien que nous nous efforcions d'assurer l'exactitude, veuillez noter que les traductions automatisées peuvent contenir des erreurs ou des inexactitudes. Le document original dans sa langue d'origine doit être considéré comme la source faisant autorité. Pour des informations critiques, il est recommandé de recourir à une traduction professionnelle réalisée par un humain. Nous déclinons toute responsabilité en cas de malentendus ou d'interprétations erronées résultant de l'utilisation de cette traduction.