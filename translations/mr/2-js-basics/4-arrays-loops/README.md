<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "9029f96b0e034839c1799f4595e4bb66",
  "translation_date": "2025-08-28T16:19:11+00:00",
  "source_file": "2-js-basics/4-arrays-loops/README.md",
  "language_code": "mr"
}
-->
# JavaScript मूलभूत गोष्टी: Arrays आणि Loops

![JavaScript Basics - Arrays](../../../../translated_images/webdev101-js-arrays.439d7528b8a294558d0e4302e448d193f8ad7495cc407539cc81f1afe904b470.mr.png)
> स्केच नोट [Tomomi Imura](https://twitter.com/girlie_mac) यांच्याकडून

## प्री-लेक्चर क्विझ
[प्री-लेक्चर क्विझ](https://ff-quizzes.netlify.app/web/quiz/13)

ही शिकवण JavaScript च्या मूलभूत गोष्टींवर आधारित आहे, जी वेबवर इंटरॅक्टिव्हिटी प्रदान करते. या शिकवणीत तुम्ही arrays आणि loops बद्दल शिकाल, जे डेटा हाताळण्यासाठी वापरले जातात.

[![Arrays](https://img.youtube.com/vi/1U4qTyq02Xw/0.jpg)](https://youtube.com/watch?v=1U4qTyq02Xw "Arrays")

[![Loops](https://img.youtube.com/vi/Eeh7pxtTZ3k/0.jpg)](https://www.youtube.com/watch?v=Eeh7pxtTZ3k "Loops")

> 🎥 वर दिलेल्या प्रतिमांवर क्लिक करा arrays आणि loops बद्दल व्हिडिओ पाहण्यासाठी.

> तुम्ही ही शिकवण [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-arrays/?WT.mc_id=academic-77807-sagibbon) वर घेऊ शकता!

## Arrays

डेटासह काम करणे ही कोणत्याही भाषेसाठी सामान्य गोष्ट आहे, आणि डेटा संरचनात्मक स्वरूपात, जसे की arrays मध्ये आयोजित केल्यास हे कार्य खूप सोपे होते. Arrays मध्ये, डेटा एका यादीसारख्या संरचनेत संग्रहित केला जातो. Arrays चा एक मोठा फायदा म्हणजे तुम्ही एका array मध्ये वेगवेगळ्या प्रकारचा डेटा संग्रहित करू शकता.

✅ Arrays आपल्या आजूबाजूला आहेत! तुम्ही एखाद्या वास्तविक जीवनातील उदाहरणाचा विचार करू शकता का, जसे की सौर पॅनेल array?

Array साठी सिंटॅक्स म्हणजे चौकोनी कंसांची एक जोडी.

```javascript
let myArray = [];
```

हे रिक्त array आहे, परंतु arrays आधीच डेटा भरून घोषित केले जाऊ शकतात. Array मधील अनेक मूल्ये अल्पविरामाने वेगळ्या केल्या जातात.

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
```

Array मधील मूल्यांना **index** नावाचे एक अद्वितीय मूल्य दिले जाते, जे array च्या सुरुवातीपासूनच्या अंतरावर आधारित असते. वरील उदाहरणात, "Chocolate" या स्ट्रिंग मूल्याचा index 0 आहे, आणि "Rocky Road" चा index 4 आहे. Array मूल्ये मिळवण्यासाठी, बदलण्यासाठी किंवा घालण्यासाठी index चा चौकोनी कंसांसह वापर करा.

✅ तुम्हाला आश्चर्य वाटते का की arrays 0 index पासून सुरू होतात? काही प्रोग्रामिंग भाषांमध्ये, indexes 1 पासून सुरू होतात. यामागे एक मनोरंजक इतिहास आहे, जो तुम्ही [Wikipedia वर वाचू शकता](https://en.wikipedia.org/wiki/Zero-based_numbering).

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors[2]; //"Vanilla"
```

तुम्ही index चा उपयोग करून मूल्य बदलू शकता, असे:

```javascript
iceCreamFlavors[4] = "Butter Pecan"; //Changed "Rocky Road" to "Butter Pecan"
```

आणि तुम्ही दिलेल्या index वर नवीन मूल्य घालू शकता, असे:

```javascript
iceCreamFlavors[5] = "Cookie Dough"; //Added "Cookie Dough"
```

✅ Array मध्ये मूल्ये जोडण्यासाठी array operators जसे की array.push() वापरणे अधिक सामान्य आहे.

Array मध्ये किती आयटम आहेत हे शोधण्यासाठी `length` प्रॉपर्टी वापरा.

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors.length; //5
```

✅ स्वतः प्रयत्न करा! तुमच्या ब्राउझरच्या कन्सोलमध्ये स्वतः तयार केलेल्या array वर काम करा आणि त्यात बदल करा.

## Loops

Loops आपल्याला पुनरावृत्ती किंवा **iterative** कार्ये करण्यास अनुमती देतात आणि बरेच वेळ आणि कोड वाचवू शकतात. प्रत्येक iteration मध्ये त्यांचे variables, values, आणि conditions वेगळे असू शकतात. JavaScript मध्ये loops चे वेगवेगळे प्रकार आहेत, आणि त्यामध्ये थोडेसे फरक असले तरी ते मूलतः एकच कार्य करतात: डेटा वर loop करणे.

### For Loop

`for` loop मध्ये iterate करण्यासाठी 3 भाग आवश्यक असतात:
- `counter` एक variable जो सामान्यतः iterations ची संख्या मोजण्यासाठी एका संख्येसह initialized केला जातो
- `condition` एक expression जो comparison operators वापरतो आणि `false` झाल्यावर loop थांबतो
- `iteration-expression` प्रत्येक iteration च्या शेवटी चालतो, सामान्यतः counter value बदलण्यासाठी वापरला जातो
  
```javascript
// Counting up to 10
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

✅ हे कोड ब्राउझर कन्सोलमध्ये चालवा. तुम्ही counter, condition, किंवा iteration expression मध्ये छोटे बदल केल्यास काय होते? तुम्ही ते उलट चालवू शकता का, countdown तयार करत?

### While loop

`for` loop च्या सिंटॅक्सच्या विपरीत, `while` loops फक्त एक condition आवश्यक असते, जे condition `false` झाल्यावर loop थांबवते. Loops मधील conditions सामान्यतः counters सारख्या इतर values वर अवलंबून असतात, आणि loop दरम्यान व्यवस्थापित करणे आवश्यक असते. Counters साठी सुरुवातीची values loop च्या बाहेर तयार करावी लागतात, आणि condition पूर्ण करण्यासाठी कोणतेही expressions, counter बदलणे यासह, loop च्या आत ठेवावे लागते.

```javascript
//Counting up to 10
let i = 0;
while (i < 10) {
 console.log(i);
 i++;
}
```

✅ तुम्ही for loop ऐवजी while loop का निवडाल? StackOverflow वर 17K viewers याच प्रश्नावर होते, आणि काही मते [तुमच्यासाठी मनोरंजक असू शकतात](https://stackoverflow.com/questions/39969145/while-loops-vs-for-loops-in-javascript).

## Loops आणि Arrays

Arrays सहसा loops सह वापरले जातात कारण बहुतेक conditions ला loop थांबवण्यासाठी array ची length आवश्यक असते, आणि index देखील counter value असू शकतो.

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];

for (let i = 0; i < iceCreamFlavors.length; i++) {
  console.log(iceCreamFlavors[i]);
} //Ends when all flavors are printed
```

✅ तुमच्या ब्राउझरच्या कन्सोलमध्ये स्वतः तयार केलेल्या array वर loop करण्याचा प्रयोग करा.

---

## 🚀 Challenge

Arrays वर loop करण्याचे for आणि while loops व्यतिरिक्त इतर मार्ग आहेत. [forEach](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach), [for-of](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/for...of), आणि [map](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/map) यांचा वापर करून तुमचा array loop पुन्हा लिहा.

## पोस्ट-लेक्चर क्विझ
[पोस्ट-लेक्चर क्विझ](https://ff-quizzes.netlify.app/web/quiz/14)

## पुनरावलोकन आणि स्व-अभ्यास

JavaScript मधील arrays मध्ये अनेक पद्धती असतात, ज्या डेटा हाताळण्यासाठी अत्यंत उपयुक्त असतात. [या पद्धतींबद्दल वाचा](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array) आणि तुमच्या स्वतःच्या array वर काही पद्धती (जसे की push, pop, slice आणि splice) वापरून पहा.

## असाइनमेंट

[Loop an Array](assignment.md)

---

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी, कृपया लक्षात ठेवा की स्वयंचलित भाषांतरांमध्ये त्रुटी किंवा अचूकतेचा अभाव असू शकतो. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून निर्माण होणाऱ्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.