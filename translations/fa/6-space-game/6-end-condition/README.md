<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-29T14:31:06+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "fa"
}
-->
# ساخت یک بازی فضایی بخش ۶: پایان و شروع مجدد

## آزمون پیش از درس

[آزمون پیش از درس](https://ff-quizzes.netlify.app/web/quiz/39)

روش‌های مختلفی برای بیان یک *شرط پایان* در بازی وجود دارد. این شما هستید که به عنوان سازنده بازی تصمیم می‌گیرید چرا بازی به پایان رسیده است. در اینجا چند دلیل آورده شده است، اگر فرض کنیم در مورد بازی فضایی که تاکنون ساخته‌اید صحبت می‌کنیم:

- **`N` سفینه دشمن نابود شده است**: این روش بسیار رایج است، به خصوص اگر بازی را به مراحل مختلف تقسیم کنید و نیاز باشد `N` سفینه دشمن را برای تکمیل یک مرحله نابود کنید.
- **سفینه شما نابود شده است**: در برخی بازی‌ها، اگر سفینه شما نابود شود، بازی را می‌بازید. یک روش رایج دیگر این است که مفهوم "جان" را در بازی داشته باشید. هر بار که سفینه شما نابود می‌شود، یک جان از دست می‌دهید. وقتی تمام جان‌ها تمام شوند، بازی را می‌بازید.
- **شما `N` امتیاز جمع‌آوری کرده‌اید**: یک شرط پایان دیگر این است که شما امتیاز جمع‌آوری کنید. اینکه چگونه امتیاز کسب کنید به شما بستگی دارد، اما معمولاً به فعالیت‌هایی مانند نابود کردن سفینه دشمن یا جمع‌آوری آیتم‌هایی که هنگام نابودی دشمن‌ها رها می‌شوند، امتیاز تعلق می‌گیرد.
- **تکمیل یک مرحله**: این ممکن است شامل چندین شرط باشد، مانند نابودی `X` سفینه دشمن، جمع‌آوری `Y` امتیاز یا شاید جمع‌آوری یک آیتم خاص.

## شروع مجدد

اگر افراد از بازی شما لذت ببرند، احتمالاً می‌خواهند دوباره آن را بازی کنند. وقتی بازی به هر دلیلی تمام می‌شود، باید گزینه‌ای برای شروع مجدد ارائه دهید.

✅ کمی فکر کنید که تحت چه شرایطی یک بازی به پایان می‌رسد و سپس چگونه به شما پیشنهاد شروع مجدد داده می‌شود.

## چه چیزی بسازید

شما باید این قوانین را به بازی خود اضافه کنید:

1. **برنده شدن در بازی**. وقتی تمام سفینه‌های دشمن نابود شدند، شما بازی را می‌برید. همچنین یک پیام پیروزی نمایش دهید.
2. **شروع مجدد**. وقتی تمام جان‌های شما از دست رفت یا بازی برنده شد، باید راهی برای شروع مجدد بازی ارائه دهید. به یاد داشته باشید! شما باید بازی را دوباره مقداردهی اولیه کنید و وضعیت قبلی بازی را پاک کنید.

## مراحل پیشنهادی

فایل‌هایی که برای شما ایجاد شده‌اند را در پوشه `your-work` پیدا کنید. این پوشه باید شامل موارد زیر باشد:

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

پروژه خود را در پوشه `your_work` با تایپ کردن دستور زیر شروع کنید:

```bash
cd your-work
npm start
```

دستور بالا یک سرور HTTP را در آدرس `http://localhost:5000` راه‌اندازی می‌کند. یک مرورگر باز کنید و این آدرس را وارد کنید. بازی شما باید در حالت قابل بازی باشد.

> نکته: برای جلوگیری از هشدارها در Visual Studio Code، تابع `window.onload` را ویرایش کنید تا `gameLoopId` را همان‌طور که هست (بدون `let`) فراخوانی کند و متغیر `gameLoopId` را در بالای فایل به صورت مستقل تعریف کنید: `let gameLoopId;`

### اضافه کردن کد

1. **ردیابی شرط پایان**. کدی اضافه کنید که تعداد دشمنان یا نابودی سفینه قهرمان را ردیابی کند، با اضافه کردن این دو تابع:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **اضافه کردن منطق به مدیریت پیام‌ها**. `eventEmitter` را ویرایش کنید تا این شرایط را مدیریت کند:

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

1. **اضافه کردن انواع جدید پیام‌ها**. این پیام‌ها را به شیء constants اضافه کنید:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **اضافه کردن کد شروع مجدد** کدی که بازی را با فشار یک دکمه انتخابی دوباره شروع کند.

   1. **گوش دادن به فشار کلید `Enter`**. EventListener پنجره خود را ویرایش کنید تا به این فشار گوش دهد:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **اضافه کردن پیام شروع مجدد**. این پیام را به ثابت Messages اضافه کنید:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **پیاده‌سازی قوانین بازی**. قوانین زیر را پیاده‌سازی کنید:

   1. **شرط برد بازیکن**. وقتی تمام سفینه‌های دشمن نابود شدند، یک پیام پیروزی نمایش دهید.

      1. ابتدا یک تابع `displayMessage()` ایجاد کنید:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. یک تابع `endGame()` ایجاد کنید:

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

   1. **منطق شروع مجدد**. وقتی تمام جان‌ها از دست رفت یا بازیکن بازی را برد، نمایش دهید که بازی می‌تواند دوباره شروع شود. همچنین وقتی کلید *شروع مجدد* فشرده شد، بازی را دوباره شروع کنید (می‌توانید تصمیم بگیرید که کدام کلید به شروع مجدد اختصاص داده شود).

      1. تابع `resetGame()` را ایجاد کنید:

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

     1. یک فراخوانی به `eventEmitter` برای بازنشانی بازی در `initGame()` اضافه کنید:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. یک تابع `clear()` به EventEmitter اضافه کنید:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 تبریک می‌گویم، کاپیتان! بازی شما کامل شد! آفرین! 🚀 💥 👽

---

## 🚀 چالش

یک صدا اضافه کنید! آیا می‌توانید یک صدا برای بهبود تجربه بازی اضافه کنید، مثلاً وقتی لیزر برخورد می‌کند، یا قهرمان می‌میرد یا برنده می‌شود؟ به این [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) نگاهی بیندازید تا یاد بگیرید چگونه با استفاده از JavaScript صدا پخش کنید.

## آزمون پس از درس

[آزمون پس از درس](https://ff-quizzes.netlify.app/web/quiz/40)

## مرور و مطالعه شخصی

تکلیف شما این است که یک نمونه بازی جدید ایجاد کنید، بنابراین برخی از بازی‌های جالب موجود را بررسی کنید تا ببینید چه نوع بازی‌ای ممکن است بسازید.

## تکلیف

[ساخت یک بازی نمونه](assignment.md)

---

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما برای دقت تلاش می‌کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نادرستی‌هایی باشند. سند اصلی به زبان بومی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما هیچ مسئولیتی در قبال سوءتفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.