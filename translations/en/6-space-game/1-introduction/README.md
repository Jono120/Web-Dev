<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "979cfcce2413a87d9e4c67eb79234bc3",
  "translation_date": "2025-08-29T13:22:15+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "en"
}
-->
# Build a Space Game Part 1: Introduction

![video](../../../../6-space-game/images/pewpew.gif)

## Pre-Lecture Quiz

[Pre-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/29)

### Inheritance and Composition in game development

In earlier lessons, you didn’t need to worry much about the design architecture of the apps you built, as the projects were small in scope. However, as your applications grow in size and complexity, architectural decisions become more important. There are two major approaches to building larger applications in JavaScript: *composition* and *inheritance*. Both have their advantages and disadvantages, but let’s explore them in the context of a game.

✅ One of the most famous programming books ever written is about [design patterns](https://en.wikipedia.org/wiki/Design_Patterns).

In a game, you have `game objects`, which are objects that exist on the screen. This means they have a location on a Cartesian coordinate system, defined by `x` and `y` coordinates. As you develop a game, you’ll notice that all your game objects share some standard properties, common to every game you create. These include:

- **location-based**: Most, if not all, game elements are location-based. This means they have an `x` and `y` coordinate.
- **movable**: These are objects that can move to a new location. Typically, this includes heroes, monsters, or NPCs (non-player characters), but not static objects like trees.
- **self-destructing**: These objects exist for a limited time before marking themselves for deletion. This is often represented by a `dead` or `destroyed` boolean that signals to the game engine that the object should no longer be rendered.
- **cool-down**: 'Cool-down' is a common property for short-lived objects. For example, a piece of text or a graphical effect like an explosion that should only appear for a few milliseconds.

✅ Think about a game like Pac-Man. Can you identify the four object types listed above in this game?

### Expressing behavior

The properties described above represent behaviors that game objects can have. So how do we encode these behaviors? We can express them as methods associated with either classes or objects.

**Classes**

One approach is to use `classes` along with `inheritance` to add specific behaviors to a class.

✅ Inheritance is an important concept to understand. Learn more in [MDN's article about inheritance](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain).

In code, a game object might look like this:

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

✅ Take a few minutes to imagine how a Pac-Man character (like Inky, Pinky, or Blinky) could be written in JavaScript.

**Composition**

Another way to handle object inheritance is through *Composition*. In this approach, objects express their behavior like this:

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

**Which pattern should I use?**

The choice is yours. JavaScript supports both paradigms.

--

Another common pattern in game development addresses the challenge of managing the game’s user experience and performance.

## Pub/sub pattern

✅ Pub/Sub stands for 'publish-subscribe'

This pattern is based on the idea that different parts of your application shouldn’t need to know about each other. Why is this important? It makes it easier to understand the overall system and simplifies making changes to behavior when needed. Here’s how it works:

- **message**: A message is typically a text string, sometimes accompanied by an optional payload (data that provides additional context about the message). For example, a common message in a game might be `KEY_PRESSED_ENTER`.
- **publisher**: This component *publishes* a message and sends it to all subscribers.
- **subscriber**: This component *listens* for specific messages and performs a task in response, such as firing a laser.

The implementation is relatively small but incredibly powerful. Here’s an example:

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

To use the code above, we can create a simple implementation:

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

In this example, we connect a keyboard event, `ArrowLeft`, to send the `HERO_MOVE_LEFT` message. We then listen for that message and move the `hero` accordingly. The strength of this pattern lies in the fact that the event listener and the hero don’t need to know about each other. You could remap `ArrowLeft` to the `A` key, or even assign a completely different action to `ArrowLeft` by making a few changes to the eventEmitter’s `on` function:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

As your game grows in complexity, this pattern remains consistent, keeping your code clean and manageable. It’s highly recommended to adopt this approach.

---

## 🚀 Challenge

Think about how the pub-sub pattern could improve a game. Which parts of the game should emit events, and how should the game respond to them? Use your creativity to imagine a new game and how its components might interact.

## Post-Lecture Quiz

[Post-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/30)

## Review & Self Study

Learn more about Pub/Sub by [reading about it](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon).

## Assignment

[Mock up a game](assignment.md)

---

**Disclaimer**:  
This document has been translated using the AI translation service [Co-op Translator](https://github.com/Azure/co-op-translator). While we strive for accuracy, please note that automated translations may contain errors or inaccuracies. The original document in its native language should be regarded as the authoritative source. For critical information, professional human translation is recommended. We are not responsible for any misunderstandings or misinterpretations resulting from the use of this translation.