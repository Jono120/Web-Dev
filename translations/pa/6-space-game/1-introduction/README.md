<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "979cfcce2413a87d9e4c67eb79234bc3",
  "translation_date": "2025-08-28T17:05:05+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "pa"
}
-->
# ਸਪੇਸ ਗੇਮ ਬਣਾਓ ਭਾਗ 1: ਪਰਿਚਯ

![video](../../../../6-space-game/images/pewpew.gif)

## ਲੈਕਚਰ ਤੋਂ ਪਹਿਲਾਂ ਕਵਿਜ਼

[ਲੈਕਚਰ ਤੋਂ ਪਹਿਲਾਂ ਕਵਿਜ਼](https://ff-quizzes.netlify.app/web/quiz/29)

### ਗੇਮ ਡਿਵੈਲਪਮੈਂਟ ਵਿੱਚ Inheritance ਅਤੇ Composition

ਪਿਛਲੇ ਪਾਠਾਂ ਵਿੱਚ, ਤੁਸੀਂ ਜੋ ਐਪ ਬਣਾਏ ਉਹ ਛੋਟੇ ਪ੍ਰਾਜੈਕਟ ਸਨ, ਇਸ ਲਈ ਡਿਜ਼ਾਈਨ ਆਰਕੀਟੈਕਚਰ ਬਾਰੇ ਜ਼ਿਆਦਾ ਸੋਚਣ ਦੀ ਲੋੜ ਨਹੀਂ ਸੀ। ਪਰ ਜਦੋਂ ਤੁਹਾਡੇ ਐਪਲੀਕੇਸ਼ਨ ਵੱਡੇ ਹੋਣ ਲੱਗਦੇ ਹਨ, ਤਾਂ ਆਰਕੀਟੈਕਚਰਲ ਫੈਸਲੇ ਮਹੱਤਵਪੂਰਨ ਹੋ ਜਾਂਦੇ ਹਨ। ਜਾਵਾਸਕ੍ਰਿਪਟ ਵਿੱਚ ਵੱਡੇ ਐਪਲੀਕੇਸ਼ਨ ਬਣਾਉਣ ਦੇ ਦੋ ਮੁੱਖ ਤਰੀਕੇ ਹਨ: *composition* ਜਾਂ *inheritance*। ਦੋਹਾਂ ਦੇ ਫਾਇਦੇ ਅਤੇ ਨੁਕਸਾਨ ਹਨ, ਪਰ ਆਓ ਇਸਨੂੰ ਇੱਕ ਗੇਮ ਦੇ ਸੰਦਰਭ ਵਿੱਚ ਸਮਝੀਏ।

✅ ਸਭ ਤੋਂ ਮਸ਼ਹੂਰ ਪ੍ਰੋਗ੍ਰਾਮਿੰਗ ਕਿਤਾਬਾਂ ਵਿੱਚੋਂ ਇੱਕ [ਡਿਜ਼ਾਈਨ ਪੈਟਰਨਜ਼](https://en.wikipedia.org/wiki/Design_Patterns) ਬਾਰੇ ਹੈ।

ਇੱਕ ਗੇਮ ਵਿੱਚ ਤੁਹਾਡੇ ਕੋਲ `game objects` ਹੁੰਦੇ ਹਨ, ਜੋ ਸਕ੍ਰੀਨ 'ਤੇ ਮੌਜੂਦ ਹੁੰਦੇ ਹਨ। ਇਸਦਾ ਮਤਲਬ ਹੈ ਕਿ ਉਹਨਾਂ ਦੀ ਕਾਰਟੀਸ਼ੀਅਨ ਕੋਆਰਡੀਨੇਟ ਸਿਸਟਮ 'ਤੇ ਸਥਿਤੀ ਹੁੰਦੀ ਹੈ, ਜਿਸਨੂੰ `x` ਅਤੇ `y` ਕੋਆਰਡੀਨੇਟ ਨਾਲ ਦਰਸਾਇਆ ਜਾਂਦਾ ਹੈ। ਜਦੋਂ ਤੁਸੀਂ ਗੇਮ ਡਿਵੈਲਪ ਕਰਦੇ ਹੋ, ਤਾਂ ਤੁਹਾਨੂੰ ਪਤਾ ਲੱਗੇਗਾ ਕਿ ਤੁਹਾਡੇ ਸਾਰੇ ਗੇਮ ਆਬਜੈਕਟਸ ਵਿੱਚ ਕੁਝ ਸਧਾਰਨ ਗੁਣ ਹੁੰਦੇ ਹਨ, ਜੋ ਹਰ ਗੇਮ ਵਿੱਚ ਸਾਂਝੇ ਹੁੰਦੇ ਹਨ:

- **ਸਥਿਤੀ-ਅਧਾਰਿਤ** ਜ਼ਿਆਦਾਤਰ, ਜੇਕਰ ਸਾਰੇ ਨਹੀਂ, ਗੇਮ ਦੇ ਤੱਤ ਸਥਿਤੀ-ਅਧਾਰਿਤ ਹੁੰਦੇ ਹਨ। ਇਸਦਾ ਮਤਲਬ ਹੈ ਕਿ ਉਹਨਾਂ ਦੀ ਸਥਿਤੀ ਹੁੰਦੀ ਹੈ, `x` ਅਤੇ `y`।
- **ਹਿਲਣ ਵਾਲੇ** ਇਹ ਉਹ ਆਬਜੈਕਟ ਹੁੰਦੇ ਹਨ ਜੋ ਨਵੀਂ ਸਥਿਤੀ ਵੱਲ ਹਿਲ ਸਕਦੇ ਹਨ। ਇਹ ਆਮ ਤੌਰ 'ਤੇ ਹੀਰੋ, ਮੌਂਸਟਰ ਜਾਂ NPC (ਨਾਨ-ਪਲੇਅਰ ਕਿਰਦਾਰ) ਹੁੰਦੇ ਹਨ, ਪਰ ਉਦਾਹਰਣ ਲਈ, ਇੱਕ ਸਥਿਰ ਆਬਜੈਕਟ ਜਿਵੇਂ ਕਿ ਦਰੱਖਤ ਨਹੀਂ।
- **ਆਪਣੇ ਆਪ ਨਸ਼ਟ ਹੋਣ ਵਾਲੇ** ਇਹ ਆਬਜੈਕਟ ਸਿਰਫ਼ ਕੁਝ ਸਮੇਂ ਲਈ ਮੌਜੂਦ ਰਹਿੰਦੇ ਹਨ ਅਤੇ ਫਿਰ ਮਿਟਾਉਣ ਲਈ ਤਿਆਰ ਹੋ ਜਾਂਦੇ ਹਨ। ਆਮ ਤੌਰ 'ਤੇ ਇਹ ਇੱਕ `dead` ਜਾਂ `destroyed` ਬੂਲੀਅਨ ਨਾਲ ਦਰਸਾਇਆ ਜਾਂਦਾ ਹੈ ਜੋ ਗੇਮ ਇੰਜਨ ਨੂੰ ਸੰਕੇਤ ਦਿੰਦਾ ਹੈ ਕਿ ਇਸ ਆਬਜੈਕਟ ਨੂੰ ਹੁਣ ਰੈਂਡਰ ਨਹੀਂ ਕੀਤਾ ਜਾਣਾ ਚਾਹੀਦਾ।
- **ਕੂਲ-ਡਾਊਨ** 'ਕੂਲ-ਡਾਊਨ' ਛੋਟੇ ਸਮੇਂ ਲਈ ਮੌਜੂਦ ਆਬਜੈਕਟਸ ਵਿੱਚ ਇੱਕ ਆਮ ਗੁਣ ਹੈ। ਇੱਕ ਆਮ ਉਦਾਹਰਣ ਇੱਕ ਟੈਕਸਟ ਜਾਂ ਗ੍ਰਾਫਿਕਲ ਪ੍ਰਭਾਵ (ਜਿਵੇਂ ਕਿ ਧਮਾਕਾ) ਹੈ ਜੋ ਸਿਰਫ਼ ਕੁਝ ਮਿਲੀਸੈਕੰਡ ਲਈ ਦਿਖਾਈ ਦੇਣਾ ਚਾਹੀਦਾ ਹੈ।

✅ ਪੈਕ-ਮੈਨ ਵਰਗੇ ਗੇਮ ਬਾਰੇ ਸੋਚੋ। ਕੀ ਤੁਸੀਂ ਇਸ ਗੇਮ ਵਿੱਚ ਉਪਰੋਕਤ ਚਾਰ ਆਬਜੈਕਟ ਪ੍ਰਕਾਰਾਂ ਦੀ ਪਛਾਣ ਕਰ ਸਕਦੇ ਹੋ?

### ਵਿਹਾਰ ਨੂੰ ਪ੍ਰਗਟ ਕਰਨਾ

ਉਪਰੋਕਤ ਸਾਰੇ ਉਹ ਵਿਹਾਰ ਹਨ ਜੋ ਗੇਮ ਆਬਜੈਕਟਸ ਵਿੱਚ ਹੋ ਸਕਦੇ ਹਨ। ਤਾਂ ਅਸੀਂ ਇਹਨਾਂ ਨੂੰ ਕਿਵੇਂ ਕੋਡ ਕਰਦੇ ਹਾਂ? ਅਸੀਂ ਇਹ ਵਿਹਾਰ ਕਲਾਸਾਂ ਜਾਂ ਆਬਜੈਕਟਸ ਨਾਲ ਜੁੜੇ ਮੈਥਡਸ ਦੇ ਰੂਪ ਵਿੱਚ ਪ੍ਰਗਟ ਕਰ ਸਕਦੇ ਹਾਂ।

**ਕਲਾਸਾਂ**

ਵਿਚਾਰ ਇਹ ਹੈ ਕਿ `classes` ਨੂੰ `inheritance` ਦੇ ਨਾਲ ਵਰਤ ਕੇ ਇੱਕ ਕਲਾਸ ਵਿੱਚ ਵਿਹਾਰ ਸ਼ਾਮਲ ਕੀਤਾ ਜਾਵੇ।

✅ Inheritance ਇੱਕ ਮਹੱਤਵਪੂਰਨ ਸੰਕਲਪ ਹੈ। ਇਸ ਬਾਰੇ ਹੋਰ ਜਾਣੋ [MDN ਦੇ ਲੇਖ](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) ਵਿੱਚ।

ਕੋਡ ਰਾਹੀਂ ਪ੍ਰਗਟ ਕੀਤਾ ਗਿਆ, ਇੱਕ ਗੇਮ ਆਬਜੈਕਟ ਆਮ ਤੌਰ 'ਤੇ ਇਸ ਤਰ੍ਹਾਂ ਲੱਗਦਾ ਹੈ:

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

✅ ਕੁਝ ਮਿੰਟ ਲਓ ਅਤੇ ਪੈਕ-ਮੈਨ ਦੇ ਹੀਰੋ (ਉਦਾਹਰਣ ਲਈ, ਇੰਕੀ, ਪਿੰਕੀ ਜਾਂ ਬਲਿੰਕੀ) ਨੂੰ ਦੁਬਾਰਾ ਸੋਚੋ ਅਤੇ ਇਸਨੂੰ ਜਾਵਾਸਕ੍ਰਿਪਟ ਵਿੱਚ ਕਿਵੇਂ ਲਿਖਿਆ ਜਾਵੇਗਾ।

**Composition**

ਆਬਜੈਕਟ Inheritance ਨੂੰ ਸੰਭਾਲਣ ਦਾ ਇੱਕ ਵੱਖਰਾ ਤਰੀਕਾ *Composition* ਹੈ। ਫਿਰ, ਆਬਜੈਕਟਸ ਆਪਣਾ ਵਿਹਾਰ ਇਸ ਤਰ੍ਹਾਂ ਪ੍ਰਗਟ ਕਰਦੇ ਹਨ:

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

**ਮੈਨੂੰ ਕਿਹੜਾ ਪੈਟਰਨ ਵਰਤਣਾ ਚਾਹੀਦਾ ਹੈ?**

ਇਹ ਤੁਹਾਡੇ ਉੱਤੇ ਨਿਰਭਰ ਕਰਦਾ ਹੈ ਕਿ ਤੁਸੀਂ ਕਿਹੜਾ ਪੈਟਰਨ ਚੁਣਦੇ ਹੋ। ਜਾਵਾਸਕ੍ਰਿਪਟ ਦੋਹਾਂ ਪੈਰਾਡਾਈਮਜ਼ ਦਾ ਸਮਰਥਨ ਕਰਦਾ ਹੈ।

--

ਗੇਮ ਡਿਵੈਲਪਮੈਂਟ ਵਿੱਚ ਇੱਕ ਹੋਰ ਆਮ ਪੈਟਰਨ ਗੇਮ ਦੇ ਯੂਜ਼ਰ ਅਨੁਭਵ ਅਤੇ ਪ੍ਰਦਰਸ਼ਨ ਨੂੰ ਸੰਭਾਲਣ ਦੀ ਸਮੱਸਿਆ ਨੂੰ ਹੱਲ ਕਰਦਾ ਹੈ।

## Pub/sub ਪੈਟਰਨ

✅ Pub/Sub ਦਾ ਮਤਲਬ ਹੈ 'publish-subscribe'

ਇਹ ਪੈਟਰਨ ਇਸ ਵਿਚਾਰ ਨੂੰ ਹੱਲ ਕਰਦਾ ਹੈ ਕਿ ਤੁਹਾਡੇ ਐਪਲੀਕੇਸ਼ਨ ਦੇ ਵੱਖ-ਵੱਖ ਹਿੱਸਿਆਂ ਨੂੰ ਇੱਕ-ਦੂਜੇ ਬਾਰੇ ਜਾਣਨ ਦੀ ਲੋੜ ਨਹੀਂ ਹੋਣੀ ਚਾਹੀਦੀ। ਕਿਉਂ? ਇਹ ਸਮਝਣਾ ਬਹੁਤ ਆਸਾਨ ਬਣਾਉਂਦਾ ਹੈ ਕਿ ਕੁੱਲ ਮਿਲਾ ਕੇ ਕੀ ਹੋ ਰਿਹਾ ਹੈ ਜੇਕਰ ਵੱਖ-ਵੱਖ ਹਿੱਸੇ ਵੱਖਰੇ ਹਨ। ਇਹ ਅਚਾਨਕ ਵਿਹਾਰ ਬਦਲਣ ਨੂੰ ਵੀ ਆਸਾਨ ਬਣਾਉਂਦਾ ਹੈ ਜੇਕਰ ਤੁਹਾਨੂੰ ਲੋੜ ਹੋਵੇ। ਅਸੀਂ ਇਹ ਕਿਵੇਂ ਕਰਦੇ ਹਾਂ? ਅਸੀਂ ਕੁਝ ਸੰਕਲਪ ਸਥਾਪਿਤ ਕਰਕੇ ਇਹ ਕਰਦੇ ਹਾਂ:

- **ਸੁਨੇਹਾ**: ਇੱਕ ਸੁਨੇਹਾ ਆਮ ਤੌਰ 'ਤੇ ਇੱਕ ਟੈਕਸਟ ਸਟ੍ਰਿੰਗ ਹੁੰਦੀ ਹੈ ਜਿਸਦੇ ਨਾਲ ਇੱਕ ਵਿਕਲਪਿਕ payload (ਡਾਟਾ ਦਾ ਟੁਕੜਾ ਜੋ ਸੁਨੇਹੇ ਬਾਰੇ ਸਪਸ਼ਟਤਾ ਦਿੰਦਾ ਹੈ) ਹੁੰਦਾ ਹੈ। ਗੇਮ ਵਿੱਚ ਇੱਕ ਆਮ ਸੁਨੇਹਾ ਹੋ ਸਕਦਾ ਹੈ `KEY_PRESSED_ENTER`।
- **ਪਬਲਿਸ਼ਰ**: ਇਹ ਤੱਤ ਇੱਕ ਸੁਨੇਹਾ *ਪਬਲਿਸ਼* ਕਰਦਾ ਹੈ ਅਤੇ ਇਸਨੂੰ ਸਾਰੇ ਸਬਸਕ੍ਰਾਈਬਰਾਂ ਨੂੰ ਭੇਜਦਾ ਹੈ।
- **ਸਬਸਕ੍ਰਾਈਬਰ**: ਇਹ ਤੱਤ ਖਾਸ ਸੁਨੇਹਿਆਂ ਨੂੰ *ਸੁਣਦਾ* ਹੈ ਅਤੇ ਇਸ ਸੁਨੇਹੇ ਨੂੰ ਪ੍ਰਾਪਤ ਕਰਨ ਦੇ ਨਤੀਜੇ ਵਜੋਂ ਕੁਝ ਕੰਮ ਕਰਦਾ ਹੈ, ਜਿਵੇਂ ਕਿ ਲੇਜ਼ਰ ਚਲਾਉਣਾ।

ਇਸਦੀ ਇੰਪਲੀਮੈਂਟੇਸ਼ਨ ਬਹੁਤ ਛੋਟੀ ਹੁੰਦੀ ਹੈ ਪਰ ਇਹ ਇੱਕ ਬਹੁਤ ਸ਼ਕਤੀਸ਼ਾਲੀ ਪੈਟਰਨ ਹੈ। ਇਹ ਇਸ ਤਰ੍ਹਾਂ ਲਾਗੂ ਕੀਤਾ ਜਾ ਸਕਦਾ ਹੈ:

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

ਉਪਰੋਕਤ ਕੋਡ ਨੂੰ ਵਰਤਣ ਲਈ ਅਸੀਂ ਇੱਕ ਬਹੁਤ ਛੋਟੀ ਇੰਪਲੀਮੈਂਟੇਸ਼ਨ ਬਣਾ ਸਕਦੇ ਹਾਂ:

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

ਉਪਰੋਕਤ ਵਿੱਚ ਅਸੀਂ ਇੱਕ ਕੀਬੋਰਡ ਇਵੈਂਟ, `ArrowLeft` ਨੂੰ ਕਨੈਕਟ ਕੀਤਾ ਅਤੇ `HERO_MOVE_LEFT` ਸੁਨੇਹਾ ਭੇਜਿਆ। ਅਸੀਂ ਉਸ ਸੁਨੇਹੇ ਨੂੰ ਸੁਣਦੇ ਹਾਂ ਅਤੇ ਨਤੀਜੇ ਵਜੋਂ `hero` ਨੂੰ ਹਿਲਾਉਂਦੇ ਹਾਂ। ਇਸ ਪੈਟਰਨ ਦੀ ਤਾਕਤ ਇਹ ਹੈ ਕਿ ਇਵੈਂਟ ਲਿਸਨਰ ਅਤੇ ਹੀਰੋ ਇੱਕ-ਦੂਜੇ ਬਾਰੇ ਨਹੀਂ ਜਾਣਦੇ। ਤੁਸੀਂ `ArrowLeft` ਨੂੰ `A` ਕੀ ਨਾਲ ਰੀਮੈਪ ਕਰ ਸਕਦੇ ਹੋ। ਇਸ ਤੋਂ ਇਲਾਵਾ, ਇਹ ਸੰਭਵ ਹੋਵੇਗਾ ਕਿ `ArrowLeft` 'ਤੇ ਕੁਝ ਬਿਲਕੁਲ ਵੱਖਰਾ ਕੀਤਾ ਜਾਵੇ, ਸਿਰਫ਼ eventEmitter ਦੇ `on` ਫੰਕਸ਼ਨ ਵਿੱਚ ਕੁਝ ਸੋਧਾਂ ਕਰਕੇ:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

ਜਦੋਂ ਤੁਹਾਡੀ ਗੇਮ ਵਧਦੀ ਹੈ ਅਤੇ ਜਟਿਲ ਹੋ ਜਾਂਦੀ ਹੈ, ਇਹ ਪੈਟਰਨ ਜਟਿਲਤਾ ਵਿੱਚ ਸਥਿਰ ਰਹਿੰਦਾ ਹੈ ਅਤੇ ਤੁਹਾਡਾ ਕੋਡ ਸਾਫ਼ ਰਹਿੰਦਾ ਹੈ। ਇਸ ਪੈਟਰਨ ਨੂੰ ਅਪਨਾਉਣ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ।

---

## 🚀 ਚੁਣੌਤੀ

ਸੋਚੋ ਕਿ pub-sub ਪੈਟਰਨ ਇੱਕ ਗੇਮ ਨੂੰ ਕਿਵੇਂ ਬਿਹਤਰ ਬਣਾ ਸਕਦਾ ਹੈ। ਕਿਹੜੇ ਹਿੱਸੇ ਇਵੈਂਟ ਜਾਰੀ ਕਰਨੇ ਚਾਹੀਦੇ ਹਨ, ਅਤੇ ਗੇਮ ਨੂੰ ਉਹਨਾਂ 'ਤੇ ਕਿਵੇਂ ਪ੍ਰਤੀਕਿਰਿਆ ਕਰਨੀ ਚਾਹੀਦੀ ਹੈ? ਹੁਣ ਤੁਹਾਡੇ ਕੋਲ ਰਚਨਾਤਮਕ ਹੋਣ ਦਾ ਮੌਕਾ ਹੈ, ਇੱਕ ਨਵੀਂ ਗੇਮ ਬਾਰੇ ਸੋਚੋ ਅਤੇ ਇਸਦੇ ਹਿੱਸੇ ਕਿਵੇਂ ਵਿਹਾਰ ਕਰ ਸਕਦੇ ਹਨ।

## ਲੈਕਚਰ ਤੋਂ ਬਾਅਦ ਕਵਿਜ਼

[ਲੈਕਚਰ ਤੋਂ ਬਾਅਦ ਕਵਿਜ਼](https://ff-quizzes.netlify.app/web/quiz/30)

## ਸਮੀਖਿਆ ਅਤੇ ਸਵੈ ਅਧਿਐਨ

Pub/Sub ਬਾਰੇ ਹੋਰ ਜਾਣੋ [ਇਸ ਬਾਰੇ ਪੜ੍ਹ ਕੇ](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon)।

## ਅਸਾਈਨਮੈਂਟ

[ਇੱਕ ਗੇਮ ਮੌਕਅੱਪ ਕਰੋ](assignment.md)

---

**ਅਸਵੀਕਤੀ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਹਾਲਾਂਕਿ ਅਸੀਂ ਸਹੀਅਤ ਲਈ ਯਤਨਸ਼ੀਲ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁੱਤੀਆਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼ ਨੂੰ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।