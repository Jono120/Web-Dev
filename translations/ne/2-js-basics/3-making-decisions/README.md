<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f7009631b73556168ca435120a231c98",
  "translation_date": "2025-08-28T16:38:40+00:00",
  "source_file": "2-js-basics/3-making-decisions/README.md",
  "language_code": "ne"
}
-->
# जाभास्क्रिप्टको आधारभूत कुरा: निर्णय लिनु

![जाभास्क्रिप्टको आधारभूत कुरा - निर्णय लिनु](../../../../translated_images/webdev101-js-decisions.69e1b20f272dd1f0b1cb2f8adaff3ed2a77c4f91db96d8a0594132a353fa189a.ne.png)

> स्केच नोट [Tomomi Imura](https://twitter.com/girlie_mac) द्वारा

## प्रि-लेक्चर क्विज

[प्रि-लेक्चर क्विज](https://ff-quizzes.netlify.app/web/quiz/11)

निर्णय लिनु र तपाईंको कोड कसरी चल्छ भन्ने क्रम नियन्त्रण गर्नुले तपाईंको कोडलाई पुन: प्रयोगयोग्य र बलियो बनाउँछ। यो खण्डले जाभास्क्रिप्टमा डाटा प्रवाह नियन्त्रण गर्ने सिन्ट्याक्स र यसलाई Boolean डाटा प्रकारसँग प्रयोग गर्दा यसको महत्त्वलाई समेट्छ।

[![निर्णय लिनु](https://img.youtube.com/vi/SxTp8j-fMMY/0.jpg)](https://youtube.com/watch?v=SxTp8j-fMMY "निर्णय लिनु")

> 🎥 माथिको तस्बिरमा क्लिक गरेर निर्णय लिनु सम्बन्धी भिडियो हेर्नुहोस्।

> तपाईं यो पाठ [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-if-else/?WT.mc_id=academic-77807-sagibbon) मा लिन सक्नुहुन्छ!

## Boolean को संक्षिप्त पुनरावलोकन

Boolean मा केवल दुई मानहरू हुन सक्छन्: `true` वा `false`। Boolean ले निर्णय गर्न मद्दत गर्छ कि कुन लाइनको कोड निश्चित सर्तहरू पूरा हुँदा चल्नेछ।

तपाईं Boolean लाई यसरी `true` वा `false` मा सेट गर्न सक्नुहुन्छ:

`let myTrueBool = true`  
`let myFalseBool = false`

✅ Boolean को नाम अंग्रेज गणितज्ञ, दार्शनिक र तर्कशास्त्री George Boole (1815–1864) बाट राखिएको हो।

## तुलना अपरेटरहरू र Boolean

अपरेटरहरू सर्तहरूको मूल्याङ्कन गर्न प्रयोग गरिन्छ, जसले Boolean मान सिर्जना गर्दछ। तल बारम्बार प्रयोग गरिने अपरेटरहरूको सूची छ।

| चिन्ह | विवरण                                                                                                                                                     | उदाहरण             |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| `<`    | **कम छ**: दुई मानहरूको तुलना गर्छ र यदि बाँया पक्षको मान दायाँ पक्षभन्दा कम छ भने `true` Boolean डाटा प्रकार फर्काउँछ                              | `5 < 6 // true`    |
| `<=`   | **कम वा बराबर छ**: दुई मानहरूको तुलना गर्छ र यदि बाँया पक्षको मान दायाँ पक्षभन्दा कम वा बराबर छ भने `true` Boolean डाटा प्रकार फर्काउँछ              | `5 <= 6 // true`   |
| `>`    | **ठूलो छ**: दुई मानहरूको तुलना गर्छ र यदि बाँया पक्षको मान दायाँ पक्षभन्दा ठूलो छ भने `true` Boolean डाटा प्रकार फर्काउँछ                             | `5 > 6 // false`   |
| `>=`   | **ठूलो वा बराबर छ**: दुई मानहरूको तुलना गर्छ र यदि बाँया पक्षको मान दायाँ पक्षभन्दा ठूलो वा बराबर छ भने `true` Boolean डाटा प्रकार फर्काउँछ         | `5 >= 6 // false`  |
| `===`  | **सख्त समानता**: दुई मानहरूको तुलना गर्छ र यदि दायाँ र बाँया पक्षका मानहरू समान छन् र एउटै डाटा प्रकारका छन् भने `true` Boolean डाटा प्रकार फर्काउँछ | `5 === 6 // false` |
| `!==`  | **असमानता**: दुई मानहरूको तुलना गर्छ र सख्त समानता अपरेटरले फर्काउने विपरीत Boolean मान फर्काउँछ                                                      | `5 !== 6 // true`  |

✅ आफ्नो ब्राउजरको कन्सोलमा केही तुलना लेखेर आफ्नो ज्ञान जाँच गर्नुहोस्। के कुनै फर्काइएको डाटाले तपाईंलाई अचम्मित गर्‍यो?

## If स्टेटमेन्ट

If स्टेटमेन्टले आफ्नो ब्लकभित्रको कोड तब चलाउँछ जब सर्त `true` हुन्छ।

```javascript
if (condition) {
  //Condition is true. Code in this block will run.
}
```

तर्कशास्त्रीय अपरेटरहरू प्राय: सर्त बनाउन प्रयोग गरिन्छ।

```javascript
let currentMoney;
let laptopPrice;

if (currentMoney >= laptopPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
}
```

## If..Else स्टेटमेन्ट

`else` स्टेटमेन्टले आफ्नो ब्लकभित्रको कोड तब चलाउँछ जब सर्त `false` हुन्छ। यो `if` स्टेटमेन्टसँग वैकल्पिक हुन्छ।

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

✅ यो कोड र तलको कोडलाई ब्राउजर कन्सोलमा चलाएर आफ्नो बुझाइ जाँच गर्नुहोस्। `currentMoney` र `laptopPrice` भेरिएबलहरूको मान परिवर्तन गरेर फर्काइएको `console.log()` परिवर्तन गर्नुहोस्।

## Switch स्टेटमेन्ट

`switch` स्टेटमेन्ट विभिन्न सर्तहरूमा आधारित भएर विभिन्न कार्यहरू प्रदर्शन गर्न प्रयोग गरिन्छ। `switch` स्टेटमेन्ट प्रयोग गरेर कार्यान्वयन गर्नुपर्ने कोड ब्लक चयन गर्नुहोस्।

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

✅ यो कोड र तलको कोडलाई ब्राउजर कन्सोलमा चलाएर आफ्नो बुझाइ जाँच गर्नुहोस्। `a` भेरिएबलको मान परिवर्तन गरेर फर्काइएको `console.log()` परिवर्तन गर्नुहोस्।

## तर्कशास्त्रीय अपरेटरहरू र Boolean

निर्णय लिनका लागि कहिलेकाहीँ एकभन्दा बढी तुलना आवश्यक पर्न सक्छ, जसलाई तर्कशास्त्रीय अपरेटरहरूसँग जोडेर Boolean मान उत्पादन गर्न सकिन्छ।

| चिन्ह | विवरण                                                                                     | उदाहरण                                                                 |
| ------ | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `&&`   | **तर्कशास्त्रीय AND**: दुई Boolean अभिव्यक्तिहरू तुलना गर्छ। दुवै पक्ष `true` भए मात्र `true` फर्काउँछ | `(5 > 6) && (5 < 6 ) // एउटा पक्ष false छ, अर्को true छ। फर्काउँछ false` |
| `\|\|` | **तर्कशास्त्रीय OR**: दुई Boolean अभिव्यक्तिहरू तुलना गर्छ। कम्तीमा एउटा पक्ष `true` भए `true` फर्काउँछ | `(5 > 6) \|\| (5 < 6) // एउटा पक्ष false छ, अर्को true छ। फर्काउँछ true` |
| `!`    | **तर्कशास्त्रीय NOT**: Boolean अभिव्यक्तिको विपरीत मान फर्काउँछ                             | `!(5 > 6) // 5, 6 भन्दा ठूलो छैन, तर "!" ले true फर्काउँछ`             |

## तर्कशास्त्रीय अपरेटरहरूसँग सर्तहरू र निर्णयहरू

तर्कशास्त्रीय अपरेटरहरू if..else स्टेटमेन्टमा सर्त बनाउन प्रयोग गर्न सकिन्छ।

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

### नकारात्मक अपरेटर

तपाईंले अहिलेसम्म देख्नुभएको छ कि कसरी `if...else` स्टेटमेन्ट प्रयोग गरेर सर्तात्मक तर्क सिर्जना गर्न सकिन्छ। `if` मा जाने कुनै पनि कुरा true/false मा मूल्याङ्कन हुनुपर्छ। `!` अपरेटर प्रयोग गरेर तपाईं अभिव्यक्तिलाई _नकार्न_ सक्नुहुन्छ। यसले यसरी देखिन्छ:

```javascript
if (!condition) {
  // runs if condition is false
} else {
  // runs if condition is true
}
```

### Ternary अभिव्यक्तिहरू

`if...else` मात्र निर्णय तर्क व्यक्त गर्ने तरिका होइन। तपाईंले Ternary अपरेटर नामक अर्को तरिका पनि प्रयोग गर्न सक्नुहुन्छ। यसको सिन्ट्याक्स यसरी देखिन्छ:

```javascript
let variable = condition ? <return this if true> : <return this if false>
```

तल एउटा थप स्पष्ट उदाहरण छ:

```javascript
let firstNumber = 20;
let secondNumber = 10;
let biggestNumber = firstNumber > secondNumber ? firstNumber : secondNumber;
```

✅ यो कोडलाई केही पटक पढ्न समय लिनुहोस्। के तपाईं यी अपरेटरहरू कसरी काम गरिरहेका छन् भनेर बुझ्नुभयो?

माथिको कोडले भन्छ:

- यदि `firstNumber`, `secondNumber` भन्दा ठूलो छ
- भने `firstNumber` लाई `biggestNumber` मा असाइन गर्नुहोस्
- अन्यथा `secondNumber` लाई असाइन गर्नुहोस्।

Ternary अभिव्यक्ति तलको कोड लेख्ने संक्षिप्त तरिका मात्र हो:

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

पहिले तर्कशास्त्रीय अपरेटरहरूसँग लेखिएको र त्यसपछि Ternary अभिव्यक्तिको प्रयोग गरेर पुन: लेखिएको प्रोग्राम सिर्जना गर्नुहोस्। तपाईंलाई कुन सिन्ट्याक्स मनपर्छ?

---

## पोस्ट-लेक्चर क्विज

[पोस्ट-लेक्चर क्विज](https://ff-quizzes.netlify.app/web/quiz/12)

## समीक्षा र आत्म-अध्ययन

प्रयोगकर्ताका लागि उपलब्ध धेरै अपरेटरहरूको बारेमा थप पढ्नुहोस् [MDN मा](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators)।

Josh Comeau को उत्कृष्ट [अपरेटर लुकअप](https://joshwcomeau.com/operator-lookup/) हेर्नुहोस्!

## असाइनमेन्ट

[अपरेटरहरू](assignment.md)

---

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरेर अनुवाद गरिएको हो। हामी शुद्धताको लागि प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छ। यसको मूल भाषा मा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीको लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।