<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "979cfcce2413a87d9e4c67eb79234bc3",
  "translation_date": "2025-08-28T23:00:11+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "bn"
}
-->
# স্পেস গেম তৈরি করুন পার্ট ১: পরিচিতি

![video](../../../../6-space-game/images/pewpew.gif)

## প্রাক-লেকচার কুইজ

[প্রাক-লেকচার কুইজ](https://ff-quizzes.netlify.app/web/quiz/29)

### গেম ডেভেলপমেন্টে ইনহেরিটেন্স এবং কম্পোজিশন

আগের পাঠগুলোতে, আপনি যে অ্যাপ তৈরি করেছেন তার ডিজাইন আর্কিটেকচার নিয়ে খুব বেশি চিন্তা করার দরকার পড়েনি, কারণ প্রকল্পগুলো খুব ছোট পরিসরের ছিল। তবে, যখন আপনার অ্যাপ্লিকেশন আকার এবং পরিসরে বৃদ্ধি পায়, তখন আর্কিটেকচারাল সিদ্ধান্তগুলো বড় বিষয় হয়ে দাঁড়ায়। জাভাস্ক্রিপ্টে বড় অ্যাপ্লিকেশন তৈরি করার দুটি প্রধান পদ্ধতি রয়েছে: *কম্পোজিশন* বা *ইনহেরিটেন্স*। উভয়েরই সুবিধা এবং অসুবিধা রয়েছে, তবে আসুন এগুলো একটি গেমের প্রেক্ষাপটে ব্যাখ্যা করি।

✅ প্রোগ্রামিং সম্পর্কিত সবচেয়ে বিখ্যাত বইগুলোর একটি [ডিজাইন প্যাটার্নস](https://en.wikipedia.org/wiki/Design_Patterns) নিয়ে।

একটি গেমে আপনার কাছে `গেম অবজেক্ট` থাকে, যা স্ক্রিনে উপস্থিত থাকে। এর মানে হলো এগুলোর একটি অবস্থান থাকে কার্টেসিয়ান কোঅর্ডিনেট সিস্টেমে, যা `x` এবং `y` কোঅর্ডিনেট দ্বারা চিহ্নিত হয়। যখন আপনি একটি গেম তৈরি করবেন, আপনি লক্ষ্য করবেন যে আপনার সমস্ত গেম অবজেক্টের একটি সাধারণ বৈশিষ্ট্য থাকে, যা প্রতিটি গেমের জন্য সাধারণ, যেমন:

- **অবস্থান-ভিত্তিক** বেশিরভাগ, যদি না সব, গেম উপাদান অবস্থান-ভিত্তিক হয়। এর মানে হলো এগুলোর একটি অবস্থান থাকে, একটি `x` এবং `y`।
- **চলনযোগ্য** এগুলো এমন অবজেক্ট যা নতুন অবস্থানে যেতে পারে। সাধারণত এটি একটি হিরো, একটি মনস্টার বা একটি NPC (নন প্লেয়ার ক্যারেক্টার), তবে উদাহরণস্বরূপ, একটি স্থির অবজেক্ট যেমন একটি গাছ নয়।
- **স্ব-ধ্বংসকারী** এই অবজেক্টগুলো শুধুমাত্র একটি নির্দিষ্ট সময়ের জন্য বিদ্যমান থাকে, তারপর তারা মুছে ফেলার জন্য প্রস্তুত হয়। সাধারণত এটি একটি `dead` বা `destroyed` বুলিয়ান দ্বারা উপস্থাপিত হয় যা গেম ইঞ্জিনকে সংকেত দেয় যে এই অবজেক্টটি আর রেন্ডার করা উচিত নয়।
- **কুল-ডাউন** 'কুল-ডাউন' একটি সাধারণ বৈশিষ্ট্য যা স্বল্পস্থায়ী অবজেক্টগুলোর মধ্যে দেখা যায়। একটি সাধারণ উদাহরণ হলো একটি টেক্সট বা গ্রাফিকাল ইফেক্ট যেমন একটি বিস্ফোরণ যা শুধুমাত্র কয়েক মিলিসেকেন্ডের জন্য দেখা উচিত।

✅ একটি গেম যেমন Pac-Man নিয়ে চিন্তা করুন। আপনি কি এই গেমে উপরের চারটি অবজেক্ট টাইপ চিহ্নিত করতে পারেন?

### আচরণ প্রকাশ করা

উপরে আমরা যা বর্ণনা করেছি তা হলো গেম অবজেক্টগুলোর আচরণ। তাহলে আমরা এগুলো কীভাবে এনকোড করব? আমরা এই আচরণগুলো ক্লাস বা অবজেক্টের সাথে সম্পর্কিত মেথড হিসেবে প্রকাশ করতে পারি।

**ক্লাস**

ধারণাটি হলো `ক্লাস` এবং `ইনহেরিটেন্স` ব্যবহার করে একটি ক্লাসে নির্দিষ্ট আচরণ যোগ করা।

✅ ইনহেরিটেন্স একটি গুরুত্বপূর্ণ ধারণা। [MDN-এর ইনহেরিটেন্স সম্পর্কিত নিবন্ধ](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) থেকে আরও জানুন।

কোডের মাধ্যমে প্রকাশ করলে, একটি গেম অবজেক্ট সাধারণত এরকম দেখতে পারে:

```javascript

//set up the class GameObject
class GameObject {
  constructor(x, y, type) {
    this.x = x;
    this.y = y;
    this.type = type;
  }
}

//this class will extend the GameObject's inherent class properties
class Movable extends GameObject {
  constructor(x,y, type) {
    super(x,y, type)
  }

//this movable object can be moved on the screen
  moveTo(x, y) {
    this.x = x;
    this.y = y;
  }
}

//this is a specific class that extends the Movable class, so it can take advantage of all the properties that it inherits
class Hero extends Movable {
  constructor(x,y) {
    super(x,y, 'Hero')
  }
}

//this class, on the other hand, only inherits the GameObject properties
class Tree extends GameObject {
  constructor(x,y) {
    super(x,y, 'Tree')
  }
}

//a hero can move...
const hero = new Hero();
hero.moveTo(5,5);

//but a tree cannot
const tree = new Tree();
```

✅ কয়েক মিনিট সময় নিয়ে Pac-Man এর একটি হিরো (উদাহরণস্বরূপ, Inky, Pinky বা Blinky) কল্পনা করুন এবং এটি কীভাবে জাভাস্ক্রিপ্টে লেখা হবে তা ভাবুন।

**কম্পোজিশন**

অবজেক্ট ইনহেরিটেন্স পরিচালনার একটি ভিন্ন উপায় হলো *কম্পোজিশন* ব্যবহার করা। তখন অবজেক্টগুলো তাদের আচরণ এভাবে প্রকাশ করে:

```javascript
//create a constant gameObject
const gameObject = {
  x: 0,
  y: 0,
  type: ''
};

//...and a constant movable
const movable = {
  moveTo(x, y) {
    this.x = x;
    this.y = y;
  }
}
//then the constant movableObject is composed of the gameObject and movable constants
const movableObject = {...gameObject, ...movable};

//then create a function to create a new Hero who inherits the movableObject properties
function createHero(x, y) {
  return {
    ...movableObject,
    x,
    y,
    type: 'Hero'
  }
}
//...and a static object that inherits only the gameObject properties
function createStatic(x, y, type) {
  return {
    ...gameObject
    x,
    y,
    type
  }
}
//create the hero and move it
const hero = createHero(10,10);
hero.moveTo(5,5);
//and create a static tree which only stands around
const tree = createStatic(0,0, 'Tree'); 
```

**কোন প্যাটার্নটি ব্যবহার করব?**

আপনার উপর নির্ভর করে আপনি কোন প্যাটার্নটি বেছে নেবেন। জাভাস্ক্রিপ্ট উভয় পদ্ধতিই সমর্থন করে।

--

গেম ডেভেলপমেন্টে আরেকটি সাধারণ প্যাটার্ন হলো গেমের ব্যবহারকারীর অভিজ্ঞতা এবং পারফরম্যান্স পরিচালনা করার সমস্যা সমাধান করা।

## পাব/সাব প্যাটার্ন

✅ Pub/Sub এর অর্থ 'publish-subscribe'

এই প্যাটার্নটি ধারণা দেয় যে আপনার অ্যাপ্লিকেশনের বিভিন্ন অংশ একে অপরের সম্পর্কে জানবে না। কেন? এটি সাধারণভাবে কী ঘটছে তা বোঝা অনেক সহজ করে তোলে যদি বিভিন্ন অংশ আলাদা থাকে। এটি আচরণ হঠাৎ পরিবর্তন করাও সহজ করে তোলে যদি প্রয়োজন হয়। আমরা এটি কীভাবে অর্জন করি? আমরা কিছু ধারণা প্রতিষ্ঠা করে এটি করি:

- **মেসেজ**: একটি মেসেজ সাধারণত একটি টেক্সট স্ট্রিং হয় যা একটি ঐচ্ছিক পে-লোড (একটি ডেটা যা মেসেজটি সম্পর্কে স্পষ্ট করে) সহ থাকে। একটি গেমে একটি সাধারণ মেসেজ হতে পারে `KEY_PRESSED_ENTER`।
- **পাবলিশার**: এই উপাদানটি একটি মেসেজ *পাবলিশ* করে এবং এটি সমস্ত সাবস্ক্রাইবারদের কাছে পাঠায়।
- **সাবস্ক্রাইবার**: এই উপাদানটি নির্দিষ্ট মেসেজগুলো *শোনে* এবং এই মেসেজটি পাওয়ার ফলস্বরূপ কিছু কাজ সম্পন্ন করে, যেমন একটি লেজার চালানো।

এর বাস্তবায়ন আকারে খুব ছোট হলেও এটি একটি অত্যন্ত শক্তিশালী প্যাটার্ন। এটি কীভাবে বাস্তবায়িত হতে পারে তা এখানে দেখুন:

```javascript
//set up an EventEmitter class that contains listeners
class EventEmitter {
  constructor() {
    this.listeners = {};
  }
//when a message is received, let the listener to handle its payload
  on(message, listener) {
    if (!this.listeners[message]) {
      this.listeners[message] = [];
    }
    this.listeners[message].push(listener);
  }
//when a message is sent, send it to a listener with some payload
  emit(message, payload = null) {
    if (this.listeners[message]) {
      this.listeners[message].forEach(l => l(message, payload))
    }
  }
}

```

উপরে উল্লেখিত কোড ব্যবহার করে আমরা একটি খুব ছোট বাস্তবায়ন তৈরি করতে পারি:

```javascript
//set up a message structure
const Messages = {
  HERO_MOVE_LEFT: 'HERO_MOVE_LEFT'
};
//invoke the eventEmitter you set up above
const eventEmitter = new EventEmitter();
//set up a hero
const hero = createHero(0,0);
//let the eventEmitter know to watch for messages pertaining to the hero moving left, and act on it
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});

//set up the window to listen for the keyup event, specifically if the left arrow is hit, emit a message to move the hero left
window.addEventListener('keyup', (evt) => {
  if (evt.key === 'ArrowLeft') {
    eventEmitter.emit(Messages.HERO_MOVE_LEFT)
  }
});
```

উপরে আমরা একটি কিবোর্ড ইভেন্ট, `ArrowLeft` সংযুক্ত করেছি এবং `HERO_MOVE_LEFT` মেসেজ পাঠিয়েছি। আমরা সেই মেসেজটি শুনি এবং ফলস্বরূপ `hero` কে সরাই। এই প্যাটার্নের শক্তি হলো ইভেন্ট লিসনার এবং হিরো একে অপরের সম্পর্কে জানে না। আপনি `ArrowLeft` কে `A` কীতে পুনরায় ম্যাপ করতে পারেন। এছাড়াও, এটি সম্ভব হবে `ArrowLeft` এ সম্পূর্ণ ভিন্ন কিছু করার জন্য ইভেন্টEmitter এর `on` ফাংশনে কয়েকটি সম্পাদনা করে:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

যখন আপনার গেম বড় হয় এবং জটিল হয়ে ওঠে, এই প্যাটার্নটি জটিলতায় একই থাকে এবং আপনার কোড পরিষ্কার থাকে। এই প্যাটার্নটি গ্রহণ করার জন্য এটি সত্যিই সুপারিশ করা হয়।

---

## 🚀 চ্যালেঞ্জ

ভাবুন কীভাবে পাব-সাব প্যাটার্ন একটি গেমকে উন্নত করতে পারে। কোন অংশগুলো ইভেন্ট পাঠাবে, এবং গেমটি কীভাবে সেগুলোর প্রতিক্রিয়া জানাবে? এখন আপনার সৃজনশীল হওয়ার সুযোগ, একটি নতুন গেম নিয়ে চিন্তা করুন এবং এর অংশগুলো কীভাবে আচরণ করতে পারে তা ভাবুন।

## পোস্ট-লেকচার কুইজ

[পোস্ট-লেকচার কুইজ](https://ff-quizzes.netlify.app/web/quiz/30)

## পর্যালোচনা এবং স্ব-অধ্যয়ন

পাব/সাব সম্পর্কে আরও জানুন [এটি পড়ে](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon)।

## অ্যাসাইনমেন্ট

[একটি গেমের মক আপ তৈরি করুন](assignment.md)

---

**দাবিত্যাগ**:  
এই নথিটি AI অনুবাদ পরিষেবা [Co-op Translator](https://github.com/Azure/co-op-translator) ব্যবহার করে অনুবাদ করা হয়েছে। আমরা যথাসাধ্য সঠিকতা নিশ্চিত করার চেষ্টা করি, তবে অনুগ্রহ করে মনে রাখবেন যে স্বয়ংক্রিয় অনুবাদে ত্রুটি বা অসঙ্গতি থাকতে পারে। মূল ভাষায় থাকা নথিটিকে প্রামাণিক উৎস হিসেবে বিবেচনা করা উচিত। গুরুত্বপূর্ণ তথ্যের জন্য, পেশাদার মানব অনুবাদ সুপারিশ করা হয়। এই অনুবাদ ব্যবহারের ফলে কোনো ভুল বোঝাবুঝি বা ভুল ব্যাখ্যা হলে আমরা তার জন্য দায়ী থাকব না।