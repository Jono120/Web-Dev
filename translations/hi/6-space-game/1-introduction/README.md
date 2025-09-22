<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "979cfcce2413a87d9e4c67eb79234bc3",
  "translation_date": "2025-08-29T15:57:09+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "hi"
}
-->
# स्पेस गेम बनाएं भाग 1: परिचय

![वीडियो](../../../../6-space-game/images/pewpew.gif)

## प्री-लेक्चर क्विज़

[प्री-लेक्चर क्विज़](https://ff-quizzes.netlify.app/web/quiz/29)

### गेम डेवलपमेंट में इनहेरिटेंस और कंपोज़िशन

पिछले पाठों में, आपके द्वारा बनाए गए ऐप्स के डिज़ाइन आर्किटेक्चर के बारे में ज्यादा सोचने की ज़रूरत नहीं थी, क्योंकि प्रोजेक्ट्स का दायरा बहुत छोटा था। हालांकि, जब आपके एप्लिकेशन का आकार और दायरा बढ़ता है, तो आर्किटेक्चरल निर्णय अधिक महत्वपूर्ण हो जाते हैं। जावास्क्रिप्ट में बड़े एप्लिकेशन बनाने के दो प्रमुख तरीके हैं: *कंपोज़िशन* या *इनहेरिटेंस*। दोनों के अपने फायदे और नुकसान हैं, लेकिन आइए इन्हें एक गेम के संदर्भ में समझते हैं।

✅ अब तक लिखी गई सबसे प्रसिद्ध प्रोग्रामिंग किताबों में से एक [डिज़ाइन पैटर्न्स](https://en.wikipedia.org/wiki/Design_Patterns) के बारे में है।

एक गेम में आपके पास `गेम ऑब्जेक्ट्स` होते हैं, जो स्क्रीन पर मौजूद ऑब्जेक्ट्स होते हैं। इसका मतलब है कि उनका एक स्थान होता है, जो कार्टेशियन कोऑर्डिनेट सिस्टम पर `x` और `y` कोऑर्डिनेट्स द्वारा दर्शाया जाता है। जब आप एक गेम विकसित करते हैं, तो आप देखेंगे कि आपके सभी गेम ऑब्जेक्ट्स में कुछ सामान्य गुण होते हैं, जो हर गेम में समान होते हैं, जैसे:

- **स्थान आधारित**: अधिकांश, यदि सभी नहीं, गेम एलिमेंट्स स्थान आधारित होते हैं। इसका मतलब है कि उनका एक स्थान होता है, `x` और `y`।
- **चलने योग्य**: ये ऐसे ऑब्जेक्ट्स होते हैं जो एक नए स्थान पर जा सकते हैं। आमतौर पर ये हीरो, मॉन्स्टर या एनपीसी (नॉन प्लेयर कैरेक्टर) होते हैं, लेकिन उदाहरण के लिए, एक स्थिर वस्तु जैसे पेड़ नहीं।
- **स्वयं-विनाशकारी**: ये ऑब्जेक्ट्स केवल एक निश्चित समय अवधि के लिए मौजूद रहते हैं और फिर खुद को डिलीट करने के लिए तैयार कर लेते हैं। आमतौर पर इसे `dead` या `destroyed` बूलियन द्वारा दर्शाया जाता है, जो गेम इंजन को संकेत देता है कि इस ऑब्जेक्ट को अब रेंडर नहीं किया जाना चाहिए।
- **कूल-डाउन**: 'कूल-डाउन' एक सामान्य गुण है जो अल्पकालिक ऑब्जेक्ट्स में पाया जाता है। इसका एक सामान्य उदाहरण एक टेक्स्ट का टुकड़ा या ग्राफिकल इफेक्ट (जैसे विस्फोट) है, जिसे केवल कुछ मिलीसेकंड के लिए देखा जाना चाहिए।

✅ एक गेम जैसे पैक-मैन के बारे में सोचें। क्या आप इस गेम में ऊपर सूचीबद्ध चार ऑब्जेक्ट प्रकारों की पहचान कर सकते हैं?

### व्यवहार व्यक्त करना

ऊपर जो कुछ भी हमने वर्णित किया, वह गेम ऑब्जेक्ट्स का व्यवहार है। तो हम इसे कैसे कोड करते हैं? हम इस व्यवहार को या तो क्लासेस या ऑब्जेक्ट्स से जुड़े मेथड्स के रूप में व्यक्त कर सकते हैं।

**क्लासेस**

आइडिया यह है कि `क्लासेस` का उपयोग `इनहेरिटेंस` के साथ किया जाए ताकि किसी क्लास में एक निश्चित व्यवहार जोड़ा जा सके।

✅ इनहेरिटेंस एक महत्वपूर्ण अवधारणा है जिसे समझना चाहिए। [MDN के इनहेरिटेंस पर लेख](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) पर और जानें।

कोड के माध्यम से व्यक्त किया गया, एक गेम ऑब्जेक्ट आमतौर पर इस तरह दिख सकता है:

```javascript

//set up the class GameObject
class GameObject {
  constructor(x, y, type) {
    this.x = x;
    this.y = y;
    this.type = type;
  }
}

//this class will extend the GameObject's inherent class properties
class Movable extends GameObject {
  constructor(x,y, type) {
    super(x,y, type)
  }

//this movable object can be moved on the screen
  moveTo(x, y) {
    this.x = x;
    this.y = y;
  }
}

//this is a specific class that extends the Movable class, so it can take advantage of all the properties that it inherits
class Hero extends Movable {
  constructor(x,y) {
    super(x,y, 'Hero')
  }
}

//this class, on the other hand, only inherits the GameObject properties
class Tree extends GameObject {
  constructor(x,y) {
    super(x,y, 'Tree')
  }
}

//a hero can move...
const hero = new Hero();
hero.moveTo(5,5);

//but a tree cannot
const tree = new Tree();
```

✅ कुछ मिनट लें और पैक-मैन के हीरो (जैसे इनकी, पिंकी या ब्लिंकी) को फिर से कल्पना करें और सोचें कि इसे जावास्क्रिप्ट में कैसे लिखा जाएगा।

**कंपोज़िशन**

ऑब्जेक्ट इनहेरिटेंस को संभालने का एक अलग तरीका *कंपोज़िशन* का उपयोग करना है। तब, ऑब्जेक्ट्स इस तरह से अपना व्यवहार व्यक्त करते हैं:

```javascript
//create a constant gameObject
const gameObject = {
  x: 0,
  y: 0,
  type: ''
};

//...and a constant movable
const movable = {
  moveTo(x, y) {
    this.x = x;
    this.y = y;
  }
}
//then the constant movableObject is composed of the gameObject and movable constants
const movableObject = {...gameObject, ...movable};

//then create a function to create a new Hero who inherits the movableObject properties
function createHero(x, y) {
  return {
    ...movableObject,
    x,
    y,
    type: 'Hero'
  }
}
//...and a static object that inherits only the gameObject properties
function createStatic(x, y, type) {
  return {
    ...gameObject
    x,
    y,
    type
  }
}
//create the hero and move it
const hero = createHero(10,10);
hero.moveTo(5,5);
//and create a static tree which only stands around
const tree = createStatic(0,0, 'Tree'); 
```

**मुझे कौन सा पैटर्न उपयोग करना चाहिए?**

यह आप पर निर्भर करता है कि आप कौन सा पैटर्न चुनते हैं। जावास्क्रिप्ट इन दोनों पैटर्न्स का समर्थन करता है।

--

गेम डेवलपमेंट में एक और सामान्य पैटर्न गेम के उपयोगकर्ता अनुभव और प्रदर्शन को संभालने की समस्या को हल करता है।

## पब/सब पैटर्न

✅ पब/सब का मतलब है 'पब्लिश-सब्सक्राइब'

यह पैटर्न इस विचार को संबोधित करता है कि आपके एप्लिकेशन के विभिन्न हिस्सों को एक-दूसरे के बारे में नहीं पता होना चाहिए। ऐसा क्यों? यह सामान्य रूप से यह देखना बहुत आसान बनाता है कि क्या हो रहा है, यदि विभिन्न हिस्से अलग-अलग हैं। यह अचानक व्यवहार बदलने को भी आसान बनाता है, यदि आपको इसकी आवश्यकता हो। हम इसे कैसे प्राप्त करते हैं? हम कुछ अवधारणाओं को स्थापित करके ऐसा करते हैं:

- **संदेश**: एक संदेश आमतौर पर एक टेक्स्ट स्ट्रिंग होता है, जिसके साथ एक वैकल्पिक पेलोड (डेटा का एक टुकड़ा जो संदेश के बारे में स्पष्ट करता है) होता है। गेम में एक सामान्य संदेश हो सकता है `KEY_PRESSED_ENTER`।
- **पब्लिशर**: यह तत्व एक संदेश *पब्लिश* करता है और इसे सभी सब्सक्राइबर्स को भेजता है।
- **सब्सक्राइबर**: यह तत्व विशिष्ट संदेशों को *सुनता* है और इस संदेश को प्राप्त करने के परिणामस्वरूप कुछ कार्य करता है, जैसे लेज़र फायर करना।

इसका कार्यान्वयन आकार में बहुत छोटा है, लेकिन यह एक बहुत ही शक्तिशाली पैटर्न है। इसे इस तरह लागू किया जा सकता है:

```javascript
//set up an EventEmitter class that contains listeners
class EventEmitter {
  constructor() {
    this.listeners = {};
  }
//when a message is received, let the listener to handle its payload
  on(message, listener) {
    if (!this.listeners[message]) {
      this.listeners[message] = [];
    }
    this.listeners[message].push(listener);
  }
//when a message is sent, send it to a listener with some payload
  emit(message, payload = null) {
    if (this.listeners[message]) {
      this.listeners[message].forEach(l => l(message, payload))
    }
  }
}

```

ऊपर दिए गए कोड का उपयोग करने के लिए, हम एक बहुत छोटा कार्यान्वयन बना सकते हैं:

```javascript
//set up a message structure
const Messages = {
  HERO_MOVE_LEFT: 'HERO_MOVE_LEFT'
};
//invoke the eventEmitter you set up above
const eventEmitter = new EventEmitter();
//set up a hero
const hero = createHero(0,0);
//let the eventEmitter know to watch for messages pertaining to the hero moving left, and act on it
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});

//set up the window to listen for the keyup event, specifically if the left arrow is hit, emit a message to move the hero left
window.addEventListener('keyup', (evt) => {
  if (evt.key === 'ArrowLeft') {
    eventEmitter.emit(Messages.HERO_MOVE_LEFT)
  }
});
```

ऊपर, हम एक कीबोर्ड इवेंट, `ArrowLeft` को कनेक्ट करते हैं और `HERO_MOVE_LEFT` संदेश भेजते हैं। हम उस संदेश को सुनते हैं और परिणामस्वरूप `हीरो` को मूव करते हैं। इस पैटर्न की ताकत यह है कि इवेंट लिसनर और हीरो एक-दूसरे के बारे में नहीं जानते। आप `ArrowLeft` को `A` कुंजी पर रीमैप कर सकते हैं। इसके अलावा, यह संभव होगा कि `ArrowLeft` पर कुछ पूरी तरह से अलग किया जाए, इवेंटएमिटर के `on` फ़ंक्शन में कुछ संपादन करके:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

जैसे-जैसे आपका गेम बढ़ता है और चीजें अधिक जटिल हो जाती हैं, यह पैटर्न जटिलता में समान रहता है और आपका कोड साफ रहता है। इस पैटर्न को अपनाने की सिफारिश की जाती है।

---

## 🚀 चुनौती

सोचें कि पब-सब पैटर्न एक गेम को कैसे बेहतर बना सकता है। कौन से हिस्से इवेंट्स को एमिट करें, और गेम को उन पर कैसे प्रतिक्रिया देनी चाहिए? अब आपके पास एक नया गेम सोचने और इसके हिस्सों के व्यवहार की कल्पना करने का मौका है।

## पोस्ट-लेक्चर क्विज़

[पोस्ट-लेक्चर क्विज़](https://ff-quizzes.netlify.app/web/quiz/30)

## समीक्षा और स्व-अध्ययन

पब/सब के बारे में और जानें [इसे पढ़कर](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon)।

## असाइनमेंट

[एक गेम का मॉकअप बनाएं](assignment.md)

---

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता सुनिश्चित करने का प्रयास करते हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को प्रामाणिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम उत्तरदायी नहीं हैं।