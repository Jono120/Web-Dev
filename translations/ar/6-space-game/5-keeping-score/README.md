<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "adda95e02afa3fbee67b6e385b1109e1",
  "translation_date": "2025-08-28T15:01:54+00:00",
  "source_file": "6-space-game/5-keeping-score/README.md",
  "language_code": "ar"
}
-->
# بناء لعبة فضاء الجزء الخامس: النقاط والأرواح

## اختبار ما قبل الدرس

[اختبار ما قبل الدرس](https://ff-quizzes.netlify.app/web/quiz/37)

في هذا الدرس، ستتعلم كيفية إضافة النقاط إلى اللعبة وحساب الأرواح.

## رسم النص على الشاشة

لكي تتمكن من عرض نقاط اللعبة على الشاشة، ستحتاج إلى معرفة كيفية وضع النص على الشاشة. الإجابة هي باستخدام طريقة `fillText()` على كائن الـ canvas. يمكنك أيضًا التحكم في جوانب أخرى مثل نوع الخط المستخدم، لون النص وحتى محاذاته (يسار، يمين، وسط). أدناه يوجد كود يرسم نصًا على الشاشة.

```javascript
ctx.font = "30px Arial";
ctx.fillStyle = "red";
ctx.textAlign = "right";
ctx.fillText("show this on the screen", 0, 0);
```

✅ اقرأ المزيد عن [كيفية إضافة النص إلى canvas](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_text)، ولا تتردد في جعل النص يبدو أكثر جاذبية!

## الحياة كمفهوم في الألعاب

مفهوم الحياة في الألعاب هو مجرد رقم. في سياق لعبة الفضاء، من الشائع تخصيص عدد معين من الأرواح يتم خصمها واحدة تلو الأخرى عندما تتعرض سفينتك للضرر. من الجميل أن تعرض تمثيلًا رسوميًا لهذا مثل سفن صغيرة أو قلوب بدلاً من رقم.

## ما الذي سنبنيه

لنقم بإضافة التالي إلى لعبتك:

- **نقاط اللعبة**: لكل سفينة عدو يتم تدميرها، يجب أن يحصل البطل على بعض النقاط، نقترح 100 نقطة لكل سفينة. يجب عرض نقاط اللعبة في الزاوية السفلية اليسرى.
- **الأرواح**: سفينتك لديها ثلاث أرواح. تخسر حياة في كل مرة تصطدم فيها سفينة عدو بسفينتك. يجب عرض عدد الأرواح في الزاوية السفلية اليمنى باستخدام الرسم التالي ![صورة الحياة](../../../../translated_images/life.6fb9f50d53ee0413cd91aa411f7c296e10a1a6de5c4a4197c718b49bf7d63ebf.ar.png).

## الخطوات الموصى بها

حدد الملفات التي تم إنشاؤها لك في مجلد `your-work`. يجب أن يحتوي على التالي:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
-| index.html
-| app.js
-| package.json
```

ابدأ مشروعك من مجلد `your_work` بكتابة:

```bash
cd your-work
npm start
```

سيقوم الأمر أعلاه بتشغيل خادم HTTP على العنوان `http://localhost:5000`. افتح متصفحًا وأدخل هذا العنوان، في الوقت الحالي يجب أن يعرض البطل وجميع الأعداء، وعند الضغط على الأسهم اليسرى واليمنى، يتحرك البطل ويمكنه إسقاط الأعداء.

### إضافة الكود

1. **انسخ الأصول المطلوبة** من مجلد `solution/assets/` إلى مجلد `your-work`؛ ستضيف أصلًا باسم `life.png`. أضف `lifeImg` إلى دالة `window.onload`:

    ```javascript
    lifeImg = await loadTexture("assets/life.png");
    ```

1. أضف `lifeImg` إلى قائمة الأصول:

    ```javascript
    let heroImg,
    ...
    lifeImg,
    ...
    eventEmitter = new EventEmitter();
    ```
  
2. **أضف المتغيرات**. أضف كودًا يمثل إجمالي النقاط (0) وعدد الأرواح المتبقية (3)، واعرض هذه القيم على الشاشة.

3. **قم بتوسيع دالة `updateGameObjects()`**. قم بتوسيع دالة `updateGameObjects()` للتعامل مع اصطدامات الأعداء:

    ```javascript
    enemies.forEach(enemy => {
        const heroRect = hero.rectFromGameObject();
        if (intersectRect(heroRect, enemy.rectFromGameObject())) {
          eventEmitter.emit(Messages.COLLISION_ENEMY_HERO, { enemy });
        }
      })
    ```

4. **أضف الأرواح والنقاط**. 
   1. **تهيئة المتغيرات**. تحت `this.cooldown = 0` في فئة `Hero`، قم بتعيين الأرواح والنقاط:

        ```javascript
        this.life = 3;
        this.points = 0;
        ```

   1. **رسم المتغيرات على الشاشة**. قم برسم هذه القيم على الشاشة:

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

   1. **إضافة الدوال إلى حلقة اللعبة**. تأكد من إضافة هذه الوظائف إلى دالة `window.onload` تحت `updateGameObjects()`:

        ```javascript
        drawPoints();
        drawLife();
        ```

1. **تنفيذ قواعد اللعبة**. قم بتنفيذ قواعد اللعبة التالية:

   1. **لكل اصطدام بين البطل والعدو**، قم بخصم حياة.
   
      قم بتوسيع فئة `Hero` لتنفيذ هذا الخصم:

        ```javascript
        decrementLife() {
          this.life--;
          if (this.life === 0) {
            this.dead = true;
          }
        }
        ```

   2. **لكل ليزر يصيب عدوًا**، قم بزيادة نقاط اللعبة بمقدار 100 نقطة.

      قم بتوسيع فئة `Hero` لتنفيذ هذه الزيادة:
    
        ```javascript
          incrementPoints() {
            this.points += 100;
          }
        ```

        أضف هذه الوظائف إلى مرسلات أحداث الاصطدام:

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

✅ قم ببعض البحث لاكتشاف ألعاب أخرى تم إنشاؤها باستخدام JavaScript/Canvas. ما هي السمات المشتركة بينها؟

بنهاية هذا العمل، يجب أن ترى سفن "الحياة" الصغيرة في الزاوية السفلية اليمنى، النقاط في الزاوية السفلية اليسرى، ويجب أن ترى عدد الأرواح يتناقص عند الاصطدام مع الأعداء والنقاط تزداد عند إسقاط الأعداء. عمل رائع! لعبتك أصبحت شبه مكتملة.

---

## 🚀 التحدي

كودك أصبح شبه مكتمل. هل يمكنك تصور الخطوات التالية؟

## اختبار ما بعد الدرس

[اختبار ما بعد الدرس](https://ff-quizzes.netlify.app/web/quiz/38)

## المراجعة والدراسة الذاتية

ابحث عن طرق يمكنك من خلالها زيادة أو تقليل نقاط اللعبة والأرواح. هناك بعض محركات الألعاب المثيرة للاهتمام مثل [PlayFab](https://playfab.com). كيف يمكن أن يؤدي استخدام أحد هذه المحركات إلى تحسين لعبتك؟

## الواجب

[بناء لعبة تسجيل النقاط](assignment.md)

---

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الرسمي. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.