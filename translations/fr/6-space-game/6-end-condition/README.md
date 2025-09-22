<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-29T13:38:36+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "fr"
}
-->
# Construire un jeu spatial Partie 6 : Fin et redémarrage

## Quiz avant le cours

[Quiz avant le cours](https://ff-quizzes.netlify.app/web/quiz/39)

Il existe différentes façons d'exprimer une *condition de fin* dans un jeu. En tant que créateur du jeu, c'est à vous de décider pourquoi le jeu se termine. Voici quelques raisons possibles, en supposant que nous parlons du jeu spatial que vous avez construit jusqu'à présent :

- **`N` vaisseaux ennemis ont été détruits** : Il est assez courant, si vous divisez un jeu en différents niveaux, de devoir détruire `N` vaisseaux ennemis pour terminer un niveau.
- **Votre vaisseau a été détruit** : Il existe des jeux où vous perdez si votre vaisseau est détruit. Une autre approche courante est d'introduire le concept de vies. Chaque fois que votre vaisseau est détruit, une vie est déduite. Une fois toutes les vies perdues, vous perdez la partie.
- **Vous avez collecté `N` points** : Une autre condition de fin courante est de collecter des points. La manière dont vous obtenez ces points dépend de vous, mais il est fréquent d'attribuer des points à diverses activités comme détruire un vaisseau ennemi ou collecter des objets qui tombent lorsque des ennemis sont détruits.
- **Terminer un niveau** : Cela peut impliquer plusieurs conditions, comme détruire `X` vaisseaux ennemis, collecter `Y` points ou peut-être récupérer un objet spécifique.

## Redémarrage

Si les joueurs apprécient votre jeu, ils voudront probablement y rejouer. Une fois le jeu terminé, quelle qu'en soit la raison, vous devriez offrir une option pour redémarrer.

✅ Réfléchissez aux conditions dans lesquelles un jeu se termine, puis à la manière dont vous invitez les joueurs à redémarrer.

## Ce que vous allez construire

Vous allez ajouter ces règles à votre jeu :

1. **Gagner la partie**. Une fois que tous les vaisseaux ennemis ont été détruits, vous gagnez la partie. Affichez également un message de victoire.
1. **Redémarrer**. Une fois que toutes vos vies sont perdues ou que le jeu est gagné, vous devez offrir une option pour redémarrer le jeu. N'oubliez pas ! Vous devrez réinitialiser le jeu et effacer l'état précédent.

## Étapes recommandées

Repérez les fichiers qui ont été créés pour vous dans le sous-dossier `your-work`. Il devrait contenir les éléments suivants :

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
  -| life.png
-| index.html
-| app.js
-| package.json
```

Démarrez votre projet dans le dossier `your_work` en tapant :

```bash
cd your-work
npm start
```

Cela lancera un serveur HTTP à l'adresse `http://localhost:5000`. Ouvrez un navigateur et entrez cette adresse. Votre jeu devrait être jouable.

> astuce : pour éviter les avertissements dans Visual Studio Code, modifiez la fonction `window.onload` pour appeler `gameLoopId` tel quel (sans `let`), et déclarez `gameLoopId` en haut du fichier, indépendamment : `let gameLoopId;`

### Ajouter du code

1. **Suivre la condition de fin**. Ajoutez du code pour suivre le nombre d'ennemis ou vérifier si le vaisseau du héros a été détruit en ajoutant ces deux fonctions :

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **Ajouter une logique aux gestionnaires de messages**. Modifiez le `eventEmitter` pour gérer ces conditions :

    ```javascript
    eventEmitter.on(Messages.COLLISION_ENEMY_LASER, (_, { first, second }) => {
        first.dead = true;
        second.dead = true;
        hero.incrementPoints();

        if (isEnemiesDead()) {
          eventEmitter.emit(Messages.GAME_END_WIN);
        }
    });

    eventEmitter.on(Messages.COLLISION_ENEMY_HERO, (_, { enemy }) => {
        enemy.dead = true;
        hero.decrementLife();
        if (isHeroDead())  {
          eventEmitter.emit(Messages.GAME_END_LOSS);
          return; // loss before victory
        }
        if (isEnemiesDead()) {
          eventEmitter.emit(Messages.GAME_END_WIN);
        }
    });
    
    eventEmitter.on(Messages.GAME_END_WIN, () => {
        endGame(true);
    });
      
    eventEmitter.on(Messages.GAME_END_LOSS, () => {
      endGame(false);
    });
    ```

1. **Ajouter de nouveaux types de messages**. Ajoutez ces messages à l'objet constants :

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **Ajouter le code de redémarrage** pour redémarrer le jeu en appuyant sur une touche sélectionnée.

   1. **Écouter la touche `Entrée`**. Modifiez l'eventListener de votre fenêtre pour écouter cette touche :

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **Ajouter un message de redémarrage**. Ajoutez ce message à votre constante Messages :

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **Implémenter les règles du jeu**. Implémentez les règles suivantes :

   1. **Condition de victoire du joueur**. Lorsque tous les vaisseaux ennemis sont détruits, affichez un message de victoire.

      1. Tout d'abord, créez une fonction `displayMessage()` :

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. Créez une fonction `endGame()` :

        ```javascript
        function endGame(win) {
          clearInterval(gameLoopId);
        
          // set a delay so we are sure any paints have finished
          setTimeout(() => {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = "black";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            if (win) {
              displayMessage(
                "Victory!!! Pew Pew... - Press [Enter] to start a new game Captain Pew Pew",
                "green"
              );
            } else {
              displayMessage(
                "You died !!! Press [Enter] to start a new game Captain Pew Pew"
              );
            }
          }, 200)  
        }
        ```

   1. **Logique de redémarrage**. Lorsque toutes les vies sont perdues ou que le joueur a gagné, affichez que le jeu peut être redémarré. Redémarrez également le jeu lorsque la touche de *redémarrage* est pressée (vous pouvez décider quelle touche sera utilisée pour redémarrer).

      1. Créez la fonction `resetGame()` :

        ```javascript
        function resetGame() {
          if (gameLoopId) {
            clearInterval(gameLoopId);
            eventEmitter.clear();
            initGame();
            gameLoopId = setInterval(() => {
              ctx.clearRect(0, 0, canvas.width, canvas.height);
              ctx.fillStyle = "black";
              ctx.fillRect(0, 0, canvas.width, canvas.height);
              drawPoints();
              drawLife();
              updateGameObjects();
              drawGameObjects(ctx);
            }, 100);
          }
        }
        ```

     1. Ajoutez un appel à `eventEmitter` pour réinitialiser le jeu dans `initGame()` :

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. Ajoutez une fonction `clear()` à l'EventEmitter :

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 Félicitations, Capitaine ! Votre jeu est terminé ! Bien joué ! 🚀 💥 👽

---

## 🚀 Défi

Ajoutez un son ! Pouvez-vous ajouter un son pour améliorer l'expérience de jeu, peut-être lorsqu'un laser touche une cible, ou lorsque le héros meurt ou gagne ? Consultez ce [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) pour apprendre à jouer un son avec JavaScript.

## Quiz après le cours

[Quiz après le cours](https://ff-quizzes.netlify.app/web/quiz/40)

## Révision et auto-apprentissage

Votre mission est de créer un nouveau jeu d'exemple, alors explorez certains des jeux intéressants disponibles pour voir quel type de jeu vous pourriez construire.

## Devoir

[Créer un jeu d'exemple](assignment.md)

---

**Avertissement** :  
Ce document a été traduit à l'aide du service de traduction automatique [Co-op Translator](https://github.com/Azure/co-op-translator). Bien que nous nous efforcions d'assurer l'exactitude, veuillez noter que les traductions automatisées peuvent contenir des erreurs ou des inexactitudes. Le document original dans sa langue d'origine doit être considéré comme la source faisant autorité. Pour des informations critiques, il est recommandé de faire appel à une traduction humaine professionnelle. Nous déclinons toute responsabilité en cas de malentendus ou d'interprétations erronées résultant de l'utilisation de cette traduction.