<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a6ce295ff03bb49df7a3e17e6e7100a0",
  "translation_date": "2025-08-28T15:02:13+00:00",
  "source_file": "6-space-game/4-collision-detection/README.md",
  "language_code": "ar"
}
-->
# بناء لعبة فضاء الجزء الرابع: إضافة الليزر واكتشاف التصادمات

## اختبار ما قبل المحاضرة

[اختبار ما قبل المحاضرة](https://ff-quizzes.netlify.app/web/quiz/35)

في هذه الدرس ستتعلم كيفية إطلاق الليزر باستخدام JavaScript! سنضيف عنصرين إلى لعبتنا:

- **الليزر**: يتم إطلاق هذا الليزر من سفينة البطل عموديًا نحو الأعلى.
- **اكتشاف التصادمات**، كجزء من تنفيذ القدرة على *الإطلاق*، سنضيف بعض قواعد اللعبة الممتعة:
   - **الليزر يصيب العدو**: يموت العدو إذا أصيب بالليزر.
   - **الليزر يصيب أعلى الشاشة**: يتم تدمير الليزر إذا أصاب الجزء العلوي من الشاشة.
   - **تصادم العدو والبطل**: يتم تدمير العدو والبطل إذا اصطدموا ببعضهم البعض.
   - **العدو يصيب أسفل الشاشة**: يتم تدمير العدو والبطل إذا وصل العدو إلى أسفل الشاشة.

باختصار، أنت -- *البطل* -- تحتاج إلى إصابة جميع الأعداء بالليزر قبل أن يتمكنوا من الوصول إلى أسفل الشاشة.

✅ قم بإجراء بحث صغير حول أول لعبة كمبيوتر تم كتابتها على الإطلاق. ما هي وظيفتها؟

لنكن أبطالًا معًا!

## اكتشاف التصادمات

كيف نقوم باكتشاف التصادمات؟ نحتاج إلى التفكير في كائنات اللعبة كأنها مستطيلات تتحرك. لماذا؟ لأن الصورة المستخدمة لرسم كائن اللعبة هي مستطيل: يحتوي على `x`، `y`، `width` و `height`.

إذا تقاطع مستطيلان، مثل البطل والعدو، يحدث تصادم. ما يجب أن يحدث بعد ذلك يعتمد على قواعد اللعبة. لتنفيذ اكتشاف التصادمات تحتاج إلى ما يلي:

1. طريقة للحصول على تمثيل مستطيل لكائن اللعبة، شيء مثل هذا:

   ```javascript
   rectFromGameObject() {
     return {
       top: this.y,
       left: this.x,
       bottom: this.y + this.height,
       right: this.x + this.width
     }
   }
   ```

2. وظيفة مقارنة، يمكن أن تبدو هذه الوظيفة كما يلي:

   ```javascript
   function intersectRect(r1, r2) {
     return !(r2.left > r1.right ||
       r2.right < r1.left ||
       r2.top > r1.bottom ||
       r2.bottom < r1.top);
   }
   ```

## كيف ندمر الأشياء

لتدمير الأشياء في اللعبة، تحتاج إلى إعلام اللعبة بأنه يجب ألا يتم رسم هذا العنصر في حلقة اللعبة التي يتم تشغيلها على فاصل زمني معين. طريقة للقيام بذلك هي وضع علامة على كائن اللعبة كـ *ميت* عندما يحدث شيء ما، مثل هذا:

```javascript
// collision happened
enemy.dead = true
```

ثم يمكنك متابعة تصفية الكائنات *الميتة* قبل إعادة رسم الشاشة، مثل هذا:

```javascript
gameObjects = gameObject.filter(go => !go.dead);
```

## كيف نطلق الليزر

إطلاق الليزر يعني الاستجابة لحدث مفتاح وإنشاء كائن يتحرك في اتجاه معين. لذلك نحتاج إلى تنفيذ الخطوات التالية:

1. **إنشاء كائن ليزر**: من أعلى سفينة البطل، يبدأ بالتحرك نحو الأعلى باتجاه أعلى الشاشة عند إنشائه.
2. **إرفاق كود لحدث مفتاح**: نحتاج إلى اختيار مفتاح على لوحة المفاتيح يمثل إطلاق اللاعب لليزر.
3. **إنشاء كائن لعبة يبدو كأنه ليزر** عند الضغط على المفتاح.

## فترة التهدئة لليزر

يحتاج الليزر إلى الإطلاق في كل مرة تضغط فيها على مفتاح، مثل *المسافة* على سبيل المثال. لمنع اللعبة من إنتاج عدد كبير جدًا من الليزرات في وقت قصير، نحتاج إلى إصلاح ذلك. يتم الإصلاح عن طريق تنفيذ ما يسمى بـ *فترة التهدئة*، وهي مؤقت يضمن أن الليزر يمكن إطلاقه فقط في فترات محددة. يمكنك تنفيذ ذلك بالطريقة التالية:

```javascript
class Cooldown {
  constructor(time) {
    this.cool = false;
    setTimeout(() => {
      this.cool = true;
    }, time)
  }
}

class Weapon {
  constructor {
  }
  fire() {
    if (!this.cooldown || this.cooldown.cool) {
      // produce a laser
      this.cooldown = new Cooldown(500);
    } else {
      // do nothing - it hasn't cooled down yet.
    }
  }
}
```

✅ ارجع إلى الدرس الأول في سلسلة لعبة الفضاء لتذكير نفسك بـ *فترات التهدئة*.

## ما الذي سنبنيه

ستأخذ الكود الموجود (الذي يجب أن تكون قد نظفته وأعدت ترتيبه) من الدرس السابق، وتقوم بتوسيعه. إما أن تبدأ بالكود من الجزء الثاني أو تستخدم الكود في [الجزء الثالث - البداية](../../../../../../../../../your-work).

> نصيحة: الليزر الذي ستعمل عليه موجود بالفعل في مجلد الأصول الخاص بك ومشار إليه في الكود الخاص بك.

- **إضافة اكتشاف التصادمات**، عندما يصطدم الليزر بشيء ما، يجب تطبيق القواعد التالية:
   1. **الليزر يصيب العدو**: يموت العدو إذا أصيب بالليزر.
   2. **الليزر يصيب أعلى الشاشة**: يتم تدمير الليزر إذا أصاب الجزء العلوي من الشاشة.
   3. **تصادم العدو والبطل**: يتم تدمير العدو والبطل إذا اصطدموا ببعضهم البعض.
   4. **العدو يصيب أسفل الشاشة**: يتم تدمير العدو والبطل إذا وصل العدو إلى أسفل الشاشة.

## الخطوات الموصى بها

حدد الملفات التي تم إنشاؤها لك في مجلد `your-work`. يجب أن تحتوي على ما يلي:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
-| index.html
-| app.js
-| package.json
```

ابدأ مشروعك في مجلد `your_work` عن طريق كتابة:

```bash
cd your-work
npm start
```

سيقوم الأمر أعلاه بتشغيل خادم HTTP على العنوان `http://localhost:5000`. افتح متصفحًا وأدخل هذا العنوان، في الوقت الحالي يجب أن يعرض البطل وجميع الأعداء، ولكن لا شيء يتحرك - حتى الآن :).

### إضافة الكود

1. **إعداد تمثيل مستطيل لكائن اللعبة للتعامل مع التصادمات** الكود أدناه يسمح لك بالحصول على تمثيل مستطيل لـ `GameObject`. قم بتعديل فئة GameObject لتوسيعها:

    ```javascript
    rectFromGameObject() {
        return {
          top: this.y,
          left: this.x,
          bottom: this.y + this.height,
          right: this.x + this.width,
        };
      }
    ```

2. **إضافة كود يتحقق من التصادمات** ستكون هذه وظيفة جديدة تختبر ما إذا كان مستطيلان يتقاطعان:

    ```javascript
    function intersectRect(r1, r2) {
      return !(
        r2.left > r1.right ||
        r2.right < r1.left ||
        r2.top > r1.bottom ||
        r2.bottom < r1.top
      );
    }
    ```

3. **إضافة قدرة إطلاق الليزر**
   1. **إضافة رسالة حدث المفتاح**. يجب أن يقوم مفتاح *المسافة* بإنشاء ليزر فوق سفينة البطل. أضف ثلاث ثوابت في كائن Messages:

       ```javascript
        KEY_EVENT_SPACE: "KEY_EVENT_SPACE",
        COLLISION_ENEMY_LASER: "COLLISION_ENEMY_LASER",
        COLLISION_ENEMY_HERO: "COLLISION_ENEMY_HERO",
       ```

   1. **التعامل مع مفتاح المسافة**. قم بتعديل وظيفة `window.addEventListener` الخاصة بـ keyup للتعامل مع المسافة:

      ```javascript
        } else if(evt.keyCode === 32) {
          eventEmitter.emit(Messages.KEY_EVENT_SPACE);
        }
      ```

    1. **إضافة مستمعين**. قم بتعديل وظيفة `initGame()` للتأكد من أن البطل يمكنه الإطلاق عند الضغط على مفتاح المسافة:

       ```javascript
       eventEmitter.on(Messages.KEY_EVENT_SPACE, () => {
        if (hero.canFire()) {
          hero.fire();
        }
       ```

       وأضف وظيفة جديدة `eventEmitter.on()` لضمان السلوك عند اصطدام العدو بالليزر:

          ```javascript
          eventEmitter.on(Messages.COLLISION_ENEMY_LASER, (_, { first, second }) => {
            first.dead = true;
            second.dead = true;
          })
          ```

   1. **تحريك الكائن**، تأكد من أن الليزر يتحرك تدريجيًا إلى أعلى الشاشة. ستقوم بإنشاء فئة جديدة Laser تمتد من `GameObject`، كما فعلت من قبل: 
   
      ```javascript
        class Laser extends GameObject {
        constructor(x, y) {
          super(x,y);
          (this.width = 9), (this.height = 33);
          this.type = 'Laser';
          this.img = laserImg;
          let id = setInterval(() => {
            if (this.y > 0) {
              this.y -= 15;
            } else {
              this.dead = true;
              clearInterval(id);
            }
          }, 100)
        }
      }
      ```

   1. **التعامل مع التصادمات**، قم بتنفيذ قواعد التصادم لليزر. أضف وظيفة `updateGameObjects()` التي تختبر الكائنات المتصادمة للإصابات:

      ```javascript
      function updateGameObjects() {
        const enemies = gameObjects.filter(go => go.type === 'Enemy');
        const lasers = gameObjects.filter((go) => go.type === "Laser");
      // laser hit something
        lasers.forEach((l) => {
          enemies.forEach((m) => {
            if (intersectRect(l.rectFromGameObject(), m.rectFromGameObject())) {
            eventEmitter.emit(Messages.COLLISION_ENEMY_LASER, {
              first: l,
              second: m,
            });
          }
         });
      });

        gameObjects = gameObjects.filter(go => !go.dead);
      }  
      ```

      تأكد من إضافة `updateGameObjects()` إلى حلقة اللعبة في `window.onload`.

   4. **تنفيذ فترة التهدئة** لليزر، بحيث يمكن إطلاقه فقط في فترات محددة.

      أخيرًا، قم بتعديل فئة Hero بحيث يمكنها التهدئة:

       ```javascript
      class Hero extends GameObject {
        constructor(x, y) {
          super(x, y);
          (this.width = 99), (this.height = 75);
          this.type = "Hero";
          this.speed = { x: 0, y: 0 };
          this.cooldown = 0;
        }
        fire() {
          gameObjects.push(new Laser(this.x + 45, this.y - 10));
          this.cooldown = 500;
    
          let id = setInterval(() => {
            if (this.cooldown > 0) {
              this.cooldown -= 100;
            } else {
              clearInterval(id);
            }
          }, 200);
        }
        canFire() {
          return this.cooldown === 0;
        }
      }
      ```

في هذه المرحلة، أصبحت لعبتك تحتوي على بعض الوظائف! يمكنك التنقل باستخدام مفاتيح الأسهم، إطلاق الليزر باستخدام مفتاح المسافة، واختفاء الأعداء عند إصابتهم. أحسنت!

---

## 🚀 التحدي

أضف انفجارًا! ألقِ نظرة على أصول اللعبة في [مستودع فن الفضاء](../../../../6-space-game/solution/spaceArt/readme.txt) وحاول إضافة انفجار عندما يصيب الليزر كائنًا فضائيًا.

## اختبار ما بعد المحاضرة

[اختبار ما بعد المحاضرة](https://ff-quizzes.netlify.app/web/quiz/36)

## المراجعة والدراسة الذاتية

جرب تعديل الفواصل الزمنية في لعبتك حتى الآن. ماذا يحدث عندما تغيرها؟ اقرأ المزيد عن [أحداث توقيت JavaScript](https://www.freecodecamp.org/news/javascript-timing-events-settimeout-and-setinterval/).

## الواجب

[استكشاف التصادمات](assignment.md)

---

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الرسمي. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة ناتجة عن استخدام هذه الترجمة.