<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "9029f96b0e034839c1799f4595e4bb66",
  "translation_date": "2025-08-28T15:27:46+00:00",
  "source_file": "2-js-basics/4-arrays-loops/README.md",
  "language_code": "ur"
}
-->
# جاوا اسکرپٹ کی بنیادی باتیں: Arrays اور Loops

![جاوا اسکرپٹ کی بنیادی باتیں - Arrays](../../../../translated_images/webdev101-js-arrays.439d7528b8a294558d0e4302e448d193f8ad7495cc407539cc81f1afe904b470.ur.png)
> اسکیچ نوٹ از [Tomomi Imura](https://twitter.com/girlie_mac)

## لیکچر سے پہلے کا کوئز
[لیکچر سے پہلے کا کوئز](https://ff-quizzes.netlify.app/web/quiz/13)

یہ سبق جاوا اسکرپٹ کی بنیادی باتوں کا احاطہ کرتا ہے، وہ زبان جو ویب پر انٹرایکٹیویٹی فراہم کرتی ہے۔ اس سبق میں، آپ Arrays اور Loops کے بارے میں سیکھیں گے، جو ڈیٹا کو منظم کرنے کے لیے استعمال ہوتے ہیں۔

[![Arrays](https://img.youtube.com/vi/1U4qTyq02Xw/0.jpg)](https://youtube.com/watch?v=1U4qTyq02Xw "Arrays")

[![Loops](https://img.youtube.com/vi/Eeh7pxtTZ3k/0.jpg)](https://www.youtube.com/watch?v=Eeh7pxtTZ3k "Loops")

> 🎥 اوپر دی گئی تصاویر پر کلک کریں Arrays اور Loops کے بارے میں ویڈیوز دیکھنے کے لیے۔

> آپ یہ سبق [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-arrays/?WT.mc_id=academic-77807-sagibbon) پر لے سکتے ہیں!

## Arrays

ڈیٹا کے ساتھ کام کرنا کسی بھی زبان کے لیے ایک عام کام ہے، اور جب ڈیٹا کو ایک ساختی فارمیٹ میں منظم کیا جاتا ہے، جیسے Arrays، تو یہ کام بہت آسان ہو جاتا ہے۔ Arrays کے ساتھ، ڈیٹا کو ایک فہرست جیسی ساخت میں محفوظ کیا جاتا ہے۔ Arrays کا ایک بڑا فائدہ یہ ہے کہ آپ ایک Array میں مختلف قسم کے ڈیٹا کو محفوظ کر سکتے ہیں۔

✅ Arrays ہمارے ارد گرد موجود ہیں! کیا آپ کسی حقیقی زندگی کی مثال دے سکتے ہیں، جیسے سولر پینل Arrays؟

Array کے لیے syntax ایک جوڑے مربع بریکٹس ہیں۔

```javascript
let myArray = [];
```

یہ ایک خالی Array ہے، لیکن Arrays کو پہلے سے ڈیٹا کے ساتھ اعلان کیا جا سکتا ہے۔ Array میں متعدد اقدار کو کاما کے ذریعے الگ کیا جاتا ہے۔

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
```

Array کی اقدار کو ایک منفرد قدر دی جاتی ہے جسے **index** کہا جاتا ہے، جو ایک عددی قدر ہے جو Array کے آغاز سے اس کی دوری کی بنیاد پر دی جاتی ہے۔ اوپر دی گئی مثال میں، "Chocolate" کی string قدر کا index 0 ہے، اور "Rocky Road" کا index 4 ہے۔ آپ مربع بریکٹس کے ساتھ index کا استعمال کر کے Array کی اقدار کو حاصل، تبدیل، یا داخل کر سکتے ہیں۔

✅ کیا آپ کو حیرت ہوتی ہے کہ Arrays صفر index سے شروع ہوتے ہیں؟ کچھ پروگرامنگ زبانوں میں indexes 1 سے شروع ہوتے ہیں۔ اس کے پیچھے ایک دلچسپ تاریخ ہے، جسے آپ [Wikipedia پر پڑھ سکتے ہیں](https://en.wikipedia.org/wiki/Zero-based_numbering)۔

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors[2]; //"Vanilla"
```

آپ index کا استعمال کر کے قدر کو تبدیل کر سکتے ہیں، جیسے:

```javascript
iceCreamFlavors[4] = "Butter Pecan"; //Changed "Rocky Road" to "Butter Pecan"
```

اور آپ کسی دیے گئے index پر نئی قدر داخل کر سکتے ہیں، جیسے:

```javascript
iceCreamFlavors[5] = "Cookie Dough"; //Added "Cookie Dough"
```

✅ Arrays میں اقدار شامل کرنے کا ایک زیادہ عام طریقہ array operators جیسے array.push() کا استعمال ہے۔

یہ معلوم کرنے کے لیے کہ Array میں کتنی اشیاء ہیں، `length` پراپرٹی کا استعمال کریں۔

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors.length; //5
```

✅ خود آزمائیں! اپنے براؤزر کے کنسول میں ایک Array بنائیں اور اسے منظم کریں۔

## Loops

Loops ہمیں بار بار یا **iterative** کام انجام دینے کی اجازت دیتے ہیں، اور یہ وقت اور کوڈ کی بچت کرتے ہیں۔ ہر iteration میں متغیرات، اقدار، اور شرائط مختلف ہو سکتی ہیں۔ جاوا اسکرپٹ میں مختلف قسم کے Loops ہیں، اور ان سب میں معمولی فرق ہے، لیکن بنیادی طور پر وہ ایک ہی کام کرتے ہیں: ڈیٹا پر loop کرنا۔

### For Loop

`for` loop کو iterate کرنے کے لیے 3 حصے درکار ہوتے ہیں:
- `counter` ایک متغیر جو عام طور پر ایک عدد کے ساتھ شروع کیا جاتا ہے جو iterations کی تعداد گنتا ہے
- `condition` ایک اظہار جو comparison operators کا استعمال کرتا ہے تاکہ loop کو `false` ہونے پر روک سکے
- `iteration-expression` ہر iteration کے آخر میں چلتا ہے، عام طور پر counter قدر کو تبدیل کرنے کے لیے استعمال ہوتا ہے

```javascript
// Counting up to 10
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

✅ اس کوڈ کو براؤزر کنسول میں چلائیں۔ کیا ہوتا ہے جب آپ counter، condition، یا iteration expression میں چھوٹے چھوٹے تبدیلیاں کرتے ہیں؟ کیا آپ اسے الٹا چلا سکتے ہیں، ایک countdown بناتے ہوئے؟

### While loop

`for` loop کے syntax کے برعکس، `while` loops کو صرف ایک condition کی ضرورت ہوتی ہے جو loop کو اس وقت روکے گی جب condition `false` ہو جائے۔ Loops میں conditions عام طور پر دیگر اقدار جیسے counters پر انحصار کرتی ہیں، اور loop کے دوران ان کا انتظام کرنا ضروری ہوتا ہے۔ counters کے لیے ابتدائی اقدار کو loop کے باہر بنایا جانا چاہیے، اور condition کو پورا کرنے کے لیے کوئی بھی expressions، بشمول counter کو تبدیل کرنا، loop کے اندر برقرار رکھنا ضروری ہے۔

```javascript
//Counting up to 10
let i = 0;
while (i < 10) {
 console.log(i);
 i++;
}
```

✅ آپ `for` loop کے بجائے `while` loop کیوں منتخب کریں گے؟ StackOverflow پر 17K ناظرین نے یہی سوال کیا، اور کچھ آراء [آپ کے لیے دلچسپ ہو سکتی ہیں](https://stackoverflow.com/questions/39969145/while-loops-vs-for-loops-in-javascript)۔

## Loops اور Arrays

Arrays اکثر Loops کے ساتھ استعمال ہوتے ہیں کیونکہ زیادہ تر conditions کو loop کو روکنے کے لیے Array کی لمبائی کی ضرورت ہوتی ہے، اور index بھی counter قدر ہو سکتا ہے۔

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];

for (let i = 0; i < iceCreamFlavors.length; i++) {
  console.log(iceCreamFlavors[i]);
} //Ends when all flavors are printed
```

✅ اپنے براؤزر کے کنسول میں اپنے بنائے ہوئے Array پر loop کرنے کے ساتھ تجربہ کریں۔

---

## 🚀 چیلنج

Arrays پر loop کرنے کے دیگر طریقے بھی ہیں، جیسے [forEach](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)، [for-of](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/for...of)، اور [map](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/map)۔ اپنے Array loop کو ان میں سے کسی ایک تکنیک کا استعمال کرتے ہوئے دوبارہ لکھیں۔

## لیکچر کے بعد کا کوئز
[لیکچر کے بعد کا کوئز](https://ff-quizzes.netlify.app/web/quiz/14)

## جائزہ اور خود مطالعہ

جاوا اسکرپٹ میں Arrays کے ساتھ بہت سے methods منسلک ہیں، جو ڈیٹا کو منظم کرنے کے لیے انتہائی مفید ہیں۔ [ان methods کے بارے میں پڑھیں](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array) اور انہیں اپنے بنائے ہوئے Array پر آزمائیں (جیسے push، pop، slice اور splice)۔

## اسائنمنٹ

[Loop an Array](assignment.md)

---

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا غیر درستیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔