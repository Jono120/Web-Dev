<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "979cfcce2413a87d9e4c67eb79234bc3",
  "translation_date": "2025-08-29T14:31:27+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "fa"
}
-->
# ساخت یک بازی فضایی قسمت اول: مقدمه

![ویدیو](../../../../6-space-game/images/pewpew.gif)

## آزمون پیش از درس

[آزمون پیش از درس](https://ff-quizzes.netlify.app/web/quiz/29)

### ارث‌بری و ترکیب در توسعه بازی

در درس‌های قبلی، نیازی نبود که زیاد نگران معماری طراحی اپلیکیشن‌هایی که ساختید باشید، زیرا پروژه‌ها بسیار کوچک بودند. اما وقتی اپلیکیشن‌های شما بزرگ‌تر و پیچیده‌تر می‌شوند، تصمیمات معماری اهمیت بیشتری پیدا می‌کنند. دو رویکرد اصلی برای ساخت اپلیکیشن‌های بزرگ‌تر در جاوااسکریپت وجود دارد: *ترکیب* یا *ارث‌بری*. هر دو مزایا و معایب خود را دارند، اما بیایید آن‌ها را در زمینه یک بازی توضیح دهیم.

✅ یکی از معروف‌ترین کتاب‌های برنامه‌نویسی که تاکنون نوشته شده است، مربوط به [الگوهای طراحی](https://en.wikipedia.org/wiki/Design_Patterns) است.

در یک بازی، شما `اشیاء بازی` دارید که اشیائی هستند که روی صفحه نمایش وجود دارند. این بدان معناست که آن‌ها یک مکان در سیستم مختصات کارتزین دارند که با داشتن مختصات `x` و `y` مشخص می‌شود. وقتی یک بازی را توسعه می‌دهید، متوجه خواهید شد که تمام اشیاء بازی شما یک ویژگی استاندارد دارند که در هر بازی مشترک است، یعنی عناصری که:

- **مبتنی بر مکان** هستند. بیشتر، اگر نه همه، عناصر بازی مبتنی بر مکان هستند. این بدان معناست که آن‌ها یک مکان دارند، یعنی `x` و `y`.
- **قابل حرکت** هستند. این‌ها اشیائی هستند که می‌توانند به مکان جدیدی حرکت کنند. معمولاً این‌ها یک قهرمان، یک هیولا یا یک شخصیت غیرقابل بازی (NPC) هستند، اما نه به عنوان مثال، یک شیء ثابت مانند یک درخت.
- **خود تخریب‌کننده** هستند. این اشیاء فقط برای مدت زمان مشخصی وجود دارند و سپس خودشان را برای حذف آماده می‌کنند. معمولاً این با یک بولین `dead` یا `destroyed` نشان داده می‌شود که به موتور بازی اعلام می‌کند که این شیء دیگر نباید نمایش داده شود.
- **دارای زمان خنک شدن** هستند. 'زمان خنک شدن' یک ویژگی معمول در اشیاء کوتاه‌مدت است. یک مثال معمول یک قطعه متن یا اثر گرافیکی مانند یک انفجار است که فقط باید برای چند میلی‌ثانیه دیده شود.

✅ به یک بازی مانند پک‌من فکر کنید. آیا می‌توانید چهار نوع شیء ذکر شده در بالا را در این بازی شناسایی کنید؟

### بیان رفتار

تمام مواردی که در بالا توضیح داده شد، رفتارهایی هستند که اشیاء بازی می‌توانند داشته باشند. پس چگونه آن‌ها را کدنویسی کنیم؟ می‌توانیم این رفتارها را به عنوان متدهایی مرتبط با کلاس‌ها یا اشیاء بیان کنیم.

**کلاس‌ها**

ایده این است که از `کلاس‌ها` همراه با `ارث‌بری` استفاده کنیم تا یک رفتار خاص را به یک کلاس اضافه کنیم.

✅ ارث‌بری یک مفهوم مهم برای درک است. اطلاعات بیشتر را در [مقاله MDN درباره ارث‌بری](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) بخوانید.

به صورت کدنویسی، یک شیء بازی معمولاً می‌تواند به این شکل باشد:

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

✅ چند دقیقه وقت بگذارید و یک قهرمان پک‌من (مثلاً اینکی، پینکی یا بلینکی) را تصور کنید و ببینید چگونه می‌توان آن را در جاوااسکریپت نوشت.

**ترکیب**

یک روش دیگر برای مدیریت ارث‌بری اشیاء استفاده از *ترکیب* است. در این روش، اشیاء رفتار خود را به این شکل بیان می‌کنند:

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

**کدام الگو را باید استفاده کنم؟**

انتخاب الگو به شما بستگی دارد. جاوااسکریپت از هر دو این پارادایم‌ها پشتیبانی می‌کند.

--

یک الگوی دیگر که در توسعه بازی رایج است، به مشکل مدیریت تجربه کاربری و عملکرد بازی می‌پردازد.

## الگوی انتشار/اشتراک

✅ Pub/Sub مخفف 'انتشار-اشتراک' است.

این الگو به این ایده می‌پردازد که بخش‌های مختلف اپلیکیشن شما نباید درباره یکدیگر بدانند. چرا؟ این کار باعث می‌شود که به طور کلی راحت‌تر ببینید چه اتفاقی در حال رخ دادن است اگر بخش‌های مختلف جدا باشند. همچنین تغییر رفتار در صورت نیاز آسان‌تر می‌شود. چگونه این کار را انجام دهیم؟ با ایجاد برخی مفاهیم:

- **پیام**: یک پیام معمولاً یک رشته متنی است که همراه با یک بار داده اختیاری (یک قطعه داده که توضیح می‌دهد پیام درباره چیست) می‌آید. یک پیام معمولی در یک بازی می‌تواند `KEY_PRESSED_ENTER` باشد.
- **ناشر**: این عنصر یک پیام را *منتشر* می‌کند و آن را به تمام مشترکین ارسال می‌کند.
- **مشترک**: این عنصر به پیام‌های خاص *گوش می‌دهد* و به عنوان نتیجه دریافت این پیام، کاری انجام می‌دهد، مانند شلیک یک لیزر.

پیاده‌سازی این الگو بسیار کوچک است اما یک الگوی بسیار قدرتمند است. در اینجا نحوه پیاده‌سازی آن آمده است:

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

برای استفاده از کد بالا می‌توانیم یک پیاده‌سازی بسیار کوچک ایجاد کنیم:

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

در بالا، یک رویداد صفحه کلید، `ArrowLeft` را متصل می‌کنیم و پیام `HERO_MOVE_LEFT` را ارسال می‌کنیم. به آن پیام گوش می‌دهیم و به عنوان نتیجه، `hero` را حرکت می‌دهیم. قدرت این الگو در این است که شنونده رویداد و قهرمان هیچ اطلاعی از یکدیگر ندارند. شما می‌توانید `ArrowLeft` را به کلید `A` بازنگری کنید. علاوه بر این، امکان انجام کاری کاملاً متفاوت روی `ArrowLeft` با ایجاد چند تغییر در تابع `on` رویداد‌Emitter وجود دارد:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

وقتی بازی شما بزرگ‌تر و پیچیده‌تر می‌شود، این الگو همچنان در پیچیدگی ثابت می‌ماند و کد شما تمیز باقی می‌ماند. واقعاً توصیه می‌شود که این الگو را بپذیرید.

---

## 🚀 چالش

به این فکر کنید که چگونه الگوی انتشار-اشتراک می‌تواند یک بازی را بهبود بخشد. کدام بخش‌ها باید رویدادها را منتشر کنند و بازی چگونه باید به آن‌ها واکنش نشان دهد؟ اکنون فرصت شماست که خلاق باشید و به یک بازی جدید فکر کنید و اینکه بخش‌های آن چگونه ممکن است رفتار کنند.

## آزمون پس از درس

[آزمون پس از درس](https://ff-quizzes.netlify.app/web/quiz/30)

## مرور و مطالعه شخصی

اطلاعات بیشتری درباره انتشار/اشتراک با [مطالعه درباره آن](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon) کسب کنید.

## تکلیف

[یک بازی طراحی کنید](assignment.md)

---

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما برای دقت تلاش می‌کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نادرستی‌هایی باشند. سند اصلی به زبان اصلی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما هیچ مسئولیتی در قبال سوءتفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.