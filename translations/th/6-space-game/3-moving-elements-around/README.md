<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a9a161871de7706cb0e23b1bd0c74559",
  "translation_date": "2025-08-29T07:32:14+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "th"
}
-->
# สร้างเกมอวกาศ ตอนที่ 3: เพิ่มการเคลื่อนไหว

## แบบทดสอบก่อนเรียน

[แบบทดสอบก่อนเรียน](https://ff-quizzes.netlify.app/web/quiz/33)

เกมจะสนุกขึ้นเมื่อมีเอเลี่ยนเคลื่อนไหวบนหน้าจอ! ในเกมนี้ เราจะใช้การเคลื่อนไหวสองประเภท:

- **การเคลื่อนไหวด้วยคีย์บอร์ด/เมาส์**: เมื่อผู้ใช้โต้ตอบกับคีย์บอร์ดหรือเมาส์เพื่อเคลื่อนย้ายวัตถุบนหน้าจอ
- **การเคลื่อนไหวที่เกิดจากเกม**: เมื่อเกมเคลื่อนย้ายวัตถุในช่วงเวลาที่กำหนด

แล้วเราจะเคลื่อนย้ายสิ่งต่าง ๆ บนหน้าจอได้อย่างไร? ทุกอย่างเกี่ยวกับพิกัดคาร์ทีเซียน: เราเปลี่ยนตำแหน่ง (x, y) ของวัตถุแล้ววาดหน้าจอใหม่

โดยทั่วไป คุณต้องทำตามขั้นตอนต่อไปนี้เพื่อให้เกิด *การเคลื่อนไหว* บนหน้าจอ:

1. **ตั้งค่าตำแหน่งใหม่** สำหรับวัตถุ; สิ่งนี้จำเป็นเพื่อให้รู้สึกว่าวัตถุได้เคลื่อนที่
2. **ล้างหน้าจอ** หน้าจอต้องถูกล้างระหว่างการวาดใหม่ เราสามารถล้างได้โดยการวาดสี่เหลี่ยมที่เติมด้วยสีพื้นหลัง
3. **วาดวัตถุใหม่** ที่ตำแหน่งใหม่ การทำเช่นนี้จะทำให้เราสามารถเคลื่อนย้ายวัตถุจากตำแหน่งหนึ่งไปยังอีกตำแหน่งหนึ่งได้สำเร็จ

นี่คือตัวอย่างโค้ด:

```javascript
//set the hero's location
hero.x += 5;
// clear the rectangle that hosts the hero
ctx.clearRect(0, 0, canvas.width, canvas.height);
// redraw the game background and hero
ctx.fillRect(0, 0, canvas.width, canvas.height)
ctx.fillStyle = "black";
ctx.drawImage(heroImg, hero.x, hero.y);
```

✅ คุณคิดว่าเหตุใดการวาดฮีโร่ของคุณหลายเฟรมต่อวินาทีอาจส่งผลต่อประสิทธิภาพ? อ่านเพิ่มเติมเกี่ยวกับ [ทางเลือกสำหรับรูปแบบนี้](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas)

## จัดการเหตุการณ์คีย์บอร์ด

คุณจัดการเหตุการณ์โดยการเชื่อมต่อเหตุการณ์เฉพาะกับโค้ด เหตุการณ์คีย์บอร์ดจะถูกเรียกใช้บนหน้าต่างทั้งหมด ในขณะที่เหตุการณ์เมาส์ เช่น `click` สามารถเชื่อมต่อกับการคลิกองค์ประกอบเฉพาะ เราจะใช้เหตุการณ์คีย์บอร์ดตลอดโครงการนี้

ในการจัดการเหตุการณ์ คุณต้องใช้เมธอด `addEventListener()` ของหน้าต่างและให้พารามิเตอร์สองตัวเป็นอินพุต พารามิเตอร์แรกคือชื่อของเหตุการณ์ เช่น `keyup` พารามิเตอร์ที่สองคือฟังก์ชันที่จะถูกเรียกใช้เมื่อเหตุการณ์เกิดขึ้น

นี่คือตัวอย่าง:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

สำหรับเหตุการณ์คีย์ มีคุณสมบัติสองอย่างในเหตุการณ์ที่คุณสามารถใช้เพื่อดูว่าคีย์ใดถูกกด:

- `key` เป็นตัวแทนข้อความของคีย์ที่ถูกกด เช่น `ArrowUp`
- `keyCode` เป็นตัวแทนตัวเลข เช่น `37` ซึ่งสอดคล้องกับ `ArrowLeft`

✅ การจัดการเหตุการณ์คีย์มีประโยชน์นอกเหนือจากการพัฒนาเกม คุณคิดว่าเทคนิคนี้สามารถนำไปใช้ในด้านอื่นได้อย่างไร?

### คีย์พิเศษ: ข้อควรระวัง

มีคีย์ *พิเศษ* บางตัวที่ส่งผลต่อหน้าต่าง ซึ่งหมายความว่าหากคุณกำลังฟังเหตุการณ์ `keyup` และคุณใช้คีย์พิเศษเหล่านี้เพื่อเคลื่อนย้ายฮีโร่ของคุณ มันจะทำให้เกิดการเลื่อนแนวนอนด้วย ด้วยเหตุนี้ คุณอาจต้องการ *ปิด* พฤติกรรมเริ่มต้นของเบราว์เซอร์ในขณะที่คุณสร้างเกมของคุณ คุณต้องใช้โค้ดแบบนี้:

```javascript
let onKeyDown = function (e) {
  console.log(e.keyCode);
  switch (e.keyCode) {
    case 37:
    case 39:
    case 38:
    case 40: // Arrow keys
    case 32:
      e.preventDefault();
      break; // Space
    default:
      break; // do not block other keys
  }
};

window.addEventListener('keydown', onKeyDown);
```

โค้ดด้านบนจะทำให้คีย์ลูกศรและคีย์ Space มีพฤติกรรม *เริ่มต้น* ถูกปิด การปิดพฤติกรรมเกิดขึ้นเมื่อเราเรียก `e.preventDefault()`

## การเคลื่อนไหวที่เกิดจากเกม

เราสามารถทำให้สิ่งต่าง ๆ เคลื่อนไหวได้เองโดยใช้ตัวจับเวลา เช่น ฟังก์ชัน `setTimeout()` หรือ `setInterval()` ที่อัปเดตตำแหน่งของวัตถุในแต่ละช่วงเวลา นี่คือตัวอย่างโค้ด:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## วงลูปของเกม

วงลูปของเกมเป็นแนวคิดที่เป็นฟังก์ชันที่ถูกเรียกใช้ในช่วงเวลาปกติ มันถูกเรียกว่าวงลูปของเกมเพราะทุกสิ่งที่ควรมองเห็นได้สำหรับผู้ใช้จะถูกวาดในวงลูป วงลูปของเกมใช้วัตถุเกมทั้งหมดที่เป็นส่วนหนึ่งของเกม วาดทั้งหมด ยกเว้นในกรณีที่วัตถุไม่ควรเป็นส่วนหนึ่งของเกมอีกต่อไป ตัวอย่างเช่น หากวัตถุเป็นศัตรูที่ถูกเลเซอร์ยิงและระเบิด มันจะไม่เป็นส่วนหนึ่งของวงลูปเกมอีกต่อไป (คุณจะได้เรียนรู้เพิ่มเติมในบทเรียนถัดไป)

นี่คือตัวอย่างวงลูปของเกมในโค้ด:

```javascript
let gameLoopId = setInterval(() =>
  function gameLoop() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = "black";
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    drawHero();
    drawEnemies();
    drawStaticObjects();
}, 200);
```

วงลูปด้านบนจะถูกเรียกใช้ทุก ๆ `200` มิลลิวินาทีเพื่อวาดแคนวาส คุณสามารถเลือกช่วงเวลาที่เหมาะสมที่สุดสำหรับเกมของคุณ

## ดำเนินการสร้างเกมอวกาศต่อ

คุณจะนำโค้ดที่มีอยู่และขยายมันต่อไป คุณสามารถเริ่มต้นด้วยโค้ดที่คุณทำเสร็จในส่วนที่ I หรือใช้โค้ดใน [Part II- starter](../../../../6-space-game/3-moving-elements-around/your-work)

- **เคลื่อนย้ายฮีโร่**: คุณจะเพิ่มโค้ดเพื่อให้สามารถเคลื่อนย้ายฮีโร่โดยใช้คีย์ลูกศร
- **เคลื่อนย้ายศัตรู**: คุณจะต้องเพิ่มโค้ดเพื่อให้ศัตรูเคลื่อนที่จากบนลงล่างในอัตราที่กำหนด

## ขั้นตอนที่แนะนำ

ค้นหาไฟล์ที่ถูกสร้างไว้ให้คุณในโฟลเดอร์ `your-work` มันควรมีดังนี้:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

เริ่มโครงการของคุณในโฟลเดอร์ `your_work` โดยพิมพ์:

```bash
cd your-work
npm start
```

โค้ดด้านบนจะเริ่ม HTTP Server ที่ที่อยู่ `http://localhost:5000` เปิดเบราว์เซอร์และใส่ที่อยู่นั้น ตอนนี้มันควรแสดงฮีโร่และศัตรูทั้งหมด; แต่ยังไม่มีอะไรเคลื่อนไหว!

### เพิ่มโค้ด

1. **เพิ่มวัตถุเฉพาะ** สำหรับ `hero` และ `enemy` และ `game object` ซึ่งควรมีคุณสมบัติ `x` และ `y` (จำส่วน [Inheritance or composition](../README.md) )

   *คำแนะนำ* `game object` ควรเป็นวัตถุที่มี `x` และ `y` และความสามารถในการวาดตัวเองลงบนแคนวาส

   >คำแนะนำ: เริ่มต้นด้วยการเพิ่มคลาส GameObject ใหม่พร้อมตัวสร้างที่กำหนดไว้ดังนี้ และวาดมันลงบนแคนวาส:
  
    ```javascript
        
    class GameObject {
      constructor(x, y) {
        this.x = x;
        this.y = y;
        this.dead = false;
        this.type = "";
        this.width = 0;
        this.height = 0;
        this.img = undefined;
      }
    
      draw(ctx) {
        ctx.drawImage(this.img, this.x, this.y, this.width, this.height);
      }
    }
    ```

    จากนั้น ขยาย GameObject นี้เพื่อสร้าง Hero และ Enemy
    
    ```javascript
    class Hero extends GameObject {
      constructor(x, y) {
        ...it needs an x, y, type, and speed
      }
    }
    ```

    ```javascript
    class Enemy extends GameObject {
      constructor(x, y) {
        super(x, y);
        (this.width = 98), (this.height = 50);
        this.type = "Enemy";
        let id = setInterval(() => {
          if (this.y < canvas.height - this.height) {
            this.y += 5;
          } else {
            console.log('Stopped at', this.y)
            clearInterval(id);
          }
        }, 300)
      }
    }
    ```

2. **เพิ่มตัวจัดการเหตุการณ์คีย์** เพื่อจัดการการนำทางด้วยคีย์ (เคลื่อนย้ายฮีโร่ขึ้น/ลง ซ้าย/ขวา)

   *จำไว้* ว่ามันเป็นระบบคาร์ทีเซียน มุมบนซ้ายคือ `0,0` และอย่าลืมเพิ่มโค้ดเพื่อหยุด *พฤติกรรมเริ่มต้น*

   >คำแนะนำ: สร้างฟังก์ชัน onKeyDown ของคุณและเชื่อมต่อมันกับหน้าต่าง:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   ตรวจสอบคอนโซลของเบราว์เซอร์ ณ จุดนี้ และดูการกดคีย์ที่ถูกบันทึก

3. **นำไปใช้** [Pub sub pattern](../README.md) สิ่งนี้จะช่วยให้โค้ดของคุณสะอาดขึ้นเมื่อคุณทำตามส่วนที่เหลือ

   ในการทำส่วนสุดท้ายนี้ คุณสามารถ:

   1. **เพิ่มตัวฟังเหตุการณ์** บนหน้าต่าง:

       ```javascript
        window.addEventListener("keyup", (evt) => {
          if (evt.key === "ArrowUp") {
            eventEmitter.emit(Messages.KEY_EVENT_UP);
          } else if (evt.key === "ArrowDown") {
            eventEmitter.emit(Messages.KEY_EVENT_DOWN);
          } else if (evt.key === "ArrowLeft") {
            eventEmitter.emit(Messages.KEY_EVENT_LEFT);
          } else if (evt.key === "ArrowRight") {
            eventEmitter.emit(Messages.KEY_EVENT_RIGHT);
          }
        });
        ```

    1. **สร้างคลาส EventEmitter** เพื่อเผยแพร่และสมัครรับข้อความ:

        ```javascript
        class EventEmitter {
          constructor() {
            this.listeners = {};
          }
        
          on(message, listener) {
            if (!this.listeners[message]) {
              this.listeners[message] = [];
            }
            this.listeners[message].push(listener);
          }
        
          emit(message, payload = null) {
            if (this.listeners[message]) {
              this.listeners[message].forEach((l) => l(message, payload));
            }
          }
        }
        ```

    1. **เพิ่มค่าคงที่** และตั้งค่า EventEmitter:

        ```javascript
        const Messages = {
          KEY_EVENT_UP: "KEY_EVENT_UP",
          KEY_EVENT_DOWN: "KEY_EVENT_DOWN",
          KEY_EVENT_LEFT: "KEY_EVENT_LEFT",
          KEY_EVENT_RIGHT: "KEY_EVENT_RIGHT",
        };
        
        let heroImg, 
            enemyImg, 
            laserImg,
            canvas, ctx, 
            gameObjects = [], 
            hero, 
            eventEmitter = new EventEmitter();
        ```

    1. **เริ่มต้นเกม**

    ```javascript
    function initGame() {
      gameObjects = [];
      createEnemies();
      createHero();
    
      eventEmitter.on(Messages.KEY_EVENT_UP, () => {
        hero.y -=5 ;
      })
    
      eventEmitter.on(Messages.KEY_EVENT_DOWN, () => {
        hero.y += 5;
      });
    
      eventEmitter.on(Messages.KEY_EVENT_LEFT, () => {
        hero.x -= 5;
      });
    
      eventEmitter.on(Messages.KEY_EVENT_RIGHT, () => {
        hero.x += 5;
      });
    }
    ```

1. **ตั้งค่าวงลูปของเกม**

   ปรับปรุงฟังก์ชัน window.onload เพื่อเริ่มต้นเกมและตั้งค่าวงลูปของเกมในช่วงเวลาที่เหมาะสม คุณจะเพิ่มลำแสงเลเซอร์ด้วย:

    ```javascript
    window.onload = async () => {
      canvas = document.getElementById("canvas");
      ctx = canvas.getContext("2d");
      heroImg = await loadTexture("assets/player.png");
      enemyImg = await loadTexture("assets/enemyShip.png");
      laserImg = await loadTexture("assets/laserRed.png");
    
      initGame();
      let gameLoopId = setInterval(() => {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = "black";
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        drawGameObjects(ctx);
      }, 100)
      
    };
    ```

5. **เพิ่มโค้ด** เพื่อเคลื่อนย้ายศัตรูในช่วงเวลาที่กำหนด

    ปรับปรุงฟังก์ชัน `createEnemies()` เพื่อสร้างศัตรูและเพิ่มพวกมันลงในคลาส gameObjects ใหม่:

    ```javascript
    function createEnemies() {
      const MONSTER_TOTAL = 5;
      const MONSTER_WIDTH = MONSTER_TOTAL * 98;
      const START_X = (canvas.width - MONSTER_WIDTH) / 2;
      const STOP_X = START_X + MONSTER_WIDTH;
    
      for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          const enemy = new Enemy(x, y);
          enemy.img = enemyImg;
          gameObjects.push(enemy);
        }
      }
    }
    ```
    
    และเพิ่มฟังก์ชัน `createHero()` เพื่อทำกระบวนการคล้ายกันสำหรับฮีโร่
    
    ```javascript
    function createHero() {
      hero = new Hero(
        canvas.width / 2 - 45,
        canvas.height - canvas.height / 4
      );
      hero.img = heroImg;
      gameObjects.push(hero);
    }
    ```

    และสุดท้าย เพิ่มฟังก์ชัน `drawGameObjects()` เพื่อเริ่มการวาด:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    ศัตรูของคุณควรเริ่มเคลื่อนที่เข้าหายานอวกาศฮีโร่ของคุณ!

---

## 🚀 ความท้าทาย

อย่างที่คุณเห็น โค้ดของคุณอาจกลายเป็น 'โค้ดสปาเก็ตตี้' เมื่อคุณเริ่มเพิ่มฟังก์ชันและตัวแปรและคลาส คุณจะจัดระเบียบโค้ดของคุณให้ดีขึ้นเพื่อให้อ่านง่ายขึ้นได้อย่างไร? ลองร่างระบบเพื่อจัดระเบียบโค้ดของคุณ แม้ว่ามันจะยังอยู่ในไฟล์เดียว

## แบบทดสอบหลังเรียน

[แบบทดสอบหลังเรียน](https://ff-quizzes.netlify.app/web/quiz/34)

## ทบทวนและศึกษาด้วยตนเอง

แม้ว่าเราจะเขียนเกมของเราโดยไม่ใช้เฟรมเวิร์ก แต่มีเฟรมเวิร์ก Canvas ที่ใช้ JavaScript สำหรับการพัฒนาเกมมากมาย ใช้เวลาสักครู่เพื่อ [อ่านเกี่ยวกับสิ่งเหล่านี้](https://github.com/collections/javascript-game-engines)

## งานที่ได้รับมอบหมาย

[แสดงความคิดเห็นในโค้ดของคุณ](assignment.md)

---

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามอย่างเต็มที่เพื่อให้การแปลมีความถูกต้อง แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่แม่นยำ เอกสารต้นฉบับในภาษาต้นทางควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ แนะนำให้ใช้บริการแปลภาษามนุษย์ที่เป็นมืออาชีพ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความที่ผิดพลาดซึ่งเกิดจากการใช้การแปลนี้