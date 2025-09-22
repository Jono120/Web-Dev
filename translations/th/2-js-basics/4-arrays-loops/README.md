<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "9029f96b0e034839c1799f4595e4bb66",
  "translation_date": "2025-08-29T07:36:52+00:00",
  "source_file": "2-js-basics/4-arrays-loops/README.md",
  "language_code": "th"
}
-->
# พื้นฐาน JavaScript: อาเรย์และลูป

![JavaScript Basics - Arrays](../../../../translated_images/webdev101-js-arrays.439d7528b8a294558d0e4302e448d193f8ad7495cc407539cc81f1afe904b470.th.png)
> สเก็ตโน้ตโดย [Tomomi Imura](https://twitter.com/girlie_mac)

## แบบทดสอบก่อนเรียน
[แบบทดสอบก่อนเรียน](https://ff-quizzes.netlify.app/web/quiz/13)

บทเรียนนี้ครอบคลุมพื้นฐานของ JavaScript ซึ่งเป็นภาษาที่ช่วยเพิ่มความสามารถในการโต้ตอบบนเว็บ ในบทเรียนนี้ คุณจะได้เรียนรู้เกี่ยวกับอาเรย์และลูป ซึ่งใช้ในการจัดการข้อมูล

[![Arrays](https://img.youtube.com/vi/1U4qTyq02Xw/0.jpg)](https://youtube.com/watch?v=1U4qTyq02Xw "Arrays")

[![Loops](https://img.youtube.com/vi/Eeh7pxtTZ3k/0.jpg)](https://www.youtube.com/watch?v=Eeh7pxtTZ3k "Loops")

> 🎥 คลิกที่ภาพด้านบนเพื่อดูวิดีโอเกี่ยวกับอาเรย์และลูป

> คุณสามารถเรียนบทเรียนนี้ได้ที่ [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-arrays/?WT.mc_id=academic-77807-sagibbon)!

## อาเรย์

การทำงานกับข้อมูลเป็นงานที่พบได้บ่อยในทุกภาษา และจะง่ายขึ้นมากเมื่อข้อมูลถูกจัดระเบียบในรูปแบบโครงสร้าง เช่น อาเรย์ ด้วยอาเรย์ ข้อมูลจะถูกจัดเก็บในโครงสร้างที่คล้ายกับรายการ ข้อดีอย่างหนึ่งของอาเรย์คือคุณสามารถจัดเก็บข้อมูลหลายประเภทในอาเรย์เดียวกันได้

✅ อาเรย์มีอยู่รอบตัวเรา! คุณนึกถึงตัวอย่างอาเรย์ในชีวิตจริงได้ไหม เช่น แผงโซลาร์เซลล์ที่เรียงกันเป็นอาเรย์?

ไวยากรณ์ของอาเรย์คือการใช้วงเล็บเหลี่ยมคู่

```javascript
let myArray = [];
```

นี่คือตัวอย่างอาเรย์เปล่า แต่คุณสามารถประกาศอาเรย์ที่มีข้อมูลอยู่แล้วได้ ค่าหลายค่าในอาเรย์จะถูกคั่นด้วยเครื่องหมายจุลภาค

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
```

ค่าของอาเรย์จะถูกกำหนดค่าที่ไม่ซ้ำกันเรียกว่า **ดัชนี (index)** ซึ่งเป็นตัวเลขจำนวนเต็มที่กำหนดตามระยะห่างจากจุดเริ่มต้นของอาเรย์ ในตัวอย่างด้านบน ค่าสตริง "Chocolate" มีดัชนีเป็น 0 และดัชนีของ "Rocky Road" คือ 4 คุณสามารถใช้ดัชนีร่วมกับวงเล็บเหลี่ยมเพื่อดึง เปลี่ยน หรือเพิ่มค่าของอาเรย์ได้

✅ คุณแปลกใจไหมที่ดัชนีของอาเรย์เริ่มต้นที่ 0? ในบางภาษาการเขียนโปรแกรม ดัชนีเริ่มต้นที่ 1 มีประวัติที่น่าสนใจเกี่ยวกับเรื่องนี้ ซึ่งคุณสามารถ [อ่านเพิ่มเติมได้ใน Wikipedia](https://en.wikipedia.org/wiki/Zero-based_numbering)

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors[2]; //"Vanilla"
```

คุณสามารถใช้ดัชนีเพื่อเปลี่ยนค่าได้ เช่นนี้:

```javascript
iceCreamFlavors[4] = "Butter Pecan"; //Changed "Rocky Road" to "Butter Pecan"
```

และคุณสามารถเพิ่มค่าใหม่ในดัชนีที่กำหนดได้ เช่นนี้:

```javascript
iceCreamFlavors[5] = "Cookie Dough"; //Added "Cookie Dough"
```

✅ วิธีที่พบบ่อยกว่าในการเพิ่มค่าในอาเรย์คือการใช้ตัวดำเนินการอาเรย์ เช่น array.push()

หากต้องการทราบจำนวนรายการในอาเรย์ ให้ใช้คุณสมบัติ `length`

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors.length; //5
```

✅ ลองทำด้วยตัวเอง! ใช้คอนโซลของเบราว์เซอร์เพื่อสร้างและจัดการอาเรย์ที่คุณสร้างขึ้นเอง

## ลูป

ลูปช่วยให้เราทำงานที่ซ้ำซ้อนหรือ **วนซ้ำ** ได้ และช่วยประหยัดเวลาและโค้ดได้มาก การวนซ้ำแต่ละครั้งสามารถเปลี่ยนแปลงตัวแปร ค่า และเงื่อนไขได้ มีลูปหลายประเภทใน JavaScript ซึ่งแต่ละประเภทมีความแตกต่างเล็กน้อย แต่โดยพื้นฐานแล้วทำหน้าที่เหมือนกัน: วนซ้ำข้อมูล

### For Loop

`for` loop ต้องการ 3 ส่วนในการวนซ้ำ:
- `counter` ตัวแปรที่มักจะเริ่มต้นด้วยตัวเลขที่นับจำนวนครั้งของการวนซ้ำ
- `condition` นิพจน์ที่ใช้ตัวดำเนินการเปรียบเทียบเพื่อหยุดลูปเมื่อค่าเป็น `false`
- `iteration-expression` ทำงานเมื่อสิ้นสุดการวนซ้ำแต่ละครั้ง โดยปกติจะใช้เปลี่ยนค่าของตัวนับ

```javascript
// Counting up to 10
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

✅ รันโค้ดนี้ในคอนโซลของเบราว์เซอร์ จะเกิดอะไรขึ้นเมื่อคุณเปลี่ยนแปลงตัวนับ เงื่อนไข หรือการแสดงออกของการวนซ้ำเล็กน้อย? คุณสามารถทำให้มันวนถอยหลังเพื่อสร้างการนับถอยหลังได้หรือไม่?

### While loop

แตกต่างจากไวยากรณ์ของ `for` loop, `while` loop ต้องการเพียงเงื่อนไขเดียวที่จะหยุดลูปเมื่อเงื่อนไขกลายเป็น `false` เงื่อนไขในลูปมักจะพึ่งพาค่าต่างๆ เช่น ตัวนับ และต้องจัดการระหว่างลูป ค่าตั้งต้นของตัวนับต้องถูกสร้างขึ้นนอกลูป และนิพจน์ใดๆ ที่จะทำให้เงื่อนไขเป็นจริง รวมถึงการเปลี่ยนแปลงตัวนับต้องถูกจัดการภายในลูป

```javascript
//Counting up to 10
let i = 0;
while (i < 10) {
 console.log(i);
 i++;
}
```

✅ ทำไมคุณถึงเลือกใช้ for loop แทน while loop? มีผู้ชม 17,000 คนที่มีคำถามเดียวกันใน StackOverflow และบางความคิดเห็น [อาจน่าสนใจสำหรับคุณ](https://stackoverflow.com/questions/39969145/while-loops-vs-for-loops-in-javascript)

## ลูปและอาเรย์

อาเรย์มักถูกใช้ร่วมกับลูป เพราะเงื่อนไขส่วนใหญ่ต้องการความยาวของอาเรย์เพื่อหยุดลูป และดัชนีสามารถใช้เป็นค่าของตัวนับได้

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];

for (let i = 0; i < iceCreamFlavors.length; i++) {
  console.log(iceCreamFlavors[i]);
} //Ends when all flavors are printed
```

✅ ลองทดลองวนซ้ำอาเรย์ที่คุณสร้างขึ้นเองในคอนโซลของเบราว์เซอร์

---

## 🚀 ความท้าทาย

ยังมีวิธีอื่นๆ ในการวนซ้ำอาเรย์นอกเหนือจาก for และ while loop เช่น [forEach](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach), [for-of](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/for...of), และ [map](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/map) ลองเขียนลูปอาเรย์ของคุณใหม่โดยใช้เทคนิคเหล่านี้

## แบบทดสอบหลังเรียน
[แบบทดสอบหลังเรียน](https://ff-quizzes.netlify.app/web/quiz/14)

## ทบทวนและศึกษาด้วยตัวเอง

อาเรย์ใน JavaScript มีเมธอดมากมายที่มีประโยชน์อย่างยิ่งสำหรับการจัดการข้อมูล [อ่านเพิ่มเติมเกี่ยวกับเมธอดเหล่านี้](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array) และลองใช้บางเมธอด (เช่น push, pop, slice และ splice) กับอาเรย์ที่คุณสร้างขึ้นเอง

## งานที่ได้รับมอบหมาย

[วนซ้ำอาเรย์](assignment.md)

---

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามให้การแปลมีความถูกต้อง แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่แม่นยำ เอกสารต้นฉบับในภาษาต้นทางควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ ขอแนะนำให้ใช้บริการแปลภาษาจากผู้เชี่ยวชาญ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความที่ผิดพลาดซึ่งเกิดจากการใช้การแปลนี้