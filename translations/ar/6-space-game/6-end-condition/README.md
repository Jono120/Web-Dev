<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-28T15:03:26+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "ar"
}
-->
# بناء لعبة فضاء الجزء السادس: النهاية وإعادة التشغيل

## اختبار ما قبل المحاضرة

[اختبار ما قبل المحاضرة](https://ff-quizzes.netlify.app/web/quiz/39)

هناك طرق مختلفة للتعبير عن *شرط النهاية* في اللعبة. الأمر متروك لك كمُصمم اللعبة لتحديد سبب انتهاء اللعبة. إليك بعض الأسباب، إذا افترضنا أننا نتحدث عن لعبة الفضاء التي كنت تبنيها حتى الآن:

- **تم تدمير `N` من سفن العدو**: من الشائع جدًا إذا قمت بتقسيم اللعبة إلى مستويات مختلفة أن تحتاج إلى تدمير `N` من سفن العدو لإكمال المستوى.
- **تم تدمير سفينتك**: هناك بالتأكيد ألعاب تخسر فيها اللعبة إذا تم تدمير سفينتك. نهج شائع آخر هو مفهوم "الحياة". في كل مرة يتم فيها تدمير سفينتك يتم خصم حياة. بمجرد فقدان جميع الأرواح، تخسر اللعبة.
- **لقد جمعت `N` نقاط**: شرط نهاية شائع آخر هو جمع النقاط. كيفية الحصول على النقاط متروك لك، ولكن من الشائع جدًا تخصيص نقاط لأنشطة مختلفة مثل تدمير سفينة العدو أو جمع العناصر التي تسقطها السفن عند تدميرها.
- **إكمال مستوى**: قد يتضمن ذلك عدة شروط مثل تدمير `X` من سفن العدو، جمع `Y` نقاط، أو ربما جمع عنصر معين.

## إعادة التشغيل

إذا استمتع الناس بلعبتك، فمن المحتمل أن يرغبوا في إعادة لعبها. بمجرد انتهاء اللعبة لأي سبب كان، يجب أن تقدم خيارًا لإعادة التشغيل.

✅ فكر قليلاً في الظروف التي تجد فيها اللعبة تنتهي، ثم كيف يتم تحفيزك لإعادة التشغيل.

## ما الذي ستبنيه

ستقوم بإضافة هذه القواعد إلى لعبتك:

1. **الفوز باللعبة**. بمجرد تدمير جميع سفن العدو، تفوز باللعبة. بالإضافة إلى ذلك، قم بعرض رسالة انتصار.
1. **إعادة التشغيل**. بمجرد فقدان جميع الأرواح أو الفوز باللعبة، يجب أن تقدم طريقة لإعادة تشغيل اللعبة. تذكر! ستحتاج إلى إعادة تهيئة اللعبة ومسح حالة اللعبة السابقة.

## الخطوات الموصى بها

حدد الملفات التي تم إنشاؤها لك في مجلد `your-work`. يجب أن يحتوي على ما يلي:

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

ابدأ مشروعك في مجلد `your_work` عن طريق كتابة:

```bash
cd your-work
npm start
```

سيقوم الأمر أعلاه بتشغيل خادم HTTP على العنوان `http://localhost:5000`. افتح متصفحًا وأدخل هذا العنوان. يجب أن تكون لعبتك في حالة قابلة للعب.

> نصيحة: لتجنب التحذيرات في Visual Studio Code، قم بتحرير وظيفة `window.onload` لاستدعاء `gameLoopId` كما هو (بدون `let`)، وقم بتعريف `gameLoopId` في أعلى الملف بشكل مستقل: `let gameLoopId;`

### إضافة الكود

1. **تتبع شرط النهاية**. أضف كودًا يتتبع عدد الأعداء، أو إذا تم تدمير سفينة البطل عن طريق إضافة هاتين الوظيفتين:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **إضافة منطق إلى معالجات الرسائل**. قم بتحرير `eventEmitter` لمعالجة هذه الشروط:

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

1. **إضافة أنواع رسائل جديدة**. أضف هذه الرسائل إلى كائن constants:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **إضافة كود إعادة التشغيل**. أضف كودًا يعيد تشغيل اللعبة عند الضغط على زر محدد.

   1. **الاستماع إلى ضغط مفتاح `Enter`**. قم بتحرير مستمع الأحداث الخاص بنافذتك للاستماع إلى هذا الضغط:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **إضافة رسالة إعادة التشغيل**. أضف هذه الرسالة إلى constant الخاص بالرسائل:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **تنفيذ قواعد اللعبة**. قم بتنفيذ قواعد اللعبة التالية:

   1. **شرط فوز اللاعب**. عندما يتم تدمير جميع سفن العدو، قم بعرض رسالة انتصار.

      1. أولاً، قم بإنشاء وظيفة `displayMessage()`:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. قم بإنشاء وظيفة `endGame()`:

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

   1. **منطق إعادة التشغيل**. عندما يتم فقدان جميع الأرواح أو يفوز اللاعب باللعبة، قم بعرض أن اللعبة يمكن إعادة تشغيلها. بالإضافة إلى ذلك، قم بإعادة تشغيل اللعبة عند الضغط على مفتاح *إعادة التشغيل* (يمكنك تحديد المفتاح الذي يجب أن يتم تعيينه لإعادة التشغيل).

      1. قم بإنشاء وظيفة `resetGame()`:

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

     1. أضف استدعاء إلى `eventEmitter` لإعادة ضبط اللعبة في `initGame()`:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. أضف وظيفة `clear()` إلى EventEmitter:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 تهانينا، أيها القبطان! لعبتك مكتملة! عمل رائع! 🚀 💥 👽

---

## 🚀 تحدي

أضف صوتًا! هل يمكنك إضافة صوت لتحسين تجربة اللعب، ربما عند حدوث ضربة ليزر، أو عندما يموت البطل أو يفوز؟ ألقِ نظرة على هذا [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) لتتعلم كيفية تشغيل الصوت باستخدام JavaScript.

## اختبار ما بعد المحاضرة

[اختبار ما بعد المحاضرة](https://ff-quizzes.netlify.app/web/quiz/40)

## المراجعة والدراسة الذاتية

مهمتك هي إنشاء لعبة نموذجية جديدة، لذا استكشف بعض الألعاب المثيرة للاهتمام الموجودة لترى نوع اللعبة التي قد تبنيها.

## المهمة

[بناء لعبة نموذجية](assignment.md)

---

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الموثوق. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.