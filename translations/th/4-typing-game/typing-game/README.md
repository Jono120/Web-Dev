<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1b0aeccb600f83c603cd70cb42df594d",
  "translation_date": "2025-08-29T07:41:45+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "th"
}
-->
# การสร้างเกมโดยใช้เหตุการณ์

## แบบทดสอบก่อนการบรรยาย

[แบบทดสอบก่อนการบรรยาย](https://ff-quizzes.netlify.app/web/quiz/21)

## การเขียนโปรแกรมแบบขับเคลื่อนด้วยเหตุการณ์

เมื่อเราสร้างแอปพลิเคชันบนเบราว์เซอร์ เราจะต้องสร้างส่วนติดต่อผู้ใช้แบบกราฟิก (GUI) เพื่อให้ผู้ใช้สามารถโต้ตอบกับสิ่งที่เราสร้างขึ้นได้ วิธีที่พบบ่อยที่สุดในการโต้ตอบกับเบราว์เซอร์คือการคลิกและพิมพ์ในองค์ประกอบต่างๆ ความท้าทายที่เราต้องเผชิญในฐานะนักพัฒนาคือ เราไม่รู้ว่าผู้ใช้จะทำสิ่งเหล่านี้เมื่อใด!

[การเขียนโปรแกรมแบบขับเคลื่อนด้วยเหตุการณ์](https://en.wikipedia.org/wiki/Event-driven_programming) คือชื่อของการเขียนโปรแกรมประเภทที่เราต้องใช้เพื่อสร้าง GUI ของเรา หากเราลองแยกวลีนี้ออก เราจะพบคำสำคัญคือ **เหตุการณ์** [เหตุการณ์](https://www.merriam-webster.com/dictionary/event) ตามที่ Merriam-Webster ให้คำจำกัดความไว้ว่า "สิ่งที่เกิดขึ้น" ซึ่งอธิบายสถานการณ์ของเราได้อย่างสมบูรณ์แบบ เรารู้ว่าสิ่งหนึ่งจะเกิดขึ้นที่เราต้องการให้โค้ดตอบสนอง แต่เราไม่รู้ว่ามันจะเกิดขึ้นเมื่อใด

วิธีที่เราระบุส่วนของโค้ดที่เราต้องการให้ทำงานคือการสร้างฟังก์ชัน เมื่อเราพูดถึง [การเขียนโปรแกรมเชิงกระบวนการ](https://en.wikipedia.org/wiki/Procedural_programming) ฟังก์ชันจะถูกเรียกใช้งานตามลำดับที่กำหนดไว้ สิ่งนี้จะเป็นจริงในกรณีของการเขียนโปรแกรมแบบขับเคลื่อนด้วยเหตุการณ์เช่นกัน ความแตกต่างคือ **วิธีการ** ที่ฟังก์ชันจะถูกเรียกใช้งาน

เพื่อจัดการกับเหตุการณ์ (การคลิกปุ่ม การพิมพ์ ฯลฯ) เราจะลงทะเบียน **ตัวฟังเหตุการณ์** ตัวฟังเหตุการณ์คือตัวฟังก์ชันที่รอให้เหตุการณ์เกิดขึ้นและทำงานเพื่อตอบสนอง ตัวฟังเหตุการณ์สามารถอัปเดต UI เรียกใช้เซิร์ฟเวอร์ หรือทำสิ่งอื่นๆ ที่จำเป็นเพื่อตอบสนองต่อการกระทำของผู้ใช้ เราสามารถเพิ่มตัวฟังเหตุการณ์ได้โดยใช้ [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) และส่งฟังก์ชันที่ต้องการให้ทำงาน

> **NOTE:** ควรสังเกตว่ามีหลายวิธีในการสร้างตัวฟังเหตุการณ์ คุณสามารถใช้ฟังก์ชันนิรนามหรือสร้างฟังก์ชันที่มีชื่อได้ คุณยังสามารถใช้ทางลัดต่างๆ เช่น การตั้งค่าคุณสมบัติ `click` หรือใช้ `addEventListener` ในการฝึกนี้ เราจะมุ่งเน้นไปที่ `addEventListener` และฟังก์ชันนิรนาม เนื่องจากเป็นเทคนิคที่นักพัฒนาเว็บใช้บ่อยที่สุด และยังมีความยืดหยุ่นมากที่สุด เพราะ `addEventListener` ใช้ได้กับทุกเหตุการณ์ และสามารถระบุชื่อเหตุการณ์เป็นพารามิเตอร์ได้

### เหตุการณ์ที่พบบ่อย

มี [เหตุการณ์มากมาย](https://developer.mozilla.org/docs/Web/Events) ที่คุณสามารถฟังได้เมื่อสร้างแอปพลิเคชัน โดยพื้นฐานแล้ว ทุกสิ่งที่ผู้ใช้ทำบนหน้าเว็บจะทำให้เกิดเหตุการณ์ ซึ่งช่วยให้คุณมีพลังมากมายในการสร้างประสบการณ์ที่คุณต้องการให้ผู้ใช้ได้รับ โชคดีที่โดยปกติคุณจะต้องใช้เหตุการณ์เพียงไม่กี่อย่าง นี่คือตัวอย่างเหตุการณ์ที่พบบ่อย (รวมถึงสองเหตุการณ์ที่เราจะใช้ในการสร้างเกมของเรา):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): ผู้ใช้คลิกบางสิ่ง เช่น ปุ่มหรือไฮเปอร์ลิงก์
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): ผู้ใช้คลิกปุ่มเมาส์ขวา
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): ผู้ใช้ไฮไลต์ข้อความบางส่วน
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): ผู้ใช้ป้อนข้อความ

## การสร้างเกม

เราจะสร้างเกมเพื่อสำรวจว่าเหตุการณ์ทำงานอย่างไรใน JavaScript เกมของเราจะทดสอบทักษะการพิมพ์ของผู้เล่น ซึ่งเป็นหนึ่งในทักษะที่ถูกมองข้ามมากที่สุดที่นักพัฒนาทุกคนควรมี เราทุกคนควรฝึกฝนการพิมพ์! ลำดับทั่วไปของเกมจะเป็นดังนี้:

- ผู้เล่นคลิกปุ่มเริ่มและได้รับข้อความให้พิมพ์
- ผู้เล่นพิมพ์ข้อความให้เร็วที่สุดในกล่องข้อความ
  - เมื่อพิมพ์แต่ละคำเสร็จ คำถัดไปจะถูกไฮไลต์
  - หากผู้เล่นพิมพ์ผิด กล่องข้อความจะเปลี่ยนเป็นสีแดง
  - เมื่อผู้เล่นพิมพ์ข้อความเสร็จ จะมีข้อความแสดงความสำเร็จพร้อมเวลาที่ใช้

มาเริ่มสร้างเกมของเราและเรียนรู้เกี่ยวกับเหตุการณ์กันเถอะ!

### โครงสร้างไฟล์

เราจะต้องใช้ไฟล์ทั้งหมดสามไฟล์: **index.html**, **script.js** และ **style.css** มาเริ่มตั้งค่าไฟล์เหล่านี้เพื่อให้งานของเราง่ายขึ้น

- สร้างโฟลเดอร์ใหม่สำหรับงานของคุณโดยเปิดคอนโซลหรือหน้าต่างเทอร์มินัลและใช้คำสั่งต่อไปนี้:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- เปิด Visual Studio Code

```bash
code .
```

- เพิ่มไฟล์สามไฟล์ในโฟลเดอร์ใน Visual Studio Code โดยตั้งชื่อดังนี้:
  - index.html
  - script.js
  - style.css

## สร้างส่วนติดต่อผู้ใช้

หากเราสำรวจข้อกำหนด เราจะรู้ว่าเราต้องการองค์ประกอบบางอย่างในหน้า HTML ของเรา สิ่งนี้คล้ายกับสูตรอาหารที่เราต้องการส่วนผสมบางอย่าง:

- พื้นที่สำหรับแสดงข้อความที่ผู้ใช้ต้องพิมพ์
- พื้นที่สำหรับแสดงข้อความ เช่น ข้อความแสดงความสำเร็จ
- กล่องข้อความสำหรับการพิมพ์
- ปุ่มเริ่ม

องค์ประกอบแต่ละอย่างจะต้องมี ID เพื่อให้เราสามารถทำงานกับมันใน JavaScript ของเราได้ นอกจากนี้เรายังจะเพิ่มการอ้างอิงไปยังไฟล์ CSS และ JavaScript ที่เราจะสร้าง

สร้างไฟล์ใหม่ชื่อ **index.html** และเพิ่ม HTML ต่อไปนี้:

```html
<!-- inside index.html -->
<html>
<head>
  <title>Typing game</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Typing game!</h1>
  <p>Practice your typing skills with a quote from Sherlock Holmes. Click **start** to begin!</p>
  <p id="quote"></p> <!-- This will display our quote -->
  <p id="message"></p> <!-- This will display any status messages -->
  <div>
    <input type="text" aria-label="current word" id="typed-value" /> <!-- The textbox for typing -->
    <button type="button" id="start">Start</button> <!-- To start the game -->
  </div>
  <script src="script.js"></script>
</body>
</html>
```

### เปิดแอปพลิเคชัน

การพัฒนาแบบวนซ้ำเพื่อดูว่าทุกอย่างดูเป็นอย่างไรเป็นสิ่งที่ดีที่สุดเสมอ มาเปิดแอปพลิเคชันของเรากัน มีส่วนขยายที่ยอดเยี่ยมสำหรับ Visual Studio Code ชื่อ [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) ซึ่งจะโฮสต์แอปพลิเคชันของคุณในเครื่องและรีเฟรชเบราว์เซอร์ทุกครั้งที่คุณบันทึก

- ติดตั้ง [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) โดยทำตามลิงก์และคลิก **Install**
  - เบราว์เซอร์จะขอให้คุณเปิด Visual Studio Code และ Visual Studio Code จะขอให้คุณดำเนินการติดตั้ง
  - รีสตาร์ท Visual Studio Code หากได้รับแจ้ง
- เมื่อติดตั้งแล้ว ใน Visual Studio Code ให้คลิก Ctrl-Shift-P (หรือ Cmd-Shift-P) เพื่อเปิดคำสั่งพาเลต
- พิมพ์ **Live Server: Open with Live Server**
  - Live Server จะเริ่มโฮสต์แอปพลิเคชันของคุณ
- เปิดเบราว์เซอร์และไปที่ **https://localhost:5500**
- ตอนนี้คุณควรเห็นหน้าที่คุณสร้างขึ้น!

มาเพิ่มฟังก์ชันการทำงานกันเถอะ

## เพิ่ม CSS

เมื่อเราได้สร้าง HTML แล้ว มาเพิ่ม CSS สำหรับการจัดรูปแบบหลัก เราจำเป็นต้องไฮไลต์คำที่ผู้เล่นควรพิมพ์ และเปลี่ยนสีของกล่องข้อความหากสิ่งที่พวกเขาพิมพ์ไม่ถูกต้อง เราจะทำสิ่งนี้ด้วยสองคลาส

สร้างไฟล์ใหม่ชื่อ **style.css** และเพิ่มไวยากรณ์ต่อไปนี้:

```css
/* inside style.css */
.highlight {
  background-color: yellow;
}

.error {
  background-color: lightcoral;
  border: red;
}
```

✅ สำหรับ CSS คุณสามารถจัดวางหน้าเว็บของคุณในแบบที่คุณต้องการ ใช้เวลาสักครู่เพื่อทำให้หน้าดูสวยงามขึ้น:

- เลือกฟอนต์ที่แตกต่าง
- เพิ่มสีให้กับหัวข้อ
- ปรับขนาดองค์ประกอบ

## JavaScript

เมื่อเราได้สร้าง UI แล้ว ถึงเวลาที่จะมุ่งเน้นไปที่ JavaScript ซึ่งจะให้ตรรกะของเกม เราจะแบ่งสิ่งนี้ออกเป็นขั้นตอนเล็กๆ:

- [สร้างค่าคงที่](../../../../4-typing-game/typing-game)
- [ตัวฟังเหตุการณ์สำหรับเริ่มเกม](../../../../4-typing-game/typing-game)
- [ตัวฟังเหตุการณ์สำหรับการพิมพ์](../../../../4-typing-game/typing-game)

แต่ก่อนอื่น สร้างไฟล์ใหม่ชื่อ **script.js**

### สร้างค่าคงที่

เราจะต้องใช้บางรายการเพื่อให้งานเขียนโปรแกรมของเราง่ายขึ้น เช่นเดียวกับสูตรอาหาร นี่คือสิ่งที่เราต้องการ:

- อาร์เรย์ที่มีรายการข้อความทั้งหมด
- อาร์เรย์ว่างเปล่าสำหรับเก็บคำทั้งหมดในข้อความปัจจุบัน
- พื้นที่สำหรับเก็บดัชนีของคำที่ผู้เล่นกำลังพิมพ์
- เวลาที่ผู้เล่นคลิกเริ่ม

เรายังต้องการการอ้างอิงถึงองค์ประกอบ UI:

- กล่องข้อความ (**typed-value**)
- การแสดงข้อความ (**quote**)
- ข้อความ (**message**)

```javascript
// inside script.js
// all of our quotes
const quotes = [
    'When you have eliminated the impossible, whatever remains, however improbable, must be the truth.',
    'There is nothing more deceptive than an obvious fact.',
    'I ought to know by this time that when a fact appears to be opposed to a long train of deductions it invariably proves to be capable of bearing some other interpretation.',
    'I never make exceptions. An exception disproves the rule.',
    'What one man can invent another can discover.',
    'Nothing clears up a case so much as stating it to another person.',
    'Education never ends, Watson. It is a series of lessons, with the greatest for the last.',
];
// store the list of words and the index of the word the player is currently typing
let words = [];
let wordIndex = 0;
// the starting time
let startTime = Date.now();
// page elements
const quoteElement = document.getElementById('quote');
const messageElement = document.getElementById('message');
const typedValueElement = document.getElementById('typed-value');
```

✅ ลองเพิ่มข้อความเพิ่มเติมในเกมของคุณ

> **NOTE:** เราสามารถดึงองค์ประกอบได้ทุกเมื่อในโค้ดโดยใช้ `document.getElementById` เนื่องจากเราจะอ้างถึงองค์ประกอบเหล่านี้เป็นประจำ เราจะหลีกเลี่ยงข้อผิดพลาดจากการพิมพ์ผิดด้วยการใช้ค่าคงที่ เฟรมเวิร์กอย่าง [Vue.js](https://vuejs.org/) หรือ [React](https://reactjs.org/) สามารถช่วยคุณจัดการโค้ดได้ดียิ่งขึ้น

ใช้เวลาสักครู่เพื่อดูวิดีโอเกี่ยวกับการใช้ `const`, `let` และ `var`

[![ประเภทของตัวแปร](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "ประเภทของตัวแปร")

> 🎥 คลิกที่ภาพด้านบนเพื่อดูวิดีโอเกี่ยวกับตัวแปร

### เพิ่มตรรกะการเริ่มต้น

ในการเริ่มเกม ผู้เล่นจะคลิกปุ่มเริ่ม แน่นอนว่าเราไม่รู้ว่าพวกเขาจะคลิกเมื่อใด นี่คือจุดที่ [ตัวฟังเหตุการณ์](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) มีบทบาท ตัวฟังเหตุการณ์จะช่วยให้เราฟังบางสิ่งที่เกิดขึ้น (เหตุการณ์) และทำงานโค้ดเพื่อตอบสนอง ในกรณีของเรา เราต้องการให้โค้ดทำงานเมื่อผู้ใช้คลิกเริ่ม

เมื่อผู้ใช้คลิก **เริ่ม** เราจำเป็นต้องเลือกข้อความ ตั้งค่า UI และตั้งค่าการติดตามคำปัจจุบันและเวลา ด้านล่างนี้คือ JavaScript ที่คุณต้องเพิ่ม เราจะอธิบายหลังจากบล็อกโค้ด

```javascript
// at the end of script.js
document.getElementById('start').addEventListener('click', () => {
  // get a quote
  const quoteIndex = Math.floor(Math.random() * quotes.length);
  const quote = quotes[quoteIndex];
  // Put the quote into an array of words
  words = quote.split(' ');
  // reset the word index for tracking
  wordIndex = 0;

  // UI updates
  // Create an array of span elements so we can set a class
  const spanWords = words.map(function(word) { return `<span>${word} </span>`});
  // Convert into string and set as innerHTML on quote display
  quoteElement.innerHTML = spanWords.join('');
  // Highlight the first word
  quoteElement.childNodes[0].className = 'highlight';
  // Clear any prior messages
  messageElement.innerText = '';

  // Setup the textbox
  // Clear the textbox
  typedValueElement.value = '';
  // set focus
  typedValueElement.focus();
  // set the event handler

  // Start the timer
  startTime = new Date().getTime();
});
```

มาแยกโค้ดกันดู!

- ตั้งค่าการติดตามคำ
  - ใช้ [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) และ [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) เพื่อสุ่มเลือกข้อความจากอาร์เรย์ `quotes`
  - แปลง `quote` เป็นอาร์เรย์ของ `words` เพื่อให้เราสามารถติดตามคำที่ผู้เล่นกำลังพิมพ์
  - ตั้งค่า `wordIndex` เป็น 0 เนื่องจากผู้เล่นจะเริ่มที่คำแรก
- ตั้งค่า UI
  - สร้างอาร์เรย์ `spanWords` ซึ่งมีแต่ละคำในองค์ประกอบ `span`
    - สิ่งนี้จะช่วยให้เราไฮไลต์คำบนหน้าจอ
  - `join` อาร์เรย์เพื่อสร้างสตริงที่เราสามารถใช้เพื่ออัปเดต `innerHTML` บน `quoteElement`
    - สิ่งนี้จะแสดงข้อความให้ผู้เล่นเห็น
  - ตั้งค่า `className` ของ `span` แรกเป็น `highlight` เพื่อไฮไลต์เป็นสีเหลือง
  - ล้าง `messageElement` โดยตั้งค่า `innerText` เป็น `''`
- ตั้งค่ากล่องข้อความ
  - ล้างค่า `value` ปัจจุบันบน `typedValueElement`
  - ตั้งค่า `focus` ไปที่ `typedValueElement`
- เริ่มตัวจับเวลาโดยเรียก `getTime`

### เพิ่มตรรกะการพิมพ์

เมื่อผู้เล่นพิมพ์ จะมีการเรียกเหตุการณ์ `input` ตัวฟังเหตุการณ์นี้จะตรวจสอบให้แน่ใจว่าผู้เล่นพิมพ์คำถูกต้อง และจัดการสถานะปัจจุบันของเกม กลับไปที่ **script.js** และเพิ่มโค้ดต่อไปนี้ที่ท้ายไฟล์ เราจะอธิบายหลังจากนั้น

```javascript
// at the end of script.js
typedValueElement.addEventListener('input', () => {
  // Get the current word
  const currentWord = words[wordIndex];
  // get the current value
  const typedValue = typedValueElement.value;

  if (typedValue === currentWord && wordIndex === words.length - 1) {
    // end of sentence
    // Display success
    const elapsedTime = new Date().getTime() - startTime;
    const message = `CONGRATULATIONS! You finished in ${elapsedTime / 1000} seconds.`;
    messageElement.innerText = message;
  } else if (typedValue.endsWith(' ') && typedValue.trim() === currentWord) {
    // end of word
    // clear the typedValueElement for the new word
    typedValueElement.value = '';
    // move to the next word
    wordIndex++;
    // reset the class name for all elements in quote
    for (const wordElement of quoteElement.childNodes) {
      wordElement.className = '';
    }
    // highlight the new word
    quoteElement.childNodes[wordIndex].className = 'highlight';
  } else if (currentWord.startsWith(typedValue)) {
    // currently correct
    // highlight the next word
    typedValueElement.className = '';
  } else {
    // error state
    typedValueElement.className = 'error';
  }
});
```

มาแยกโค้ดกันดู! เราเริ่มต้นด้วยการดึงคำปัจจุบันและค่าที่ผู้เล่นพิมพ์มาจนถึงตอนนี้ จากนั้นเราจะตรวจสอบตามลำดับว่า ข้อความเสร็จสมบูรณ์หรือไม่ คำเสร็จสมบูรณ์หรือไม่ คำถูกต้องหรือไม่ หรือสุดท้าย มีข้อผิดพลาดหรือไม่

- ข้อความเสร็จสมบูรณ์ ซึ่งระบุโดย `typedValue` เท่ากับ `currentWord` และ `wordIndex` เท่ากับหนึ่งน้อยกว่าความยาวของ `words`
  - คำนวณ `elapsedTime` โดยลบ `startTime` ออกจากเวลาปัจจุบัน
  - หาร `elapsedTime` ด้วย 1,000 เพื่อแปลงจากมิลลิวินาทีเป็นวินาที
  - แสดงข้อความแสดงความสำเร็จ
- คำเสร็จสมบูรณ์ ซึ่งระบุโดย `typedValue` ลงท้ายด้วยช่องว่าง (จบคำ) และ `typedValue` เท่ากับ `currentWord`
  - ตั้งค่า `value` บน `typedElement` เป็น `''` เพื่อให้พิมพ์คำถัดไปได้
  - เพิ่มค่า `wordIndex` เพื่อย้ายไปยังคำถัดไป
  - วนลูปผ่าน `childNodes` ทั้งหมดของ `quoteElement` เพื่อตั้งค่า `className` เป็น `''` เพื่อกลับไปยังการแสดงผลเริ่มต้น
  - ตั้งค่า `className` ของคำปัจจุบันเป็น `highlight` เพื่อระบุว่าเป็นคำถัดไปที่ต้องพิมพ์
- คำที่พิมพ์ถูกต้องในปัจจุบัน (แต่ยังไม่เสร็จสมบูรณ์) ซึ่งระบุโดย `currentWord` เริ่มต้นด้วย `typedValue`
  - ตรวจสอบให้แน่ใจว่า `typedValueElement` แสดงผลเป็นค่าเริ่มต้นโดยการล้าง `className`
- หากมาถึงจุดนี้ แสดงว่ามีข้อผิดพลาด
  - ตั้งค่า `className` บน `typedValueElement` เป็น `error`

## ทดสอบแอปพลิเคชันของคุณ

คุณมาถึงจุดสิ้นสุดแล้ว! ขั้นตอนสุดท้ายคือการตรวจสอบว่าแอปพลิเคชันของคุณทำงานหรือไม่ ลองเล่นดู! ไม่ต้องกังวลหากมีข้อผิดพลาด **นักพัฒนาทุกคน** มีข้อผิดพลาด ตรวจสอบข้อความและแก้ไขข้อผิดพลาดตามความจำเป็น

คลิกที่ **เริ่ม** และเริ่มพิมพ์! มันควรจะดูเหมือนกับแอนิเมชันที่เราเห็นก่อนหน้านี้

![แอนิเมชันของเกมที่กำลังทำงาน](../../../../4-typing-game/images/demo.gif)

---

## 🚀 ความท้าทาย

เพิ่มฟังก์ชันการทำงานเพิ่มเติม

- ปิดใช้งานตัวฟังเหตุการณ์ `input` เมื่อเกมเสร็จสิ้น และเปิดใช้งานอีกครั้งเมื่อคลิกปุ่ม
- ปิดใช้งานกล่องข้อความเมื่อผู้เล่นพิมพ์ข้อความเสร็จ
- แสดงกล่องข้อความแบบโมดอลพร้อมข้อความแสดงความสำเร็จ
- เก็บคะแนนสูงสุดโดยใช้ [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)
## แบบทดสอบหลังการบรรยาย

[แบบทดสอบหลังการบรรยาย](https://ff-quizzes.netlify.app/web/quiz/22)

## ทบทวนและศึกษาด้วยตนเอง

ศึกษาเพิ่มเติมเกี่ยวกับ [เหตุการณ์ทั้งหมดที่มีให้ใช้งาน](https://developer.mozilla.org/docs/Web/Events) สำหรับนักพัฒนาผ่านเว็บเบราว์เซอร์ และพิจารณาสถานการณ์ที่คุณจะใช้แต่ละเหตุการณ์

## งานที่ได้รับมอบหมาย

[สร้างเกมคีย์บอร์ดใหม่](assignment.md)

---

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามให้การแปลมีความถูกต้องมากที่สุด แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่ถูกต้อง เอกสารต้นฉบับในภาษาดั้งเดิมควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ ขอแนะนำให้ใช้บริการแปลภาษามืออาชีพ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความผิดที่เกิดจากการใช้การแปลนี้