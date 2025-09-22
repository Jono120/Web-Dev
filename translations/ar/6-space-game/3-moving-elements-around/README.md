<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a9a161871de7706cb0e23b1bd0c74559",
  "translation_date": "2025-08-28T15:01:21+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "ar"
}
-->
# بناء لعبة الفضاء الجزء الثالث: إضافة الحركة

## اختبار ما قبل المحاضرة

[اختبار ما قبل المحاضرة](https://ff-quizzes.netlify.app/web/quiz/33)

الألعاب ليست ممتعة كثيرًا حتى تبدأ الكائنات الفضائية بالتحرك على الشاشة! في هذه اللعبة، سنستخدم نوعين من الحركات:

- **حركة لوحة المفاتيح/الفأرة**: عندما يتفاعل المستخدم مع لوحة المفاتيح أو الفأرة لتحريك كائن على الشاشة.
- **حركة ناتجة عن اللعبة**: عندما تقوم اللعبة بتحريك كائن بفاصل زمني معين.

إذن، كيف نحرك الأشياء على الشاشة؟ الأمر كله يتعلق بالإحداثيات الكارتيزية: نقوم بتغيير موقع الكائن (x, y) ثم نعيد رسم الشاشة.

عادةً ما تحتاج إلى الخطوات التالية لتحقيق *الحركة* على الشاشة:

1. **تحديد موقع جديد** للكائن؛ هذا ضروري لإدراك أن الكائن قد تحرك.
2. **مسح الشاشة**، يجب مسح الشاشة بين عمليات الرسم. يمكننا مسحها برسم مستطيل بلون الخلفية.
3. **إعادة رسم الكائن** في الموقع الجديد. من خلال ذلك نحقق أخيرًا تحريك الكائن من موقع إلى آخر.

إليك كيف يمكن أن يبدو ذلك في الكود:

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

✅ هل يمكنك التفكير في سبب قد يؤدي إلى تكاليف أداء عند إعادة رسم بطلك عدة إطارات في الثانية؟ اقرأ عن [بدائل لهذا النمط](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas).

## التعامل مع أحداث لوحة المفاتيح

يمكنك التعامل مع الأحداث عن طريق ربط أحداث محددة بالكود. يتم تشغيل أحداث لوحة المفاتيح على النافذة بأكملها، بينما يمكن ربط أحداث الفأرة مثل `click` بالنقر على عنصر معين. سنستخدم أحداث لوحة المفاتيح طوال هذا المشروع.

للتعامل مع حدث، تحتاج إلى استخدام طريقة `addEventListener()` الخاصة بالنافذة وتزويدها بمعاملين. المعامل الأول هو اسم الحدث، مثل `keyup`. المعامل الثاني هو الدالة التي يجب استدعاؤها نتيجة لحدوث الحدث.

إليك مثال:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

بالنسبة لأحداث المفاتيح، هناك خاصيتان على الحدث يمكنك استخدامهما لمعرفة المفتاح الذي تم الضغط عليه:

- `key`، وهي تمثيل نصي للمفتاح المضغوط، مثل `ArrowUp`.
- `keyCode`، وهي تمثيل رقمي، مثل `37`، الذي يتوافق مع `ArrowLeft`.

✅ التلاعب بأحداث المفاتيح مفيد خارج تطوير الألعاب. ما هي الاستخدامات الأخرى التي يمكنك التفكير فيها لهذه التقنية؟

### المفاتيح الخاصة: تنبيه

هناك بعض المفاتيح *الخاصة* التي تؤثر على النافذة. هذا يعني أنه إذا كنت تستمع إلى حدث `keyup` واستخدمت هذه المفاتيح الخاصة لتحريك بطلك، فستؤدي أيضًا إلى التمرير الأفقي. لهذا السبب قد ترغب في *إيقاف* هذا السلوك الافتراضي للمتصفح أثناء بناء لعبتك. ستحتاج إلى كود مثل هذا:

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

يضمن الكود أعلاه أن مفاتيح الأسهم ومفتاح المسافة يتم *إيقاف* سلوكها الافتراضي. تحدث آلية *الإيقاف* عندما نستدعي `e.preventDefault()`.

## الحركة الناتجة عن اللعبة

يمكننا جعل الأشياء تتحرك من تلقاء نفسها باستخدام مؤقتات مثل دالة `setTimeout()` أو `setInterval()` التي تقوم بتحديث موقع الكائن في كل نبضة أو فاصل زمني. إليك كيف يمكن أن يبدو ذلك:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## حلقة اللعبة

حلقة اللعبة هي مفهوم يشير إلى دالة يتم استدعاؤها على فترات منتظمة. تُسمى حلقة اللعبة لأنها ترسم كل ما يجب أن يكون مرئيًا للمستخدم داخل الحلقة. تستخدم حلقة اللعبة جميع كائنات اللعبة التي تشكل جزءًا من اللعبة، وترسمها جميعًا ما لم يكن هناك سبب يجعلها ليست جزءًا من اللعبة بعد الآن. على سبيل المثال، إذا كان الكائن عدوًا أصيب بشعاع ليزر وانفجر، فلن يكون جزءًا من حلقة اللعبة الحالية (ستتعلم المزيد عن هذا في الدروس اللاحقة).

إليك كيف يمكن أن تبدو حلقة اللعبة عادةً، معبرًا عنها بالكود:

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

يتم استدعاء الحلقة أعلاه كل `200` مللي ثانية لإعادة رسم اللوحة. لديك القدرة على اختيار الفاصل الزمني الأنسب للعبتك.

## متابعة لعبة الفضاء

ستأخذ الكود الحالي وتقوم بتوسيعه. إما أن تبدأ بالكود الذي أكملته في الجزء الأول أو تستخدم الكود في [الجزء الثاني - البداية](../../../../6-space-game/3-moving-elements-around/your-work).

- **تحريك البطل**: ستضيف كودًا يضمن إمكانية تحريك البطل باستخدام مفاتيح الأسهم.
- **تحريك الأعداء**: ستحتاج أيضًا إلى إضافة كود يضمن تحرك الأعداء من الأعلى إلى الأسفل بمعدل معين.

## الخطوات الموصى بها

حدد الملفات التي تم إنشاؤها لك في مجلد `your-work`. يجب أن تحتوي على ما يلي:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

ابدأ مشروعك في مجلد `your_work` بكتابة:

```bash
cd your-work
npm start
```

سيؤدي ذلك إلى تشغيل خادم HTTP على العنوان `http://localhost:5000`. افتح متصفحًا وأدخل هذا العنوان، في الوقت الحالي يجب أن يعرض البطل وجميع الأعداء؛ لا شيء يتحرك - حتى الآن!

### إضافة الكود

1. **إضافة كائنات مخصصة** لـ `hero` و`enemy` و`game object`، يجب أن تحتوي على خصائص `x` و`y`. (تذكر الجزء الخاص بـ [الوراثة أو التركيب](../README.md)).

   *تلميح*: يجب أن يكون `game object` هو الكائن الذي يحتوي على `x` و`y` والقدرة على رسم نفسه على اللوحة.

   > تلميح: ابدأ بإضافة فئة GameObject جديدة مع مُنشئها كما هو موضح أدناه، ثم ارسمها على اللوحة:

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

    الآن، قم بتمديد GameObject لإنشاء البطل والعدو.

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

2. **إضافة معالجات أحداث المفاتيح** للتعامل مع التنقل بالمفاتيح (تحريك البطل لأعلى/أسفل، يسار/يمين).

   *تذكر*: إنه نظام إحداثيات كارتيزي، الزاوية العلوية اليسرى هي `0,0`. تذكر أيضًا إضافة كود لإيقاف *السلوك الافتراضي*.

   > تلميح: أنشئ دالة onKeyDown واربطها بالنافذة:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   تحقق من وحدة التحكم في المتصفح في هذه المرحلة، وشاهد ضغطات المفاتيح التي يتم تسجيلها.

3. **تنفيذ** [نمط النشر والاشتراك](../README.md)، سيحافظ هذا على نظافة الكود أثناء متابعة الأجزاء المتبقية.

   للقيام بهذا الجزء الأخير، يمكنك:

   1. **إضافة مستمع حدث** على النافذة:

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

    1. **إنشاء فئة EventEmitter** للنشر والاشتراك في الرسائل:

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

    1. **إضافة ثوابت** وإعداد EventEmitter:

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

    1. **تهيئة اللعبة**

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

1. **إعداد حلقة اللعبة**

   أعد كتابة دالة window.onload لتهيئة اللعبة وإعداد حلقة اللعبة بفاصل زمني مناسب. ستضيف أيضًا شعاع ليزر:

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

5. **إضافة كود** لتحريك الأعداء بفاصل زمني معين

    أعد كتابة دالة `createEnemies()` لإنشاء الأعداء ودفعهم إلى فئة gameObjects الجديدة:

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
    
    وأضف دالة `createHero()` للقيام بعملية مشابهة للبطل.

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

    وأخيرًا، أضف دالة `drawGameObjects()` لبدء الرسم:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    يجب أن يبدأ أعداؤك بالتقدم نحو سفينة البطل الفضائية!

---

## 🚀 التحدي

كما ترى، يمكن أن يتحول الكود الخاص بك إلى "كود سباغيتي" عندما تبدأ في إضافة وظائف ومتغيرات وفئات. كيف يمكنك تنظيم الكود الخاص بك بشكل أفضل ليكون أكثر قابلية للقراءة؟ قم برسم نظام لتنظيم الكود الخاص بك، حتى لو كان لا يزال موجودًا في ملف واحد.

## اختبار ما بعد المحاضرة

[اختبار ما بعد المحاضرة](https://ff-quizzes.netlify.app/web/quiz/34)

## المراجعة والدراسة الذاتية

بينما نكتب لعبتنا بدون استخدام أطر عمل، هناك العديد من أطر العمل المستندة إلى JavaScript لتطوير الألعاب باستخدام اللوحة. خصص بعض الوقت لقراءة المزيد عن [هذه الأطر](https://github.com/collections/javascript-game-engines).

## الواجب

[قم بتعليق الكود الخاص بك](assignment.md)

---

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الموثوق. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة ناتجة عن استخدام هذه الترجمة.