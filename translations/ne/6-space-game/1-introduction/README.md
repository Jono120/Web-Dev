<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "979cfcce2413a87d9e4c67eb79234bc3",
  "translation_date": "2025-08-28T16:37:38+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "ne"
}
-->
# स्पेस गेम बनाउनुहोस् भाग १: परिचय

![video](../../../../6-space-game/images/pewpew.gif)

## प्रि-लेक्चर क्विज

[प्रि-लेक्चर क्विज](https://ff-quizzes.netlify.app/web/quiz/29)

### खेल विकासमा इनहेरिटेन्स र कम्पोजिसन

अघिल्ला पाठहरूमा, तपाईंले बनाएका एप्सको डिजाइन आर्किटेक्चरको बारेमा धेरै सोच्न आवश्यक थिएन, किनभने परियोजनाहरू सानो दायरामा थिए। तर, जब तपाईंका एप्लिकेसनहरू आकार र दायरामा बढ्छन्, आर्किटेक्चरल निर्णयहरू महत्त्वपूर्ण बन्छन्। जाभास्क्रिप्टमा ठूला एप्लिकेसनहरू बनाउन दुई प्रमुख दृष्टिकोणहरू छन्: *कम्पोजिसन* वा *इनहेरिटेन्स*। दुबैको आफ्नै फाइदा र बेफाइदा छन्, तर यसलाई खेलको सन्दर्भबाट बुझौं।

✅ सबैभन्दा प्रसिद्ध प्रोग्रामिङ पुस्तकहरूमध्ये एक [डिजाइन प्याटर्न्स](https://en.wikipedia.org/wiki/Design_Patterns) को बारेमा हो।

खेलमा तपाईंसँग `game objects` हुन्छन्, जुन स्क्रिनमा हुने वस्तुहरू हुन्। यसको मतलब तिनीहरूको कार्टेसियन कोअर्डिनेट प्रणालीमा स्थान हुन्छ, जसलाई `x` र `y` कोअर्डिनेटले परिभाषित गरिन्छ। जब तपाईं खेल विकास गर्नुहुन्छ, तपाईंले देख्नुहुनेछ कि तपाईंका सबै खेल वस्तुहरूमा केही मानक विशेषताहरू हुन्छन्, जुन तपाईंले बनाउने हरेक खेलका लागि समान हुन्छन्। ती विशेषताहरू हुन्:

- **स्थान-आधारित**: प्रायः सबै खेलका तत्वहरू स्थान-आधारित हुन्छन्। यसको मतलब तिनीहरूको `x` र `y` स्थान हुन्छ।
- **चलायमान**: यी वस्तुहरू नयाँ स्थानमा सर्न सक्छन्। यो प्रायः नायक, राक्षस वा NPC (गैर-खेलाडी पात्र) हुन्छ, तर उदाहरणका लागि, रूखजस्तो स्थिर वस्तु हुँदैन।
- **आफै-विनाशकारी**: यी वस्तुहरू निश्चित समयको लागि मात्र अस्तित्वमा रहन्छन् र त्यसपछि मेटिन तयार हुन्छन्। सामान्यतया यो `dead` वा `destroyed` बूलियनले प्रतिनिधित्व गरिन्छ, जसले खेल इन्जिनलाई यो वस्तु अब रेंडर गर्न नपर्ने संकेत दिन्छ।
- **कूल-डाउन**: 'कूल-डाउन' छोटो समयका वस्तुहरूमा सामान्य विशेषता हो। यसको उदाहरण भनेको केही मिलिसेकेन्डका लागि मात्र देखिनुपर्ने पाठ वा विस्फोटजस्तो ग्राफिकल प्रभाव हो।

✅ प्याक-म्यानजस्तो खेलको बारेमा सोच्नुहोस्। के तपाईंले माथि सूचीबद्ध चारवटा वस्तु प्रकारहरू यस खेलमा पहिचान गर्न सक्नुहुन्छ?

### व्यवहार व्यक्त गर्दै

माथि वर्णन गरिएका सबै खेल वस्तुहरूको व्यवहार हो। त्यसोभए हामी यसलाई कसरी कोड गर्छौं? हामी यस व्यवहारलाई कक्षाहरू वा वस्तुहरूसँग सम्बन्धित विधिहरूको रूपमा व्यक्त गर्न सक्छौं।

**कक्षाहरू**

विचार यो हो कि `classes` लाई `inheritance` सँग मिलाएर कक्षामा निश्चित व्यवहार थप्न प्रयोग गरिन्छ।

✅ इनहेरिटेन्स महत्त्वपूर्ण अवधारणा हो। [MDN को इनहेरिटेन्सको लेख](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) मा थप जान्नुहोस्।

कोडमार्फत व्यक्त गर्दा, खेल वस्तु सामान्यतया यसरी देखिन्छ:

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

✅ केही मिनेट समय लिएर प्याक-म्यान नायक (उदाहरणका लागि, इन्की, पिन्की वा ब्लिन्की) लाई पुनः कल्पना गर्नुहोस् र यसलाई जाभास्क्रिप्टमा कसरी लेखिनेछ भनेर सोच्नुहोस्।

**कम्पोजिसन**

वस्तु इनहेरिटेन्सलाई ह्यान्डल गर्ने अर्को तरिका भनेको *कम्पोजिसन* प्रयोग गर्नु हो। त्यसपछि, वस्तुहरूले आफ्नो व्यवहार यसरी व्यक्त गर्छन्:

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

**कुन पैटर्न प्रयोग गर्ने?**

तपाईं कुन पैटर्न प्रयोग गर्ने भन्ने निर्णय तपाईंको हातमा छ। जाभास्क्रिप्टले यी दुवै दृष्टिकोणलाई समर्थन गर्छ।

--

खेल विकासमा अर्को सामान्य पैटर्नले खेलको प्रयोगकर्ता अनुभव र प्रदर्शनलाई ह्यान्डल गर्ने समस्यालाई सम्बोधन गर्छ।

## पब/सब पैटर्न

✅ पब/सबको अर्थ 'पब्लिश-सब्स्क्राइब' हो।

यो पैटर्नले तपाईंको एप्लिकेसनका विभिन्न भागहरूले एकअर्काको बारेमा थाहा नपाउने विचारलाई सम्बोधन गर्छ। किन? यसले सामान्यतया के भइरहेको छ भनेर बुझ्न सजिलो बनाउँछ यदि विभिन्न भागहरू अलग छन् भने। यसले तपाईंलाई अचानक व्यवहार परिवर्तन गर्न आवश्यक परेमा पनि सजिलो बनाउँछ। हामी यो कसरी पूरा गर्छौं? हामी केही अवधारणाहरू स्थापना गरेर यो गर्छौं:

- **सन्देश**: सन्देश सामान्यतया पाठ स्ट्रिङ हुन्छ, जससँग वैकल्पिक पेलोड (सन्देशको बारेमा स्पष्ट पार्ने डाटा) हुन्छ। खेलमा एउटा सामान्य सन्देश `KEY_PRESSED_ENTER` हुन सक्छ।
- **पब्लिशर**: यो तत्वले सन्देश *पब्लिश* गर्छ र सबै सब्स्क्राइबरहरूलाई पठाउँछ।
- **सब्स्क्राइबर**: यो तत्वले विशिष्ट सन्देशहरू *सुन्छ* र यो सन्देश प्राप्त भएपछि कुनै कार्य गर्दछ, जस्तै लेजर फायर गर्नु।

यसको कार्यान्वयन सानो आकारको हुन्छ तर यो धेरै शक्तिशाली पैटर्न हो। यसलाई यसरी कार्यान्वयन गर्न सकिन्छ:

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

माथिको कोड प्रयोग गर्न हामी सानो कार्यान्वयन बनाउन सक्छौं:

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

माथि हामीले `ArrowLeft` कीबोर्ड इभेन्टलाई जडान गर्यौं र `HERO_MOVE_LEFT` सन्देश पठायौं। हामीले त्यो सन्देश सुनेर नायकलाई सार्यौं। यस पैटर्नको बल यो हो कि इभेन्ट लिस्नर र नायकले एकअर्काको बारेमा थाहा पाउँदैनन्। तपाईंले `ArrowLeft` लाई `A` कुञ्जीमा पुनः म्याप गर्न सक्नुहुन्छ। थप रूपमा, `ArrowLeft` मा केही पूर्ण रूपमा फरक गर्न सम्भव हुनेछ इभेन्टइमिटरको `on` फङ्सनमा केही सम्पादन गरेर:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

जब तपाईंको खेल बढ्छ र जटिल बन्छ, यो पैटर्न जटिलतामा स्थिर रहन्छ र तपाईंको कोड सफा रहन्छ। यो पैटर्न अपनाउन अत्यधिक सिफारिस गरिन्छ।

---

## 🚀 चुनौती

पब-सब पैटर्नले खेललाई कसरी सुधार गर्न सक्छ भनेर सोच्नुहोस्। कुन भागहरूले इभेन्टहरू उत्सर्जन गर्नुपर्छ, र खेलले तिनीहरूमा कसरी प्रतिक्रिया दिनुपर्छ? अब नयाँ खेलको कल्पना गर्ने र यसको भागहरूले कसरी व्यवहार गर्न सक्छन् भनेर सोच्ने मौका हो।

## पोस्ट-लेक्चर क्विज

[पोस्ट-लेक्चर क्विज](https://ff-quizzes.netlify.app/web/quiz/30)

## समीक्षा र आत्म-अध्ययन

पब/सबको बारेमा [पढेर](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon) थप जान्नुहोस्।

## असाइनमेन्ट

[खेलको मोकअप बनाउनुहोस्](assignment.md)

---

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरेर अनुवाद गरिएको छ। हामी शुद्धताको लागि प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छ। यसको मूल भाषा मा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीको लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।