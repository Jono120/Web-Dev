<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-29T11:51:41+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "bg"
}
-->
# Създаване на космическа игра, част 6: Край и рестарт

## Предварителен тест

[Предварителен тест](https://ff-quizzes.netlify.app/web/quiz/39)

Има различни начини да изразите *условие за край* в играта. Вие, като създател на играта, решавате защо играта приключва. Ето някои причини, ако приемем, че говорим за космическата игра, която създавате досега:

- **Унищожени са `N` вражески кораби**: Това е доста често срещано, ако разделите играта на различни нива, където трябва да унищожите `N` вражески кораби, за да завършите нивото.
- **Вашият кораб е унищожен**: Има игри, в които губите, ако вашият кораб бъде унищожен. Друг често срещан подход е концепцията за животи. Всеки път, когато вашият кораб бъде унищожен, се отнема един живот. Когато всички животи бъдат загубени, играта приключва.
- **Събрани са `N` точки**: Друго често срещано условие за край е събирането на точки. Как ще получите точки зависи от вас, но е доста често срещано да се присъждат точки за различни дейности, като унищожаване на вражески кораб или събиране на предмети, които се *пускат*, когато бъдат унищожени.
- **Завършване на ниво**: Това може да включва няколко условия, като унищожени `X` вражески кораби, събрани `Y` точки или може би събиране на конкретен предмет.

## Рестартиране

Ако хората харесват вашата игра, вероятно ще искат да я играят отново. След като играта приключи по каквато и да е причина, трябва да предложите опция за рестарт.

✅ Помислете малко за условията, при които една игра приключва, и как ви подканват да я рестартирате.

## Какво да създадете

Ще добавите следните правила към вашата игра:

1. **Победа в играта**. След като всички вражески кораби бъдат унищожени, печелите играта. Освен това покажете някакво съобщение за победа.
1. **Рестарт**. След като всички животи бъдат загубени или играта бъде спечелена, трябва да предложите начин за рестартиране на играта. Запомнете! Ще трябва да инициализирате играта отново и да изчистите предишното състояние на играта.

## Препоръчителни стъпки

Намерете файловете, които са създадени за вас в подпапката `your-work`. Тя трябва да съдържа следното:

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

Започнете проекта си в папката `your_work`, като въведете:

```bash
cd your-work
npm start
```

Горната команда ще стартира HTTP сървър на адрес `http://localhost:5000`. Отворете браузър и въведете този адрес. Вашата игра трябва да е в състояние за игра.

> съвет: за да избегнете предупреждения в Visual Studio Code, редактирайте функцията `window.onload`, така че да извиква `gameLoopId` без `let`, и декларирайте `gameLoopId` в началото на файла, независимо: `let gameLoopId;`

### Добавяне на код

1. **Проследяване на условието за край**. Добавете код, който следи броя на враговете или дали героичният кораб е унищожен, като добавите тези две функции:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **Добавяне на логика към обработчиците на съобщения**. Редактирайте `eventEmitter`, за да обработва тези условия:

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

1. **Добавяне на нови типове съобщения**. Добавете тези съобщения към обекта constants:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **Добавяне на код за рестарт**. Добавете код, който рестартира играта при натискане на избран бутон.

   1. **Слушане за натискане на клавиш `Enter`**. Редактирайте eventListener на вашия прозорец, за да слуша за това натискане:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **Добавяне на съобщение за рестарт**. Добавете това съобщение към constants на Messages:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **Реализиране на правила за игра**. Реализирайте следните правила за игра:

   1. **Условие за победа на играча**. Когато всички вражески кораби бъдат унищожени, покажете съобщение за победа.

      1. Първо, създайте функция `displayMessage()`:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. Създайте функция `endGame()`:

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

   1. **Логика за рестарт**. Когато всички животи бъдат загубени или играчът спечели играта, покажете, че играта може да бъде рестартирана. Освен това рестартирайте играта, когато бъде натиснат клавишът за *рестарт* (можете да решите кой клавиш да бъде свързан с рестарт).

      1. Създайте функция `resetGame()`:

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

     1. Добавете извикване към `eventEmitter`, за да рестартирате играта в `initGame()`:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. Добавете функция `clear()` към EventEmitter:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 Поздравления, капитане! Вашата игра е завършена! Браво! 🚀 💥 👽

---

## 🚀 Предизвикателство

Добавете звук! Можете ли да добавите звук, за да подобрите играта, например когато има лазерен удар, или когато героят умира или печели? Разгледайте този [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play), за да научите как да възпроизвеждате звук с помощта на JavaScript.

## Финален тест

[Финален тест](https://ff-quizzes.netlify.app/web/quiz/40)

## Преглед и самостоятелно обучение

Вашата задача е да създадете нова примерна игра, така че разгледайте някои интересни игри, за да видите какъв тип игра бихте могли да създадете.

## Задание

[Създайте примерна игра](assignment.md)

---

**Отказ от отговорност**:  
Този документ е преведен с помощта на AI услуга за превод [Co-op Translator](https://github.com/Azure/co-op-translator). Въпреки че се стремим към точност, моля, имайте предвид, че автоматизираните преводи може да съдържат грешки или неточности. Оригиналният документ на неговия изходен език трябва да се счита за авторитетен източник. За критична информация се препоръчва професионален превод от човек. Не носим отговорност за каквито и да е недоразумения или погрешни интерпретации, произтичащи от използването на този превод.