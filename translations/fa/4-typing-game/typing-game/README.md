<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1b0aeccb600f83c603cd70cb42df594d",
  "translation_date": "2025-08-29T14:36:28+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "fa"
}
-->
# ایجاد یک بازی با استفاده از رویدادها

## آزمون پیش از درس

[آزمون پیش از درس](https://ff-quizzes.netlify.app/web/quiz/21)

## برنامه‌نویسی مبتنی بر رویداد

هنگام ایجاد یک برنامه مبتنی بر مرورگر، ما یک رابط کاربری گرافیکی (GUI) برای کاربر فراهم می‌کنیم تا هنگام تعامل با چیزی که ساخته‌ایم از آن استفاده کند. رایج‌ترین روش تعامل با مرورگر از طریق کلیک کردن و تایپ کردن در عناصر مختلف است. چالش ما به عنوان توسعه‌دهنده این است که نمی‌دانیم چه زمانی کاربر این عملیات را انجام خواهد داد!

[برنامه‌نویسی مبتنی بر رویداد](https://en.wikipedia.org/wiki/Event-driven_programming) نام نوع برنامه‌نویسی است که برای ایجاد GUI نیاز داریم. اگر این عبارت را کمی تجزیه کنیم، کلمه اصلی اینجا **رویداد** است. [رویداد](https://www.merriam-webster.com/dictionary/event)، طبق تعریف Merriam-Webster، به معنای "چیزی که اتفاق می‌افتد" است. این تعریف کاملاً وضعیت ما را توصیف می‌کند. ما می‌دانیم که چیزی قرار است اتفاق بیفتد که می‌خواهیم در پاسخ به آن کدی اجرا کنیم، اما نمی‌دانیم چه زمانی رخ خواهد داد.

راهی که برای علامت‌گذاری بخشی از کد که می‌خواهیم اجرا شود استفاده می‌کنیم، ایجاد یک تابع است. وقتی به [برنامه‌نویسی رویه‌ای](https://en.wikipedia.org/wiki/Procedural_programming) فکر می‌کنیم، توابع به ترتیب خاصی فراخوانی می‌شوند. همین موضوع در برنامه‌نویسی مبتنی بر رویداد نیز صادق است. تفاوت در این است که **چگونه** توابع فراخوانی می‌شوند.

برای مدیریت رویدادها (کلیک کردن دکمه، تایپ کردن و غیره)، ما **شنونده‌های رویداد** ثبت می‌کنیم. شنونده رویداد یک تابع است که منتظر وقوع یک رویداد می‌ماند و در پاسخ اجرا می‌شود. شنونده‌های رویداد می‌توانند رابط کاربری را به‌روزرسانی کنند، درخواست‌هایی به سرور ارسال کنند یا هر کار دیگری که در پاسخ به عمل کاربر نیاز است انجام دهند. ما یک شنونده رویداد را با استفاده از [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) و ارائه یک تابع برای اجرا اضافه می‌کنیم.

> **NOTE:** ارزش دارد که بدانید روش‌های متعددی برای ایجاد شنونده‌های رویداد وجود دارد. شما می‌توانید از توابع ناشناس استفاده کنید یا توابع نام‌گذاری شده ایجاد کنید. همچنین می‌توانید از میانبرهای مختلفی مانند تنظیم خاصیت `click` یا استفاده از `addEventListener` بهره ببرید. در تمرین ما، تمرکز بر `addEventListener` و توابع ناشناس خواهد بود، زیرا این روش احتمالاً رایج‌ترین تکنیکی است که توسعه‌دهندگان وب استفاده می‌کنند. همچنین این روش انعطاف‌پذیرترین است، زیرا `addEventListener` برای همه رویدادها کار می‌کند و نام رویداد می‌تواند به‌عنوان یک پارامتر ارائه شود.

### رویدادهای رایج

[ده‌ها رویداد](https://developer.mozilla.org/docs/Web/Events) وجود دارد که هنگام ایجاد یک برنامه می‌توانید به آن‌ها گوش دهید. اساساً هر کاری که کاربر در یک صفحه انجام می‌دهد یک رویداد ایجاد می‌کند، که به شما قدرت زیادی می‌دهد تا تجربه‌ای که می‌خواهید را برای او فراهم کنید. خوشبختانه، معمولاً فقط به تعداد کمی از رویدادها نیاز خواهید داشت. در اینجا چند رویداد رایج آورده شده است (از جمله دو موردی که هنگام ایجاد بازی خود استفاده خواهیم کرد):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): کاربر روی چیزی کلیک کرده است، معمولاً یک دکمه یا لینک
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): کاربر دکمه راست ماوس را کلیک کرده است
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): کاربر متنی را انتخاب کرده است
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): کاربر متنی وارد کرده است

## ایجاد بازی

ما قصد داریم یک بازی ایجاد کنیم تا نحوه کار رویدادها در جاوااسکریپت را بررسی کنیم. بازی ما مهارت تایپ کردن بازیکن را آزمایش می‌کند، که یکی از مهارت‌های کم‌اهمیت اما بسیار مهمی است که همه توسعه‌دهندگان باید داشته باشند. همه ما باید مهارت تایپ کردن خود را تمرین کنیم! جریان کلی بازی به این صورت خواهد بود:

- بازیکن روی دکمه شروع کلیک می‌کند و یک نقل‌قول برای تایپ کردن به او نمایش داده می‌شود
- بازیکن نقل‌قول را در یک جعبه متن به سریع‌ترین شکل ممکن تایپ می‌کند
  - با تکمیل هر کلمه، کلمه بعدی برجسته می‌شود
  - اگر بازیکن اشتباه تایپ کند، جعبه متن به رنگ قرمز تغییر می‌کند
  - وقتی بازیکن نقل‌قول را کامل کرد، یک پیام موفقیت با زمان سپری شده نمایش داده می‌شود

بیایید بازی خود را بسازیم و درباره رویدادها یاد بگیریم!

### ساختار فایل

ما به سه فایل نیاز داریم: **index.html**، **script.js** و **style.css**. بیایید آن‌ها را تنظیم کنیم تا کارمان راحت‌تر شود.

- یک پوشه جدید برای کار خود ایجاد کنید. برای این کار، یک کنسول یا پنجره ترمینال باز کنید و دستور زیر را اجرا کنید:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- Visual Studio Code را باز کنید

```bash
code .
```

- سه فایل با نام‌های زیر به پوشه در Visual Studio Code اضافه کنید:
  - index.html
  - script.js
  - style.css

## ایجاد رابط کاربری

اگر نیازمندی‌ها را بررسی کنیم، می‌دانیم که به چند عنصر در صفحه HTML خود نیاز داریم. این شبیه یک دستور پخت است که به چند ماده اولیه نیاز داریم:

- جایی برای نمایش نقل‌قولی که کاربر باید تایپ کند
- جایی برای نمایش پیام‌ها، مانند پیام موفقیت
- یک جعبه متن برای تایپ کردن
- یک دکمه شروع

هر یک از این عناصر به شناسه‌هایی نیاز دارند تا بتوانیم با آن‌ها در جاوااسکریپت کار کنیم. همچنین باید ارجاعاتی به فایل‌های CSS و جاوااسکریپت که قرار است ایجاد کنیم اضافه کنیم.

یک فایل جدید با نام **index.html** ایجاد کنید. HTML زیر را اضافه کنید:

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

### اجرای برنامه

همیشه بهتر است به صورت تدریجی توسعه دهید تا ببینید همه چیز چگونه به نظر می‌رسد. بیایید برنامه خود را اجرا کنیم. یک افزونه فوق‌العاده برای Visual Studio Code به نام [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) وجود دارد که برنامه شما را به صورت محلی میزبانی می‌کند و هر بار که ذخیره می‌کنید مرورگر را تازه‌سازی می‌کند.

- [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) را نصب کنید. برای این کار، روی لینک کلیک کنید و گزینه **Install** را انتخاب کنید
  - مرورگر از شما می‌خواهد Visual Studio Code را باز کنید، و سپس Visual Studio Code از شما می‌خواهد نصب را انجام دهید
  - اگر درخواست شد، Visual Studio Code را مجدداً راه‌اندازی کنید
- پس از نصب، در Visual Studio Code، کلیدهای Ctrl-Shift-P (یا Cmd-Shift-P) را فشار دهید تا پالت دستورات باز شود
- عبارت **Live Server: Open with Live Server** را تایپ کنید
  - Live Server شروع به میزبانی برنامه شما می‌کند
- یک مرورگر باز کنید و به آدرس **https://localhost:5500** بروید
- اکنون باید صفحه‌ای که ایجاد کرده‌اید را ببینید!

بیایید کمی عملکرد اضافه کنیم.

## افزودن CSS

با ایجاد HTML، بیایید CSS را برای استایل اصلی اضافه کنیم. ما باید کلمه‌ای که بازیکن باید تایپ کند را برجسته کنیم و جعبه متن را در صورت اشتباه تایپ کردن رنگی کنیم. این کار را با دو کلاس انجام خواهیم داد.

یک فایل جدید با نام **style.css** ایجاد کنید و سینتکس زیر را اضافه کنید.

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

✅ وقتی صحبت از CSS می‌شود، می‌توانید صفحه خود را به هر شکلی که دوست دارید طراحی کنید. کمی وقت بگذارید و صفحه را جذاب‌تر کنید:

- یک فونت متفاوت انتخاب کنید
- هدرها را رنگی کنید
- اندازه آیتم‌ها را تغییر دهید

## جاوااسکریپت

با ایجاد رابط کاربری، اکنون زمان آن است که توجه خود را به جاوااسکریپت معطوف کنیم که منطق را فراهم می‌کند. ما این کار را به چند مرحله تقسیم خواهیم کرد:

- [ایجاد ثابت‌ها](../../../../4-typing-game/typing-game)
- [شنونده رویداد برای شروع بازی](../../../../4-typing-game/typing-game)
- [شنونده رویداد برای تایپ کردن](../../../../4-typing-game/typing-game)

اما ابتدا یک فایل جدید با نام **script.js** ایجاد کنید.

### افزودن ثابت‌ها

ما به چند آیتم نیاز داریم تا کار برنامه‌نویسی را برای خود آسان‌تر کنیم. دوباره، مشابه یک دستور پخت، این‌ها چیزی است که نیاز داریم:

- آرایه‌ای با لیست تمام نقل‌قول‌ها
- آرایه‌ای خالی برای ذخیره تمام کلمات نقل‌قول فعلی
- فضایی برای ذخیره شاخص کلمه‌ای که بازیکن در حال تایپ کردن آن است
- زمانی که بازیکن روی شروع کلیک کرده است

ما همچنین می‌خواهیم ارجاعاتی به عناصر رابط کاربری داشته باشیم:

- جعبه متن (**typed-value**)
- نمایش نقل‌قول (**quote**)
- پیام (**message**)

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

✅ نقل‌قول‌های بیشتری به بازی خود اضافه کنید

> **NOTE:** ما می‌توانیم عناصر را هر زمان که بخواهیم در کد با استفاده از `document.getElementById` بازیابی کنیم. به دلیل اینکه قرار است به طور مرتب به این عناصر ارجاع دهیم، برای جلوگیری از اشتباهات تایپی با رشته‌های متنی، از ثابت‌ها استفاده می‌کنیم. فریم‌ورک‌هایی مانند [Vue.js](https://vuejs.org/) یا [React](https://reactjs.org/) می‌توانند به شما کمک کنند تا کد خود را بهتر مدیریت کنید.

چند دقیقه وقت بگذارید و یک ویدیو درباره استفاده از `const`، `let` و `var` تماشا کنید.

[![انواع متغیرها](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "انواع متغیرها")

> 🎥 روی تصویر بالا کلیک کنید تا ویدیویی درباره متغیرها مشاهده کنید.

### افزودن منطق شروع

برای شروع بازی، بازیکن روی شروع کلیک خواهد کرد. البته، ما نمی‌دانیم چه زمانی او روی شروع کلیک خواهد کرد. اینجاست که یک [شنونده رویداد](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) وارد عمل می‌شود. شنونده رویداد به ما اجازه می‌دهد منتظر وقوع چیزی (یک رویداد) باشیم و در پاسخ کدی اجرا کنیم. در مورد ما، می‌خواهیم کدی اجرا کنیم وقتی کاربر روی شروع کلیک می‌کند.

وقتی کاربر روی **شروع** کلیک می‌کند، باید یک نقل‌قول انتخاب کنیم، رابط کاربری را تنظیم کنیم و ردیابی کلمه فعلی و زمان‌بندی را تنظیم کنیم. در زیر جاوااسکریپتی که باید اضافه کنید آورده شده است؛ پس از بلوک اسکریپت آن را توضیح می‌دهیم.

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

بیایید کد را تجزیه کنیم!

- تنظیم ردیابی کلمات
  - استفاده از [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) و [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) به ما اجازه می‌دهد به صورت تصادفی یک نقل‌قول از آرایه `quotes` انتخاب کنیم
  - ما `quote` را به یک آرایه از `words` تبدیل می‌کنیم تا بتوانیم کلمه‌ای که بازیکن در حال تایپ کردن آن است را ردیابی کنیم
  - `wordIndex` روی 0 تنظیم می‌شود، زیرا بازیکن با اولین کلمه شروع خواهد کرد
- تنظیم رابط کاربری
  - یک آرایه از `spanWords` ایجاد کنید که هر کلمه را داخل یک عنصر `span` قرار می‌دهد
    - این به ما اجازه می‌دهد کلمه را روی نمایشگر برجسته کنیم
  - آرایه را با `join` ترکیب کنید تا یک رشته ایجاد شود که بتوانیم از آن برای به‌روزرسانی `innerHTML` روی `quoteElement` استفاده کنیم
    - این نقل‌قول را به بازیکن نمایش خواهد داد
  - `className` اولین عنصر `span` را روی `highlight` تنظیم کنید تا آن را به رنگ زرد برجسته کند
  - `messageElement` را با تنظیم `innerText` روی `''` پاک کنید
- تنظیم جعبه متن
  - مقدار فعلی `typedValueElement` را پاک کنید
  - فوکوس را روی `typedValueElement` تنظیم کنید
- تایمر را با فراخوانی `getTime` شروع کنید

### افزودن منطق تایپ کردن

هنگامی که بازیکن تایپ می‌کند، یک رویداد `input` ایجاد می‌شود. این شنونده رویداد بررسی می‌کند که آیا بازیکن کلمه را به درستی تایپ می‌کند و وضعیت فعلی بازی را مدیریت می‌کند. به فایل **script.js** بازگردید و کد زیر را به انتهای آن اضافه کنید. پس از آن، کد را تجزیه می‌کنیم.

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

بیایید کد را تجزیه کنیم! ما با گرفتن کلمه فعلی و مقداری که بازیکن تاکنون تایپ کرده است شروع می‌کنیم. سپس منطق آبشاری داریم، جایی که بررسی می‌کنیم آیا نقل‌قول کامل شده است، کلمه کامل شده است، کلمه درست تایپ شده است یا (در نهایت)، آیا خطایی وجود دارد.

- نقل‌قول کامل شده است، که با برابر بودن `typedValue` با `currentWord` و برابر بودن `wordIndex` با یکی کمتر از `length` آرایه `words` مشخص می‌شود
  - `elapsedTime` را با کم کردن `startTime` از زمان فعلی محاسبه کنید
  - `elapsedTime` را بر 1,000 تقسیم کنید تا از میلی‌ثانیه به ثانیه تبدیل شود
  - یک پیام موفقیت نمایش دهید
- کلمه کامل شده است، که با پایان یافتن `typedValue` با یک فاصله (پایان کلمه) و برابر بودن `typedValue` با `currentWord` مشخص می‌شود
  - مقدار `value` روی `typedElement` را روی `''` تنظیم کنید تا اجازه دهد کلمه بعدی تایپ شود
  - `wordIndex` را افزایش دهید تا به کلمه بعدی منتقل شود
  - از طریق تمام `childNodes` روی `quoteElement` حلقه بزنید تا `className` را روی `''` تنظیم کنید و به نمایش پیش‌فرض بازگردید
  - `className` کلمه فعلی را روی `highlight` تنظیم کنید تا آن را به‌عنوان کلمه بعدی برای تایپ علامت‌گذاری کند
- کلمه به درستی تایپ شده است (اما کامل نشده)، که با شروع شدن `currentWord` با `typedValue` مشخص می‌شود
  - اطمینان حاصل کنید که `typedValueElement` به صورت پیش‌فرض نمایش داده می‌شود با پاک کردن `className`
- اگر به اینجا رسیدیم، خطایی وجود دارد
  - `className` روی `typedValueElement` را روی `error` تنظیم کنید

## برنامه خود را آزمایش کنید

شما به پایان رسیدید! آخرین مرحله این است که مطمئن شوید برنامه شما کار می‌کند. امتحان کنید! نگران خطاها نباشید؛ **همه توسعه‌دهندگان** خطا دارند. پیام‌ها را بررسی کنید و در صورت نیاز اشکال‌زدایی کنید.

روی **شروع** کلیک کنید و شروع به تایپ کنید! باید شبیه انیمیشنی که قبلاً دیدیم باشد.

![انیمیشن بازی در حال اجرا](../../../../4-typing-game/images/demo.gif)

---

## 🚀 چالش

عملکرد بیشتری اضافه کنید

- شنونده رویداد `input` را پس از تکمیل غیرفعال کنید و هنگام کلیک کردن دکمه دوباره فعال کنید
- جعبه متن را هنگامی که بازیکن نقل‌قول را کامل کرد غیرفعال کنید
- یک پنجره مودال با پیام موفقیت نمایش دهید
- امتیازات بالا را با استفاده از [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage) ذخیره کنید
## آزمون پس از سخنرانی

[آزمون پس از سخنرانی](https://ff-quizzes.netlify.app/web/quiz/22)

## مرور و مطالعه شخصی

در مورد [تمام رویدادهای موجود](https://developer.mozilla.org/docs/Web/Events) که از طریق مرورگر وب در دسترس توسعه‌دهنده هستند مطالعه کنید و سناریوهایی را که ممکن است هر یک از آنها را استفاده کنید، در نظر بگیرید.

## تکلیف

[یک بازی جدید با صفحه‌کلید بسازید](assignment.md)

---

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما برای دقت تلاش می‌کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نادقتی‌هایی باشند. سند اصلی به زبان اصلی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما هیچ مسئولیتی در قبال سوءتفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.