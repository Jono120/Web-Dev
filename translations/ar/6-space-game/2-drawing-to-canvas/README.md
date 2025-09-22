<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "056641280211e52fd0adb81b6058ec55",
  "translation_date": "2025-08-28T15:03:03+00:00",
  "source_file": "6-space-game/2-drawing-to-canvas/README.md",
  "language_code": "ar"
}
-->
# بناء لعبة فضاء الجزء الثاني: رسم البطل والوحوش على اللوحة

## اختبار ما قبل المحاضرة

[اختبار ما قبل المحاضرة](https://ff-quizzes.netlify.app/web/quiz/31)

## اللوحة

اللوحة هي عنصر HTML لا يحتوي على محتوى افتراضيًا؛ إنها مساحة فارغة. تحتاج إلى إضافة محتوى إليها عن طريق الرسم عليها.

✅ اقرأ [المزيد عن واجهة برمجة تطبيقات اللوحة](https://developer.mozilla.org/docs/Web/API/Canvas_API) على MDN.

عادةً ما يتم تعريفها كجزء من جسم الصفحة كما يلي:

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

في الأعلى، قمنا بتحديد `id` و`width` و`height`.

- `id`: قم بتعيينه حتى تتمكن من الحصول على مرجع عند الحاجة للتفاعل معه.
- `width`: هذا هو عرض العنصر.
- `height`: هذا هو ارتفاع العنصر.

## رسم أشكال هندسية بسيطة

تستخدم اللوحة نظام إحداثيات ديكارتي للرسم. وبالتالي، تستخدم محور x ومحور y للتعبير عن مكان وجود شيء ما. الموقع `0,0` هو الزاوية العلوية اليسرى، والزاوية السفلية اليمنى هي ما قمت بتحديده كعرض وارتفاع للوحة.

![شبكة اللوحة](../../../../translated_images/canvas_grid.5f209da785ded492a01ece440e3032afe51efa500cc2308e5ea4252487ceaf0b.ar.png)  
> الصورة من [MDN](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes)

للرسم على عنصر اللوحة، ستحتاج إلى اتباع الخطوات التالية:

1. **الحصول على مرجع** لعنصر اللوحة.
1. **الحصول على مرجع** لعنصر السياق الذي يجلس على عنصر اللوحة.
1. **تنفيذ عملية الرسم** باستخدام عنصر السياق.

الكود للخطوات أعلاه يبدو عادةً كما يلي:

```javascript
// draws a red rectangle
//1. get the canvas reference
canvas = document.getElementById("myCanvas");

//2. set the context to 2D to draw basic shapes
ctx = canvas.getContext("2d");

//3. fill it with the color red
ctx.fillStyle = 'red';

//4. and draw a rectangle with these parameters, setting location and size
ctx.fillRect(0,0, 200, 200) // x,y,width, height
```

✅ تركز واجهة برمجة تطبيقات اللوحة بشكل أساسي على الأشكال ثنائية الأبعاد، ولكن يمكنك أيضًا رسم عناصر ثلاثية الأبعاد على موقع ويب؛ لهذا، قد تستخدم [واجهة برمجة تطبيقات WebGL](https://developer.mozilla.org/docs/Web/API/WebGL_API).

يمكنك رسم جميع أنواع الأشياء باستخدام واجهة برمجة تطبيقات اللوحة مثل:

- **الأشكال الهندسية**، لقد أظهرنا بالفعل كيفية رسم مستطيل، ولكن هناك المزيد مما يمكنك رسمه.
- **النصوص**، يمكنك رسم نص بأي خط ولون ترغب فيه.
- **الصور**، يمكنك رسم صورة بناءً على أصل صورة مثل .jpg أو .png على سبيل المثال.

✅ جربها! أنت تعرف كيفية رسم مستطيل، هل يمكنك رسم دائرة على الصفحة؟ ألقِ نظرة على بعض الرسومات المثيرة للاهتمام باستخدام اللوحة على CodePen. إليك [مثال مثير للإعجاب](https://codepen.io/dissimulate/pen/KrAwx).

## تحميل ورسم أصل صورة

يمكنك تحميل أصل صورة عن طريق إنشاء كائن `Image` وتعيين خاصية `src` الخاصة به. ثم تستمع إلى حدث `load` لمعرفة متى يكون جاهزًا للاستخدام. يبدو الكود كما يلي:

### تحميل الأصل

```javascript
const img = new Image();
img.src = 'path/to/my/image.png';
img.onload = () => {
  // image loaded and ready to be used
}
```

### نمط تحميل الأصل

يُوصى بتغليف الكود أعلاه في بناء مثل هذا، بحيث يكون من الأسهل استخدامه ولا تحاول التلاعب به إلا عندما يتم تحميله بالكامل:

```javascript
function loadAsset(path) {
  return new Promise((resolve) => {
    const img = new Image();
    img.src = path;
    img.onload = () => {
      // image loaded and ready to be used
      resolve(img);
    }
  })
}

// use like so

async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')
}

```

لرسم أصول اللعبة على الشاشة، سيبدو الكود الخاص بك كما يلي:

```javascript
async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')

  canvas = document.getElementById("myCanvas");
  ctx = canvas.getContext("2d");
  ctx.drawImage(heroImg, canvas.width/2,canvas.height/2);
  ctx.drawImage(monsterImg, 0,0);
}
```

## الآن حان الوقت لبدء بناء لعبتك

### ما الذي ستبنيه

ستقوم ببناء صفحة ويب تحتوي على عنصر لوحة. يجب أن تعرض شاشة سوداء بحجم `1024*768`. لقد وفرنا لك صورتين:

- سفينة البطل

   ![سفينة البطل](../../../../translated_images/player.dd24c1afa8c71e9b82b2958946d4bad13308681392d4b5ddcc61a0e818ef8088.ar.png)

- 5*5 وحوش

   ![سفينة الوحش](../../../../translated_images/enemyShip.5df2a822c16650c2fb3c06652e8ec8120cdb9122a6de46b9a1a56d54db22657f.ar.png)

### الخطوات الموصى بها لبدء التطوير

حدد الملفات التي تم إنشاؤها لك في مجلد `your-work`. يجب أن يحتوي على ما يلي:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

افتح نسخة من هذا المجلد في Visual Studio Code. تحتاج إلى إعداد بيئة تطوير محلية، ويفضل أن تكون مع Visual Studio Code مع NPM وNode مثبتين. إذا لم يكن لديك `npm` مثبتًا على جهاز الكمبيوتر الخاص بك، [إليك كيفية القيام بذلك](https://www.npmjs.com/get-npm).

ابدأ مشروعك عن طريق التنقل إلى مجلد `your_work`:

```bash
cd your-work
npm start
```

سيقوم الكود أعلاه بتشغيل خادم HTTP على العنوان `http://localhost:5000`. افتح متصفحًا وأدخل هذا العنوان. إنها صفحة فارغة الآن، ولكن هذا سيتغير.

> ملاحظة: لرؤية التغييرات على شاشتك، قم بتحديث المتصفح.

### إضافة الكود

أضف الكود المطلوب إلى `your-work/app.js` لحل ما يلي:

1. **رسم** لوحة بخلفية سوداء  
   > نصيحة: أضف سطرين تحت التعليق المناسب في `/app.js`، وقم بتعيين عنصر `ctx` ليكون أسودًا، وإعداد الإحداثيات العلوية/اليسرى عند 0,0، والارتفاع والعرض ليكونا مساويين للوحة.

2. **تحميل** القوام  
   > نصيحة: أضف صور اللاعب والعدو باستخدام `await loadTexture` وتمرير مسار الصورة. لن تراها على الشاشة بعد!

3. **رسم** البطل في وسط الشاشة في النصف السفلي  
   > نصيحة: استخدم واجهة برمجة تطبيقات `drawImage` لرسم heroImg على الشاشة، مع إعداد `canvas.width / 2 - 45` و`canvas.height - canvas.height / 4)`.

4. **رسم** 5*5 وحوش  
   > نصيحة: الآن يمكنك إلغاء تعليق الكود لرسم الأعداء على الشاشة. بعد ذلك، انتقل إلى وظيفة `createEnemies` وقم ببنائها.

   أولاً، قم بإعداد بعض الثوابت:

    ```javascript
    const MONSTER_TOTAL = 5;
    const MONSTER_WIDTH = MONSTER_TOTAL * 98;
    const START_X = (canvas.width - MONSTER_WIDTH) / 2;
    const STOP_X = START_X + MONSTER_WIDTH;
    ```

    ثم، قم بإنشاء حلقة لرسم مصفوفة الوحوش على الشاشة:

    ```javascript
    for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          ctx.drawImage(enemyImg, x, y);
        }
      }
    ```

## النتيجة

يجب أن تبدو النتيجة النهائية كما يلي:

![شاشة سوداء مع بطل و5*5 وحوش](../../../../translated_images/partI-solution.36c53b48c9ffae2a5e15496b23b604ba5393433e4bf91608a7a0a020eb7a2691.ar.png)

## الحل

يرجى محاولة حلها بنفسك أولاً، ولكن إذا واجهت صعوبة، يمكنك الاطلاع على [الحل](../../../../6-space-game/2-drawing-to-canvas/solution/app.js).

---

## 🚀 التحدي

لقد تعلمت عن الرسم باستخدام واجهة برمجة تطبيقات اللوحة ثنائية الأبعاد؛ ألقِ نظرة على [واجهة برمجة تطبيقات WebGL](https://developer.mozilla.org/docs/Web/API/WebGL_API)، وحاول رسم كائن ثلاثي الأبعاد.

## اختبار ما بعد المحاضرة

[اختبار ما بعد المحاضرة](https://ff-quizzes.netlify.app/web/quiz/32)

## المراجعة والدراسة الذاتية

تعرف على المزيد حول واجهة برمجة تطبيقات اللوحة من خلال [قراءتها](https://developer.mozilla.org/docs/Web/API/Canvas_API).

## الواجب

[العب مع واجهة برمجة تطبيقات اللوحة](assignment.md)

---

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو عدم دقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الرسمي. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.