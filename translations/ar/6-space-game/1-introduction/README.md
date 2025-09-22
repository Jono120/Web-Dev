<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "979cfcce2413a87d9e4c67eb79234bc3",
  "translation_date": "2025-08-28T15:03:44+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "ar"
}
-->
# بناء لعبة فضاء الجزء الأول: المقدمة

![video](../../../../6-space-game/images/pewpew.gif)

## اختبار ما قبل المحاضرة

[اختبار ما قبل المحاضرة](https://ff-quizzes.netlify.app/web/quiz/29)

### الوراثة والتركيب في تطوير الألعاب

في الدروس السابقة، لم يكن هناك حاجة كبيرة للقلق بشأن تصميم هيكل التطبيقات التي قمت ببنائها، حيث كانت المشاريع صغيرة النطاق. ومع ذلك، عندما تنمو تطبيقاتك في الحجم والنطاق، تصبح القرارات المعمارية أكثر أهمية. هناك نهجان رئيسيان لإنشاء تطبيقات أكبر في JavaScript: *التركيب* أو *الوراثة*. لكل منهما إيجابيات وسلبيات، ولكن دعونا نشرحها في سياق لعبة.

✅ أحد أشهر الكتب البرمجية على الإطلاق يتعلق بـ [أنماط التصميم](https://en.wikipedia.org/wiki/Design_Patterns).

في اللعبة، لديك `كائنات اللعبة` وهي كائنات تظهر على الشاشة. هذا يعني أنها تمتلك موقعًا على نظام الإحداثيات الديكارتي، يتميز بوجود إحداثيات `x` و `y`. أثناء تطوير اللعبة، ستلاحظ أن جميع كائنات اللعبة لديها خصائص قياسية، مشتركة في كل لعبة تقوم بإنشائها، وهي عناصر:

- **تعتمد على الموقع** معظم، إن لم يكن كل، عناصر اللعبة تعتمد على الموقع. هذا يعني أنها تمتلك موقعًا، إحداثيات `x` و `y`.
- **قابلة للحركة** هذه كائنات يمكنها الانتقال إلى موقع جديد. عادةً ما تكون هذه الكائنات بطلًا، وحشًا أو شخصية غير لاعبة (NPC)، ولكن ليس على سبيل المثال، كائن ثابت مثل شجرة.
- **تدمير ذاتي** هذه الكائنات موجودة فقط لفترة زمنية محددة قبل أن يتم إعدادها للحذف. عادةً ما يتم تمثيل ذلك بـ `dead` أو `destroyed` وهي قيمة منطقية تشير إلى محرك اللعبة بأن هذا الكائن لم يعد يجب عرضه.
- **فترة التهدئة** "فترة التهدئة" هي خاصية نموذجية بين الكائنات قصيرة العمر. مثال نموذجي هو قطعة نص أو تأثير رسومي مثل انفجار يجب أن يُرى فقط لبضع ميلي ثانية.

✅ فكر في لعبة مثل Pac-Man. هل يمكنك تحديد الأنواع الأربعة للكائنات المذكورة أعلاه في هذه اللعبة؟

### التعبير عن السلوك

كل ما وصفناه أعلاه هو سلوك يمكن أن تمتلكه كائنات اللعبة. إذًا كيف يمكننا ترميز ذلك؟ يمكننا التعبير عن هذا السلوك كطرق مرتبطة إما بـ `classes` أو `objects`.

**الفئات (Classes)**

الفكرة هي استخدام `الفئات` بالتزامن مع `الوراثة` لتحقيق إضافة سلوك معين إلى الفئة.

✅ الوراثة مفهوم مهم لفهمه. تعرف على المزيد من خلال [مقال MDN عن الوراثة](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain).

معبرًا عنه عبر الكود، يمكن أن يبدو كائن اللعبة عادةً هكذا:

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

✅ خذ بضع دقائق لإعادة تصور بطل Pac-Man (مثل Inky، Pinky أو Blinky) وكيف يمكن كتابته في JavaScript.

**التركيب (Composition)**

طريقة مختلفة للتعامل مع وراثة الكائنات هي باستخدام *التركيب*. ثم تعبر الكائنات عن سلوكها بهذا الشكل:

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

**أي نمط يجب أن أستخدم؟**

الأمر متروك لك لتحديد النمط الذي تختاره. JavaScript تدعم كلا النهجين.

--

نمط آخر شائع في تطوير الألعاب يعالج مشكلة التعامل مع تجربة المستخدم وأداء اللعبة.

## نمط النشر/الاشتراك (Pub/sub)

✅ Pub/Sub تعني "النشر-الاشتراك"

هذا النمط يعالج فكرة أن الأجزاء المختلفة من تطبيقك لا يجب أن تعرف عن بعضها البعض. لماذا؟ لأنه يجعل من السهل رؤية ما يجري بشكل عام إذا كانت الأجزاء منفصلة. كما يجعل من السهل تغيير السلوك فجأة إذا لزم الأمر. كيف نحقق ذلك؟ نقوم بذلك من خلال إنشاء بعض المفاهيم:

- **الرسالة**: الرسالة عادةً ما تكون سلسلة نصية مصحوبة ببيانات اختيارية (قطعة بيانات توضح ما تدور حوله الرسالة). رسالة نموذجية في اللعبة يمكن أن تكون `KEY_PRESSED_ENTER`.
- **الناشر**: هذا العنصر *ينشر* رسالة ويرسلها إلى جميع المشتركين.
- **المشترك**: هذا العنصر *يستمع* إلى رسائل محددة وينفذ مهمة معينة نتيجة تلقي هذه الرسالة، مثل إطلاق الليزر.

التنفيذ صغير الحجم ولكنه نمط قوي جدًا. إليك كيف يمكن تنفيذه:

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

لاستخدام الكود أعلاه، يمكننا إنشاء تنفيذ صغير جدًا:

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

في المثال أعلاه، قمنا بربط حدث لوحة المفاتيح، `ArrowLeft`، وأرسلنا رسالة `HERO_MOVE_LEFT`. نستمع إلى تلك الرسالة ونحرك `hero` كنتيجة لذلك. قوة هذا النمط تكمن في أن مستمع الحدث والبطل لا يعرفان عن بعضهما البعض. يمكنك إعادة تعيين `ArrowLeft` إلى مفتاح `A`. بالإضافة إلى ذلك، سيكون من الممكن القيام بشيء مختلف تمامًا عند الضغط على `ArrowLeft` من خلال إجراء بعض التعديلات على وظيفة `on` الخاصة بـ `eventEmitter`:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

مع ازدياد تعقيد الأمور عندما تنمو لعبتك، يظل هذا النمط ثابتًا في التعقيد ويبقى الكود نظيفًا. من الموصى بشدة تبني هذا النمط.

---

## 🚀 التحدي

فكر في كيفية تحسين نمط النشر-الاشتراك للعبة. ما هي الأجزاء التي يجب أن تصدر أحداثًا، وكيف يجب أن تتفاعل اللعبة معها؟ الآن لديك فرصة للإبداع، فكر في لعبة جديدة وكيف يمكن أن تتصرف أجزاؤها.

## اختبار ما بعد المحاضرة

[اختبار ما بعد المحاضرة](https://ff-quizzes.netlify.app/web/quiz/30)

## المراجعة والدراسة الذاتية

تعرف على المزيد حول النشر-الاشتراك من خلال [قراءة المزيد عنه](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon).

## الواجب

[تصميم لعبة](assignment.md)

---

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الرسمي. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.