<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1b0aeccb600f83c603cd70cb42df594d",
  "translation_date": "2025-08-29T16:02:53+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "hi"
}
-->
# इवेंट्स का उपयोग करके गेम बनाना

## प्री-लेक्चर क्विज़

[प्री-लेक्चर क्विज़](https://ff-quizzes.netlify.app/web/quiz/21)

## इवेंट-ड्रिवन प्रोग्रामिंग

जब हम ब्राउज़र आधारित एप्लिकेशन बनाते हैं, तो हम उपयोगकर्ता के लिए एक ग्राफिकल यूजर इंटरफेस (GUI) प्रदान करते हैं, जिससे वे हमारे बनाए गए एप्लिकेशन के साथ इंटरैक्ट कर सकें। ब्राउज़र के साथ इंटरैक्ट करने का सबसे सामान्य तरीका विभिन्न तत्वों पर क्लिक करना और टाइप करना है। एक डेवलपर के रूप में हमारी चुनौती यह है कि हमें यह नहीं पता होता कि उपयोगकर्ता ये ऑपरेशन कब करेंगे!

[इवेंट-ड्रिवन प्रोग्रामिंग](https://en.wikipedia.org/wiki/Event-driven_programming) वह प्रकार की प्रोग्रामिंग है जिसकी हमें GUI बनाने के लिए आवश्यकता होती है। यदि हम इस वाक्यांश को थोड़ा तोड़ें, तो हम देखेंगे कि इसका मुख्य शब्द **इवेंट** है। [इवेंट](https://www.merriam-webster.com/dictionary/event) को Merriam-Webster के अनुसार "कुछ ऐसा जो होता है" के रूप में परिभाषित किया गया है। यह हमारी स्थिति को पूरी तरह से वर्णित करता है। हमें पता है कि कुछ ऐसा होने वाला है जिसके लिए हम प्रतिक्रिया में कुछ कोड निष्पादित करना चाहते हैं, लेकिन हमें यह नहीं पता कि यह कब होगा।

हम जिस कोड को निष्पादित करना चाहते हैं उसे चिह्नित करने का तरीका एक फ़ंक्शन बनाना है। जब हम [प्रोसीजरल प्रोग्रामिंग](https://en.wikipedia.org/wiki/Procedural_programming) के बारे में सोचते हैं, तो फ़ंक्शन एक विशिष्ट क्रम में कॉल किए जाते हैं। यही बात इवेंट-ड्रिवन प्रोग्रामिंग के साथ भी सही है। फर्क सिर्फ इतना है कि **कैसे** फ़ंक्शन कॉल किए जाएंगे।

इवेंट्स (जैसे बटन क्लिक करना, टाइप करना आदि) को संभालने के लिए, हम **इवेंट लिसनर्स** रजिस्टर करते हैं। इवेंट लिसनर एक फ़ंक्शन होता है जो किसी इवेंट के होने का इंतजार करता है और प्रतिक्रिया में निष्पादित होता है। इवेंट लिसनर्स UI को अपडेट कर सकते हैं, सर्वर को कॉल कर सकते हैं, या उपयोगकर्ता की क्रिया के जवाब में जो भी करना आवश्यक हो वह कर सकते हैं। हम [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) का उपयोग करके और निष्पादित करने के लिए एक फ़ंक्शन प्रदान करके इवेंट लिसनर जोड़ते हैं।

> **NOTE:** यह ध्यान देने योग्य है कि इवेंट लिसनर्स बनाने के कई तरीके हैं। आप गुमनाम फ़ंक्शन का उपयोग कर सकते हैं, या नामित फ़ंक्शन बना सकते हैं। आप विभिन्न शॉर्टकट्स का उपयोग कर सकते हैं, जैसे `click` प्रॉपर्टी सेट करना, या `addEventListener` का उपयोग करना। हमारे अभ्यास में हम `addEventListener` और गुमनाम फ़ंक्शन पर ध्यान केंद्रित करेंगे, क्योंकि यह वेब डेवलपर्स द्वारा उपयोग की जाने वाली सबसे सामान्य तकनीक है। यह सबसे लचीला भी है, क्योंकि `addEventListener` सभी इवेंट्स के लिए काम करता है, और इवेंट का नाम एक पैरामीटर के रूप में प्रदान किया जा सकता है।

### सामान्य इवेंट्स

ऐप्लिकेशन बनाते समय आपके लिए [कई इवेंट्स](https://developer.mozilla.org/docs/Web/Events) उपलब्ध हैं। मूल रूप से उपयोगकर्ता द्वारा पेज पर किया गया कोई भी कार्य एक इवेंट को ट्रिगर करता है, जो आपको यह सुनिश्चित करने की शक्ति देता है कि उन्हें वह अनुभव मिले जो आप चाहते हैं। सौभाग्य से, आपको आमतौर पर केवल कुछ ही इवेंट्स की आवश्यकता होती है। यहां कुछ सामान्य इवेंट्स दिए गए हैं (जिनमें से दो का उपयोग हम अपने गेम बनाते समय करेंगे):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): उपयोगकर्ता ने किसी चीज़ पर क्लिक किया, आमतौर पर बटन या हाइपरलिंक
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): उपयोगकर्ता ने राइट माउस बटन क्लिक किया
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): उपयोगकर्ता ने कुछ टेक्स्ट को हाइलाइट किया
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): उपयोगकर्ता ने कुछ टेक्स्ट इनपुट किया

## गेम बनाना

हम इवेंट्स के काम करने के तरीके को समझने के लिए एक गेम बनाएंगे। हमारा गेम खिलाड़ी की टाइपिंग स्किल का परीक्षण करेगा, जो सभी डेवलपर्स के लिए एक अत्यधिक महत्वपूर्ण कौशल है। हमें अपनी टाइपिंग का अभ्यास करते रहना चाहिए! गेम का सामान्य प्रवाह इस प्रकार होगा:

- खिलाड़ी स्टार्ट बटन पर क्लिक करता है और टाइप करने के लिए एक कोट प्रस्तुत किया जाता है
- खिलाड़ी टेक्स्टबॉक्स में कोट को जितनी जल्दी हो सके टाइप करता है
  - जैसे ही प्रत्येक शब्द पूरा होता है, अगला शब्द हाइलाइट हो जाता है
  - यदि खिलाड़ी ने टाइपो किया है, तो टेक्स्टबॉक्स लाल हो जाता है
  - जब खिलाड़ी कोट पूरा करता है, तो एक सफलता संदेश प्रदर्शित होता है और समय दिखाया जाता है

आइए अपना गेम बनाएं और इवेंट्स के बारे में जानें!

### फाइल संरचना

हमें कुल तीन फाइलों की आवश्यकता होगी: **index.html**, **script.js** और **style.css**। आइए उन्हें सेटअप करें ताकि हमारा काम आसान हो जाए।

- एक नया फोल्डर बनाएं और कंसोल या टर्मिनल विंडो में निम्नलिखित कमांड चलाएं:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- Visual Studio Code खोलें

```bash
code .
```

- Visual Studio Code में फोल्डर में तीन फाइलें जोड़ें:
  - index.html
  - script.js
  - style.css

## यूजर इंटरफेस बनाएं

यदि हम आवश्यकताओं का विश्लेषण करें, तो हमें अपने HTML पेज पर कुछ तत्वों की आवश्यकता होगी। यह एक रेसिपी की तरह है, जहां हमें कुछ सामग्री चाहिए:

- उपयोगकर्ता के लिए टाइप करने के लिए कोट प्रदर्शित करने की जगह
- कोई भी संदेश प्रदर्शित करने की जगह, जैसे सफलता संदेश
- टाइपिंग के लिए एक टेक्स्टबॉक्स
- एक स्टार्ट बटन

इनमें से प्रत्येक को IDs की आवश्यकता होगी ताकि हम उन्हें अपने JavaScript में उपयोग कर सकें। हम उन CSS और JavaScript फाइलों के संदर्भ भी जोड़ेंगे जिन्हें हम बनाने जा रहे हैं।

एक नई फाइल **index.html** बनाएं। निम्नलिखित HTML जोड़ें:

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

### एप्लिकेशन लॉन्च करें

हमेशा बेहतर होता है कि हम धीरे-धीरे डेवलप करें और देखें कि चीजें कैसी दिखती हैं। आइए अपना एप्लिकेशन लॉन्च करें। Visual Studio Code के लिए एक शानदार एक्सटेंशन है [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon), जो आपके एप्लिकेशन को लोकली होस्ट करेगा और हर बार जब आप सेव करेंगे तो ब्राउज़र को रिफ्रेश करेगा।

- [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) इंस्टॉल करें
  - ब्राउज़र आपको Visual Studio Code खोलने के लिए कहेगा, और फिर Visual Studio Code इंस्टॉलेशन करने के लिए कहेगा
  - यदि Visual Studio Code आपको पुनः आरंभ करने के लिए कहे, तो करें
- Visual Studio Code में, Ctrl-Shift-P (या Cmd-Shift-P) दबाएं और कमांड पैलेट खोलें
- **Live Server: Open with Live Server** टाइप करें
  - Live Server आपके एप्लिकेशन को होस्ट करना शुरू कर देगा
- ब्राउज़र खोलें और **https://localhost:5500** पर जाएं
- अब आपको वह पेज दिखना चाहिए जो आपने बनाया है!

आइए कुछ फंक्शनलिटी जोड़ें।

## CSS जोड़ें

हमारे HTML के साथ, आइए कोर स्टाइलिंग के लिए CSS जोड़ें। हमें उस शब्द को हाइलाइट करना होगा जिसे खिलाड़ी टाइप कर रहा है, और यदि उन्होंने गलत टाइप किया है तो टेक्स्टबॉक्स को रंगीन बनाना होगा। हम इसे दो क्लासेस के साथ करेंगे।

एक नई फाइल **style.css** बनाएं और निम्नलिखित सिंटैक्स जोड़ें।

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

✅ CSS के मामले में आप अपने पेज को जैसा चाहें वैसा डिज़ाइन कर सकते हैं। थोड़ा समय लें और पेज को अधिक आकर्षक बनाएं:

- एक अलग फॉन्ट चुनें
- हेडर्स को रंगीन बनाएं
- आइटम्स का आकार बदलें

## JavaScript

हमारे UI के साथ, अब हम JavaScript पर ध्यान केंद्रित करेंगे जो लॉजिक प्रदान करेगा। हम इसे कुछ चरणों में तोड़ेंगे:

- [कॉन्स्टेंट्स बनाएं](../../../../4-typing-game/typing-game)
- [गेम शुरू करने के लिए इवेंट लिसनर](../../../../4-typing-game/typing-game)
- [टाइपिंग के लिए इवेंट लिसनर](../../../../4-typing-game/typing-game)

लेकिन पहले, एक नई फाइल **script.js** बनाएं।

### कॉन्स्टेंट्स जोड़ें

हमें प्रोग्रामिंग को आसान बनाने के लिए कुछ आइटम्स की आवश्यकता होगी। यह एक रेसिपी की तरह है, जहां हमें कुछ सामग्री चाहिए:

- सभी कोट्स की सूची वाला एक ऐरे
- वर्तमान कोट के सभी शब्दों को स्टोर करने के लिए एक खाली ऐरे
- खिलाड़ी जिस शब्द को टाइप कर रहा है उसका इंडेक्स स्टोर करने की जगह
- खिलाड़ी ने स्टार्ट पर क्लिक किया था उस समय को स्टोर करने की जगह

हमें UI तत्वों के संदर्भ भी चाहिए:

- टेक्स्टबॉक्स (**typed-value**)
- कोट डिस्प्ले (**quote**)
- संदेश (**message**)

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

✅ अपने गेम में और कोट्स जोड़ें

> **NOTE:** हम `document.getElementById` का उपयोग करके जब चाहें कोड में तत्वों को प्राप्त कर सकते हैं। चूंकि हम इन तत्वों को नियमित रूप से संदर्भित करने जा रहे हैं, हम स्ट्रिंग लिटरल में टाइपो से बचने के लिए कॉन्स्टेंट्स का उपयोग करेंगे। [Vue.js](https://vuejs.org/) या [React](https://reactjs.org/) जैसे फ्रेमवर्क्स आपके कोड को केंद्रीकृत करने में मदद कर सकते हैं।

`const`, `let` और `var` का उपयोग करने पर एक वीडियो देखें:

[![वेरिएबल्स के प्रकार](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "वेरिएबल्स के प्रकार")

> 🎥 ऊपर दी गई छवि पर क्लिक करें वेरिएबल्स के बारे में वीडियो देखने के लिए।

### स्टार्ट लॉजिक जोड़ें

गेम शुरू करने के लिए, खिलाड़ी स्टार्ट पर क्लिक करेगा। बेशक, हमें यह नहीं पता कि वे स्टार्ट पर कब क्लिक करेंगे। यही वह जगह है जहां [इवेंट लिसनर](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) काम आता है। इवेंट लिसनर हमें किसी चीज़ के होने (इवेंट) का इंतजार करने और प्रतिक्रिया में कोड निष्पादित करने की अनुमति देगा। हमारे मामले में, हम चाहते हैं कि जब उपयोगकर्ता स्टार्ट पर क्लिक करे तो कोड निष्पादित हो।

जब उपयोगकर्ता **स्टार्ट** पर क्लिक करता है, तो हमें एक कोट चुनना होगा, यूजर इंटरफेस सेटअप करना होगा, और वर्तमान शब्द और टाइमिंग के लिए ट्रैकिंग सेटअप करनी होगी। नीचे वह JavaScript है जिसे आपको जोड़ना होगा; हम इसे स्क्रिप्ट ब्लॉक के बाद चर्चा करेंगे।

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

आइए कोड को तोड़ें!

- शब्द ट्रैकिंग सेटअप करें
  - [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) और [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) का उपयोग हमें `quotes` ऐरे से रैंडमली एक कोट चुनने की अनुमति देता है
  - हम `quote` को `words` ऐरे में बदलते हैं ताकि हम उस शब्द को ट्रैक कर सकें जिसे खिलाड़ी वर्तमान में टाइप कर रहा है
  - `wordIndex` को 0 पर सेट किया जाता है, क्योंकि खिलाड़ी पहले शब्द से शुरू करेगा
- UI सेटअप करें
  - `spanWords` का एक ऐरे बनाएं, जिसमें प्रत्येक शब्द एक `span` तत्व के अंदर हो
    - यह हमें डिस्प्ले पर शब्द को हाइलाइट करने की अनुमति देगा
  - `join` का उपयोग करके ऐरे को एक स्ट्रिंग में बदलें जिसे हम `quoteElement` के `innerHTML` को अपडेट करने के लिए उपयोग कर सकते हैं
    - यह कोट को खिलाड़ी को प्रदर्शित करेगा
  - पहले `span` तत्व के `className` को `highlight` पर सेट करें ताकि इसे पीले रंग में हाइलाइट किया जा सके
  - `messageElement` को साफ करें और `innerText` को `''` पर सेट करें
- टेक्स्टबॉक्स सेटअप करें
  - वर्तमान `value` को `typedValueElement` पर साफ करें
  - `typedValueElement` पर `focus` सेट करें
- टाइमर शुरू करें `getTime` को कॉल करके

### टाइपिंग लॉजिक जोड़ें

जैसे ही खिलाड़ी टाइप करता है, एक `input` इवेंट उठाया जाएगा। यह इवेंट लिसनर यह सुनिश्चित करेगा कि खिलाड़ी शब्द को सही तरीके से टाइप कर रहा है, और गेम की वर्तमान स्थिति को संभालेगा। **script.js** में वापस जाएं और निम्नलिखित कोड को अंत में जोड़ें। हम इसे बाद में तोड़ेंगे।

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

आइए कोड को तोड़ें! हम वर्तमान शब्द और खिलाड़ी द्वारा अब तक टाइप किए गए मूल्य को प्राप्त करके शुरू करते हैं। फिर हमारे पास वॉटरफॉल लॉजिक है, जहां हम जांचते हैं कि कोट पूरा है, शब्द पूरा है, शब्द सही है, या (अंत में), कोई त्रुटि है।

- कोट पूरा है, जिसे `typedValue` के `currentWord` के बराबर होने और `wordIndex` के `words` की `length` से एक कम होने से संकेत मिलता है
  - `elapsedTime` की गणना वर्तमान समय से `startTime` घटाकर करें
  - `elapsedTime` को 1,000 से विभाजित करें ताकि इसे मिलीसेकंड से सेकंड में बदल सकें
  - एक सफलता संदेश प्रदर्शित करें
- शब्द पूरा है, जिसे `typedValue` के स्पेस के साथ समाप्त होने और `typedValue` के `currentWord` के बराबर होने से संकेत मिलता है
  - अगले शब्द को टाइप करने की अनुमति देने के लिए `typedElement` पर `value` को `''` पर सेट करें
  - अगले शब्द पर जाने के लिए `wordIndex` को बढ़ाएं
  - `quoteElement` के सभी `childNodes` के माध्यम से लूप करें और `className` को `''` पर सेट करें ताकि इसे डिफ़ॉल्ट डिस्प्ले पर वापस लाया जा सके
  - वर्तमान शब्द के `className` को `highlight` पर सेट करें ताकि इसे टाइप करने के लिए अगला शब्द फ्लैग किया जा सके
- शब्द वर्तमान में सही तरीके से टाइप किया गया है (लेकिन पूरा नहीं हुआ है), जिसे `currentWord` के `typedValue` से शुरू होने से संकेत मिलता है
  - `typedValueElement` को डिफ़ॉल्ट रूप से प्रदर्शित करने के लिए सुनिश्चित करें और `className` को साफ करें
- यदि हम यहां तक पहुंच गए हैं, तो हमारे पास एक त्रुटि है
  - `typedValueElement` पर `className` को `error` पर सेट करें

## अपने एप्लिकेशन का परीक्षण करें

आप अंत तक पहुंच गए हैं! अंतिम चरण यह सुनिश्चित करना है कि हमारा एप्लिकेशन काम करता है। इसे आज़माएं! यदि कोई त्रुटि है तो चिंता न करें; **सभी डेवलपर्स** को त्रुटियां होती हैं। संदेशों की जांच करें और आवश्यकतानुसार डिबग करें।

**स्टार्ट** पर क्लिक करें और टाइप करना शुरू करें! यह कुछ इस तरह दिखना चाहिए जैसा हमने पहले एनिमेशन में देखा था।

![गेम का डेमो](../../../../4-typing-game/images/demo.gif)

---

## 🚀 चुनौती

अधिक फंक्शनलिटी जोड़ें

- कोट पूरा होने पर `input` इवेंट लिसनर को डिसेबल करें, और बटन क्लिक करने पर इसे फिर से सक्षम करें
- जब खिलाड़ी कोट पूरा करता है तो टेक्स्टबॉक्स को डिसेबल करें
- सफलता संदेश के साथ एक मोडल डायलॉग बॉक्स प्रदर्शित करें
- [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage) का उपयोग करके हाई स्कोर स्टोर करें
## पोस्ट-लेक्चर क्विज़

[पोस्ट-लेक्चर क्विज़](https://ff-quizzes.netlify.app/web/quiz/22)

## समीक्षा और स्व-अध्ययन

वेब ब्राउज़र के माध्यम से डेवलपर के लिए उपलब्ध [सभी इवेंट्स](https://developer.mozilla.org/docs/Web/Events) के बारे में पढ़ें, और उन परिस्थितियों पर विचार करें जिनमें आप प्रत्येक का उपयोग करेंगे।

## असाइनमेंट

[एक नया कीबोर्ड गेम बनाएं](assignment.md)

---

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता सुनिश्चित करने का प्रयास करते हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को प्रामाणिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम उत्तरदायी नहीं हैं।