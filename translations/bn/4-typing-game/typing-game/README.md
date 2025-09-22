<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1b0aeccb600f83c603cd70cb42df594d",
  "translation_date": "2025-08-28T23:05:52+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "bn"
}
-->
# ইভেন্ট ব্যবহার করে একটি গেম তৈরি করা

## প্রাক-লেকচার কুইজ

[প্রাক-লেকচার কুইজ](https://ff-quizzes.netlify.app/web/quiz/21)

## ইভেন্ট চালিত প্রোগ্রামিং

ব্রাউজার ভিত্তিক অ্যাপ্লিকেশন তৈরি করার সময়, আমরা ব্যবহারকারীর জন্য একটি গ্রাফিকাল ইউজার ইন্টারফেস (GUI) প্রদান করি, যা তারা আমাদের তৈরি করা জিনিসের সাথে ইন্টারঅ্যাক্ট করতে ব্যবহার করে। ব্রাউজারের সাথে ইন্টারঅ্যাক্ট করার সবচেয়ে সাধারণ উপায় হল বিভিন্ন উপাদানে ক্লিক করা এবং টাইপ করা। একজন ডেভেলপার হিসেবে আমাদের চ্যালেঞ্জ হল, আমরা জানি না তারা কখন এই কাজগুলো করবে!

[ইভেন্ট চালিত প্রোগ্রামিং](https://en.wikipedia.org/wiki/Event-driven_programming) হল সেই ধরনের প্রোগ্রামিং যা আমাদের GUI তৈরি করতে করতে হয়। যদি আমরা এই শব্দটি একটু বিশ্লেষণ করি, তাহলে আমরা দেখতে পাই মূল শব্দটি হল **ইভেন্ট**। [ইভেন্ট](https://www.merriam-webster.com/dictionary/event), মেরিয়াম-ওয়েবস্টারের মতে, "কিছু যা ঘটে" হিসাবে সংজ্ঞায়িত করা হয়েছে। এটি আমাদের পরিস্থিতি পুরোপুরি বর্ণনা করে। আমরা জানি কিছু ঘটতে যাচ্ছে যার জন্য আমরা কিছু কোড কার্যকর করতে চাই, কিন্তু আমরা জানি না এটি কখন ঘটবে।

আমরা যে কোডের অংশটি কার্যকর করতে চাই তা চিহ্নিত করার উপায় হল একটি ফাংশন তৈরি করা। যখন আমরা [প্রসিডিউরাল প্রোগ্রামিং](https://en.wikipedia.org/wiki/Procedural_programming) নিয়ে চিন্তা করি, তখন ফাংশনগুলো একটি নির্দিষ্ট ক্রমে কল করা হয়। ইভেন্ট চালিত প্রোগ্রামিংয়ের ক্ষেত্রেও একই জিনিস সত্য হবে। পার্থক্য হল **কীভাবে** ফাংশনগুলো কল করা হবে।

ইভেন্ট (বাটন ক্লিক করা, টাইপ করা ইত্যাদি) পরিচালনা করতে, আমরা **ইভেন্ট লিসনার** নিবন্ধন করি। একটি ইভেন্ট লিসনার হল একটি ফাংশন যা একটি ইভেন্ট ঘটার জন্য অপেক্ষা করে এবং প্রতিক্রিয়ায় কার্যকর হয়। ইভেন্ট লিসনার UI আপডেট করতে পারে, সার্ভারে কল করতে পারে, বা ব্যবহারকারীর ক্রিয়ার প্রতিক্রিয়ায় যা কিছু করা দরকার তা করতে পারে। আমরা [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) ব্যবহার করে একটি ইভেন্ট লিসনার যোগ করি এবং কার্যকর করার জন্য একটি ফাংশন প্রদান করি।

> **NOTE:** ইভেন্ট লিসনার তৈরি করার অনেক উপায় রয়েছে। আপনি অ্যানোনিমাস ফাংশন ব্যবহার করতে পারেন, অথবা নামযুক্ত ফাংশন তৈরি করতে পারেন। আপনি বিভিন্ন শর্টকাট ব্যবহার করতে পারেন, যেমন `click` প্রপার্টি সেট করা, অথবা `addEventListener` ব্যবহার করা। আমাদের অনুশীলনে আমরা `addEventListener` এবং অ্যানোনিমাস ফাংশনের উপর ফোকাস করব, কারণ এটি ওয়েব ডেভেলপারদের সবচেয়ে সাধারণ কৌশল। এটি সবচেয়ে নমনীয়ও, কারণ `addEventListener` সব ইভেন্টের জন্য কাজ করে এবং ইভেন্টের নাম প্যারামিটার হিসেবে প্রদান করা যায়।

### সাধারণ ইভেন্ট

অ্যাপ্লিকেশন তৈরি করার সময় আপনি শুনতে পারেন এমন [ডজনখানেক ইভেন্ট](https://developer.mozilla.org/docs/Web/Events) রয়েছে। মূলত ব্যবহারকারী একটি পৃষ্ঠায় যা কিছু করে তা একটি ইভেন্ট তৈরি করে, যা আপনাকে তাদের পছন্দসই অভিজ্ঞতা নিশ্চিত করার জন্য প্রচুর ক্ষমতা দেয়। সৌভাগ্যক্রমে, সাধারণত আপনাকে শুধুমাত্র কয়েকটি ইভেন্টের প্রয়োজন হবে। এখানে কয়েকটি সাধারণ ইভেন্ট রয়েছে (যার মধ্যে দুটি আমরা আমাদের গেম তৈরি করার সময় ব্যবহার করব):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): ব্যবহারকারী কিছু ক্লিক করেছে, সাধারণত একটি বাটন বা হাইপারলিঙ্ক
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): ব্যবহারকারী ডান মাউস বাটন ক্লিক করেছে
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): ব্যবহারকারী কিছু টেক্সট হাইলাইট করেছে
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): ব্যবহারকারী কিছু টেক্সট ইনপুট করেছে

## গেম তৈরি করা

আমরা ইভেন্টগুলো কীভাবে কাজ করে তা অন্বেষণ করতে একটি গেম তৈরি করতে যাচ্ছি। আমাদের গেমটি একজন খেলোয়াড়ের টাইপিং দক্ষতা পরীক্ষা করবে, যা সমস্ত ডেভেলপারদের জন্য সবচেয়ে অবমূল্যায়িত দক্ষতাগুলোর মধ্যে একটি। আমাদের সবার টাইপিং অনুশীলন করা উচিত! গেমটির সাধারণ প্রবাহটি এরকম হবে:

- খেলোয়াড় স্টার্ট বাটনে ক্লিক করে এবং টাইপ করার জন্য একটি কোট পায়
- খেলোয়াড় একটি টেক্সটবক্সে যত দ্রুত সম্ভব কোটটি টাইপ করে
  - প্রতিটি শব্দ সম্পন্ন হওয়ার সাথে সাথে পরবর্তীটি হাইলাইট হয়
  - যদি খেলোয়াড়ের টাইপিংয়ে ভুল থাকে, টেক্সটবক্সটি লাল হয়ে যায়
  - যখন খেলোয়াড় কোটটি সম্পন্ন করে, একটি সফলতার বার্তা প্রদর্শিত হয় এবং সময় গণনা দেখানো হয়

চলুন আমাদের গেমটি তৈরি করি এবং ইভেন্ট সম্পর্কে শিখি!

### ফাইলের কাঠামো

আমাদের মোট তিনটি ফাইলের প্রয়োজন হবে: **index.html**, **script.js** এবং **style.css**। চলুন এগুলো সেটআপ করি যাতে আমাদের কাজ সহজ হয়।

- একটি নতুন ফোল্ডার তৈরি করুন আপনার কাজের জন্য। কনসোল বা টার্মিনাল উইন্ডো খুলুন এবং নিম্নলিখিত কমান্ড দিন:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- ভিজ্যুয়াল স্টুডিও কোড খুলুন

```bash
code .
```

- ফোল্ডারে তিনটি ফাইল যোগ করুন ভিজ্যুয়াল স্টুডিও কোডে নিম্নলিখিত নাম দিয়ে:
  - index.html
  - script.js
  - style.css

## ইউজার ইন্টারফেস তৈরি করা

যদি আমরা প্রয়োজনীয়তাগুলো বিশ্লেষণ করি, তাহলে আমরা জানি আমাদের HTML পৃষ্ঠায় কয়েকটি উপাদানের প্রয়োজন হবে। এটি একটি রেসিপির মতো, যেখানে আমাদের কিছু উপাদান দরকার:

- ব্যবহারকারীর টাইপ করার জন্য কোট প্রদর্শনের জায়গা
- বার্তা প্রদর্শনের জায়গা, যেমন সফলতার বার্তা
- টাইপ করার জন্য একটি টেক্সটবক্স
- একটি স্টার্ট বাটন

প্রতিটি উপাদানের জন্য ID প্রয়োজন হবে যাতে আমরা সেগুলো আমাদের জাভাস্ক্রিপ্টে ব্যবহার করতে পারি। আমরা CSS এবং জাভাস্ক্রিপ্ট ফাইলগুলোর রেফারেন্সও যোগ করব যা আমরা তৈরি করতে যাচ্ছি।

একটি নতুন ফাইল তৈরি করুন যার নাম **index.html**। নিম্নলিখিত HTML যোগ করুন:

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

### অ্যাপ্লিকেশন চালু করা

সবসময়ই ভালো হয় ধাপে ধাপে ডেভেলপ করা যাতে জিনিসগুলো দেখতে কেমন তা বোঝা যায়। চলুন আমাদের অ্যাপ্লিকেশন চালু করি। ভিজ্যুয়াল স্টুডিও কোডের জন্য একটি চমৎকার এক্সটেনশন রয়েছে [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon), যা আপনার অ্যাপ্লিকেশনটি লোকালভাবে হোস্ট করবে এবং আপনি যখনই সেভ করবেন তখন ব্রাউজারটি রিফ্রেশ করবে।

- [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) ইনস্টল করুন। লিঙ্কে ক্লিক করুন এবং **Install** বাটনে ক্লিক করুন।
  - ব্রাউজার আপনাকে ভিজ্যুয়াল স্টুডিও কোড খুলতে বলবে, এবং তারপর ভিজ্যুয়াল স্টুডিও কোড ইনস্টলেশন সম্পন্ন করতে বলবে।
  - প্রয়োজন হলে ভিজ্যুয়াল স্টুডিও কোড পুনরায় চালু করুন।
- ইনস্টল করার পর, ভিজ্যুয়াল স্টুডিও কোডে Ctrl-Shift-P (বা Cmd-Shift-P) চাপুন কমান্ড প্যালেট খুলতে।
- টাইপ করুন **Live Server: Open with Live Server**
  - Live Server আপনার অ্যাপ্লিকেশন হোস্ট করা শুরু করবে।
- একটি ব্রাউজার খুলুন এবং **https://localhost:5500** এ যান।
- এখন আপনি তৈরি করা পৃষ্ঠাটি দেখতে পাবেন!

চলুন কিছু কার্যকারিতা যোগ করি।

## CSS যোগ করা

আমাদের HTML তৈরি করার পর, চলুন CSS যোগ করি মূল স্টাইলিংয়ের জন্য। আমাদের খেলোয়াড় যে শব্দটি টাইপ করা উচিত তা হাইলাইট করতে হবে এবং তারা ভুল টাইপ করলে টেক্সটবক্সটি রঙিন করতে হবে। আমরা এটি দুটি ক্লাস ব্যবহার করে করব।

একটি নতুন ফাইল তৈরি করুন যার নাম **style.css** এবং নিম্নলিখিত সিনট্যাক্স যোগ করুন।

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

✅ CSS-এর ক্ষেত্রে আপনি আপনার পৃষ্ঠাটি যেভাবে চান সেভাবে সাজাতে পারেন। কিছু সময় নিন এবং পৃষ্ঠাটি আরও আকর্ষণীয় করুন:

- একটি ভিন্ন ফন্ট নির্বাচন করুন
- হেডারগুলো রঙিন করুন
- আইটেমগুলো পুনরায় আকার দিন

## জাভাস্ক্রিপ্ট

আমাদের UI তৈরি করার পর, এখন আমাদের মনোযোগ কেন্দ্রীভূত করতে হবে জাভাস্ক্রিপ্টে, যা লজিক প্রদান করবে। আমরা এটি কয়েকটি ধাপে ভাগ করব:

- [কনস্ট্যান্ট তৈরি করা](../../../../4-typing-game/typing-game)
- [গেম শুরু করার ইভেন্ট লিসনার](../../../../4-typing-game/typing-game)
- [টাইপিংয়ের ইভেন্ট লিসনার](../../../../4-typing-game/typing-game)

কিন্তু প্রথমে, একটি নতুন ফাইল তৈরি করুন যার নাম **script.js**।

### কনস্ট্যান্ট যোগ করা

আমাদের প্রোগ্রামিংকে সহজ করার জন্য কয়েকটি আইটেমের প্রয়োজন হবে। আবার, এটি একটি রেসিপির মতো, যেখানে আমাদের প্রয়োজন:

- সমস্ত কোটের তালিকা সহ একটি অ্যারে
- বর্তমান কোটের সমস্ত শব্দ সংরক্ষণের জন্য একটি খালি অ্যারে
- খেলোয়াড় বর্তমানে যে শব্দটি টাইপ করছে তার সূচক সংরক্ষণের জায়গা
- খেলোয়াড় স্টার্টে ক্লিক করার সময়

আমরা UI উপাদানগুলোর রেফারেন্সও চাই:

- টেক্সটবক্স (**typed-value**)
- কোট প্রদর্শন (**quote**)
- বার্তা (**message**)

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

✅ আপনার গেমে আরও কোট যোগ করুন

> **NOTE:** আমরা যখনই কোডে উপাদানগুলো পুনরুদ্ধার করতে চাই তখন `document.getElementById` ব্যবহার করতে পারি। যেহেতু আমরা নিয়মিতভাবে এই উপাদানগুলো উল্লেখ করতে যাচ্ছি, আমরা স্ট্রিং লিটারালগুলোর টাইপো এড়াতে কনস্ট্যান্ট ব্যবহার করব। [Vue.js](https://vuejs.org/) বা [React](https://reactjs.org/) এর মতো ফ্রেমওয়ার্কগুলো আপনাকে আপনার কোড কেন্দ্রীভূত করতে আরও ভালোভাবে পরিচালনা করতে সাহায্য করতে পারে।

`const`, `let` এবং `var` ব্যবহার করার বিষয়ে একটি ভিডিও দেখুন।

[![ভেরিয়েবলের ধরন](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "ভেরিয়েবলের ধরন")

> 🎥 উপরের ছবিতে ক্লিক করুন ভেরিয়েবল সম্পর্কে একটি ভিডিও দেখতে।

### শুরু করার লজিক যোগ করা

গেমটি শুরু করতে, খেলোয়াড় স্টার্টে ক্লিক করবে। অবশ্যই, আমরা জানি না তারা কখন স্টার্টে ক্লিক করবে। এখানে একটি [ইভেন্ট লিসনার](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) কার্যকর হবে। একটি ইভেন্ট লিসনার আমাদের কিছু ঘটার জন্য (ইভেন্ট) অপেক্ষা করতে এবং প্রতিক্রিয়ায় কোড কার্যকর করতে দেয়। আমাদের ক্ষেত্রে, আমরা চাই ব্যবহারকারী যখন স্টার্টে ক্লিক করবে তখন কোড কার্যকর হবে।

যখন ব্যবহারকারী **স্টার্ট** ক্লিক করবে, তখন আমাদের একটি কোট নির্বাচন করতে হবে, ইউজার ইন্টারফেস সেটআপ করতে হবে এবং বর্তমান শব্দ এবং টাইমিংয়ের জন্য ট্র্যাকিং সেটআপ করতে হবে। নিচে জাভাস্ক্রিপ্ট রয়েছে যা আপনাকে যোগ করতে হবে; আমরা স্ক্রিপ্ট ব্লকের পরে এটি আলোচনা করব।

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

চলুন কোডটি বিশ্লেষণ করি!

- শব্দ ট্র্যাকিং সেটআপ করা
  - [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) এবং [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) ব্যবহার করে আমরা `quotes` অ্যারে থেকে একটি কোট এলোমেলোভাবে নির্বাচন করি।
  - আমরা `quote` কে `words` এর একটি অ্যারেতে রূপান্তর করি যাতে আমরা খেলোয়াড় বর্তমানে যে শব্দটি টাইপ করছে তা ট্র্যাক করতে পারি।
  - `wordIndex` 0-এ সেট করা হয়, কারণ খেলোয়াড় প্রথম শব্দ থেকে শুরু করবে।
- UI সেটআপ করা
  - `spanWords` এর একটি অ্যারে তৈরি করুন, যা প্রতিটি শব্দকে একটি `span` উপাদানের মধ্যে রাখে।
    - এটি আমাদের প্রদর্শনে শব্দটি হাইলাইট করতে সাহায্য করবে।
  - `join` ব্যবহার করে অ্যারেটিকে একটি স্ট্রিংয়ে রূপান্তর করুন যা আমরা `quoteElement` এর `innerHTML` আপডেট করতে ব্যবহার করতে পারি।
    - এটি খেলোয়াড়ের জন্য কোটটি প্রদর্শন করবে।
  - প্রথম `span` উপাদানের `className` `highlight` এ সেট করুন যাতে এটি হলুদ রঙে হাইলাইট হয়।
  - `messageElement` পরিষ্কার করুন `innerText` কে `''` সেট করে।
- টেক্সটবক্স সেটআপ করা
  - বর্তমান `typedValueElement` এর `value` পরিষ্কার করুন।
  - `typedValueElement` এ `focus` সেট করুন।
- টাইমার শুরু করুন `getTime` কল করে।

### টাইপিং লজিক যোগ করা

যখন খেলোয়াড় টাইপ করে, তখন একটি `input` ইভেন্ট তৈরি হবে। এই ইভেন্ট লিসনারটি নিশ্চিত করবে যে খেলোয়াড় শব্দটি সঠিকভাবে টাইপ করছে এবং গেমের বর্তমান অবস্থা পরিচালনা করবে। **script.js** এ ফিরে যান এবং নিচের কোডটি শেষে যোগ করুন। আমরা পরে এটি বিশ্লেষণ করব।

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

চলুন কোডটি বিশ্লেষণ করি! আমরা বর্তমান শব্দ এবং খেলোয়াড় এখন পর্যন্ত যা টাইপ করেছে তা গ্রহণ করি। তারপর আমরা ওয়াটারফল লজিক ব্যবহার করি, যেখানে আমরা যাচাই করি কোট সম্পন্ন হয়েছে কিনা, শব্দ সম্পন্ন হয়েছে কিনা, শব্দ সঠিক কিনা, অথবা (শেষে), যদি কোনো ত্রুটি থাকে।

- কোট সম্পন্ন হয়েছে, নির্দেশিত `typedValue` `currentWord` এর সমান এবং `wordIndex` `words` এর `length` এর এক কম।
  - `elapsedTime` গণনা করুন `startTime` থেকে বর্তমান সময় বিয়োগ করে।
  - `elapsedTime` কে 1,000 দিয়ে ভাগ করুন মিলিসেকেন্ড থেকে সেকেন্ডে রূপান্তর করতে।
  - একটি সফলতার বার্তা প্রদর্শন করুন।
- শব্দ সম্পন্ন হয়েছে, নির্দেশিত `typedValue` একটি স্পেস দিয়ে শেষ হয়েছে (শব্দের শেষ) এবং `typedValue` `currentWord` এর সমান।
  - পরবর্তী শব্দ টাইপ করার জন্য `typedElement` এর `value` কে `''` সেট করুন।
  - পরবর্তী শব্দে যাওয়ার জন্য `wordIndex` বৃদ্ধি করুন।
  - `quoteElement` এর সমস্ত `childNodes` এর মাধ্যমে লুপ করুন এবং `className` কে `''` সেট করুন ডিফল্ট প্রদর্শনে ফিরে যাওয়ার জন্য।
  - বর্তমান শব্দের `className` `highlight` এ সেট করুন যাতে এটি টাইপ করার জন্য পরবর্তী শব্দ হিসাবে চিহ্নিত হয়।
- শব্দটি বর্তমানে সঠিকভাবে টাইপ করা হয়েছে (কিন্তু সম্পন্ন হয়নি), নির্দেশিত `currentWord` `typedValue` দিয়ে শুরু হয়েছে।
  - `typedValueElement` কে ডিফল্ট প্রদর্শন নিশ্চিত করুন `className` পরিষ্কার করে।
- যদি আমরা এতদূর পৌঁছাই, তাহলে একটি ত্রুটি রয়েছে।
  - `typedValueElement` এর `className` `error` এ সেট করুন।

## আপনার অ্যাপ্লিকেশন পরীক্ষা করুন

আপনি শেষ পর্যন্ত পৌঁছেছেন! শেষ ধাপটি হল নিশ্চিত করা যে আমাদের অ্যাপ্লিকেশন কাজ করছে। এটি পরীক্ষা করুন! যদি কোনো ত্রুটি থাকে, চিন্তা করবেন না; **সব ডেভেলপারদেরই ত্রুটি হয়।** বার্তাগুলো পরীক্ষা করুন এবং প্রয়োজন অনুযায়ী ডিবাগ করুন।

**স্টার্ট** এ ক্লিক করুন এবং টাইপ করা শুরু করুন! এটি কিছুটা এরকম দেখতে হবে:

![গেমটি চলমান অবস্থার অ্যানিমেশন](../../../../4-typing-game/images/demo.gif)

---

## 🚀 চ্যালেঞ্জ

আরও কার্যকারিতা যোগ করুন

- সম্পন্ন হলে `input` ইভেন্ট লিসনার নিষ্ক্রিয় করুন এবং বাটন ক্লিক করলে পুনরায় সক্রিয় করুন।
- খেলোয়াড় কোট সম্পন্ন করলে টেক্সটবক্স নিষ্ক্রিয় করুন।
- সফলতার বার্তা সহ একটি মডাল ডায়ালগ বক্স প্রদর্শন করুন।
- [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage) ব্যবহার করে উচ্চ স্কোর সংরক্ষণ করুন।
## লেকচার-পরবর্তী কুইজ

[লেকচার-পরবর্তী কুইজ](https://ff-quizzes.netlify.app/web/quiz/22)

## পর্যালোচনা ও স্ব-অধ্যয়ন

[ওয়েব ব্রাউজারের মাধ্যমে ডেভেলপারদের জন্য উপলব্ধ সমস্ত ইভেন্ট](https://developer.mozilla.org/docs/Web/Events) সম্পর্কে পড়ুন এবং প্রতিটি ইভেন্ট কোন পরিস্থিতিতে ব্যবহার করবেন তা বিবেচনা করুন।

## অ্যাসাইনমেন্ট

[একটি নতুন কীবোর্ড গেম তৈরি করুন](assignment.md)

---

**অস্বীকৃতি**:  
এই নথিটি AI অনুবাদ পরিষেবা [Co-op Translator](https://github.com/Azure/co-op-translator) ব্যবহার করে অনুবাদ করা হয়েছে। আমরা যথাসম্ভব সঠিকতার জন্য চেষ্টা করি, তবে অনুগ্রহ করে মনে রাখবেন যে স্বয়ংক্রিয় অনুবাদে ত্রুটি বা অসঙ্গতি থাকতে পারে। মূল ভাষায় থাকা নথিটিকে প্রামাণিক উৎস হিসেবে বিবেচনা করা উচিত। গুরুত্বপূর্ণ তথ্যের জন্য, পেশাদার মানব অনুবাদ সুপারিশ করা হয়। এই অনুবাদ ব্যবহারের ফলে কোনো ভুল বোঝাবুঝি বা ভুল ব্যাখ্যা হলে আমরা দায়বদ্ধ থাকব না।