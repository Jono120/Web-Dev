<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-29T07:34:13+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "th"
}
-->
# สร้างเกมอวกาศ ตอนที่ 6: จบเกมและเริ่มใหม่

## แบบทดสอบก่อนเรียน

[แบบทดสอบก่อนเรียน](https://ff-quizzes.netlify.app/web/quiz/39)

มีหลายวิธีในการกำหนด *เงื่อนไขการจบเกม* ในเกม ขึ้นอยู่กับคุณในฐานะผู้สร้างเกมที่จะกำหนดว่าเกมจะจบลงเมื่อใด ต่อไปนี้เป็นเหตุผลบางประการ หากเราสมมติว่าเรากำลังพูดถึงเกมอวกาศที่คุณสร้างมาจนถึงตอนนี้:

- **ทำลายยานศัตรู `N` ลำ**: เป็นเรื่องปกติที่หากคุณแบ่งเกมออกเป็นด่านต่าง ๆ คุณอาจต้องทำลายยานศัตรู `N` ลำเพื่อผ่านด่าน
- **ยานของคุณถูกทำลาย**: มีเกมหลายเกมที่คุณจะแพ้ทันทีหากยานของคุณถูกทำลาย อีกวิธีที่พบบ่อยคือการมีระบบชีวิต (Lives) ทุกครั้งที่ยานของคุณถูกทำลายจะลดจำนวนชีวิตลง และเมื่อชีวิตหมด คุณจะแพ้เกม
- **เก็บคะแนน `N` คะแนน**: อีกเงื่อนไขการจบเกมที่พบบ่อยคือการเก็บคะแนน คุณจะได้คะแนนจากกิจกรรมต่าง ๆ เช่น การทำลายยานศัตรู หรือการเก็บไอเท็มที่ศัตรูทิ้งไว้เมื่อถูกทำลาย
- **ผ่านด่าน**: อาจมีเงื่อนไขหลายอย่าง เช่น ทำลายยานศัตรู `X` ลำ เก็บคะแนน `Y` คะแนน หรือเก็บไอเท็มเฉพาะ

## การเริ่มใหม่

หากผู้เล่นสนุกกับเกมของคุณ พวกเขาอาจต้องการเล่นซ้ำ เมื่อเกมจบลงไม่ว่าจะด้วยเหตุผลใด คุณควรมีตัวเลือกให้เริ่มเกมใหม่

✅ ลองคิดดูว่าคุณอยากให้เกมจบลงในเงื่อนไขใด และคุณจะกระตุ้นให้ผู้เล่นเริ่มเกมใหม่อย่างไร

## สิ่งที่ต้องสร้าง

คุณจะเพิ่มกฎเหล่านี้ในเกมของคุณ:

1. **ชนะเกม**: เมื่อยานศัตรูทั้งหมดถูกทำลาย คุณจะชนะเกม และแสดงข้อความแสดงความยินดี
1. **เริ่มใหม่**: เมื่อชีวิตของคุณหมดหรือเกมจบลง คุณควรมีตัวเลือกให้เริ่มเกมใหม่ อย่าลืม! คุณต้องรีเซ็ตเกมและล้างสถานะเกมก่อนหน้า

## ขั้นตอนที่แนะนำ

ค้นหาไฟล์ที่ถูกสร้างไว้ให้คุณในโฟลเดอร์ `your-work` ซึ่งควรมีไฟล์ดังนี้:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
  -| life.png
-| index.html
-| app.js
-| package.json
```

เริ่มโปรเจกต์ของคุณในโฟลเดอร์ `your_work` โดยพิมพ์:

```bash
cd your-work
npm start
```

คำสั่งข้างต้นจะเริ่ม HTTP Server ที่อยู่ `http://localhost:5000` เปิดเบราว์เซอร์และใส่ที่อยู่นี้ เกมของคุณควรอยู่ในสถานะที่สามารถเล่นได้

> เคล็ดลับ: เพื่อหลีกเลี่ยงคำเตือนใน Visual Studio Code ให้แก้ไขฟังก์ชัน `window.onload` เพื่อเรียก `gameLoopId` โดยไม่ต้องใช้ `let` และประกาศตัวแปร `gameLoopId` ไว้ที่ด้านบนของไฟล์: `let gameLoopId;`

### เพิ่มโค้ด

1. **ติดตามเงื่อนไขการจบเกม**: เพิ่มโค้ดที่ติดตามจำนวนศัตรู หรือหากยานของฮีโร่ถูกทำลาย โดยเพิ่มฟังก์ชันสองตัวนี้:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **เพิ่มตรรกะในตัวจัดการข้อความ**: แก้ไข `eventEmitter` เพื่อจัดการเงื่อนไขเหล่านี้:

    ```javascript
    eventEmitter.on(Messages.COLLISION_ENEMY_LASER, (_, { first, second }) => {
        first.dead = true;
        second.dead = true;
        hero.incrementPoints();

        if (isEnemiesDead()) {
          eventEmitter.emit(Messages.GAME_END_WIN);
        }
    });

    eventEmitter.on(Messages.COLLISION_ENEMY_HERO, (_, { enemy }) => {
        enemy.dead = true;
        hero.decrementLife();
        if (isHeroDead())  {
          eventEmitter.emit(Messages.GAME_END_LOSS);
          return; // loss before victory
        }
        if (isEnemiesDead()) {
          eventEmitter.emit(Messages.GAME_END_WIN);
        }
    });
    
    eventEmitter.on(Messages.GAME_END_WIN, () => {
        endGame(true);
    });
      
    eventEmitter.on(Messages.GAME_END_LOSS, () => {
      endGame(false);
    });
    ```

1. **เพิ่มประเภทข้อความใหม่**: เพิ่มข้อความเหล่านี้ในวัตถุ constants:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **เพิ่มโค้ดเริ่มใหม่**: เพิ่มโค้ดที่เริ่มเกมใหม่เมื่อกดปุ่มที่กำหนด

   1. **ฟังการกดปุ่ม `Enter`**: แก้ไข eventListener ของหน้าต่างให้ฟังการกดปุ่มนี้:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **เพิ่มข้อความเริ่มใหม่**: เพิ่มข้อความนี้ใน constants ของ Messages:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **นำกฎของเกมไปใช้**: นำกฎของเกมต่อไปนี้ไปใช้:

   1. **เงื่อนไขชนะของผู้เล่น**: เมื่อยานศัตรูทั้งหมดถูกทำลาย ให้แสดงข้อความแสดงความยินดี

      1. ก่อนอื่น สร้างฟังก์ชัน `displayMessage()`:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. สร้างฟังก์ชัน `endGame()`:

        ```javascript
        function endGame(win) {
          clearInterval(gameLoopId);
        
          // set a delay so we are sure any paints have finished
          setTimeout(() => {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = "black";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            if (win) {
              displayMessage(
                "Victory!!! Pew Pew... - Press [Enter] to start a new game Captain Pew Pew",
                "green"
              );
            } else {
              displayMessage(
                "You died !!! Press [Enter] to start a new game Captain Pew Pew"
              );
            }
          }, 200)  
        }
        ```

   1. **ตรรกะการเริ่มใหม่**: เมื่อชีวิตหมดหรือผู้เล่นชนะเกม ให้แสดงข้อความว่าเกมสามารถเริ่มใหม่ได้ และเริ่มเกมใหม่เมื่อกดปุ่ม *เริ่มใหม่* (คุณสามารถกำหนดปุ่มเองได้)

      1. สร้างฟังก์ชัน `resetGame()`:

        ```javascript
        function resetGame() {
          if (gameLoopId) {
            clearInterval(gameLoopId);
            eventEmitter.clear();
            initGame();
            gameLoopId = setInterval(() => {
              ctx.clearRect(0, 0, canvas.width, canvas.height);
              ctx.fillStyle = "black";
              ctx.fillRect(0, 0, canvas.width, canvas.height);
              drawPoints();
              drawLife();
              updateGameObjects();
              drawGameObjects(ctx);
            }, 100);
          }
        }
        ```

     1. เพิ่มการเรียก `eventEmitter` เพื่อรีเซ็ตเกมใน `initGame()`:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. เพิ่มฟังก์ชัน `clear()` ใน EventEmitter:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 ยินดีด้วย กัปตัน! เกมของคุณเสร็จสมบูรณ์แล้ว! ทำได้ดีมาก! 🚀 💥 👽

---

## 🚀 ความท้าทาย

เพิ่มเสียง! คุณสามารถเพิ่มเสียงเพื่อเพิ่มความสนุกในการเล่นเกม เช่น เมื่อยิงเลเซอร์โดนเป้าหมาย หรือเมื่อฮีโร่แพ้หรือชนะ ลองดู [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) นี้เพื่อเรียนรู้วิธีเล่นเสียงด้วย JavaScript

## แบบทดสอบหลังเรียน

[แบบทดสอบหลังเรียน](https://ff-quizzes.netlify.app/web/quiz/40)

## ทบทวนและศึกษาด้วยตัวเอง

งานของคุณคือการสร้างตัวอย่างเกมใหม่ ลองสำรวจเกมที่น่าสนใจต่าง ๆ เพื่อดูว่าคุณอาจสร้างเกมประเภทใดได้บ้าง

## งานที่ได้รับมอบหมาย

[สร้างตัวอย่างเกม](assignment.md)

---

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามให้การแปลมีความถูกต้อง แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่แม่นยำ เอกสารต้นฉบับในภาษาต้นทางควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ ขอแนะนำให้ใช้บริการแปลภาษามนุษย์ที่เป็นมืออาชีพ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความที่ผิดพลาดซึ่งเกิดจากการใช้การแปลนี้