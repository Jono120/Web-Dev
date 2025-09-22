<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1b0aeccb600f83c603cd70cb42df594d",
  "translation_date": "2025-08-28T15:31:24+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "ur"
}
-->
# ایونٹس کے ذریعے گیم بنانا

## لیکچر سے پہلے کا کوئز

[لیکچر سے پہلے کا کوئز](https://ff-quizzes.netlify.app/web/quiz/21)

## ایونٹ ڈرائیون پروگرامنگ

جب ہم براؤزر پر مبنی ایپلیکیشن بناتے ہیں، تو ہم صارف کے لیے ایک گرافیکل یوزر انٹرفیس (GUI) فراہم کرتے ہیں تاکہ وہ ہماری بنائی ہوئی چیز کے ساتھ تعامل کر سکیں۔ براؤزر کے ساتھ تعامل کرنے کا سب سے عام طریقہ مختلف عناصر پر کلک کرنا اور ٹائپ کرنا ہے۔ بطور ڈویلپر ہمیں ایک چیلنج کا سامنا ہوتا ہے کہ ہمیں نہیں معلوم کہ صارف یہ آپریشن کب انجام دے گا!

[ایونٹ ڈرائیون پروگرامنگ](https://en.wikipedia.org/wiki/Event-driven_programming) وہ قسم کی پروگرامنگ ہے جو ہمیں اپنے GUI بنانے کے لیے کرنی ہوتی ہے۔ اگر ہم اس اصطلاح کو تھوڑا سا توڑ کر دیکھیں، تو ہمیں یہاں کا بنیادی لفظ **ایونٹ** نظر آتا ہے۔ [ایونٹ](https://www.merriam-webster.com/dictionary/event)، میریئم-ویبسٹر کے مطابق، "کچھ ایسا جو ہوتا ہے" کے طور پر بیان کیا گیا ہے۔ یہ ہماری صورتحال کو بالکل بیان کرتا ہے۔ ہمیں معلوم ہے کہ کچھ ہونے والا ہے جس کے لیے ہم کوڈ کو جواب میں چلانا چاہتے ہیں، لیکن ہمیں نہیں معلوم کہ یہ کب ہوگا۔

جس طرح ہم کوڈ کے کسی حصے کو چلانا چاہتے ہیں، اسے نشان زد کرنے کا طریقہ ایک فنکشن بنا کر ہوتا ہے۔ جب ہم [پروسیجرل پروگرامنگ](https://en.wikipedia.org/wiki/Procedural_programming) کے بارے میں سوچتے ہیں، تو فنکشنز کو ایک خاص ترتیب میں بلایا جاتا ہے۔ یہی چیز ایونٹ ڈرائیون پروگرامنگ کے ساتھ بھی سچ ہوگی۔ فرق صرف یہ ہے کہ **فنکشنز کو کیسے بلایا جائے گا**۔

ایونٹس (بٹن کلک کرنا، ٹائپ کرنا وغیرہ) کو ہینڈل کرنے کے لیے، ہم **ایونٹ لسٹنرز** رجسٹر کرتے ہیں۔ ایونٹ لسٹنر ایک فنکشن ہوتا ہے جو کسی ایونٹ کے ہونے کا انتظار کرتا ہے اور جواب میں چلتا ہے۔ ایونٹ لسٹنرز UI کو اپ ڈیٹ کر سکتے ہیں، سرور کو کال کر سکتے ہیں، یا صارف کی کارروائی کے جواب میں جو کچھ بھی کرنے کی ضرورت ہو وہ کر سکتے ہیں۔ ہم ایونٹ لسٹنر کو [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) استعمال کرکے اور ایک فنکشن فراہم کرکے شامل کرتے ہیں۔

> **نوٹ:** یہ بات قابل ذکر ہے کہ ایونٹ لسٹنرز بنانے کے کئی طریقے ہیں۔ آپ گمنام فنکشنز استعمال کر سکتے ہیں، یا نامزد فنکشنز بنا سکتے ہیں۔ آپ مختلف شارٹ کٹس استعمال کر سکتے ہیں، جیسے `click` پراپرٹی سیٹ کرنا، یا `addEventListener` استعمال کرنا۔ ہماری مشق میں ہم `addEventListener` اور گمنام فنکشنز پر توجہ مرکوز کریں گے، کیونکہ یہ ویب ڈویلپرز کے استعمال کا سب سے عام طریقہ ہے۔ یہ سب سے زیادہ لچکدار بھی ہے، کیونکہ `addEventListener` تمام ایونٹس کے لیے کام کرتا ہے، اور ایونٹ کا نام پیرامیٹر کے طور پر فراہم کیا جا سکتا ہے۔

### عام ایونٹس

جب آپ ایپلیکیشن بنا رہے ہوں تو آپ کے لیے [درجنوں ایونٹس](https://developer.mozilla.org/docs/Web/Events) دستیاب ہیں جنہیں آپ سن سکتے ہیں۔ بنیادی طور پر صارف جو کچھ بھی صفحے پر کرتا ہے وہ ایک ایونٹ کو جنم دیتا ہے، جو آپ کو یہ طاقت دیتا ہے کہ آپ ان کے لیے مطلوبہ تجربہ یقینی بنائیں۔ خوش قسمتی سے، آپ کو عام طور پر صرف چند ایونٹس کی ضرورت ہوتی ہے۔ یہاں کچھ عام ایونٹس ہیں (جن میں سے دو ہم اپنے گیم بناتے وقت استعمال کریں گے):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): صارف نے کسی چیز پر کلک کیا، عام طور پر بٹن یا ہائپر لنک
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): صارف نے دائیں ماؤس بٹن پر کلک کیا
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): صارف نے کچھ متن کو منتخب کیا
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): صارف نے کچھ متن داخل کیا

## گیم بنانا

ہم جاوا اسکرپٹ میں ایونٹس کے کام کرنے کے طریقے کو دریافت کرنے کے لیے ایک گیم بنائیں گے۔ ہمارا گیم کھلاڑی کی ٹائپنگ مہارت کو جانچنے والا ہوگا، جو کہ تمام ڈویلپرز کے لیے ایک انتہائی کم قدر کی جانے والی مہارت ہے۔ ہمیں اپنی ٹائپنگ کی مشق کرنی چاہیے! گیم کا عمومی بہاؤ کچھ اس طرح ہوگا:

- کھلاڑی اسٹارٹ بٹن پر کلک کرتا ہے اور اسے ٹائپ کرنے کے لیے ایک اقتباس دیا جاتا ہے
- کھلاڑی اقتباس کو جتنا جلدی ہو سکے ٹیکسٹ باکس میں ٹائپ کرتا ہے
  - جیسے ہی ہر لفظ مکمل ہوتا ہے، اگلا لفظ نمایاں ہو جاتا ہے
  - اگر کھلاڑی نے غلطی کی، تو ٹیکسٹ باکس کو سرخ کر دیا جاتا ہے
  - جب کھلاڑی اقتباس مکمل کرتا ہے، تو ایک کامیابی کا پیغام دکھایا جاتا ہے جس میں گزرا ہوا وقت بتایا جاتا ہے

آئیے اپنا گیم بنائیں اور ایونٹس کے بارے میں سیکھیں!

### فائل کا ڈھانچہ

ہمیں کل تین فائلوں کی ضرورت ہوگی: **index.html**, **script.js** اور **style.css**۔ آئیے انہیں ترتیب دینے سے شروع کریں تاکہ ہمارا کام آسان ہو جائے۔

- کنسول یا ٹرمینل ونڈو کھول کر اور درج ذیل کمانڈ جاری کرکے اپنے کام کے لیے ایک نیا فولڈر بنائیں:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- ویژول اسٹوڈیو کوڈ کھولیں

```bash
code .
```

- ویژول اسٹوڈیو کوڈ میں فولڈر میں تین فائلیں شامل کریں جن کے نام درج ذیل ہوں:
  - index.html
  - script.js
  - style.css

## یوزر انٹرفیس بنائیں

اگر ہم ضروریات کو دیکھیں، تو ہمیں معلوم ہوگا کہ ہمیں اپنے HTML صفحے پر چند عناصر کی ضرورت ہوگی۔ یہ کسی ترکیب کی طرح ہے، جہاں ہمیں کچھ اجزاء کی ضرورت ہوتی ہے:

- اقتباس کو ظاہر کرنے کے لیے کہیں، جسے صارف ٹائپ کرے
- کوئی پیغام ظاہر کرنے کے لیے کہیں، جیسے کامیابی کا پیغام
- ٹائپنگ کے لیے ایک ٹیکسٹ باکس
- ایک اسٹارٹ بٹن

ان میں سے ہر ایک کو IDs کی ضرورت ہوگی تاکہ ہم انہیں اپنے جاوا اسکرپٹ میں استعمال کر سکیں۔ ہم ان CSS اور جاوا اسکرپٹ فائلوں کے حوالہ جات بھی شامل کریں گے جنہیں ہم بنانے جا رہے ہیں۔

ایک نئی فائل بنائیں جس کا نام **index.html** ہو۔ درج ذیل HTML شامل کریں:

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

### ایپلیکیشن لانچ کریں

ہمیشہ بہتر ہوتا ہے کہ ترقیاتی کام کو مرحلہ وار کریں تاکہ دیکھ سکیں کہ چیزیں کیسی لگ رہی ہیں۔ آئیے اپنی ایپلیکیشن لانچ کریں۔ ویژول اسٹوڈیو کوڈ کے لیے ایک شاندار ایکسٹینشن ہے جسے [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) کہا جاتا ہے، جو آپ کی ایپلیکیشن کو مقامی طور پر ہوسٹ کرے گا اور ہر بار جب آپ محفوظ کریں گے تو براؤزر کو ریفریش کرے گا۔

- [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) انسٹال کریں، لنک پر کلک کریں اور **Install** پر کلک کریں
  - براؤزر آپ کو ویژول اسٹوڈیو کوڈ کھولنے کے لیے کہے گا، اور پھر ویژول اسٹوڈیو کوڈ آپ کو انسٹالیشن کرنے کے لیے کہے گا
  - اگر کہا جائے تو ویژول اسٹوڈیو کوڈ کو دوبارہ شروع کریں
- انسٹال ہونے کے بعد، ویژول اسٹوڈیو کوڈ میں، Ctrl-Shift-P (یا Cmd-Shift-P) دبائیں تاکہ کمانڈ پیلیٹ کھلے
- **Live Server: Open with Live Server** ٹائپ کریں
  - Live Server آپ کی ایپلیکیشن کو ہوسٹ کرنا شروع کر دے گا
- براؤزر کھولیں اور **https://localhost:5500** پر جائیں
- آپ کو اب وہ صفحہ نظر آنا چاہیے جو آپ نے بنایا ہے!

آئیے کچھ فعالیت شامل کریں۔

## CSS شامل کریں

ہمارا HTML بننے کے بعد، آئیے کور اسٹائلنگ کے لیے CSS شامل کریں۔ ہمیں اس لفظ کو نمایاں کرنا ہوگا جسے کھلاڑی کو ٹائپ کرنا چاہیے، اور اگر انہوں نے غلط ٹائپ کیا ہو تو ٹیکسٹ باکس کو رنگین کرنا ہوگا۔ ہم یہ دو کلاسز کے ذریعے کریں گے۔

ایک نئی فائل بنائیں جس کا نام **style.css** ہو اور درج ذیل syntax شامل کریں۔

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

✅ جب بات CSS کی ہو تو آپ اپنی صفحہ کی ترتیب کو اپنی مرضی کے مطابق بنا سکتے ہیں۔ تھوڑا وقت نکالیں اور صفحہ کو مزید دلکش بنائیں:

- مختلف فونٹ منتخب کریں
- ہیڈرز کو رنگین کریں
- آئٹمز کا سائز تبدیل کریں

## جاوا اسکرپٹ

ہمارا UI بننے کے بعد، اب وقت ہے کہ ہم جاوا اسکرپٹ پر توجہ مرکوز کریں جو منطق فراہم کرے گا۔ ہم اسے چند مراحل میں تقسیم کریں گے:

- [کانسٹینٹس بنائیں](../../../../4-typing-game/typing-game)
- [گیم شروع کرنے کے لیے ایونٹ لسٹنر](../../../../4-typing-game/typing-game)
- [ٹائپنگ کے لیے ایونٹ لسٹنر](../../../../4-typing-game/typing-game)

لیکن پہلے، ایک نئی فائل بنائیں جس کا نام **script.js** ہو۔

### کانسٹینٹس شامل کریں

ہمیں پروگرامنگ کو آسان بنانے کے لیے چند آئٹمز کی ضرورت ہوگی۔ ایک بار پھر، ترکیب کی طرح، یہاں وہ چیزیں ہیں جن کی ہمیں ضرورت ہوگی:

- تمام اقتباسات کی فہرست کے ساتھ ایک array
- موجودہ اقتباس کے تمام الفاظ کو ذخیرہ کرنے کے لیے ایک خالی array
- اس لفظ کا انڈیکس ذخیرہ کرنے کی جگہ جسے کھلاڑی اس وقت ٹائپ کر رہا ہے
- وہ وقت جب کھلاڑی نے اسٹارٹ پر کلک کیا

ہم UI عناصر کے حوالہ جات بھی چاہتے ہیں:

- ٹیکسٹ باکس (**typed-value**)
- اقتباس کی نمائش (**quote**)
- پیغام (**message**)

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

✅ اپنے گیم میں مزید اقتباسات شامل کریں

> **نوٹ:** ہم کوڈ میں جب چاہیں عناصر کو `document.getElementById` استعمال کرکے حاصل کر سکتے ہیں۔ چونکہ ہم ان عناصر کا باقاعدگی سے حوالہ دیں گے، ہم اسٹرنگ لیٹرلز کے ساتھ ٹائپوز سے بچنے کے لیے کانسٹینٹس استعمال کریں گے۔ [Vue.js](https://vuejs.org/) یا [React](https://reactjs.org/) جیسے فریم ورک آپ کو اپنے کوڈ کو مرکزی بنانے میں بہتر طریقے سے مدد دے سکتے ہیں۔

ایک منٹ نکالیں اور `const`, `let` اور `var` استعمال کرنے پر ایک ویڈیو دیکھیں

[![ویریبلز کی اقسام](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "ویریبلز کی اقسام")

> 🎥 ویریبلز کے بارے میں ویڈیو دیکھنے کے لیے اوپر دی گئی تصویر پر کلک کریں۔

### اسٹارٹ لاجک شامل کریں

گیم شروع کرنے کے لیے، کھلاڑی اسٹارٹ پر کلک کرے گا۔ ظاہر ہے، ہمیں نہیں معلوم کہ وہ اسٹارٹ پر کب کلک کریں گے۔ یہ وہ جگہ ہے جہاں [ایونٹ لسٹنر](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) کام آتا ہے۔ ایونٹ لسٹنر ہمیں کسی چیز کے ہونے کا انتظار کرنے اور جواب میں کوڈ چلانے کی اجازت دے گا۔ ہمارے معاملے میں، ہم چاہتے ہیں کہ جب صارف اسٹارٹ پر کلک کرے تو کوڈ چلایا جائے۔

جب صارف **start** پر کلک کرے، تو ہمیں ایک اقتباس منتخب کرنا ہوگا، یوزر انٹرفیس کو ترتیب دینا ہوگا، اور موجودہ لفظ اور وقت کا ٹریکنگ سیٹ اپ کرنا ہوگا۔ نیچے وہ جاوا اسکرپٹ ہے جسے آپ کو شامل کرنے کی ضرورت ہے؛ ہم اسکرپٹ بلاک کے بعد اس پر بات کرتے ہیں۔

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

آئیے کوڈ کو توڑ کر دیکھیں!

- لفظ کی ٹریکنگ سیٹ اپ کریں
  - [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) اور [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) کا استعمال ہمیں `quotes` array سے تصادفی طور پر ایک اقتباس منتخب کرنے کی اجازت دیتا ہے
  - ہم `quote` کو `words` کے array میں تبدیل کرتے ہیں تاکہ ہم اس لفظ کا ٹریک کر سکیں جسے کھلاڑی اس وقت ٹائپ کر رہا ہے
  - `wordIndex` کو 0 پر سیٹ کیا جاتا ہے، کیونکہ کھلاڑی پہلے لفظ سے شروع کرے گا
- UI سیٹ اپ کریں
  - `spanWords` کا array بنائیں، جس میں ہر لفظ ایک `span` عنصر کے اندر ہوتا ہے
    - یہ ہمیں ڈسپلے پر لفظ کو نمایاں کرنے کی اجازت دے گا
  - `join` array کو ایک string بنانے کے لیے استعمال کریں جسے ہم `quoteElement` پر `innerHTML` کو اپ ڈیٹ کرنے کے لیے استعمال کر سکیں
    - یہ اقتباس کو کھلاڑی کے لیے ظاہر کرے گا
  - پہلے `span` عنصر کے `className` کو `highlight` پر سیٹ کریں تاکہ اسے پیلے رنگ کے طور پر نمایاں کیا جا سکے
  - `messageElement` کو صاف کریں اور `innerText` کو `''` پر سیٹ کریں
- ٹیکسٹ باکس سیٹ اپ کریں
  - موجودہ `value` کو `typedValueElement` پر صاف کریں
  - `typedValueElement` پر `focus` سیٹ کریں
- ٹائمر کو `getTime` کال کرکے شروع کریں

### ٹائپنگ لاجک شامل کریں

جب کھلاڑی ٹائپ کرتا ہے، تو ایک `input` ایونٹ پیدا ہوگا۔ یہ ایونٹ لسٹنر چیک کرے گا کہ آیا کھلاڑی لفظ کو صحیح طریقے سے ٹائپ کر رہا ہے، اور گیم کی موجودہ حالت کو ہینڈل کرے گا۔ **script.js** پر واپس جائیں، اور درج ذیل کوڈ آخر میں شامل کریں۔ ہم بعد میں اسے توڑ کر دیکھیں گے۔

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

آئیے کوڈ کو توڑ کر دیکھیں! ہم موجودہ لفظ اور وہ قدر حاصل کرتے ہیں جو کھلاڑی نے اب تک ٹائپ کی ہے۔ پھر ہمارے پاس واٹر فال لاجک ہے، جہاں ہم چیک کرتے ہیں کہ آیا اقتباس مکمل ہے، لفظ مکمل ہے، لفظ درست ہے، یا (آخر میں)، اگر کوئی غلطی ہے۔

- اقتباس مکمل ہے، جس کی نشاندہی `typedValue` کے `currentWord` کے برابر ہونے سے ہوتی ہے، اور `wordIndex` کے `words` کی `length` سے ایک کم ہونے سے ہوتی ہے
  - `elapsedTime` کو موجودہ وقت سے `startTime` کو منفی کرکے حساب کریں
  - `elapsedTime` کو 1,000 سے تقسیم کریں تاکہ ملی سیکنڈز کو سیکنڈز میں تبدیل کیا جا سکے
  - کامیابی کا پیغام دکھائیں
- لفظ مکمل ہے، جس کی نشاندہی `typedValue` کے اسپیس کے ساتھ ختم ہونے سے ہوتی ہے (لفظ کے آخر میں) اور `typedValue` کے `currentWord` کے برابر ہونے سے ہوتی ہے
  - اگلے لفظ کو ٹائپ کرنے کی اجازت دینے کے لیے `typedElement` پر `value` کو `''` پر سیٹ کریں
  - اگلے لفظ پر جانے کے لیے `wordIndex` کو انکریمنٹ کریں
  - `quoteElement` کے تمام `childNodes` کے ذریعے لوپ کریں تاکہ `className` کو `''` پر سیٹ کریں تاکہ ڈیفالٹ ڈسپلے پر واپس جائیں
  - موجودہ لفظ کے `className` کو `highlight` پر سیٹ کریں تاکہ اسے ٹائپ کرنے کے لیے اگلے لفظ کے طور پر نشان زد کیا جا سکے
- لفظ اس وقت درست طریقے سے ٹائپ کیا گیا ہے (لیکن مکمل نہیں)، جس کی نشاندہی `currentWord` کے `typedValue` سے شروع ہونے سے ہوتی ہے
  - `typedValueElement` کو ڈیفالٹ کے طور پر ظاہر کرنے کو یقینی بنائیں اور `className` کو صاف کریں
- اگر ہم یہاں تک پہنچ گئے ہیں، تو ہمارے پاس ایک غلطی ہے
  - `typedValueElement` پر `className` کو `error` پر سیٹ کریں

## اپنی ایپلیکیشن کی جانچ کریں

آپ آخر تک پہنچ گئے ہیں! آخری مرحلہ یہ ہے کہ یہ یقینی بنایا جائے کہ ہماری ایپلیکیشن کام کرتی ہے۔ اسے آزمائیں! اگر غلطیاں ہوں تو پریشان نہ ہوں؛ **تمام ڈویلپرز** کو غلطیاں ہوتی ہیں۔ پیغامات کا جائزہ لیں اور ضرورت کے مطابق ڈیبگ کریں۔

**start** پر کلک کریں، اور ٹائپ کرنا شروع کریں! یہ کچھ اس طرح نظر آنا چاہیے جیسے ہم نے پہلے اینیمیشن دیکھی تھی۔

![گیم کے عمل میں اینیمیشن](../../../../4-typing-game/images/demo.gif)

---

## 🚀 چیلنج

مزید فعالیت شامل کریں

- اقتباس مکمل ہونے پر `input` ایونٹ لسٹنر کو غیر فعال کریں، اور بٹن پر کلک کرنے پر اسے دوبارہ فعال کریں
- اقتباس مکمل ہونے پر ٹیکسٹ باکس کو غیر فعال کریں
- کامی
## لیکچر کے بعد کا کوئز

[لیکچر کے بعد کا کوئز](https://ff-quizzes.netlify.app/web/quiz/22)

## جائزہ اور خود مطالعہ

ویب براؤزر کے ذریعے ڈویلپر کے لیے دستیاب [تمام ایونٹس](https://developer.mozilla.org/docs/Web/Events) کے بارے میں پڑھیں، اور ان منظرناموں پر غور کریں جن میں آپ ہر ایک کا استعمال کریں گے۔

## اسائنمنٹ

[ایک نیا کی بورڈ گیم بنائیں](assignment.md)

---

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا غیر درستیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔