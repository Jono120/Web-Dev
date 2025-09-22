<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f7009631b73556168ca435120a231c98",
  "translation_date": "2025-08-28T15:26:38+00:00",
  "source_file": "2-js-basics/3-making-decisions/README.md",
  "language_code": "ur"
}
-->
# جاوا اسکرپٹ کی بنیادی باتیں: فیصلے کرنا

![جاوا اسکرپٹ کی بنیادی باتیں - فیصلے کرنا](../../../../translated_images/webdev101-js-decisions.69e1b20f272dd1f0b1cb2f8adaff3ed2a77c4f91db96d8a0594132a353fa189a.ur.png)

> اسکیچ نوٹ: [Tomomi Imura](https://twitter.com/girlie_mac)

## لیکچر سے پہلے کا کوئز

[لیکچر سے پہلے کا کوئز](https://ff-quizzes.netlify.app/web/quiz/11)

فیصلے کرنا اور اپنے کوڈ کے چلنے کے ترتیب کو کنٹرول کرنا آپ کے کوڈ کو دوبارہ استعمال کے قابل اور مضبوط بناتا ہے۔ اس سیکشن میں جاوا اسکرپٹ میں ڈیٹا کے بہاؤ کو کنٹرول کرنے کے لیے استعمال ہونے والے نحو اور اس کی اہمیت کو بیان کیا گیا ہے، خاص طور پر جب اسے Boolean ڈیٹا ٹائپس کے ساتھ استعمال کیا جائے۔

[![فیصلے کرنا](https://img.youtube.com/vi/SxTp8j-fMMY/0.jpg)](https://youtube.com/watch?v=SxTp8j-fMMY "فیصلے کرنا")

> 🎥 اوپر دی گئی تصویر پر کلک کریں فیصلے کرنے کے بارے میں ویڈیو دیکھنے کے لیے۔

> آپ یہ سبق [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-if-else/?WT.mc_id=academic-77807-sagibbon) پر لے سکتے ہیں!

## Boolean پر مختصر نظر

Boolean صرف دو ویلیوز رکھ سکتے ہیں: `true` یا `false`۔ Boolean اس بات کا فیصلہ کرنے میں مدد کرتے ہیں کہ کون سی لائنز کوڈ چلنی چاہیے جب مخصوص شرائط پوری ہوں۔

اپنے Boolean کو true یا false پر سیٹ کریں اس طرح:

`let myTrueBool = true`  
`let myFalseBool = false`

✅ Boolean کا نام انگریزی ریاضی دان، فلسفی اور منطقی George Boole (1815–1864) کے نام پر رکھا گیا ہے۔

## موازنہ آپریٹرز اور Boolean

آپریٹرز کا استعمال شرائط کا جائزہ لینے کے لیے کیا جاتا ہے، جو Boolean ویلیو پیدا کرتے ہیں۔ نیچے آپریٹرز کی ایک فہرست دی گئی ہے جو اکثر استعمال ہوتے ہیں۔

| علامت | وضاحت                                                                                                                                                   | مثال              |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| `<`    | **کم سے کم**: دو ویلیوز کا موازنہ کرتا ہے اور `true` Boolean ڈیٹا ٹائپ واپس کرتا ہے اگر بائیں طرف کی ویلیو دائیں طرف سے کم ہو                              | `5 < 6 // true`    |
| `<=`   | **کم یا برابر**: دو ویلیوز کا موازنہ کرتا ہے اور `true` Boolean ڈیٹا ٹائپ واپس کرتا ہے اگر بائیں طرف کی ویلیو دائیں طرف سے کم یا برابر ہو                  | `5 <= 6 // true`   |
| `>`    | **زیادہ**: دو ویلیوز کا موازنہ کرتا ہے اور `true` Boolean ڈیٹا ٹائپ واپس کرتا ہے اگر بائیں طرف کی ویلیو دائیں طرف سے زیادہ ہو                              | `5 > 6 // false`   |
| `>=`   | **زیادہ یا برابر**: دو ویلیوز کا موازنہ کرتا ہے اور `true` Boolean ڈیٹا ٹائپ واپس کرتا ہے اگر بائیں طرف کی ویلیو دائیں طرف سے زیادہ یا برابر ہو            | `5 >= 6 // false`  |
| `===`  | **سخت برابری**: دو ویلیوز کا موازنہ کرتا ہے اور `true` Boolean ڈیٹا ٹائپ واپس کرتا ہے اگر بائیں اور دائیں طرف کی ویلیوز برابر ہوں اور ایک ہی ڈیٹا ٹائپ ہوں | `5 === 6 // false` |
| `!==`  | **عدم برابری**: دو ویلیوز کا موازنہ کرتا ہے اور وہ Boolean ویلیو واپس کرتا ہے جو سخت برابری آپریٹر کے برعکس ہو                                            | `5 !== 6 // true`  |

✅ اپنے علم کو جانچنے کے لیے کچھ موازنہ اپنے براؤزر کے کنسول میں لکھیں۔ کیا کوئی واپس آنے والا ڈیٹا آپ کو حیران کرتا ہے؟

## If بیان

If بیان اس وقت کوڈ کو چلائے گا جب شرط true ہو۔

```javascript
if (condition) {
  //Condition is true. Code in this block will run.
}
```

منطقی آپریٹرز اکثر شرط بنانے کے لیے استعمال کیے جاتے ہیں۔

```javascript
let currentMoney;
let laptopPrice;

if (currentMoney >= laptopPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
}
```

## If..Else بیان

`else` بیان اس وقت کوڈ کو چلائے گا جب شرط false ہو۔ یہ `if` بیان کے ساتھ اختیاری ہے۔

```javascript
let currentMoney;
let laptopPrice;

if (currentMoney >= laptopPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
} else {
  //Condition is false. Code in this block will run.
  console.log("Can't afford a new laptop, yet!");
}
```

✅ اس کوڈ اور نیچے دیے گئے کوڈ کو براؤزر کنسول میں چلا کر اپنی سمجھ کو جانچیں۔ `currentMoney` اور `laptopPrice` ویریبلز کی ویلیوز کو تبدیل کریں تاکہ واپس آنے والے `console.log()` کو تبدیل کیا جا سکے۔

## Switch بیان

`switch` بیان مختلف شرائط کی بنیاد پر مختلف اعمال انجام دینے کے لیے استعمال کیا جاتا ہے۔ `switch` بیان کا استعمال کریں تاکہ کئی کوڈ بلاکس میں سے ایک کو منتخب کیا جا سکے۔

```javascript
switch (expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
  // code block
}
```

```javascript
// program using switch statement
let a = 2;

switch (a) {
  case 1:
    a = "one";
    break;
  case 2:
    a = "two";
    break;
  default:
    a = "not found";
    break;
}
console.log(`The value is ${a}`);
```

✅ اس کوڈ اور نیچے دیے گئے کوڈ کو براؤزر کنسول میں چلا کر اپنی سمجھ کو جانچیں۔ ویریبل `a` کی ویلیوز کو تبدیل کریں تاکہ واپس آنے والے `console.log()` کو تبدیل کیا جا سکے۔

## منطقی آپریٹرز اور Boolean

فیصلے کرنے کے لیے ایک سے زیادہ موازنہ کی ضرورت ہو سکتی ہے، اور انہیں منطقی آپریٹرز کے ساتھ جوڑا جا سکتا ہے تاکہ Boolean ویلیو پیدا کی جا سکے۔

| علامت | وضاحت                                                                                     | مثال                                                                 |
| ------ | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `&&`   | **منطقی AND**: دو Boolean اظہار کا موازنہ کرتا ہے۔ true **صرف** اس وقت واپس کرتا ہے جب دونوں طرف true ہوں | `(5 > 6) && (5 < 6 ) //ایک طرف false ہے، دوسری طرف true ہے۔ false واپس کرتا ہے` |
| `\|\|` | **منطقی OR**: دو Boolean اظہار کا موازنہ کرتا ہے۔ true واپس کرتا ہے اگر کم از کم ایک طرف true ہو     | `(5 > 6) \|\| (5 < 6) //ایک طرف false ہے، دوسری طرف true ہے۔ true واپس کرتا ہے` |
| `!`    | **منطقی NOT**: Boolean اظہار کی مخالف ویلیو واپس کرتا ہے                                       | `!(5 > 6) // 5 6 سے بڑا نہیں ہے، لیکن "!" true واپس کرے گا`             |

## منطقی آپریٹرز کے ساتھ شرائط اور فیصلے

منطقی آپریٹرز کو if..else بیانات میں شرائط بنانے کے لیے استعمال کیا جا سکتا ہے۔

```javascript
let currentMoney;
let laptopPrice;
let laptopDiscountPrice = laptopPrice - laptopPrice * 0.2; //Laptop price at 20 percent off

if (currentMoney >= laptopPrice || currentMoney >= laptopDiscountPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
} else {
  //Condition is true. Code in this block will run.
  console.log("Can't afford a new laptop, yet!");
}
```

### نفی آپریٹر

آپ نے اب تک دیکھا کہ کس طرح `if...else` بیان کو مشروط منطق بنانے کے لیے استعمال کیا جا سکتا ہے۔ جو کچھ بھی `if` میں جاتا ہے اسے true/false میں تبدیل ہونا چاہیے۔ `!` آپریٹر کا استعمال کرتے ہوئے آپ اظہار کو _نفی_ کر سکتے ہیں۔ یہ اس طرح نظر آئے گا:

```javascript
if (!condition) {
  // runs if condition is false
} else {
  // runs if condition is true
}
```

### تین گنا اظہار

`if...else` فیصلہ کن منطق کو ظاہر کرنے کا واحد طریقہ نہیں ہے۔ آپ کچھ ایسا بھی استعمال کر سکتے ہیں جسے تین گنا آپریٹر کہا جاتا ہے۔ اس کا نحو اس طرح نظر آتا ہے:

```javascript
let variable = condition ? <return this if true> : <return this if false>
```

نیچے ایک زیادہ ٹھوس مثال دی گئی ہے:

```javascript
let firstNumber = 20;
let secondNumber = 10;
let biggestNumber = firstNumber > secondNumber ? firstNumber : secondNumber;
```

✅ اس کوڈ کو چند بار پڑھنے کے لیے ایک منٹ نکالیں۔ کیا آپ سمجھتے ہیں کہ یہ آپریٹرز کیسے کام کر رہے ہیں؟

اوپر بیان کرتا ہے کہ:

- اگر `firstNumber` `secondNumber` سے بڑا ہے  
- تو `firstNumber` کو `biggestNumber` میں تفویض کریں  
- ورنہ `secondNumber` کو تفویض کریں۔

تین گنا اظہار کوڈ کو نیچے لکھنے کا ایک مختصر طریقہ ہے:

```javascript
let biggestNumber;
if (firstNumber > secondNumber) {
  biggestNumber = firstNumber;
} else {
  biggestNumber = secondNumber;
}
```

---

## 🚀 چیلنج

ایک پروگرام بنائیں جو پہلے منطقی آپریٹرز کے ساتھ لکھا گیا ہو، اور پھر اسے تین گنا اظہار کے ساتھ دوبارہ لکھیں۔ آپ کو کون سا نحو پسند ہے؟

---

## لیکچر کے بعد کا کوئز

[لیکچر کے بعد کا کوئز](https://ff-quizzes.netlify.app/web/quiz/12)

## جائزہ اور خود مطالعہ

صارف کے لیے دستیاب بہت سے آپریٹرز کے بارے میں مزید پڑھیں [MDN پر](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators)۔

Josh Comeau کے شاندار [آپریٹر لوک اپ](https://joshwcomeau.com/operator-lookup/) کو دیکھیں!

## اسائنمنٹ

[آپریٹرز](assignment.md)

---

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا غیر درستیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔