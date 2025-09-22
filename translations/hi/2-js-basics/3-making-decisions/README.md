<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f7009631b73556168ca435120a231c98",
  "translation_date": "2025-08-29T15:58:13+00:00",
  "source_file": "2-js-basics/3-making-decisions/README.md",
  "language_code": "hi"
}
-->
# जावास्क्रिप्ट बेसिक्स: निर्णय लेना

![जावास्क्रिप्ट बेसिक्स - निर्णय लेना](../../../../translated_images/webdev101-js-decisions.69e1b20f272dd1f0b1cb2f8adaff3ed2a77c4f91db96d8a0594132a353fa189a.hi.png)

> स्केच नोट [Tomomi Imura](https://twitter.com/girlie_mac) द्वारा

## प्री-लेक्चर क्विज़

[प्री-लेक्चर क्विज़](https://ff-quizzes.netlify.app/web/quiz/11)

निर्णय लेना और यह नियंत्रित करना कि आपका कोड किस क्रम में चलेगा, आपके कोड को पुन: उपयोगी और मजबूत बनाता है। इस सेक्शन में जावास्क्रिप्ट में डेटा फ्लो को नियंत्रित करने के लिए सिंटैक्स और Boolean डेटा टाइप्स के साथ इसके महत्व को कवर किया गया है।

[![निर्णय लेना](https://img.youtube.com/vi/SxTp8j-fMMY/0.jpg)](https://youtube.com/watch?v=SxTp8j-fMMY "निर्णय लेना")

> 🎥 निर्णय लेने के बारे में वीडियो देखने के लिए ऊपर दी गई इमेज पर क्लिक करें।

> आप इस पाठ को [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-if-else/?WT.mc_id=academic-77807-sagibbon) पर ले सकते हैं!

## Booleans पर एक संक्षिप्त पुनरावलोकन

Booleans में केवल दो मान हो सकते हैं: `true` या `false`। Booleans यह तय करने में मदद करते हैं कि कौन सी कोड की लाइनें चलेंगी जब कुछ शर्तें पूरी होंगी।

अपने Boolean को इस प्रकार `true` या `false` सेट करें:

`let myTrueBool = true`  
`let myFalseBool = false`

✅ Booleans का नाम अंग्रेज़ गणितज्ञ, दार्शनिक और तर्कशास्त्री जॉर्ज बूल (1815–1864) के नाम पर रखा गया है।

## तुलना ऑपरेटर्स और Booleans

ऑपरेटर्स का उपयोग शर्तों का मूल्यांकन करने के लिए किया जाता है, जो Boolean मान उत्पन्न करते हैं। नीचे अक्सर उपयोग किए जाने वाले ऑपरेटर्स की सूची दी गई है:

| प्रतीक | विवरण                                                                                                                                                     | उदाहरण             |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| `<`    | **कम से कम**: दो मानों की तुलना करता है और यदि बाईं ओर का मान दाईं ओर से कम है तो `true` Boolean डेटा टाइप लौटाता है                                     | `5 < 6 // true`    |
| `<=`   | **कम या बराबर**: दो मानों की तुलना करता है और यदि बाईं ओर का मान दाईं ओर से कम या बराबर है तो `true` Boolean डेटा टाइप लौटाता है                        | `5 <= 6 // true`   |
| `>`    | **अधिक**: दो मानों की तुलना करता है और यदि बाईं ओर का मान दाईं ओर से बड़ा है तो `true` Boolean डेटा टाइप लौटाता है                                       | `5 > 6 // false`   |
| `>=`   | **अधिक या बराबर**: दो मानों की तुलना करता है और यदि बाईं ओर का मान दाईं ओर से बड़ा या बराबर है तो `true` Boolean डेटा टाइप लौटाता है                    | `5 >= 6 // false`  |
| `===`  | **सख्त समानता**: दो मानों की तुलना करता है और यदि बाईं और दाईं ओर के मान समान हैं और एक ही डेटा टाइप के हैं तो `true` Boolean डेटा टाइप लौटाता है      | `5 === 6 // false` |
| `!==`  | **असमानता**: दो मानों की तुलना करता है और सख्त समानता ऑपरेटर के विपरीत Boolean मान लौटाता है                                                           | `5 !== 6 // true`  |

✅ अपने ब्राउज़र के कंसोल में कुछ तुलना लिखकर अपने ज्ञान की जांच करें। क्या कोई डेटा आपको चौंकाता है?

## If स्टेटमेंट

`if` स्टेटमेंट उन ब्लॉक्स के बीच का कोड चलाएगा यदि शर्त `true` है।

```javascript
if (condition) {
  //Condition is true. Code in this block will run.
}
```

लॉजिकल ऑपरेटर्स का उपयोग अक्सर शर्त बनाने के लिए किया जाता है।

```javascript
let currentMoney;
let laptopPrice;

if (currentMoney >= laptopPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
}
```

## If..Else स्टेटमेंट

`else` स्टेटमेंट उन ब्लॉक्स के बीच का कोड चलाएगा जब शर्त `false` हो। यह `if` स्टेटमेंट के साथ वैकल्पिक है।

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

✅ इस कोड और निम्नलिखित कोड को ब्राउज़र कंसोल में चलाकर अपनी समझ का परीक्षण करें। `currentMoney` और `laptopPrice` वेरिएबल्स के मान बदलें और देखें कि `console.log()` क्या लौटाता है।

## Switch स्टेटमेंट

`switch` स्टेटमेंट का उपयोग विभिन्न शर्तों के आधार पर विभिन्न क्रियाओं को करने के लिए किया जाता है। `switch` स्टेटमेंट का उपयोग करके कई कोड ब्लॉक्स में से एक को चुना जा सकता है।

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

✅ इस कोड और निम्नलिखित कोड को ब्राउज़र कंसोल में चलाकर अपनी समझ का परीक्षण करें। वेरिएबल `a` के मान बदलें और देखें कि `console.log()` क्या लौटाता है।

## लॉजिकल ऑपरेटर्स और Booleans

निर्णय लेने के लिए कभी-कभी एक से अधिक तुलना की आवश्यकता होती है, और इन्हें लॉजिकल ऑपरेटर्स के साथ जोड़ा जा सकता है ताकि Boolean मान उत्पन्न हो सके।

| प्रतीक | विवरण                                                                                     | उदाहरण                                                                 |
| ------ | ----------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `&&`   | **लॉजिकल AND**: दो Boolean अभिव्यक्तियों की तुलना करता है। केवल तभी `true` लौटाता है जब दोनों पक्ष `true` हों | `(5 > 6) && (5 < 6 ) // एक पक्ष false है, दूसरा true है। false लौटाता है` |
| `\|\|` | **लॉजिकल OR**: दो Boolean अभिव्यक्तियों की तुलना करता है। यदि कम से कम एक पक्ष `true` है तो `true` लौटाता है | `(5 > 6) \|\| (5 < 6) // एक पक्ष false है, दूसरा true है। true लौटाता है` |
| `!`    | **लॉजिकल NOT**: Boolean अभिव्यक्ति के विपरीत मान लौटाता है                             | `!(5 > 6) // 5, 6 से बड़ा नहीं है, लेकिन "!" true लौटाएगा`           |

## लॉजिकल ऑपरेटर्स के साथ शर्तें और निर्णय

लॉजिकल ऑपरेटर्स का उपयोग `if..else` स्टेटमेंट में शर्तें बनाने के लिए किया जा सकता है।

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

### नेगेशन ऑपरेटर

अब तक आपने देखा कि `if...else` स्टेटमेंट का उपयोग करके सशर्त तर्क कैसे बनाया जा सकता है। `if` में जो कुछ भी जाता है, उसे `true/false` में मूल्यांकन करना चाहिए। `!` ऑपरेटर का उपयोग करके आप अभिव्यक्ति को _नकार_ सकते हैं। यह इस प्रकार दिखेगा:

```javascript
if (!condition) {
  // runs if condition is false
} else {
  // runs if condition is true
}
```

### टर्नरी अभिव्यक्तियां

`if...else` निर्णय तर्क व्यक्त करने का एकमात्र तरीका नहीं है। आप टर्नरी ऑपरेटर नामक कुछ का भी उपयोग कर सकते हैं। इसका सिंटैक्स इस प्रकार दिखता है:

```javascript
let variable = condition ? <return this if true> : <return this if false>
```

नीचे एक अधिक ठोस उदाहरण दिया गया है:

```javascript
let firstNumber = 20;
let secondNumber = 10;
let biggestNumber = firstNumber > secondNumber ? firstNumber : secondNumber;
```

✅ इस कोड को कुछ बार पढ़ने के लिए एक मिनट लें। क्या आप समझते हैं कि ये ऑपरेटर्स कैसे काम कर रहे हैं?

ऊपर दिए गए कोड का मतलब है:

- यदि `firstNumber`, `secondNumber` से बड़ा है
- तो `firstNumber` को `biggestNumber` में असाइन करें
- अन्यथा `secondNumber` को असाइन करें।

टर्नरी अभिव्यक्ति नीचे दिए गए कोड को लिखने का एक संक्षिप्त तरीका है:

```javascript
let biggestNumber;
if (firstNumber > secondNumber) {
  biggestNumber = firstNumber;
} else {
  biggestNumber = secondNumber;
}
```

---

## 🚀 चुनौती

एक प्रोग्राम बनाएं जिसे पहले लॉजिकल ऑपरेटर्स के साथ लिखा गया हो, और फिर इसे टर्नरी अभिव्यक्ति का उपयोग करके फिर से लिखें। आपको कौन सा सिंटैक्स पसंद है?

---

## पोस्ट-लेक्चर क्विज़

[पोस्ट-लेक्चर क्विज़](https://ff-quizzes.netlify.app/web/quiz/12)

## समीक्षा और स्व-अध्ययन

उपयोगकर्ता के लिए उपलब्ध कई ऑपरेटर्स के बारे में अधिक पढ़ें [MDN पर](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators)।

जोश कोमाऊ के शानदार [ऑपरेटर लुकअप](https://joshwcomeau.com/operator-lookup/) को देखें!

## असाइनमेंट

[ऑपरेटर्स](assignment.md)

---

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता सुनिश्चित करने का प्रयास करते हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को प्रामाणिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम जिम्मेदार नहीं हैं।