<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "979cfcce2413a87d9e4c67eb79234bc3",
  "translation_date": "2025-08-29T07:34:35+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "th"
}
-->
# สร้างเกมอวกาศ ตอนที่ 1: บทนำ

![video](../../../../6-space-game/images/pewpew.gif)

## แบบทดสอบก่อนเรียน

[แบบทดสอบก่อนเรียน](https://ff-quizzes.netlify.app/web/quiz/29)

### การใช้ Inheritance และ Composition ในการพัฒนาเกม

ในบทเรียนก่อนหน้านี้ คุณอาจไม่ต้องกังวลเกี่ยวกับโครงสร้างการออกแบบของแอปที่คุณสร้างมากนัก เนื่องจากโปรเจกต์มีขอบเขตที่เล็ก อย่างไรก็ตาม เมื่อแอปพลิเคชันของคุณมีขนาดและขอบเขตที่ใหญ่ขึ้น การตัดสินใจด้านสถาปัตยกรรมจะกลายเป็นเรื่องสำคัญมากขึ้น มีสองแนวทางหลักในการสร้างแอปพลิเคชันขนาดใหญ่ใน JavaScript: *composition* หรือ *inheritance* ซึ่งทั้งสองมีข้อดีและข้อเสีย แต่เราจะอธิบายผ่านบริบทของเกม

✅ หนึ่งในหนังสือโปรแกรมมิ่งที่มีชื่อเสียงที่สุดเกี่ยวกับ [design patterns](https://en.wikipedia.org/wiki/Design_Patterns)

ในเกม คุณจะมี `game objects` ซึ่งเป็นวัตถุที่ปรากฏอยู่บนหน้าจอ นั่นหมายความว่ามันมีตำแหน่งในระบบพิกัดคาร์ทีเซียน โดยมีพิกัด `x` และ `y` เมื่อคุณพัฒนาเกม คุณจะสังเกตเห็นว่า game objects ทั้งหมดของคุณมีคุณสมบัติมาตรฐานที่เหมือนกันในทุกเกมที่คุณสร้าง ซึ่งได้แก่:

- **อ้างอิงตำแหน่ง** เกือบทุกองค์ประกอบในเกมจะอ้างอิงตำแหน่ง นั่นหมายความว่ามันมีตำแหน่ง `x` และ `y`
- **เคลื่อนที่ได้** วัตถุเหล่านี้สามารถเคลื่อนที่ไปยังตำแหน่งใหม่ได้ โดยปกติจะเป็นฮีโร่ มอนสเตอร์ หรือ NPC (ตัวละครที่ไม่ใช่ผู้เล่น) แต่ไม่ใช่วัตถุที่อยู่นิ่ง เช่น ต้นไม้
- **ทำลายตัวเองได้** วัตถุเหล่านี้จะมีอยู่เพียงช่วงเวลาหนึ่งก่อนที่จะตั้งค่าตัวเองให้ถูกลบออก โดยปกติจะแสดงด้วย boolean `dead` หรือ `destroyed` ที่ส่งสัญญาณไปยังเอนจินเกมว่าวัตถุนี้ไม่ควรแสดงผลอีกต่อไป
- **คูลดาวน์** 'คูลดาวน์' เป็นคุณสมบัติทั่วไปของวัตถุที่มีอายุสั้น ตัวอย่างทั่วไปคือข้อความหรือเอฟเฟกต์กราฟิก เช่น การระเบิด ที่ควรแสดงผลเพียงไม่กี่มิลลิวินาที

✅ ลองนึกถึงเกมอย่าง Pac-Man คุณสามารถระบุวัตถุทั้งสี่ประเภทที่กล่าวมานี้ในเกมได้หรือไม่?

### การแสดงพฤติกรรม

สิ่งที่เราอธิบายข้างต้นคือพฤติกรรมที่ game objects สามารถมีได้ แล้วเราจะเขียนโค้ดพฤติกรรมเหล่านี้อย่างไร? เราสามารถแสดงพฤติกรรมเหล่านี้เป็นเมธอดที่เชื่อมโยงกับคลาสหรือออบเจกต์

**Classes**

แนวคิดคือการใช้ `classes` ร่วมกับ `inheritance` เพื่อเพิ่มพฤติกรรมบางอย่างให้กับคลาส

✅ การทำความเข้าใจ Inheritance เป็นเรื่องสำคัญ เรียนรู้เพิ่มเติมได้ที่ [บทความของ MDN เกี่ยวกับ inheritance](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)

ในรูปแบบโค้ด game object อาจมีลักษณะดังนี้:

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

✅ ลองใช้เวลาสักครู่เพื่อจินตนาการถึงฮีโร่ใน Pac-Man (เช่น Inky, Pinky หรือ Blinky) และวิธีการเขียนใน JavaScript

**Composition**

อีกวิธีหนึ่งในการจัดการ inheritance ของออบเจกต์คือการใช้ *Composition* โดยที่ออบเจกต์แสดงพฤติกรรมของมันในลักษณะนี้:

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

**ควรใช้รูปแบบใด?**

ขึ้นอยู่กับคุณว่าจะเลือกใช้รูปแบบใด JavaScript รองรับทั้งสองแนวทางนี้

--

อีกหนึ่งรูปแบบที่พบบ่อยในเกมคือการจัดการประสบการณ์ผู้ใช้และประสิทธิภาพของเกม

## รูปแบบ Pub/sub

✅ Pub/Sub ย่อมาจาก 'publish-subscribe'

รูปแบบนี้เกี่ยวกับแนวคิดที่ว่าส่วนต่าง ๆ ของแอปพลิเคชันของคุณไม่ควรรู้จักกันและกัน ทำไมถึงเป็นเช่นนั้น? เพราะมันทำให้ง่ายต่อการดูภาพรวมว่าเกิดอะไรขึ้น และยังทำให้ง่ายต่อการเปลี่ยนแปลงพฤติกรรมในกรณีที่จำเป็น เราทำสิ่งนี้ได้อย่างไร? โดยการกำหนดแนวคิดบางอย่าง:

- **message**: ข้อความมักจะเป็นสตริงข้อความที่มาพร้อมกับ payload (ข้อมูลเพิ่มเติมที่อธิบายว่าข้อความเกี่ยวกับอะไร) ตัวอย่างข้อความในเกมคือ `KEY_PRESSED_ENTER`
- **publisher**: องค์ประกอบนี้ *เผยแพร่* ข้อความและส่งไปยังผู้ติดตามทั้งหมด
- **subscriber**: องค์ประกอบนี้ *ฟัง* ข้อความเฉพาะและดำเนินการบางอย่างเมื่อได้รับข้อความ เช่น การยิงเลเซอร์

การนำไปใช้งานมีขนาดเล็กมาก แต่เป็นรูปแบบที่ทรงพลังมาก นี่คือตัวอย่างการนำไปใช้:

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

เพื่อใช้โค้ดข้างต้น เราสามารถสร้างการใช้งานขนาดเล็กได้ดังนี้:

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

ในตัวอย่างข้างต้น เราเชื่อมโยงเหตุการณ์คีย์บอร์ด `ArrowLeft` และส่งข้อความ `HERO_MOVE_LEFT` เราฟังข้อความนั้นและย้าย `hero` เป็นผลลัพธ์ จุดแข็งของรูปแบบนี้คือ event listener และ hero ไม่จำเป็นต้องรู้จักกัน คุณสามารถเปลี่ยน `ArrowLeft` เป็นปุ่ม `A` ได้ นอกจากนี้ยังสามารถทำสิ่งที่แตกต่างออกไปโดยสิ้นเชิงเมื่อกด `ArrowLeft` โดยแก้ไขฟังก์ชัน `on` ของ eventEmitter เพียงเล็กน้อย:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

เมื่อเกมของคุณซับซ้อนขึ้น รูปแบบนี้ยังคงมีความซับซ้อนเท่าเดิม และโค้ดของคุณยังคงสะอาดอยู่ ขอแนะนำให้ใช้รูปแบบนี้อย่างยิ่ง

---

## 🚀 ความท้าทาย

ลองคิดดูว่ารูปแบบ pub-sub สามารถเพิ่มประสิทธิภาพให้กับเกมได้อย่างไร ส่วนใดควรส่งเหตุการณ์ และเกมควรตอบสนองต่อเหตุการณ์เหล่านั้นอย่างไร? นี่เป็นโอกาสของคุณที่จะสร้างสรรค์ ลองคิดถึงเกมใหม่และพฤติกรรมของส่วนต่าง ๆ ในเกม

## แบบทดสอบหลังเรียน

[แบบทดสอบหลังเรียน](https://ff-quizzes.netlify.app/web/quiz/30)

## ทบทวนและศึกษาด้วยตนเอง

เรียนรู้เพิ่มเติมเกี่ยวกับ Pub/Sub โดย [อ่านเพิ่มเติม](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon)

## งานที่ได้รับมอบหมาย

[ออกแบบเกมต้นแบบ](assignment.md)

---

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามให้การแปลมีความถูกต้อง แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่แม่นยำ เอกสารต้นฉบับในภาษาต้นทางควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ ขอแนะนำให้ใช้บริการแปลภาษาจากผู้เชี่ยวชาญ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความที่ผิดพลาดซึ่งเกิดจากการใช้การแปลนี้