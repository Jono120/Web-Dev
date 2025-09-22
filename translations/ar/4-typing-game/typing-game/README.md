<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1b0aeccb600f83c603cd70cb42df594d",
  "translation_date": "2025-08-28T15:09:37+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "ar"
}
-->
# إنشاء لعبة باستخدام الأحداث

## اختبار ما قبل المحاضرة

[اختبار ما قبل المحاضرة](https://ff-quizzes.netlify.app/web/quiz/21)

## البرمجة القائمة على الأحداث

عند إنشاء تطبيق يعتمد على المتصفح، نوفر واجهة مستخدم رسومية (GUI) للمستخدم للتفاعل مع ما قمنا ببنائه. الطريقة الأكثر شيوعًا للتفاعل مع المتصفح هي من خلال النقر والكتابة في عناصر مختلفة. التحدي الذي نواجهه كمطورين هو أننا لا نعرف متى سيقوم المستخدم بتنفيذ هذه العمليات!

[البرمجة القائمة على الأحداث](https://en.wikipedia.org/wiki/Event-driven_programming) هي الاسم لنوع البرمجة الذي نحتاجه لإنشاء واجهة المستخدم الرسومية. إذا قمنا بتفكيك هذه العبارة قليلاً، سنجد أن الكلمة الأساسية هنا هي **الحدث**. [الحدث](https://www.merriam-webster.com/dictionary/event)، وفقًا لميريام وبستر، يُعرّف بأنه "شيء يحدث". هذا يصف وضعنا تمامًا. نحن نعلم أن شيئًا ما سيحدث ونريد تنفيذ بعض التعليمات البرمجية استجابةً له، لكننا لا نعرف متى سيحدث ذلك.

الطريقة التي نحدد بها جزءًا من التعليمات البرمجية التي نريد تنفيذها هي من خلال إنشاء دالة. عندما نفكر في [البرمجة الإجرائية](https://en.wikipedia.org/wiki/Procedural_programming)، يتم استدعاء الدوال بترتيب محدد. نفس الشيء ينطبق على البرمجة القائمة على الأحداث. الفرق هو **كيف** يتم استدعاء الدوال.

للتعامل مع الأحداث (مثل النقر على الأزرار أو الكتابة)، نقوم بتسجيل **مستمعي الأحداث**. مستمع الحدث هو دالة تستمع لحدوث حدث معين وتُنفذ استجابةً له. يمكن لمستمعي الأحداث تحديث واجهة المستخدم، إجراء مكالمات إلى الخادم، أو أي شيء آخر يحتاج إلى القيام به استجابةً لتفاعل المستخدم. نضيف مستمع حدث باستخدام [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener)، ونوفر دالة للتنفيذ.

> **NOTE:** من الجدير بالذكر أن هناك طرقًا عديدة لإنشاء مستمعي الأحداث. يمكنك استخدام دوال مجهولة، أو إنشاء دوال مسماة. يمكنك استخدام اختصارات مختلفة، مثل تعيين خاصية `click`، أو استخدام `addEventListener`. في تمريننا، سنركز على `addEventListener` والدوال المجهولة، لأنها التقنية الأكثر شيوعًا التي يستخدمها مطورو الويب. كما أنها الأكثر مرونة، حيث تعمل `addEventListener` مع جميع الأحداث، ويمكن توفير اسم الحدث كمعامل.

### الأحداث الشائعة

هناك [عشرات الأحداث](https://developer.mozilla.org/docs/Web/Events) التي يمكنك الاستماع إليها عند إنشاء تطبيق. في الأساس، أي شيء يفعله المستخدم على الصفحة يثير حدثًا، مما يمنحك الكثير من القوة لضمان حصوله على التجربة التي ترغب بها. لحسن الحظ، عادةً ما تحتاج فقط إلى عدد قليل من الأحداث. إليك بعض الأحداث الشائعة (بما في ذلك اثنان سنستخدمهما عند إنشاء لعبتنا):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): المستخدم نقر على شيء ما، عادةً زر أو رابط
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): المستخدم نقر بزر الماوس الأيمن
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): المستخدم قام بتحديد نص
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): المستخدم أدخل نصًا

## إنشاء اللعبة

سنقوم بإنشاء لعبة لاستكشاف كيفية عمل الأحداث في JavaScript. لعبتنا ستختبر مهارة الكتابة لدى اللاعب، وهي واحدة من المهارات الأكثر أهمية التي يجب أن يمتلكها جميع المطورين. يجب علينا جميعًا ممارسة الكتابة! تدفق اللعبة العام سيكون كالتالي:

- ينقر اللاعب على زر البدء ويتم عرض اقتباس ليكتبه
- يكتب اللاعب الاقتباس بأسرع ما يمكن في مربع النص
  - عند إكمال كل كلمة، يتم تمييز الكلمة التالية
  - إذا ارتكب اللاعب خطأ، يتم تحديث مربع النص ليصبح باللون الأحمر
  - عند إكمال اللاعب للاقتباس، يتم عرض رسالة نجاح مع الوقت المستغرق

لنبدأ ببناء لعبتنا ونتعلم عن الأحداث!

### هيكل الملفات

سنحتاج إلى ثلاثة ملفات إجمالاً: **index.html**، **script.js** و **style.css**. لنبدأ بإعدادها لتسهيل العمل علينا.

- قم بإنشاء مجلد جديد لعملك عن طريق فتح نافذة وحدة التحكم أو الطرفية وإصدار الأمر التالي:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- افتح Visual Studio Code

```bash
code .
```

- أضف ثلاثة ملفات إلى المجلد في Visual Studio Code بالأسماء التالية:
  - index.html
  - script.js
  - style.css

## إنشاء واجهة المستخدم

إذا استعرضنا المتطلبات، نعلم أننا سنحتاج إلى مجموعة من العناصر في صفحة HTML الخاصة بنا. هذا يشبه الوصفة، حيث نحتاج إلى بعض المكونات:

- مكان لعرض الاقتباس الذي سيكتبه المستخدم
- مكان لعرض أي رسائل، مثل رسالة النجاح
- مربع نص للكتابة
- زر البدء

كل من هذه العناصر سيحتاج إلى معرفات (IDs) حتى نتمكن من العمل معها في JavaScript الخاص بنا. سنضيف أيضًا مراجع لملفات CSS وJavaScript التي سنقوم بإنشائها.

قم بإنشاء ملف جديد باسم **index.html**. أضف HTML التالي:

```html
<!-- inside index.html -->
<html>
<head>
  <title>Typing game</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Typing game!</h1>
  <p>Practice your typing skills with a quote from Sherlock Holmes. Click **start** to begin!</p>
  <p id="quote"></p> <!-- This will display our quote -->
  <p id="message"></p> <!-- This will display any status messages -->
  <div>
    <input type="text" aria-label="current word" id="typed-value" /> <!-- The textbox for typing -->
    <button type="button" id="start">Start</button> <!-- To start the game -->
  </div>
  <script src="script.js"></script>
</body>
</html>
```

### تشغيل التطبيق

من الأفضل دائمًا التطوير بشكل تدريجي لرؤية كيف تبدو الأمور. لنقم بتشغيل تطبيقنا. هناك إضافة رائعة لـ Visual Studio Code تُسمى [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) والتي ستقوم باستضافة تطبيقك محليًا وتحديث المتصفح في كل مرة تحفظ فيها.

- قم بتثبيت [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) باتباع الرابط والنقر على **Install**
  - سيُطلب منك من المتصفح فتح Visual Studio Code، ثم من Visual Studio Code لإجراء التثبيت
  - أعد تشغيل Visual Studio Code إذا طُلب منك ذلك
- بمجرد التثبيت، في Visual Studio Code، انقر على Ctrl-Shift-P (أو Cmd-Shift-P) لفتح لوحة الأوامر
- اكتب **Live Server: Open with Live Server**
  - سيبدأ Live Server في استضافة تطبيقك
- افتح المتصفح وانتقل إلى **https://localhost:5500**
- يجب أن ترى الآن الصفحة التي أنشأتها!

لنقم بإضافة بعض الوظائف.

## إضافة CSS

مع إنشاء HTML الخاص بنا، لنقم بإضافة CSS للتنسيق الأساسي. نحتاج إلى تمييز الكلمة التي يجب أن يكتبها اللاعب، وتلوين مربع النص إذا كان ما كتبه غير صحيح. سنقوم بذلك باستخدام فئتين.

قم بإنشاء ملف جديد باسم **style.css** وأضف الصيغة التالية.

```css
/* inside style.css */
.highlight {
  background-color: yellow;
}

.error {
  background-color: lightcoral;
  border: red;
}
```

✅ عندما يتعلق الأمر بـ CSS، يمكنك تصميم صفحتك بالطريقة التي ترغب بها. خذ بعض الوقت واجعل الصفحة تبدو أكثر جاذبية:

- اختر خطًا مختلفًا
- أضف ألوانًا للعناوين
- قم بتغيير حجم العناصر

## JavaScript

مع إنشاء واجهة المستخدم الخاصة بنا، حان الوقت للتركيز على JavaScript الذي سيوفر المنطق. سنقوم بتقسيم هذا إلى مجموعة من الخطوات:

- [إنشاء الثوابت](../../../../4-typing-game/typing-game)
- [مستمع الحدث لبدء اللعبة](../../../../4-typing-game/typing-game)
- [مستمع الحدث للكتابة](../../../../4-typing-game/typing-game)

لكن أولاً، قم بإنشاء ملف جديد باسم **script.js**.

### إضافة الثوابت

سنحتاج إلى بعض العناصر لتسهيل البرمجة. مرة أخرى، مثل الوصفة، إليك ما سنحتاجه:

- مصفوفة تحتوي على قائمة بجميع الاقتباسات
- مصفوفة فارغة لتخزين جميع الكلمات للاقتباس الحالي
- مساحة لتخزين مؤشر الكلمة التي يكتبها اللاعب حاليًا
- الوقت الذي نقر فيه اللاعب على البدء

سنحتاج أيضًا إلى مراجع لعناصر واجهة المستخدم:

- مربع النص (**typed-value**)
- عرض الاقتباس (**quote**)
- الرسالة (**message**)

```javascript
// inside script.js
// all of our quotes
const quotes = [
    'When you have eliminated the impossible, whatever remains, however improbable, must be the truth.',
    'There is nothing more deceptive than an obvious fact.',
    'I ought to know by this time that when a fact appears to be opposed to a long train of deductions it invariably proves to be capable of bearing some other interpretation.',
    'I never make exceptions. An exception disproves the rule.',
    'What one man can invent another can discover.',
    'Nothing clears up a case so much as stating it to another person.',
    'Education never ends, Watson. It is a series of lessons, with the greatest for the last.',
];
// store the list of words and the index of the word the player is currently typing
let words = [];
let wordIndex = 0;
// the starting time
let startTime = Date.now();
// page elements
const quoteElement = document.getElementById('quote');
const messageElement = document.getElementById('message');
const typedValueElement = document.getElementById('typed-value');
```

✅ قم بإضافة المزيد من الاقتباحات إلى لعبتك

> **NOTE:** يمكننا استرداد العناصر في أي وقت في الكود باستخدام `document.getElementById`. نظرًا لأننا سنشير إلى هذه العناصر بشكل منتظم، سنقوم بتجنب الأخطاء الإملائية مع النصوص الحرفية باستخدام الثوابت. يمكن أن تساعدك أطر العمل مثل [Vue.js](https://vuejs.org/) أو [React](https://reactjs.org/) في إدارة مركزية الكود بشكل أفضل.

خذ دقيقة لمشاهدة فيديو عن استخدام `const`، `let` و `var`

[![أنواع المتغيرات](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "أنواع المتغيرات")

> 🎥 انقر على الصورة أعلاه لمشاهدة فيديو عن المتغيرات.

### إضافة منطق البدء

لبدء اللعبة، سيقوم اللاعب بالنقر على زر البدء. بالطبع، لا نعرف متى سيقوم بالنقر على البدء. هنا يأتي دور [مستمع الحدث](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener). مستمع الحدث سيسمح لنا بالاستماع لحدوث شيء ما (حدث) وتنفيذ الكود استجابةً له. في حالتنا، نريد تنفيذ الكود عندما ينقر المستخدم على البدء.

عندما ينقر المستخدم على **البدء**، نحتاج إلى اختيار اقتباس، إعداد واجهة المستخدم، وإعداد تتبع الكلمة الحالية والتوقيت. أدناه هو JavaScript الذي ستحتاج إلى إضافته؛ سنناقشه بعد كتلة الكود.

```javascript
// at the end of script.js
document.getElementById('start').addEventListener('click', () => {
  // get a quote
  const quoteIndex = Math.floor(Math.random() * quotes.length);
  const quote = quotes[quoteIndex];
  // Put the quote into an array of words
  words = quote.split(' ');
  // reset the word index for tracking
  wordIndex = 0;

  // UI updates
  // Create an array of span elements so we can set a class
  const spanWords = words.map(function(word) { return `<span>${word} </span>`});
  // Convert into string and set as innerHTML on quote display
  quoteElement.innerHTML = spanWords.join('');
  // Highlight the first word
  quoteElement.childNodes[0].className = 'highlight';
  // Clear any prior messages
  messageElement.innerText = '';

  // Setup the textbox
  // Clear the textbox
  typedValueElement.value = '';
  // set focus
  typedValueElement.focus();
  // set the event handler

  // Start the timer
  startTime = new Date().getTime();
});
```

لنقم بتفكيك الكود!

- إعداد تتبع الكلمات
  - باستخدام [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) و [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random)، يمكننا اختيار اقتباس عشوائي من مصفوفة `quotes`
  - نقوم بتحويل `quote` إلى مصفوفة `words` حتى نتمكن من تتبع الكلمة التي يكتبها اللاعب حاليًا
  - يتم تعيين `wordIndex` إلى 0، حيث سيبدأ اللاعب بالكلمة الأولى
- إعداد واجهة المستخدم
  - إنشاء مصفوفة `spanWords` تحتوي على كل كلمة داخل عنصر `span`
    - هذا سيسمح لنا بتمييز الكلمة على العرض
  - استخدام `join` لإنشاء سلسلة يمكننا استخدامها لتحديث `innerHTML` على `quoteElement`
    - هذا سيعرض الاقتباس للاعب
  - تعيين `className` لأول عنصر `span` إلى `highlight` لتمييزه باللون الأصفر
  - تنظيف `messageElement` عن طريق تعيين `innerText` إلى `''`
- إعداد مربع النص
  - مسح `value` الحالي على `typedValueElement`
  - تعيين `focus` إلى `typedValueElement`
- بدء المؤقت عن طريق استدعاء `getTime`

### إضافة منطق الكتابة

عندما يكتب اللاعب، سيتم رفع حدث `input`. مستمع الحدث هذا سيتحقق من أن اللاعب يكتب الكلمة بشكل صحيح، وسيتعامل مع حالة اللعبة الحالية. بالعودة إلى **script.js**، أضف الكود التالي إلى النهاية. سنقوم بتفكيكه بعد ذلك.

```javascript
// at the end of script.js
typedValueElement.addEventListener('input', () => {
  // Get the current word
  const currentWord = words[wordIndex];
  // get the current value
  const typedValue = typedValueElement.value;

  if (typedValue === currentWord && wordIndex === words.length - 1) {
    // end of sentence
    // Display success
    const elapsedTime = new Date().getTime() - startTime;
    const message = `CONGRATULATIONS! You finished in ${elapsedTime / 1000} seconds.`;
    messageElement.innerText = message;
  } else if (typedValue.endsWith(' ') && typedValue.trim() === currentWord) {
    // end of word
    // clear the typedValueElement for the new word
    typedValueElement.value = '';
    // move to the next word
    wordIndex++;
    // reset the class name for all elements in quote
    for (const wordElement of quoteElement.childNodes) {
      wordElement.className = '';
    }
    // highlight the new word
    quoteElement.childNodes[wordIndex].className = 'highlight';
  } else if (currentWord.startsWith(typedValue)) {
    // currently correct
    // highlight the next word
    typedValueElement.className = '';
  } else {
    // error state
    typedValueElement.className = 'error';
  }
});
```

لنقم بتفكيك الكود! نبدأ بأخذ الكلمة الحالية والقيمة التي كتبها اللاعب حتى الآن. ثم لدينا منطق متسلسل، حيث نتحقق مما إذا كان الاقتباس مكتملًا، الكلمة مكتملة، الكلمة صحيحة، أو (أخيرًا)، إذا كان هناك خطأ.

- الاقتباس مكتمل، يُشار إليه بأن `typedValue` يساوي `currentWord`، و `wordIndex` يساوي واحدًا أقل من `length` لـ `words`
  - حساب `elapsedTime` عن طريق طرح `startTime` من الوقت الحالي
  - قسمة `elapsedTime` على 1,000 لتحويله من ميلي ثانية إلى ثوانٍ
  - عرض رسالة نجاح
- الكلمة مكتملة، يُشار إليها بأن `typedValue` ينتهي بمسافة (نهاية الكلمة) و `typedValue` يساوي `currentWord`
  - تعيين `value` على `typedElement` ليكون `''` للسماح بكتابة الكلمة التالية
  - زيادة `wordIndex` للانتقال إلى الكلمة التالية
  - التكرار عبر جميع `childNodes` لـ `quoteElement` لتعيين `className` إلى `''` للعودة إلى العرض الافتراضي
  - تعيين `className` للكلمة الحالية إلى `highlight` للإشارة إلى أنها الكلمة التالية للكتابة
- الكلمة مكتوبة بشكل صحيح حاليًا (لكنها ليست مكتملة)، يُشار إليها بأن `currentWord` يبدأ بـ `typedValue`
  - التأكد من عرض `typedValueElement` كافتراضي عن طريق مسح `className`
- إذا وصلنا إلى هذه النقطة، لدينا خطأ
  - تعيين `className` على `typedValueElement` إلى `error`

## اختبار التطبيق الخاص بك

لقد وصلت إلى النهاية! الخطوة الأخيرة هي التأكد من أن تطبيقنا يعمل. جربه! لا تقلق إذا كانت هناك أخطاء؛ **جميع المطورين** يواجهون أخطاء. قم بفحص الرسائل وتصحيح الأخطاء حسب الحاجة.

انقر على **البدء**، وابدأ الكتابة! يجب أن يبدو الأمر مشابهًا للرسوم المتحركة التي رأيناها سابقًا.

![رسوم متحركة للعبة أثناء العمل](../../../../4-typing-game/images/demo.gif)

---

## 🚀 التحدي

أضف المزيد من الوظائف

- تعطيل مستمع حدث `input` عند الإكمال، وإعادة تمكينه عند النقر على الزر
- تعطيل مربع النص عندما يكمل اللاعب الاقتباس
- عرض مربع حوار مودال مع رسالة النجاح
- تخزين أعلى النتائج باستخدام [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)
## اختبار ما بعد المحاضرة

[اختبار ما بعد المحاضرة](https://ff-quizzes.netlify.app/web/quiz/22)

## المراجعة والدراسة الذاتية

اقرأ عن [جميع الأحداث المتاحة](https://developer.mozilla.org/docs/Web/Events) للمطور عبر متصفح الويب، وفكر في السيناريوهات التي قد تستخدم فيها كل واحدة منها.

## الواجب

[قم بإنشاء لعبة لوحة مفاتيح جديدة](assignment.md)

---

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الموثوق. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.