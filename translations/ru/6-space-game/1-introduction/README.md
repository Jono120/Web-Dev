<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "979cfcce2413a87d9e4c67eb79234bc3",
  "translation_date": "2025-08-28T23:19:10+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "ru"
}
-->
# Создание космической игры, часть 1: Введение

![video](../../../../6-space-game/images/pewpew.gif)

## Викторина перед лекцией

[Викторина перед лекцией](https://ff-quizzes.netlify.app/web/quiz/29)

### Наследование и композиция в разработке игр

В предыдущих уроках не было особой необходимости задумываться о архитектуре приложений, которые вы создавали, так как проекты были небольшими по масштабу. Однако, когда ваши приложения становятся больше, архитектурные решения начинают играть более важную роль. Существует два основных подхода к созданию крупных приложений на JavaScript: *композиция* или *наследование*. У каждого из них есть свои плюсы и минусы, но давайте рассмотрим их в контексте игры.

✅ Одна из самых известных книг по программированию посвящена [шаблонам проектирования](https://en.wikipedia.org/wiki/Design_Patterns).

В игре есть `игровые объекты`, которые представляют собой объекты, существующие на экране. Это означает, что они имеют местоположение в декартовой системе координат, характеризуемое наличием координат `x` и `y`. В процессе разработки игры вы заметите, что все игровые объекты имеют стандартные свойства, общие для каждой игры, а именно элементы, которые:

- **основаны на местоположении** Большинство, если не все, игровые элементы основаны на местоположении. Это означает, что у них есть местоположение, `x` и `y`.
- **подвижные** Это объекты, которые могут перемещаться в новое местоположение. Обычно это герой, монстр или NPC (персонаж, не управляемый игроком), но не, например, статичный объект, такой как дерево.
- **самоуничтожающиеся** Эти объекты существуют только в течение определенного времени, после чего они подготавливаются к удалению. Обычно это представлено булевым значением `dead` или `destroyed`, которое сигнализирует игровому движку, что этот объект больше не должен отображаться.
- **с задержкой** 'Задержка' — это типичное свойство для объектов с коротким сроком жизни. Типичный пример — текст или графический эффект, например, взрыв, который должен быть виден только несколько миллисекунд.

✅ Подумайте о такой игре, как Pac-Man. Можете ли вы определить четыре типа объектов, перечисленных выше, в этой игре?

### Выражение поведения

Все, что мы описали выше, — это поведение, которое могут иметь игровые объекты. Как же мы можем закодировать это? Мы можем выразить это поведение как методы, связанные либо с классами, либо с объектами.

**Классы**

Идея заключается в использовании `классов` в сочетании с `наследованием`, чтобы добавить определенное поведение к классу.

✅ Наследование — важная концепция для понимания. Узнайте больше в [статье MDN о наследовании](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain).

В коде игровой объект может выглядеть примерно так:

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

✅ Потратьте несколько минут, чтобы представить героя Pac-Man (например, Inky, Pinky или Blinky) и как он мог бы быть написан на JavaScript.

**Композиция**

Другой способ обработки наследования объектов — использование *композиции*. Тогда объекты выражают свое поведение следующим образом:

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

**Какой шаблон выбрать?**

Выбор за вами, какой шаблон использовать. JavaScript поддерживает оба этих подхода.

--

Еще один шаблон, часто используемый в разработке игр, решает проблему управления пользовательским интерфейсом игры и производительностью.

## Шаблон Pub/Sub

✅ Pub/Sub означает 'publish-subscribe' (публикация-подписка)

Этот шаблон предполагает, что различные части вашего приложения не должны знать друг о друге. Почему это важно? Это значительно упрощает понимание происходящего в целом, если различные части разделены. Это также облегчает внезапное изменение поведения, если это необходимо. Как мы можем это реализовать? Мы делаем это, вводя несколько концепций:

- **сообщение**: Сообщение обычно представляет собой строку текста, сопровождаемую необязательной полезной нагрузкой (данными, уточняющими, о чем сообщение). Типичное сообщение в игре может быть `KEY_PRESSED_ENTER`.
- **издатель**: Этот элемент *публикует* сообщение и отправляет его всем подписчикам.
- **подписчик**: Этот элемент *слушает* определенные сообщения и выполняет какую-либо задачу в результате получения этого сообщения, например, стрельбу лазером.

Реализация довольно компактна, но это очень мощный шаблон. Вот как он может быть реализован:

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

Чтобы использовать приведенный выше код, мы можем создать очень небольшую реализацию:

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

В приведенном выше примере мы связываем событие клавиатуры, `ArrowLeft`, и отправляем сообщение `HERO_MOVE_LEFT`. Мы слушаем это сообщение и перемещаем `hero` в результате. Сила этого шаблона заключается в том, что обработчик событий и герой не знают друг о друге. Вы можете переназначить `ArrowLeft` на клавишу `A`. Кроме того, можно сделать что-то совершенно другое на `ArrowLeft`, внеся несколько изменений в функцию `on` объекта eventEmitter:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

Когда игра становится сложнее, этот шаблон сохраняет свою простоту, а ваш код остается чистым. Очень рекомендуется использовать этот шаблон.

---

## 🚀 Задание

Подумайте, как шаблон pub-sub может улучшить игру. Какие части должны генерировать события, и как игра должна на них реагировать? Сейчас у вас есть возможность проявить творческий подход, придумав новую игру и то, как ее части могут взаимодействовать.

## Викторина после лекции

[Викторина после лекции](https://ff-quizzes.netlify.app/web/quiz/30)

## Обзор и самостоятельное изучение

Узнайте больше о Pub/Sub, [прочитав об этом](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon).

## Задание

[Создайте макет игры](assignment.md)

---

**Отказ от ответственности**:  
Этот документ был переведен с помощью сервиса автоматического перевода [Co-op Translator](https://github.com/Azure/co-op-translator). Хотя мы стремимся к точности, пожалуйста, учитывайте, что автоматические переводы могут содержать ошибки или неточности. Оригинальный документ на его родном языке следует считать авторитетным источником. Для получения критически важной информации рекомендуется профессиональный перевод человеком. Мы не несем ответственности за любые недоразумения или неправильные интерпретации, возникшие в результате использования данного перевода.