<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a9a161871de7706cb0e23b1bd0c74559",
  "translation_date": "2025-08-29T14:29:20+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "fa"
}
-->
# ساخت یک بازی فضایی قسمت ۳: اضافه کردن حرکت

## آزمون پیش از درس

[آزمون پیش از درس](https://ff-quizzes.netlify.app/web/quiz/33)

بازی‌ها تا زمانی که موجودات فضایی روی صفحه حرکت نکنند خیلی جذاب نیستند! در این بازی، ما از دو نوع حرکت استفاده خواهیم کرد:

- **حرکت با کیبورد/ماوس**: زمانی که کاربر با استفاده از کیبورد یا ماوس یک شیء را روی صفحه حرکت می‌دهد.
- **حرکت ایجاد شده توسط بازی**: زمانی که بازی یک شیء را در یک بازه زمانی مشخص حرکت می‌دهد.

پس چگونه می‌توانیم اشیاء را روی صفحه حرکت دهیم؟ همه چیز به مختصات دکارتی مربوط می‌شود: ما مکان (x,y) شیء را تغییر می‌دهیم و سپس صفحه را دوباره رسم می‌کنیم.

معمولاً برای انجام *حرکت* روی صفحه به مراحل زیر نیاز دارید:

1. **تنظیم مکان جدید** برای یک شیء؛ این کار برای اینکه شیء به نظر برسد که حرکت کرده ضروری است.
2. **پاک کردن صفحه**؛ صفحه باید بین رسم‌ها پاک شود. می‌توانیم این کار را با رسم یک مستطیل که با رنگ پس‌زمینه پر شده انجام دهیم.
3. **رسم مجدد شیء** در مکان جدید. با این کار، در نهایت حرکت شیء از یک مکان به مکان دیگر انجام می‌شود.

این کد می‌تواند به این شکل باشد:

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

✅ آیا می‌توانید دلیلی بیاورید که چرا رسم مجدد قهرمان در هر فریم ممکن است هزینه‌های عملکردی ایجاد کند؟ درباره [جایگزین‌های این الگو](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas) بخوانید.

## مدیریت رویدادهای کیبورد

شما رویدادها را با اتصال رویدادهای خاص به کد مدیریت می‌کنید. رویدادهای کیبورد روی کل پنجره فعال می‌شوند، در حالی که رویدادهای ماوس مانند `click` می‌توانند به کلیک روی یک عنصر خاص متصل شوند. ما در طول این پروژه از رویدادهای کیبورد استفاده خواهیم کرد.

برای مدیریت یک رویداد، باید از متد `addEventListener()` پنجره استفاده کنید و دو پارامتر ورودی به آن بدهید. پارامتر اول نام رویداد است، برای مثال `keyup`. پارامتر دوم تابعی است که باید به عنوان نتیجه وقوع رویداد اجرا شود.

این یک مثال است:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

برای رویدادهای کلید، دو ویژگی روی رویداد وجود دارد که می‌توانید از آنها برای دیدن کلید فشرده شده استفاده کنید:

- `key`، این یک نمایش رشته‌ای از کلید فشرده شده است، برای مثال `ArrowUp`.
- `keyCode`، این یک نمایش عددی است، برای مثال `37`، که به `ArrowLeft` مربوط می‌شود.

✅ دستکاری رویدادهای کلید خارج از توسعه بازی نیز مفید است. چه استفاده‌های دیگری می‌توانید برای این تکنیک تصور کنید؟

### کلیدهای خاص: یک هشدار

برخی کلیدهای *خاص* وجود دارند که روی پنجره تأثیر می‌گذارند. این بدان معناست که اگر شما به یک رویداد `keyup` گوش دهید و از این کلیدهای خاص برای حرکت دادن قهرمان خود استفاده کنید، همچنین باعث پیمایش افقی خواهد شد. به همین دلیل ممکن است بخواهید این رفتار داخلی مرورگر را هنگام ساخت بازی خود *خاموش کنید*. شما به کدی مانند این نیاز دارید:

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

کد بالا اطمینان حاصل می‌کند که کلیدهای جهت‌دار و کلید فاصله رفتار *پیش‌فرض* خود را خاموش کرده‌اند. مکانیزم *خاموش کردن* زمانی اتفاق می‌افتد که ما `e.preventDefault()` را فراخوانی می‌کنیم.

## حرکت ایجاد شده توسط بازی

ما می‌توانیم اشیاء را با استفاده از تایمرهایی مانند `setTimeout()` یا `setInterval()` که مکان شیء را در هر تیک یا بازه زمانی به‌روزرسانی می‌کنند، به حرکت درآوریم. این کد می‌تواند به این شکل باشد:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## حلقه بازی

حلقه بازی مفهومی است که اساساً یک تابع است که در فواصل منظم فراخوانی می‌شود. به آن حلقه بازی گفته می‌شود زیرا همه چیزهایی که باید برای کاربر قابل مشاهده باشند در این حلقه رسم می‌شوند. حلقه بازی از همه اشیاء بازی که بخشی از بازی هستند استفاده می‌کند و همه آنها را رسم می‌کند، مگر اینکه به دلایلی دیگر نباید بخشی از بازی باشند. برای مثال، اگر یک شیء دشمن باشد که توسط یک لیزر مورد اصابت قرار گرفته و منفجر شده، دیگر بخشی از حلقه بازی فعلی نیست (در درس‌های بعدی بیشتر درباره این موضوع یاد خواهید گرفت).

این کد می‌تواند به این شکل باشد:

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

حلقه بالا هر `200` میلی‌ثانیه فراخوانی می‌شود تا بوم را دوباره رسم کند. شما می‌توانید بهترین بازه زمانی را که برای بازی شما منطقی است انتخاب کنید.

## ادامه بازی فضایی

شما کد موجود را گسترش خواهید داد. یا با کدی که در قسمت اول تکمیل کرده‌اید شروع کنید یا از کد [قسمت دوم - شروع](../../../../6-space-game/3-moving-elements-around/your-work) استفاده کنید.

- **حرکت دادن قهرمان**: شما کدی اضافه خواهید کرد تا بتوانید قهرمان را با استفاده از کلیدهای جهت‌دار حرکت دهید.
- **حرکت دادن دشمنان**: شما همچنین باید کدی اضافه کنید تا دشمنان از بالا به پایین با نرخ مشخص حرکت کنند.

## مراحل پیشنهادی

فایل‌هایی را که برای شما در پوشه `your-work` ایجاد شده‌اند پیدا کنید. باید شامل موارد زیر باشد:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

پروژه خود را در پوشه `your_work` با تایپ کردن شروع کنید:

```bash
cd your-work
npm start
```

کد بالا یک سرور HTTP را در آدرس `http://localhost:5000` راه‌اندازی می‌کند. یک مرورگر باز کنید و آن آدرس را وارد کنید، در حال حاضر باید قهرمان و همه دشمنان را نمایش دهد؛ هنوز هیچ چیزی حرکت نمی‌کند!

### اضافه کردن کد

1. **اضافه کردن اشیاء اختصاصی** برای `hero` و `enemy` و `game object`، آنها باید ویژگی‌های `x` و `y` داشته باشند. (بخش [وراثت یا ترکیب](../README.md) را به یاد داشته باشید).

   *نکته*: `game object` باید شیئی باشد که ویژگی‌های `x` و `y` و توانایی رسم خود روی بوم را داشته باشد.

   >نکته: با اضافه کردن یک کلاس GameObject جدید با سازنده‌ای که به شکل زیر مشخص شده شروع کنید و سپس آن را روی بوم رسم کنید:

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

    حالا این GameObject را گسترش دهید تا قهرمان و دشمن ایجاد شود.

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

2. **اضافه کردن مدیریت‌کننده‌های رویداد کلید** برای مدیریت ناوبری کلید (حرکت دادن قهرمان به بالا/پایین چپ/راست)

   *به یاد داشته باشید*: این یک سیستم دکارتی است، بالا-چپ `0,0` است. همچنین به یاد داشته باشید که کدی اضافه کنید تا *رفتار پیش‌فرض* متوقف شود.

   >نکته: تابع onKeyDown خود را ایجاد کنید و آن را به پنجره متصل کنید:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   در این مرحله کنسول مرورگر خود را بررسی کنید و ضربات کلید را مشاهده کنید.

3. **پیاده‌سازی کنید** [الگوی انتشار-اشتراک](../README.md)، این کار کد شما را تمیز نگه می‌دارد زیرا قسمت‌های باقی‌مانده را دنبال می‌کنید.

   برای انجام این قسمت آخر، می‌توانید:

   1. **یک شنونده رویداد** به پنجره اضافه کنید:

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

    1. **یک کلاس EventEmitter ایجاد کنید** برای انتشار و اشتراک پیام‌ها:

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

    1. **ثابت‌ها اضافه کنید** و EventEmitter را تنظیم کنید:

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

    1. **بازی را مقداردهی اولیه کنید**

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

1. **حلقه بازی را تنظیم کنید**

   تابع window.onload را بازنویسی کنید تا بازی را مقداردهی اولیه کند و یک حلقه بازی را در یک بازه زمانی مناسب تنظیم کند. همچنین یک پرتو لیزری اضافه خواهید کرد:

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

5. **کد اضافه کنید** تا دشمنان در یک بازه زمانی مشخص حرکت کنند

    تابع `createEnemies()` را بازنویسی کنید تا دشمنان ایجاد شوند و آنها را به کلاس جدید gameObjects اضافه کنید:

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
    
    و یک تابع `createHero()` ایجاد کنید تا فرآیند مشابهی را برای قهرمان انجام دهد.

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

    و در نهایت، یک تابع `drawGameObjects()` اضافه کنید تا رسم را شروع کند:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    دشمنان شما باید شروع به پیشروی به سمت سفینه فضایی قهرمان شما کنند!

---

## 🚀 چالش

همانطور که می‌بینید، کد شما ممکن است به کد 'اسپاگتی' تبدیل شود وقتی شروع به اضافه کردن توابع و متغیرها و کلاس‌ها می‌کنید. چگونه می‌توانید کد خود را بهتر سازماندهی کنید تا خواناتر باشد؟ یک سیستم برای سازماندهی کد خود طراحی کنید، حتی اگر هنوز در یک فایل قرار دارد.

## آزمون پس از درس

[آزمون پس از درس](https://ff-quizzes.netlify.app/web/quiz/34)

## مرور و مطالعه شخصی

در حالی که ما بازی خود را بدون استفاده از فریم‌ورک‌ها می‌نویسیم، فریم‌ورک‌های مبتنی بر Canvas جاوااسکریپت زیادی برای توسعه بازی وجود دارند. زمانی را برای [مطالعه درباره این‌ها](https://github.com/collections/javascript-game-engines) اختصاص دهید.

## تکلیف

[کد خود را توضیح دهید](assignment.md)

---

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما برای دقت تلاش می‌کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نادقتی‌هایی باشند. سند اصلی به زبان اصلی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما هیچ مسئولیتی در قبال سوءتفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.