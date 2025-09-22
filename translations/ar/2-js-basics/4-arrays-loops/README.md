<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "9029f96b0e034839c1799f4595e4bb66",
  "translation_date": "2025-08-28T15:05:53+00:00",
  "source_file": "2-js-basics/4-arrays-loops/README.md",
  "language_code": "ar"
}
-->
# أساسيات JavaScript: المصفوفات والحلقات

![أساسيات JavaScript - المصفوفات](../../../../translated_images/webdev101-js-arrays.439d7528b8a294558d0e4302e448d193f8ad7495cc407539cc81f1afe904b470.ar.png)
> رسم توضيحي بواسطة [Tomomi Imura](https://twitter.com/girlie_mac)

## اختبار ما قبل المحاضرة
[اختبار ما قبل المحاضرة](https://ff-quizzes.netlify.app/web/quiz/13)

تغطي هذه الدرس أساسيات JavaScript، اللغة التي تضيف التفاعل إلى الويب. في هذا الدرس، ستتعلم عن المصفوفات والحلقات، والتي تُستخدم لمعالجة البيانات.

[![المصفوفات](https://img.youtube.com/vi/1U4qTyq02Xw/0.jpg)](https://youtube.com/watch?v=1U4qTyq02Xw "المصفوفات")

[![الحلقات](https://img.youtube.com/vi/Eeh7pxtTZ3k/0.jpg)](https://www.youtube.com/watch?v=Eeh7pxtTZ3k "الحلقات")

> 🎥 انقر على الصور أعلاه لمشاهدة فيديوهات عن المصفوفات والحلقات.

> يمكنك أخذ هذا الدرس على [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-arrays/?WT.mc_id=academic-77807-sagibbon)!

## المصفوفات

العمل مع البيانات هو مهمة شائعة في أي لغة، ويصبح الأمر أسهل عندما يتم تنظيم البيانات في شكل هيكلي مثل المصفوفات. مع المصفوفات، يتم تخزين البيانات في هيكل يشبه القائمة. واحدة من الفوائد الرئيسية للمصفوفات هي أنه يمكنك تخزين أنواع مختلفة من البيانات في مصفوفة واحدة.

✅ المصفوفات موجودة في كل مكان حولنا! هل يمكنك التفكير في مثال واقعي لمصفوفة، مثل مصفوفة ألواح شمسية؟

صيغة المصفوفة هي زوج من الأقواس المربعة.

```javascript
let myArray = [];
```

هذه مصفوفة فارغة، ولكن يمكن تعريف المصفوفات مسبقًا مع بيانات. يتم فصل القيم المتعددة في المصفوفة بفاصلة.

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
```

يتم تعيين قيم المصفوفة قيمة فريدة تُسمى **الفهرس**، وهو رقم صحيح يتم تعيينه بناءً على المسافة من بداية المصفوفة. في المثال أعلاه، القيمة النصية "Chocolate" لها فهرس 0، وفهرس "Rocky Road" هو 4. استخدم الفهرس مع الأقواس المربعة لاسترجاع أو تغيير أو إدخال قيم المصفوفة.

✅ هل يفاجئك أن المصفوفات تبدأ من الفهرس صفر؟ في بعض لغات البرمجة، تبدأ الفهارس من 1. هناك تاريخ مثير للاهتمام حول هذا الموضوع، يمكنك [قراءته على ويكيبيديا](https://en.wikipedia.org/wiki/Zero-based_numbering).

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors[2]; //"Vanilla"
```

يمكنك الاستفادة من الفهرس لتغيير قيمة، مثل هذا:

```javascript
iceCreamFlavors[4] = "Butter Pecan"; //Changed "Rocky Road" to "Butter Pecan"
```

ويمكنك إدخال قيمة جديدة في فهرس معين مثل هذا:

```javascript
iceCreamFlavors[5] = "Cookie Dough"; //Added "Cookie Dough"
```

✅ طريقة أكثر شيوعًا لإضافة قيم إلى مصفوفة هي باستخدام مشغلات المصفوفة مثل array.push()

لمعرفة عدد العناصر الموجودة في المصفوفة، استخدم خاصية `length`.

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors.length; //5
```

✅ جرب بنفسك! استخدم وحدة التحكم في متصفحك لإنشاء ومعالجة مصفوفة من تصميمك.

## الحلقات

تسمح لنا الحلقات بتنفيذ مهام متكررة أو **تكرارية**، ويمكن أن توفر الكثير من الوقت والرمز. يمكن أن تختلف كل تكرار في متغيراتها وقيمها وشروطها. هناك أنواع مختلفة من الحلقات في JavaScript، وكلها لها اختلافات صغيرة، لكنها تقوم بنفس الوظيفة بشكل أساسي: التكرار على البيانات.

### حلقة For

تتطلب حلقة `for` ثلاثة أجزاء للتكرار:
- `counter` متغير يتم عادةً تهيئته برقم يعد عدد التكرارات
- `condition` تعبير يستخدم عوامل المقارنة لإيقاف الحلقة عندما يصبح `false`
- `iteration-expression` يتم تشغيله في نهاية كل تكرار، ويُستخدم عادةً لتغيير قيمة العداد
  
```javascript
// Counting up to 10
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

✅ قم بتشغيل هذا الرمز في وحدة التحكم في المتصفح. ماذا يحدث عندما تقوم بإجراء تغييرات صغيرة على العداد أو الشرط أو تعبير التكرار؟ هل يمكنك جعله يعمل بشكل عكسي، مما يُنشئ عد تنازلي؟

### حلقة While

على عكس صيغة حلقة `for`، تتطلب حلقات `while` فقط شرطًا لإيقاف الحلقة عندما يصبح الشرط `false`. تعتمد الشروط في الحلقات عادةً على قيم أخرى مثل العدادات، ويجب إدارتها أثناء الحلقة. يجب إنشاء قيم البداية للعدادات خارج الحلقة، وأي تعبيرات لتلبية شرط، بما في ذلك تغيير العداد، يجب الحفاظ عليها داخل الحلقة.

```javascript
//Counting up to 10
let i = 0;
while (i < 10) {
 console.log(i);
 i++;
}
```

✅ لماذا تختار حلقة for مقابل حلقة while؟ 17 ألف مشاهد كان لديهم نفس السؤال على StackOverflow، وبعض الآراء [قد تكون مثيرة للاهتمام بالنسبة لك](https://stackoverflow.com/questions/39969145/while-loops-vs-for-loops-in-javascript).

## الحلقات والمصفوفات

غالبًا ما تُستخدم المصفوفات مع الحلقات لأن معظم الشروط تتطلب طول المصفوفة لإيقاف الحلقة، ويمكن أن يكون الفهرس أيضًا قيمة العداد.

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];

for (let i = 0; i < iceCreamFlavors.length; i++) {
  console.log(iceCreamFlavors[i]);
} //Ends when all flavors are printed
```

✅ جرب التكرار على مصفوفة من تصميمك في وحدة التحكم في المتصفح. 

---

## 🚀 التحدي

هناك طرق أخرى للتكرار على المصفوفات غير الحلقات for وwhile. هناك [forEach](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)، [for-of](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/for...of)، و[map](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/map). أعد كتابة حلقة المصفوفة الخاصة بك باستخدام واحدة من هذه التقنيات.

## اختبار ما بعد المحاضرة
[اختبار ما بعد المحاضرة](https://ff-quizzes.netlify.app/web/quiz/14)

## المراجعة والدراسة الذاتية

لدى المصفوفات في JavaScript العديد من الطرق المرتبطة بها، والتي تكون مفيدة للغاية لمعالجة البيانات. [اقرأ عن هذه الطرق](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array) وجرب بعضها (مثل push، pop، slice وsplice) على مصفوفة من تصميمك.

## الواجب

[تكرار مصفوفة](assignment.md)

---

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الرسمي. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة ناتجة عن استخدام هذه الترجمة.