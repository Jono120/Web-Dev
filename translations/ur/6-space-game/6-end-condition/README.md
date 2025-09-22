<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-28T15:25:02+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "ur"
}
-->
# خلا کا کھیل بنائیں حصہ 6: اختتام اور دوبارہ شروع کریں

## لیکچر سے پہلے کا کوئز

[لیکچر سے پہلے کا کوئز](https://ff-quizzes.netlify.app/web/quiz/39)

کھیل میں *اختتام کی حالت* کو ظاہر کرنے کے مختلف طریقے ہیں۔ یہ آپ پر منحصر ہے کہ آپ بطور کھیل کے تخلیق کار یہ طے کریں کہ کھیل کیوں ختم ہوا۔ اگر ہم اس خلا کے کھیل کی بات کریں جو آپ اب تک بنا رہے ہیں، تو یہاں کچھ وجوہات ہیں:

- **`N` دشمن جہاز تباہ ہو چکے ہیں**: یہ کافی عام ہے کہ اگر آپ کھیل کو مختلف سطحوں میں تقسیم کریں تو آپ کو ایک سطح مکمل کرنے کے لیے `N` دشمن جہاز تباہ کرنے ہوں گے۔
- **آپ کا جہاز تباہ ہو گیا ہے**: کچھ کھیل ایسے بھی ہیں جہاں اگر آپ کا جہاز تباہ ہو جائے تو آپ کھیل ہار جاتے ہیں۔ ایک اور عام طریقہ یہ ہے کہ آپ کے پاس زندگیوں کا تصور ہو۔ ہر بار جب آپ کا جہاز تباہ ہو تو ایک زندگی کم ہو جائے۔ جب تمام زندگیاں ختم ہو جائیں تو آپ کھیل ہار جاتے ہیں۔
- **آپ نے `N` پوائنٹس جمع کیے ہیں**: ایک اور عام اختتام کی حالت یہ ہے کہ آپ پوائنٹس جمع کریں۔ پوائنٹس حاصل کرنے کا طریقہ آپ پر منحصر ہے، لیکن عام طور پر دشمن جہاز کو تباہ کرنے یا ان اشیاء کو جمع کرنے پر پوائنٹس دیے جاتے ہیں جو تباہ ہونے پر گرتی ہیں۔
- **ایک سطح مکمل کریں**: اس میں کئی شرائط شامل ہو سکتی ہیں جیسے `X` دشمن جہاز تباہ کرنا، `Y` پوائنٹس جمع کرنا یا شاید کوئی خاص شے حاصل کرنا۔

## دوبارہ شروع کرنا

اگر لوگ آپ کے کھیل سے لطف اندوز ہوتے ہیں تو وہ اسے دوبارہ کھیلنا چاہیں گے۔ جب بھی کھیل کسی بھی وجہ سے ختم ہو جائے تو آپ کو دوبارہ شروع کرنے کا متبادل پیش کرنا چاہیے۔

✅ ذرا سوچیں کہ کن حالات میں آپ کو لگتا ہے کہ کھیل ختم ہوتا ہے، اور پھر آپ کو دوبارہ شروع کرنے کے لیے کیسے کہا جاتا ہے۔

## کیا بنانا ہے

آپ کو اپنے کھیل میں یہ اصول شامل کرنے ہوں گے:

1. **کھیل جیتنا**۔ جب تمام دشمن جہاز تباہ ہو جائیں تو آپ کھیل جیت جاتے ہیں۔ اس کے علاوہ، کسی قسم کا فتح کا پیغام بھی دکھائیں۔
1. **دوبارہ شروع کریں**۔ جب آپ کی تمام زندگیاں ختم ہو جائیں یا کھیل جیت لیا جائے، تو آپ کو کھیل دوبارہ شروع کرنے کا راستہ پیش کرنا چاہیے۔ یاد رکھیں! آپ کو کھیل کو دوبارہ شروع کرنا ہوگا اور پچھلی کھیل کی حالت کو صاف کرنا ہوگا۔

## تجویز کردہ مراحل

`your-work` سب فولڈر میں وہ فائلیں تلاش کریں جو آپ کے لیے بنائی گئی ہیں۔ اس میں درج ذیل شامل ہونا چاہیے:

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

آپ اپنے پروجیکٹ کو `your_work` فولڈر میں درج ذیل کمانڈ سے شروع کریں:

```bash
cd your-work
npm start
```

اوپر دی گئی کمانڈ ایک HTTP سرور `http://localhost:5000` ایڈریس پر شروع کرے گی۔ ایک براؤزر کھولیں اور اس ایڈریس کو درج کریں۔ آپ کا کھیل کھیلنے کے قابل حالت میں ہونا چاہیے۔

> ٹپ: Visual Studio Code میں وارننگز سے بچنے کے لیے، `window.onload` فنکشن کو اس طرح ایڈٹ کریں کہ وہ `gameLoopId` کو کال کرے جیسا کہ ہے (بغیر `let` کے)، اور `gameLoopId` کو فائل کے اوپر الگ سے ڈکلیئر کریں: `let gameLoopId;`

### کوڈ شامل کریں

1. **اختتام کی حالت کا ٹریک رکھیں**۔ ایسا کوڈ شامل کریں جو دشمنوں کی تعداد یا ہیرو جہاز کے تباہ ہونے کا ٹریک رکھے، ان دو فنکشنز کو شامل کر کے:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **پیغام ہینڈلرز میں منطق شامل کریں**۔ `eventEmitter` کو ان حالات کو ہینڈل کرنے کے لیے ایڈٹ کریں:

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

1. **نئے پیغام کی اقسام شامل کریں**۔ ان پیغامات کو constants آبجیکٹ میں شامل کریں:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **دوبارہ شروع کرنے کا کوڈ شامل کریں**۔ ایسا کوڈ شامل کریں جو منتخب کردہ بٹن دبانے پر کھیل کو دوبارہ شروع کرے۔

   1. **کلید دبانے `Enter` کو سنیں**۔ اپنے ونڈو کے eventListener کو اس کلید کو سننے کے لیے ایڈٹ کریں:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **دوبارہ شروع کرنے کا پیغام شامل کریں**۔ اس پیغام کو اپنے Messages constant میں شامل کریں:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **کھیل کے اصول نافذ کریں**۔ درج ذیل کھیل کے اصول نافذ کریں:

   1. **کھلاڑی کی جیت کی حالت**۔ جب تمام دشمن جہاز تباہ ہو جائیں، تو فتح کا پیغام دکھائیں۔

      1. پہلے، ایک `displayMessage()` فنکشن بنائیں:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. ایک `endGame()` فنکشن بنائیں:

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

   1. **دوبارہ شروع کرنے کی منطق**۔ جب تمام زندگیاں ختم ہو جائیں یا کھلاڑی کھیل جیت جائے، تو دکھائیں کہ کھیل دوبارہ شروع کیا جا سکتا ہے۔ اس کے علاوہ، جب *دوبارہ شروع کرنے* کی کلید دبائی جائے تو کھیل دوبارہ شروع کریں (آپ فیصلہ کر سکتے ہیں کہ کون سی کلید دوبارہ شروع کرنے کے لیے میپ کی جائے)۔

      1. `resetGame()` فنکشن بنائیں:

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

     1. `initGame()` میں کھیل کو دوبارہ ترتیب دینے کے لیے `eventEmitter` کو کال شامل کریں:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. EventEmitter میں ایک `clear()` فنکشن شامل کریں:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 مبارک ہو، کپتان! آپ کا کھیل مکمل ہو گیا ہے! شاندار کام! 🚀 💥 👽

---

## 🚀 چیلنج

آواز شامل کریں! کیا آپ کھیل کے تجربے کو بہتر بنانے کے لیے آواز شامل کر سکتے ہیں، شاید جب لیزر ہٹ کرے، یا ہیرو مر جائے یا جیت جائے؟ یہ دیکھنے کے لیے [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) پر ایک نظر ڈالیں کہ جاوا اسکرپٹ کا استعمال کرتے ہوئے آواز کیسے چلائی جائے۔

## لیکچر کے بعد کا کوئز

[لیکچر کے بعد کا کوئز](https://ff-quizzes.netlify.app/web/quiz/40)

## جائزہ اور خود مطالعہ

آپ کا اسائنمنٹ ایک نیا نمونہ کھیل بنانا ہے، لہذا وہاں موجود کچھ دلچسپ کھیلوں کو دریافت کریں تاکہ یہ دیکھ سکیں کہ آپ کس قسم کا کھیل بنا سکتے ہیں۔

## اسائنمنٹ

[ایک نمونہ کھیل بنائیں](assignment.md)

---

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا غیر درستیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔