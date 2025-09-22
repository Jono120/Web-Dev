<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-28T18:15:24+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "uk"
}
-->
# Створення космічної гри, частина 6: Завершення та перезапуск

## Тест перед лекцією

[Тест перед лекцією](https://ff-quizzes.netlify.app/web/quiz/39)

Існує багато способів визначити *умову завершення* гри. Як творець гри, ви вирішуєте, чому гра закінчується. Ось кілька причин, якщо припустити, що ми говоримо про космічну гру, яку ви створювали до цього:

- **Знищено `N` ворожих кораблів**: Це досить поширено, якщо гра розділена на рівні, де потрібно знищити `N` ворожих кораблів, щоб завершити рівень.
- **Ваш корабель знищено**: У багатьох іграх ви програєте, якщо ваш корабель знищено. Інший поширений підхід — це концепція життів. Кожного разу, коли ваш корабель знищено, віднімається одне життя. Коли всі життя втрачені, гра завершується.
- **Зібрано `N` очок**: Ще одна поширена умова завершення — це збирання очок. Як саме ви отримуєте очки — залежить від вас, але часто очки присвоюються за різні дії, наприклад, знищення ворожого корабля або збирання предметів, які випадають після їх знищення.
- **Завершення рівня**: Це може включати кілька умов, таких як знищення `X` ворожих кораблів, збирання `Y` очок або, можливо, збирання певного предмета.

## Перезапуск

Якщо людям подобається ваша гра, вони, ймовірно, захочуть зіграти в неї знову. Коли гра завершується з будь-якої причини, ви повинні запропонувати можливість перезапустити її.

✅ Подумайте, за яких умов гра завершується, і як вам пропонують її перезапустити.

## Що створити

Ви додасте ці правила до своєї гри:

1. **Перемога в грі**. Коли всі ворожі кораблі знищено, ви виграєте гру. Додатково відобразіть повідомлення про перемогу.
1. **Перезапуск**. Коли всі ваші життя втрачені або гра виграна, ви повинні запропонувати спосіб перезапустити гру. Пам’ятайте! Вам потрібно буде реініціалізувати гру, і попередній стан гри має бути очищений.

## Рекомендовані кроки

Знайдіть файли, які були створені для вас у підпапці `your-work`. Вона повинна містити наступне:

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

Запустіть свій проєкт у папці `your_work`, ввівши:

```bash
cd your-work
npm start
```

Це запустить HTTP-сервер за адресою `http://localhost:5000`. Відкрийте браузер і введіть цю адресу. Ваша гра повинна бути готова до гри.

> підказка: щоб уникнути попереджень у Visual Studio Code, змініть функцію `window.onload`, щоб викликати `gameLoopId` без `let`, і оголосіть `gameLoopId` на початку файлу окремо: `let gameLoopId;`

### Додайте код

1. **Відстеження умови завершення**. Додайте код, який відстежує кількість ворогів або чи був знищений корабель героя, додавши ці дві функції:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **Додайте логіку до обробників повідомлень**. Змініть `eventEmitter`, щоб обробляти ці умови:

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

1. **Додайте нові типи повідомлень**. Додайте ці повідомлення до об’єкта constants:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **Додайте код для перезапуску**. Додайте код, який перезапускає гру при натисканні вибраної кнопки.

   1. **Слухайте натискання клавіші `Enter`**. Змініть eventListener вашого вікна, щоб слухати це натискання:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **Додайте повідомлення про перезапуск**. Додайте це повідомлення до вашого об’єкта Messages:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **Реалізуйте правила гри**. Реалізуйте наступні правила гри:

   1. **Умова перемоги гравця**. Коли всі ворожі кораблі знищено, відобразіть повідомлення про перемогу.

      1. Спочатку створіть функцію `displayMessage()`:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. Створіть функцію `endGame()`:

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

   1. **Логіка перезапуску**. Коли всі життя втрачені або гравець виграв гру, відобразіть, що гру можна перезапустити. Додатково перезапустіть гру, коли натиснуто клавішу *перезапуску* (ви можете вирішити, яка клавіша буде відповідати за перезапуск).

      1. Створіть функцію `resetGame()`:

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

     1. Додайте виклик до `eventEmitter`, щоб скинути гру в `initGame()`:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. Додайте функцію `clear()` до EventEmitter:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 Вітаємо, Капітане! Ваша гра завершена! Чудова робота! 🚀 💥 👽

---

## 🚀 Виклик

Додайте звук! Чи можете ви додати звук, щоб покращити ігровий процес, наприклад, коли лазер влучає, герой гине або перемагає? Ознайомтеся з цим [прикладом](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play), щоб дізнатися, як відтворювати звук за допомогою JavaScript.

## Тест після лекції

[Тест після лекції](https://ff-quizzes.netlify.app/web/quiz/40)

## Огляд і самостійне навчання

Ваше завдання — створити нову пробну гру, тому досліджуйте цікаві ігри, щоб побачити, яку гру ви могли б створити.

## Завдання

[Створіть пробну гру](assignment.md)

---

**Відмова від відповідальності**:  
Цей документ було перекладено за допомогою сервісу автоматичного перекладу [Co-op Translator](https://github.com/Azure/co-op-translator). Хоча ми прагнемо до точності, звертаємо вашу увагу, що автоматичні переклади можуть містити помилки або неточності. Оригінальний документ на його рідній мові слід вважати авторитетним джерелом. Для критично важливої інформації рекомендується професійний людський переклад. Ми не несемо відповідальності за будь-які непорозуміння або неправильні тлумачення, що виникли внаслідок використання цього перекладу.