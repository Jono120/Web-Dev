<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "adda95e02afa3fbee67b6e385b1109e1",
  "translation_date": "2025-08-28T15:23:41+00:00",
  "source_file": "6-space-game/5-keeping-score/README.md",
  "language_code": "ur"
}
-->
# اسپیس گیم بنائیں حصہ 5: اسکورنگ اور زندگیاں

## لیکچر سے پہلے کا کوئز

[لیکچر سے پہلے کا کوئز](https://ff-quizzes.netlify.app/web/quiz/37)

اس سبق میں، آپ سیکھیں گے کہ گیم میں اسکور کیسے شامل کیا جائے اور زندگیاں کیسے شمار کی جائیں۔

## اسکرین پر متن دکھائیں

گیم کا اسکور اسکرین پر دکھانے کے لیے، آپ کو یہ جاننا ہوگا کہ اسکرین پر متن کیسے رکھا جائے۔ اس کا جواب ہے `fillText()` میتھڈ کا استعمال کینوس آبجیکٹ پر۔ آپ دیگر پہلوؤں کو بھی کنٹرول کر سکتے ہیں جیسے کہ کون سا فونٹ استعمال کرنا ہے، متن کا رنگ اور اس کی سیدھ (بائیں، دائیں، درمیان)۔ نیچے کچھ کوڈ دیا گیا ہے جو اسکرین پر متن ڈرا کرتا ہے۔

```javascript
ctx.font = "30px Arial";
ctx.fillStyle = "red";
ctx.textAlign = "right";
ctx.fillText("show this on the screen", 0, 0);
```

✅ مزید پڑھیں [کینوس پر متن کیسے شامل کریں](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_text)، اور اپنی تخلیق کو مزید خوبصورت بنانے کے لیے آزاد ہیں!

## زندگی، گیم کا ایک تصور

گیم میں زندگی کا تصور صرف ایک عدد ہے۔ اسپیس گیم کے تناظر میں، عام طور پر کچھ زندگیاں دی جاتی ہیں جو آپ کے جہاز کو نقصان پہنچنے پر ایک ایک کر کے کم ہوتی ہیں۔ اگر آپ اسے گرافیکل طور پر دکھا سکیں جیسے چھوٹے جہاز یا دل، تو یہ زیادہ اچھا لگتا ہے۔

## کیا بنانا ہے

اپنے گیم میں درج ذیل شامل کریں:

- **گیم اسکور**: ہر دشمن جہاز کو تباہ کرنے پر، ہیرو کو کچھ پوائنٹس ملنے چاہئیں، ہم تجویز کرتے ہیں کہ ہر جہاز کے لیے 100 پوائنٹس۔ گیم اسکور نیچے بائیں جانب دکھایا جانا چاہیے۔
- **زندگی**: آپ کے جہاز کے پاس تین زندگیاں ہیں۔ ہر بار جب کوئی دشمن جہاز آپ سے ٹکراتا ہے، آپ کی ایک زندگی کم ہو جاتی ہے۔ زندگی کا اسکور نیچے دائیں جانب دکھایا جانا چاہیے اور درج ذیل گرافک سے بنایا جانا چاہیے ![زندگی کی تصویر](../../../../translated_images/life.6fb9f50d53ee0413cd91aa411f7c296e10a1a6de5c4a4197c718b49bf7d63ebf.ur.png)۔

## تجویز کردہ اقدامات

ان فائلوں کو تلاش کریں جو آپ کے لیے `your-work` سب فولڈر میں بنائی گئی ہیں۔ اس میں درج ذیل شامل ہونا چاہیے:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
-| index.html
-| app.js
-| package.json
```

اپنا پروجیکٹ `your_work` فولڈر میں شروع کریں، درج ذیل کمانڈ ٹائپ کریں:

```bash
cd your-work
npm start
```

اوپر دی گئی کمانڈ ایک HTTP سرور ایڈریس `http://localhost:5000` پر شروع کرے گی۔ ایک براؤزر کھولیں اور اس ایڈریس کو درج کریں، اس وقت یہ ہیرو اور تمام دشمنوں کو رینڈر کرے گا، اور جب آپ اپنے بائیں اور دائیں تیر کے بٹن دبائیں گے، تو ہیرو حرکت کرے گا اور دشمنوں کو گرا سکے گا۔

### کوڈ شامل کریں

1. **ضروری اثاثے کاپی کریں**۔ `solution/assets/` فولڈر سے `your-work` فولڈر میں ضروری اثاثے کاپی کریں؛ آپ کو `life.png` اثاثہ شامل کرنا ہوگا۔ `window.onload` فنکشن میں lifeImg شامل کریں:

    ```javascript
    lifeImg = await loadTexture("assets/life.png");
    ```

1. `lifeImg` کو اثاثوں کی فہرست میں شامل کریں:

    ```javascript
    let heroImg,
    ...
    lifeImg,
    ...
    eventEmitter = new EventEmitter();
    ```
  
2. **ویری ایبلز شامل کریں**۔ ایسا کوڈ شامل کریں جو آپ کے کل اسکور (0) اور باقی زندگیاں (3) کو ظاہر کرے، اور ان اسکورز کو اسکرین پر دکھائیں۔

3. **`updateGameObjects()` فنکشن کو بڑھائیں**۔ `updateGameObjects()` فنکشن کو دشمنوں کے تصادم کو ہینڈل کرنے کے لیے بڑھائیں:

    ```javascript
    enemies.forEach(enemy => {
        const heroRect = hero.rectFromGameObject();
        if (intersectRect(heroRect, enemy.rectFromGameObject())) {
          eventEmitter.emit(Messages.COLLISION_ENEMY_HERO, { enemy });
        }
      })
    ```

4. **زندگی اور پوائنٹس شامل کریں**۔ 
   1. **ویری ایبلز کو انیشیالائز کریں**۔ `Hero` کلاس میں `this.cooldown = 0` کے نیچے زندگی اور پوائنٹس سیٹ کریں:

        ```javascript
        this.life = 3;
        this.points = 0;
        ```

   1. **ویری ایبلز کو اسکرین پر ڈرا کریں**۔ ان ویلیوز کو اسکرین پر ڈرا کریں:

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

   1. **گیم لوپ میں میتھڈز شامل کریں**۔ ان فنکشنز کو `updateGameObjects()` کے نیچے `window.onload` فنکشن میں شامل کریں:

        ```javascript
        drawPoints();
        drawLife();
        ```

1. **گیم کے اصول نافذ کریں**۔ درج ذیل گیم اصول نافذ کریں:

   1. **ہر ہیرو اور دشمن کے تصادم پر**، ایک زندگی کم کریں۔
   
      `Hero` کلاس کو اس کمی کے لیے بڑھائیں:

        ```javascript
        decrementLife() {
          this.life--;
          if (this.life === 0) {
            this.dead = true;
          }
        }
        ```

   2. **ہر لیزر جو دشمن کو لگے**، گیم اسکور میں 100 پوائنٹس کا اضافہ کریں۔

      `Hero` کلاس کو اس اضافے کے لیے بڑھائیں:
    
        ```javascript
          incrementPoints() {
            this.points += 100;
          }
        ```

        ان فنکشنز کو اپنے Collision Event Emitters میں شامل کریں:

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

✅ تھوڑی تحقیق کریں اور دریافت کریں کہ جاوا اسکرپٹ/کینوس کا استعمال کرتے ہوئے بنائے گئے دیگر گیمز کون سے ہیں۔ ان کے عام خصوصیات کیا ہیں؟

اس کام کے اختتام پر، آپ کو نیچے دائیں جانب چھوٹے 'زندگی' کے جہاز، نیچے بائیں جانب پوائنٹس، اور دشمنوں سے ٹکرانے پر زندگی کی گنتی کم ہوتی اور دشمنوں کو گرانے پر پوائنٹس بڑھتے نظر آئیں گے۔ شاباش! آپ کا گیم تقریباً مکمل ہو چکا ہے۔

---

## 🚀 چیلنج

آپ کا کوڈ تقریباً مکمل ہے۔ کیا آپ اپنے اگلے اقدامات کا تصور کر سکتے ہیں؟

## لیکچر کے بعد کا کوئز

[لیکچر کے بعد کا کوئز](https://ff-quizzes.netlify.app/web/quiz/38)

## جائزہ اور خود مطالعہ

کچھ طریقے تلاش کریں جن سے آپ گیم اسکورز اور زندگیاں بڑھا اور گھٹا سکتے ہیں۔ کچھ دلچسپ گیم انجنز جیسے [PlayFab](https://playfab.com) موجود ہیں۔ ان میں سے کسی ایک کا استعمال آپ کے گیم کو کیسے بہتر بنا سکتا ہے؟

## اسائنمنٹ

[اسکورنگ گیم بنائیں](assignment.md)

---

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا غیر درستیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔