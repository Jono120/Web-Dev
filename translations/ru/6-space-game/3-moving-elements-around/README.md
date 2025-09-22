<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a9a161871de7706cb0e23b1bd0c74559",
  "translation_date": "2025-08-28T23:17:08+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "ru"
}
-->
# Создание космической игры, часть 3: Добавление движения

## Викторина перед лекцией

[Викторина перед лекцией](https://ff-quizzes.netlify.app/web/quiz/33)

Игры становятся интересными, когда на экране начинают двигаться пришельцы! В этой игре мы будем использовать два типа движений:

- **Движение с помощью клавиатуры/мыши**: когда пользователь взаимодействует с клавиатурой или мышью, чтобы переместить объект на экране.
- **Движение, инициированное игрой**: когда игра перемещает объект через определенные интервалы времени.

Итак, как же перемещать объекты на экране? Все дело в декартовых координатах: мы изменяем местоположение объекта (x, y), а затем перерисовываем экран.

Обычно для выполнения *движения* на экране вам понадобятся следующие шаги:

1. **Установить новое местоположение** объекта; это необходимо, чтобы создать впечатление, что объект переместился.
2. **Очистить экран**, экран нужно очищать между перерисовками. Мы можем очистить его, нарисовав прямоугольник, заполненный цветом фона.
3. **Перерисовать объект** в новом местоположении. Таким образом мы достигаем перемещения объекта из одного места в другое.

Вот как это может выглядеть в коде:

```javascript
//set the hero's location
hero.x += 5;
// clear the rectangle that hosts the hero
ctx.clearRect(0, 0, canvas.width, canvas.height);
// redraw the game background and hero
ctx.fillRect(0, 0, canvas.width, canvas.height)
ctx.fillStyle = "black";
ctx.drawImage(heroImg, hero.x, hero.y);
```

✅ Можете ли вы придумать причину, почему перерисовка вашего героя много раз в секунду может привести к снижению производительности? Прочитайте о [альтернативных подходах к этому паттерну](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas).

## Обработка событий клавиатуры

События обрабатываются путем привязки определенных событий к коду. События клавиатуры срабатывают для всего окна, тогда как события мыши, такие как `click`, могут быть связаны с кликом по конкретному элементу. Мы будем использовать события клавиатуры на протяжении всего проекта.

Чтобы обработать событие, нужно использовать метод `addEventListener()` окна и передать ему два параметра. Первый параметр — это имя события, например `keyup`. Второй параметр — это функция, которая должна быть вызвана в результате произошедшего события.

Вот пример:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

Для событий клавиш есть два свойства события, которые можно использовать, чтобы узнать, какая клавиша была нажата:

- `key` — строковое представление нажатой клавиши, например `ArrowUp`.
- `keyCode` — числовое представление, например `37`, соответствует `ArrowLeft`.

✅ Манипуляция событиями клавиш полезна не только в разработке игр. Какие еще применения этой техники вы можете придумать?

### Особые клавиши: предостережение

Существуют *особые* клавиши, которые влияют на окно. Это означает, что если вы слушаете событие `keyup` и используете эти особые клавиши для перемещения героя, это также вызовет горизонтальную прокрутку. Поэтому вам может понадобиться *отключить* это встроенное поведение браузера при разработке игры. Для этого нужен следующий код:

```javascript
let onKeyDown = function (e) {
  console.log(e.keyCode);
  switch (e.keyCode) {
    case 37:
    case 39:
    case 38:
    case 40: // Arrow keys
    case 32:
      e.preventDefault();
      break; // Space
    default:
      break; // do not block other keys
  }
};

window.addEventListener('keydown', onKeyDown);
```

Этот код гарантирует, что клавиши-стрелки и пробел имеют отключенное *поведение по умолчанию*. Механизм отключения срабатывает, когда мы вызываем `e.preventDefault()`.

## Движение, инициированное игрой

Мы можем заставить объекты двигаться самостоятельно, используя таймеры, такие как функции `setTimeout()` или `setInterval()`, которые обновляют местоположение объекта на каждом такте или временном интервале. Вот как это может выглядеть:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## Игровой цикл

Игровой цикл — это концепция, которая представляет собой функцию, вызываемую через регулярные интервалы. Он называется игровым циклом, так как все, что должно быть видно пользователю, рисуется в этом цикле. Игровой цикл использует все игровые объекты, которые являются частью игры, рисуя их, если только они по какой-то причине больше не должны быть частью игры. Например, если объект — это враг, который был поражен лазером и взорвался, он больше не является частью текущего игрового цикла (вы узнаете больше об этом в следующих уроках).

Вот как игровой цикл может выглядеть в коде:

```javascript
let gameLoopId = setInterval(() =>
  function gameLoop() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = "black";
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    drawHero();
    drawEnemies();
    drawStaticObjects();
}, 200);
```

Этот цикл вызывается каждые `200` миллисекунд для перерисовки холста. Вы можете выбрать интервал, который лучше всего подходит для вашей игры.

## Продолжение космической игры

Вы возьмете существующий код и расширите его. Либо начните с кода, который вы завершили в части I, либо используйте код из [части II - начальный](../../../../6-space-game/3-moving-elements-around/your-work).

- **Перемещение героя**: вы добавите код, чтобы можно было перемещать героя с помощью клавиш-стрелок.
- **Перемещение врагов**: вам также нужно будет добавить код, чтобы враги перемещались сверху вниз с заданной скоростью.

## Рекомендуемые шаги

Найдите файлы, которые были созданы для вас в подпапке `your-work`. Она должна содержать следующее:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

Начните ваш проект в папке `your_work`, введя:

```bash
cd your-work
npm start
```

Этот код запустит HTTP-сервер по адресу `http://localhost:5000`. Откройте браузер и введите этот адрес, сейчас он должен отображать героя и всех врагов; пока ничего не движется!

### Добавьте код

1. **Добавьте отдельные объекты** для `hero`, `enemy` и `game object`, они должны иметь свойства `x` и `y`. (Помните раздел о [наследовании или композиции](../README.md)).

   *ПОДСКАЗКА*: `game object` должен быть объектом с `x` и `y` и способностью рисовать себя на холсте.

   >подсказка: начните с добавления нового класса GameObject с его конструктором, как показано ниже, а затем нарисуйте его на холсте:
  
    ```javascript
        
    class GameObject {
      constructor(x, y) {
        this.x = x;
        this.y = y;
        this.dead = false;
        this.type = "";
        this.width = 0;
        this.height = 0;
        this.img = undefined;
      }
    
      draw(ctx) {
        ctx.drawImage(this.img, this.x, this.y, this.width, this.height);
      }
    }
    ```

    Теперь расширьте этот GameObject, чтобы создать Hero и Enemy.
    
    ```javascript
    class Hero extends GameObject {
      constructor(x, y) {
        ...it needs an x, y, type, and speed
      }
    }
    ```

    ```javascript
    class Enemy extends GameObject {
      constructor(x, y) {
        super(x, y);
        (this.width = 98), (this.height = 50);
        this.type = "Enemy";
        let id = setInterval(() => {
          if (this.y < canvas.height - this.height) {
            this.y += 5;
          } else {
            console.log('Stopped at', this.y)
            clearInterval(id);
          }
        }, 300)
      }
    }
    ```

2. **Добавьте обработчики событий клавиш** для управления навигацией (перемещение героя вверх/вниз, влево/вправо).

   *ПОМИНИТЕ*: это декартова система, верхний левый угол — `0,0`. Также не забудьте добавить код для отключения *поведения по умолчанию*.

   >подсказка: создайте функцию onKeyDown и привяжите ее к окну:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   На этом этапе проверьте консоль вашего браузера и наблюдайте за регистрацией нажатий клавиш.

3. **Реализуйте** [паттерн Pub-Sub](../README.md), это поможет вам сохранить чистоту кода, следуя оставшимся частям.

   Для выполнения этого последнего шага вы можете:

   1. **Добавить слушатель событий** в окно:

       ```javascript
        window.addEventListener("keyup", (evt) => {
          if (evt.key === "ArrowUp") {
            eventEmitter.emit(Messages.KEY_EVENT_UP);
          } else if (evt.key === "ArrowDown") {
            eventEmitter.emit(Messages.KEY_EVENT_DOWN);
          } else if (evt.key === "ArrowLeft") {
            eventEmitter.emit(Messages.KEY_EVENT_LEFT);
          } else if (evt.key === "ArrowRight") {
            eventEmitter.emit(Messages.KEY_EVENT_RIGHT);
          }
        });
        ```

    1. **Создать класс EventEmitter** для публикации и подписки на сообщения:

        ```javascript
        class EventEmitter {
          constructor() {
            this.listeners = {};
          }
        
          on(message, listener) {
            if (!this.listeners[message]) {
              this.listeners[message] = [];
            }
            this.listeners[message].push(listener);
          }
        
          emit(message, payload = null) {
            if (this.listeners[message]) {
              this.listeners[message].forEach((l) => l(message, payload));
            }
          }
        }
        ```

    1. **Добавить константы** и настроить EventEmitter:

        ```javascript
        const Messages = {
          KEY_EVENT_UP: "KEY_EVENT_UP",
          KEY_EVENT_DOWN: "KEY_EVENT_DOWN",
          KEY_EVENT_LEFT: "KEY_EVENT_LEFT",
          KEY_EVENT_RIGHT: "KEY_EVENT_RIGHT",
        };
        
        let heroImg, 
            enemyImg, 
            laserImg,
            canvas, ctx, 
            gameObjects = [], 
            hero, 
            eventEmitter = new EventEmitter();
        ```

    1. **Инициализировать игру**

    ```javascript
    function initGame() {
      gameObjects = [];
      createEnemies();
      createHero();
    
      eventEmitter.on(Messages.KEY_EVENT_UP, () => {
        hero.y -=5 ;
      })
    
      eventEmitter.on(Messages.KEY_EVENT_DOWN, () => {
        hero.y += 5;
      });
    
      eventEmitter.on(Messages.KEY_EVENT_LEFT, () => {
        hero.x -= 5;
      });
    
      eventEmitter.on(Messages.KEY_EVENT_RIGHT, () => {
        hero.x += 5;
      });
    }
    ```

1. **Настройте игровой цикл**

   Переработайте функцию window.onload, чтобы инициализировать игру и настроить игровой цикл с подходящим интервалом. Вы также добавите лазерный луч:

    ```javascript
    window.onload = async () => {
      canvas = document.getElementById("canvas");
      ctx = canvas.getContext("2d");
      heroImg = await loadTexture("assets/player.png");
      enemyImg = await loadTexture("assets/enemyShip.png");
      laserImg = await loadTexture("assets/laserRed.png");
    
      initGame();
      let gameLoopId = setInterval(() => {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = "black";
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        drawGameObjects(ctx);
      }, 100)
      
    };
    ```

5. **Добавьте код** для перемещения врагов через определенные интервалы

    Переработайте функцию `createEnemies()`, чтобы создать врагов и добавить их в новый класс gameObjects:

    ```javascript
    function createEnemies() {
      const MONSTER_TOTAL = 5;
      const MONSTER_WIDTH = MONSTER_TOTAL * 98;
      const START_X = (canvas.width - MONSTER_WIDTH) / 2;
      const STOP_X = START_X + MONSTER_WIDTH;
    
      for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          const enemy = new Enemy(x, y);
          enemy.img = enemyImg;
          gameObjects.push(enemy);
        }
      }
    }
    ```
    
    и добавьте функцию `createHero()`, чтобы выполнить аналогичный процесс для героя.
    
    ```javascript
    function createHero() {
      hero = new Hero(
        canvas.width / 2 - 45,
        canvas.height - canvas.height / 4
      );
      hero.img = heroImg;
      gameObjects.push(hero);
    }
    ```

    и, наконец, добавьте функцию `drawGameObjects()`, чтобы начать рисование:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    Ваши враги должны начать наступать на ваш космический корабль!

---

## 🚀 Задание

Как вы видите, ваш код может превратиться в "спагетти-код", когда вы начинаете добавлять функции, переменные и классы. Как можно лучше организовать ваш код, чтобы он был более читаемым? Нарисуйте схему системы для организации вашего кода, даже если он все еще находится в одном файле.

## Викторина после лекции

[Викторина после лекции](https://ff-quizzes.netlify.app/web/quiz/34)

## Обзор и самостоятельное изучение

Хотя мы пишем нашу игру без использования фреймворков, существует множество фреймворков на основе JavaScript для разработки игр с использованием холста. Найдите время, чтобы [почитать о них](https://github.com/collections/javascript-game-engines).

## Задание

[Комментируйте ваш код](assignment.md)

---

**Отказ от ответственности**:  
Этот документ был переведен с использованием сервиса автоматического перевода [Co-op Translator](https://github.com/Azure/co-op-translator). Хотя мы стремимся к точности, пожалуйста, учитывайте, что автоматические переводы могут содержать ошибки или неточности. Оригинальный документ на его родном языке следует считать авторитетным источником. Для получения критически важной информации рекомендуется профессиональный перевод человеком. Мы не несем ответственности за любые недоразумения или неправильные интерпретации, возникающие в результате использования данного перевода.