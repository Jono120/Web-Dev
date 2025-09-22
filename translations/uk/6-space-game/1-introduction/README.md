<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "979cfcce2413a87d9e4c67eb79234bc3",
  "translation_date": "2025-08-28T18:15:44+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "uk"
}
-->
# Створення космічної гри Частина 1: Вступ

![video](../../../../6-space-game/images/pewpew.gif)

## Тест перед лекцією

[Тест перед лекцією](https://ff-quizzes.netlify.app/web/quiz/29)

### Наслідування та композиція у розробці ігор

У попередніх уроках не було великої потреби турбуватися про архітектуру додатків, які ви створювали, оскільки проєкти були невеликими за масштабом. Однак, коли ваші додатки зростають у розмірах і складності, архітектурні рішення стають важливішими. Існує два основних підходи до створення великих додатків у JavaScript: *композиція* або *наслідування*. У кожного з них є свої переваги та недоліки, але давайте розглянемо їх у контексті гри.

✅ Одна з найвідоміших книг про програмування присвячена [шаблонам проєктування](https://en.wikipedia.org/wiki/Design_Patterns).

У грі є `ігрові об'єкти`, які є об'єктами, що існують на екрані. Це означає, що вони мають розташування в декартовій системі координат, яке характеризується наявністю координат `x` та `y`. У процесі розробки гри ви помітите, що всі ваші ігрові об'єкти мають стандартні властивості, спільні для кожної гри, яку ви створюєте, а саме елементи, які є:

- **залежними від розташування** Більшість, якщо не всі, ігрові елементи залежать від розташування. Це означає, що вони мають координати `x` та `y`.
- **рухомими** Це об'єкти, які можуть переміщатися в нове місце. Зазвичай це герой, монстр або NPC (персонаж, яким не керує гравець), але не, наприклад, статичний об'єкт, як дерево.
- **самознищуваними** Ці об'єкти існують лише протягом певного періоду часу, після чого вони готуються до видалення. Зазвичай це представлено булевою змінною `dead` або `destroyed`, яка сигналізує ігровому двигуну, що цей об'єкт більше не потрібно відображати.
- **з затримкою** 'Затримка' — це типова властивість короткотривалих об'єктів. Типовий приклад — це текст або графічний ефект, як вибух, який має бути видимим лише кілька мілісекунд.

✅ Подумайте про гру, як-от Pac-Man. Чи можете ви визначити чотири типи об'єктів, описаних вище, у цій грі?

### Вираження поведінки

Все, що ми описали вище, — це поведінка, яку можуть мати ігрові об'єкти. Як же її закодувати? Ми можемо виразити цю поведінку як методи, пов'язані з класами або об'єктами.

**Класи**

Ідея полягає в тому, щоб використовувати `класи` у поєднанні з `наслідуванням`, щоб додати певну поведінку до класу.

✅ Наслідування — це важливе поняття для розуміння. Дізнайтеся більше у [статті MDN про наслідування](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain).

У коді ігровий об'єкт зазвичай може виглядати так:

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

✅ Приділіть кілька хвилин, щоб уявити героя Pac-Man (наприклад, Inky, Pinky або Blinky) і як його можна було б написати на JavaScript.

**Композиція**

Інший спосіб обробки наслідування об'єктів — використання *композиції*. Тоді об'єкти виражають свою поведінку так:

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

**Який шаблон обрати?**

Вибір залежить від вас. JavaScript підтримує обидві ці парадигми.

--

Ще один шаблон, поширений у розробці ігор, вирішує проблему управління користувацьким досвідом гри та її продуктивністю.

## Шаблон Pub/sub

✅ Pub/Sub означає 'publish-subscribe' (публікація-підписка)

Цей шаблон вирішує ідею, що різні частини вашого додатка не повинні знати одна про одну. Чому це важливо? Це значно спрощує розуміння загальної картини, якщо різні частини відокремлені. Це також полегшує раптову зміну поведінки, якщо це необхідно. Як це реалізувати? Ми робимо це, встановлюючи кілька концепцій:

- **повідомлення**: Повідомлення зазвичай є текстовим рядком, доповненим необов'язковим корисним навантаженням (частиною даних, яка уточнює, про що йдеться у повідомленні). Типове повідомлення в грі може бути `KEY_PRESSED_ENTER`.
- **видавець**: Цей елемент *публікує* повідомлення та надсилає його всім підписникам.
- **підписник**: Цей елемент *слухає* конкретні повідомлення та виконує певне завдання в результаті отримання цього повідомлення, наприклад, стріляє лазером.

Реалізація досить компактна, але це дуже потужний шаблон. Ось як його можна реалізувати:

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

Щоб використати наведений вище код, ми можемо створити дуже маленьку реалізацію:

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

У наведеному вище прикладі ми підключаємо подію клавіатури `ArrowLeft` і надсилаємо повідомлення `HERO_MOVE_LEFT`. Ми слухаємо це повідомлення та переміщуємо `hero` як результат. Сила цього шаблону полягає в тому, що обробник подій і герой не знають один про одного. Ви можете переназначити `ArrowLeft` на клавішу `A`. Крім того, можна зробити щось зовсім інше на `ArrowLeft`, внісши кілька змін до функції `on` об'єкта eventEmitter:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

Коли ваша гра стає складнішою, цей шаблон залишається незмінним у своїй складності, а ваш код залишається чистим. Дуже рекомендується використовувати цей шаблон.

---

## 🚀 Виклик

Подумайте, як шаблон pub-sub може покращити гру. Які частини повинні надсилати події, і як гра повинна на них реагувати? Зараз у вас є шанс проявити творчість, придумуючи нову гру та те, як її частини можуть поводитися.

## Тест після лекції

[Тест після лекції](https://ff-quizzes.netlify.app/web/quiz/30)

## Огляд і самостійне навчання

Дізнайтеся більше про Pub/Sub, [прочитавши про це](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon).

## Завдання

[Створіть макет гри](assignment.md)

---

**Відмова від відповідальності**:  
Цей документ був перекладений за допомогою сервісу автоматичного перекладу [Co-op Translator](https://github.com/Azure/co-op-translator). Хоча ми прагнемо до точності, будь ласка, майте на увазі, що автоматичні переклади можуть містити помилки або неточності. Оригінальний документ на його рідній мові слід вважати авторитетним джерелом. Для критичної інформації рекомендується професійний людський переклад. Ми не несемо відповідальності за будь-які непорозуміння або неправильні тлумачення, що виникають внаслідок використання цього перекладу.