<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a9a161871de7706cb0e23b1bd0c74559",
  "translation_date": "2025-08-28T18:13:28+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "uk"
}
-->
# Створення космічної гри, частина 3: Додавання руху

## Передлекційна вікторина

[Передлекційна вікторина](https://ff-quizzes.netlify.app/web/quiz/33)

Ігри стають цікавими, коли на екрані починають рухатися прибульці! У цій грі ми використаємо два типи руху:

- **Рух за допомогою клавіатури/миші**: коли користувач взаємодіє з клавіатурою або мишею, щоб перемістити об'єкт на екрані.
- **Рух, викликаний грою**: коли гра переміщує об'єкт через певний інтервал часу.

Отже, як ми можемо переміщувати об'єкти на екрані? Все зводиться до декартових координат: ми змінюємо розташування (x, y) об'єкта, а потім перемальовуємо екран.

Зазвичай для реалізації *руху* на екрані потрібні такі кроки:

1. **Встановити нове розташування** об'єкта; це необхідно, щоб створити враження, що об'єкт перемістився.
2. **Очистити екран**, оскільки екран потрібно очищати між малюваннями. Ми можемо очистити його, намалювавши прямокутник із фоновим кольором.
3. **Перемалювати об'єкт** у новому розташуванні. Таким чином ми досягаємо переміщення об'єкта з одного місця в інше.

Ось як це може виглядати в коді:

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

✅ Чи можете ви придумати причину, чому перемальовування вашого героя багато разів на секунду може призводити до витрат продуктивності? Прочитайте про [альтернативи цьому підходу](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas).

## Обробка подій клавіатури

Події обробляються шляхом прив'язки певних подій до коду. Події клавіатури викликаються для всього вікна, тоді як події миші, наприклад `click`, можуть бути прив'язані до натискання на конкретний елемент. У цьому проєкті ми будемо використовувати події клавіатури.

Щоб обробити подію, потрібно використати метод `addEventListener()` вікна і передати йому два параметри. Перший параметр — це назва події, наприклад `keyup`. Другий параметр — це функція, яка має бути викликана в результаті події.

Ось приклад:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

Для подій клавіатури є дві властивості події, які можна використовувати, щоб дізнатися, яка клавіша була натиснута:

- `key` — це рядкове представлення натиснутої клавіші, наприклад `ArrowUp`.
- `keyCode` — це числове представлення, наприклад `37`, що відповідає `ArrowLeft`.

✅ Маніпуляція подіями клавіатури корисна не лише в розробці ігор. Які ще застосування цього підходу ви можете придумати?

### Спеціальні клавіші: застереження

Деякі *спеціальні* клавіші впливають на вікно. Це означає, що якщо ви слухаєте подію `keyup` і використовуєте ці спеціальні клавіші для переміщення героя, це також викликатиме горизонтальну прокрутку. З цієї причини ви можете захотіти *вимкнути* цю вбудовану поведінку браузера під час створення гри. Для цього потрібен такий код:

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

Цей код забезпечить вимкнення *за замовчуванням* поведінки для клавіш зі стрілками та пробілу. Механізм *вимкнення* спрацьовує, коли ми викликаємо `e.preventDefault()`.

## Рух, викликаний грою

Ми можемо змусити об'єкти рухатися самостійно, використовуючи таймери, такі як функції `setTimeout()` або `setInterval()`, які оновлюють розташування об'єкта на кожному такті або інтервалі часу. Ось як це може виглядати:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## Ігровий цикл

Ігровий цикл — це концепція, яка по суті є функцією, що викликається через регулярні інтервали. Його називають ігровим циклом, оскільки все, що має бути видимим для користувача, малюється в цьому циклі. Ігровий цикл використовує всі ігрові об'єкти, які є частиною гри, малюючи їх, якщо вони не повинні більше бути частиною гри. Наприклад, якщо об'єкт — це ворог, якого вразив лазер і він вибухнув, він більше не є частиною поточного ігрового циклу (ви дізнаєтеся більше про це в наступних уроках).

Ось як типовий ігровий цикл може виглядати в коді:

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

Цей цикл викликається кожні `200` мілісекунд для перемальовування полотна. Ви можете вибрати інтервал, який найкраще підходить для вашої гри.

## Продовження космічної гри

Ви візьмете існуючий код і розширите його. Або почніть із коду, який ви завершили в частині I, або використовуйте код із [Part II- starter](../../../../6-space-game/3-moving-elements-around/your-work).

- **Рух героя**: ви додасте код, щоб забезпечити можливість переміщення героя за допомогою клавіш зі стрілками.
- **Рух ворогів**: вам також потрібно буде додати код, щоб вороги рухалися зверху вниз із заданою швидкістю.

## Рекомендовані кроки

Знайдіть файли, які були створені для вас у підпапці `your-work`. Вона має містити наступне:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

Запустіть ваш проєкт у папці `your_work`, ввівши:

```bash
cd your-work
npm start
```

Це запустить HTTP-сервер за адресою `http://localhost:5000`. Відкрийте браузер і введіть цю адресу. Зараз має відображатися герой і всі вороги; поки що нічого не рухається!

### Додайте код

1. **Додайте окремі об'єкти** для `hero`, `enemy` і `game object`, які повинні мати властивості `x` і `y`. (Згадайте розділ про [Спадкування або композицію](../README.md)).

   *ПІДКАЗКА*: `game object` має бути тим, що має `x` і `y`, а також здатність малювати себе на полотні.

   >порада: почніть із додавання нового класу GameObject із його конструктором, як показано нижче, а потім намалюйте його на полотні:
  
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

    Тепер розширте цей GameObject, щоб створити Hero і Enemy.
    
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

2. **Додайте обробники подій клавіш**, щоб обробляти навігацію клавішами (переміщення героя вгору/вниз, вліво/вправо).

   *ПАМ'ЯТАЙТЕ*: це декартова система, верхній лівий кут — це `0,0`. Також не забудьте додати код для зупинки *поведінки за замовчуванням*.

   >порада: створіть свою функцію onKeyDown і прив'яжіть її до вікна:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   Перевірте консоль браузера на цьому етапі та спостерігайте за реєстрацією натискань клавіш.

3. **Реалізуйте** [Шаблон публікації-підписки](../README.md), щоб ваш код залишався чистим у міру виконання наступних частин.

   Для цього останнього кроку ви можете:

   1. **Додати слухача подій** у вікно:

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

    1. **Створити клас EventEmitter** для публікації та підписки на повідомлення:

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

    1. **Додати константи** та налаштувати EventEmitter:

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

    1. **Ініціалізувати гру**

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

1. **Налаштуйте ігровий цикл**

   Рефакторизуйте функцію window.onload, щоб ініціалізувати гру та налаштувати ігровий цикл із відповідним інтервалом. Ви також додасте лазерний промінь:

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

5. **Додайте код** для руху ворогів із певним інтервалом

    Рефакторизуйте функцію `createEnemies()`, щоб створити ворогів і додати їх до нового класу gameObjects:

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
    
    і додайте функцію `createHero()`, щоб виконати подібний процес для героя.
    
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

    і нарешті, додайте функцію `drawGameObjects()`, щоб почати малювання:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    Ваші вороги мають почати наступати на ваш космічний корабель героя!

---

## 🚀 Виклик

Як ви бачите, ваш код може перетворитися на "спагеті-код", коли ви починаєте додавати функції, змінні та класи. Як ви можете краще організувати свій код, щоб він був більш читабельним? Накресліть систему для організації вашого коду, навіть якщо він все ще знаходиться в одному файлі.

## Післялекційна вікторина

[Післялекційна вікторина](https://ff-quizzes.netlify.app/web/quiz/34)

## Огляд і самостійне навчання

Хоча ми пишемо нашу гру без використання фреймворків, існує багато фреймворків на основі JavaScript для розробки ігор із використанням canvas. Приділіть час для [ознайомлення з ними](https://github.com/collections/javascript-game-engines).

## Завдання

[Коментуйте свій код](assignment.md)

---

**Відмова від відповідальності**:  
Цей документ був перекладений за допомогою сервісу автоматичного перекладу [Co-op Translator](https://github.com/Azure/co-op-translator). Хоча ми прагнемо до точності, будь ласка, майте на увазі, що автоматичні переклади можуть містити помилки або неточності. Оригінальний документ на його рідній мові слід вважати авторитетним джерелом. Для критичної інформації рекомендується професійний людський переклад. Ми не несемо відповідальності за будь-які непорозуміння або неправильні тлумачення, що виникають внаслідок використання цього перекладу.