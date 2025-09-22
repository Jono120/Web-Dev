<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "adda95e02afa3fbee67b6e385b1109e1",
  "translation_date": "2025-08-29T14:29:49+00:00",
  "source_file": "6-space-game/5-keeping-score/README.md",
  "language_code": "fa"
}
-->
# ساخت یک بازی فضایی قسمت ۵: امتیازدهی و جان‌ها

## آزمون پیش از درس

[آزمون پیش از درس](https://ff-quizzes.netlify.app/web/quiz/37)

در این درس، یاد می‌گیرید که چگونه به یک بازی امتیاز اضافه کنید و جان‌ها را محاسبه کنید.

## نمایش متن روی صفحه

برای اینکه بتوانید امتیاز بازی را روی صفحه نمایش دهید، باید بدانید چگونه متن را روی صفحه قرار دهید. پاسخ استفاده از متد `fillText()` روی شیء canvas است. همچنین می‌توانید جنبه‌های دیگری مانند نوع فونت، رنگ متن و حتی تراز آن (چپ، راست، مرکز) را کنترل کنید. در زیر کدی آورده شده که متنی را روی صفحه نمایش می‌دهد.

```javascript
ctx.font = "30px Arial";
ctx.fillStyle = "red";
ctx.textAlign = "right";
ctx.fillText("show this on the screen", 0, 0);
```

✅ درباره [چگونگی اضافه کردن متن به canvas](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_text) بیشتر بخوانید و اگر دوست دارید، ظاهر آن را جذاب‌تر کنید!

## جان، به عنوان یک مفهوم در بازی

مفهوم داشتن جان در یک بازی فقط یک عدد است. در زمینه یک بازی فضایی، معمولاً مجموعه‌ای از جان‌ها اختصاص داده می‌شود که با هر بار آسیب دیدن سفینه شما، یکی از آن‌ها کم می‌شود. اگر بتوانید نمایش گرافیکی از این جان‌ها مانند سفینه‌های کوچک یا قلب‌ها به جای یک عدد نشان دهید، جذاب‌تر خواهد بود.

## چه چیزی بسازیم؟

بیایید موارد زیر را به بازی خود اضافه کنیم:

- **امتیاز بازی**: برای هر سفینه دشمن که نابود می‌شود، باید به قهرمان امتیاز داده شود. پیشنهاد ما ۱۰۰ امتیاز برای هر سفینه است. امتیاز بازی باید در پایین سمت چپ نمایش داده شود.
- **جان‌ها**: سفینه شما سه جان دارد. هر بار که یک سفینه دشمن با شما برخورد کند، یک جان از دست می‌دهید. تعداد جان‌ها باید در پایین سمت راست نمایش داده شود و از گرافیک زیر تشکیل شده باشد: ![تصویر جان](../../../../translated_images/life.6fb9f50d53ee0413cd91aa411f7c296e10a1a6de5c4a4197c718b49bf7d63ebf.fa.png).

## مراحل پیشنهادی

فایل‌هایی که برای شما ایجاد شده‌اند را در پوشه `your-work` پیدا کنید. این پوشه باید شامل موارد زیر باشد:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
-| index.html
-| app.js
-| package.json
```

پروژه خود را با پوشه `your_work` شروع کنید و دستور زیر را تایپ کنید:

```bash
cd your-work
npm start
```

دستور بالا یک سرور HTTP را در آدرس `http://localhost:5000` راه‌اندازی می‌کند. یک مرورگر باز کنید و این آدرس را وارد کنید. در حال حاضر باید قهرمان و تمام دشمنان را نمایش دهد و وقتی کلیدهای چپ و راست را فشار می‌دهید، قهرمان حرکت می‌کند و می‌تواند دشمنان را شلیک کند.

### اضافه کردن کد

1. **کپی کردن دارایی‌های مورد نیاز** از پوشه `solution/assets/` به پوشه `your-work`؛ شما باید فایل `life.png` را اضافه کنید. `lifeImg` را به تابع window.onload اضافه کنید:

    ```javascript
    lifeImg = await loadTexture("assets/life.png");
    ```

2. `lifeImg` را به لیست دارایی‌ها اضافه کنید:

    ```javascript
    let heroImg,
    ...
    lifeImg,
    ...
    eventEmitter = new EventEmitter();
    ```
  
3. **اضافه کردن متغیرها**. کدی اضافه کنید که امتیاز کل شما (۰) و تعداد جان‌های باقی‌مانده (۳) را نشان دهد و این مقادیر را روی صفحه نمایش دهید.

4. **گسترش تابع `updateGameObjects()`**. تابع `updateGameObjects()` را برای مدیریت برخوردهای دشمن گسترش دهید:

    ```javascript
    enemies.forEach(enemy => {
        const heroRect = hero.rectFromGameObject();
        if (intersectRect(heroRect, enemy.rectFromGameObject())) {
          eventEmitter.emit(Messages.COLLISION_ENEMY_HERO, { enemy });
        }
      })
    ```

5. **اضافه کردن `life` و `points`**. 
   1. **مقداردهی اولیه متغیرها**. زیر `this.cooldown = 0` در کلاس `Hero`، متغیرهای life و points را تنظیم کنید:

        ```javascript
        this.life = 3;
        this.points = 0;
        ```

   2. **نمایش متغیرها روی صفحه**. این مقادیر را روی صفحه نمایش دهید:

        ```javascript
        function drawLife() {
          // TODO, 35, 27
          const START_POS = canvas.width - 180;
          for(let i=0; i < hero.life; i++ ) {
            ctx.drawImage(
              lifeImg, 
              START_POS + (45 * (i+1) ), 
              canvas.height - 37);
          }
        }
        
        function drawPoints() {
          ctx.font = "30px Arial";
          ctx.fillStyle = "red";
          ctx.textAlign = "left";
          drawText("Points: " + hero.points, 10, canvas.height-20);
        }
        
        function drawText(message, x, y) {
          ctx.fillText(message, x, y);
        }

        ```

   3. **اضافه کردن متدها به حلقه بازی**. مطمئن شوید که این توابع را به تابع window.onload خود زیر `updateGameObjects()` اضافه کنید:

        ```javascript
        drawPoints();
        drawLife();
        ```

6. **پیاده‌سازی قوانین بازی**. قوانین زیر را پیاده‌سازی کنید:

   1. **برای هر برخورد قهرمان و دشمن**، یک جان کم کنید.
   
      کلاس `Hero` را برای این کاهش گسترش دهید:

        ```javascript
        decrementLife() {
          this.life--;
          if (this.life === 0) {
            this.dead = true;
          }
        }
        ```

   2. **برای هر لیزری که به دشمن برخورد کند**، امتیاز بازی را ۱۰۰ امتیاز افزایش دهید.

      کلاس `Hero` را برای این افزایش گسترش دهید:
    
        ```javascript
          incrementPoints() {
            this.points += 100;
          }
        ```

        این توابع را به Collision Event Emitters خود اضافه کنید:

        ```javascript
        eventEmitter.on(Messages.COLLISION_ENEMY_LASER, (_, { first, second }) => {
           first.dead = true;
           second.dead = true;
           hero.incrementPoints();
        })

        eventEmitter.on(Messages.COLLISION_ENEMY_HERO, (_, { enemy }) => {
           enemy.dead = true;
           hero.decrementLife();
        });
        ```

✅ کمی تحقیق کنید تا بازی‌های دیگری که با استفاده از JavaScript/Canvas ساخته شده‌اند را کشف کنید. ویژگی‌های مشترک آن‌ها چیست؟

در پایان این کار، باید سفینه‌های کوچک "جان" را در پایین سمت راست، امتیازات را در پایین سمت چپ ببینید و مشاهده کنید که تعداد جان‌ها با برخورد با دشمنان کاهش می‌یابد و امتیازات شما با شلیک به دشمنان افزایش می‌یابد. آفرین! بازی شما تقریباً کامل است.

---

## 🚀 چالش

کد شما تقریباً کامل است. آیا می‌توانید مراحل بعدی خود را تصور کنید؟

## آزمون پس از درس

[آزمون پس از درس](https://ff-quizzes.netlify.app/web/quiz/38)

## مرور و مطالعه شخصی

روش‌هایی را برای افزایش و کاهش امتیازات و جان‌های بازی تحقیق کنید. موتورهای بازی جالبی مانند [PlayFab](https://playfab.com) وجود دارند. استفاده از یکی از این‌ها چگونه می‌تواند بازی شما را بهبود بخشد؟

## تکلیف

[ساخت یک بازی امتیازی](assignment.md)

---

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما برای دقت تلاش می‌کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نادرستی‌هایی باشند. سند اصلی به زبان اصلی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما هیچ مسئولیتی در قبال سوءتفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.