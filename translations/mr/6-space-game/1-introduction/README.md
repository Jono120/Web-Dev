<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "979cfcce2413a87d9e4c67eb79234bc3",
  "translation_date": "2025-08-28T16:17:10+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "mr"
}
-->
# स्पेस गेम तयार करा भाग 1: परिचय

![video](../../../../6-space-game/images/pewpew.gif)

## पूर्व-व्याख्यान प्रश्नमंजुषा

[पूर्व-व्याख्यान प्रश्नमंजुषा](https://ff-quizzes.netlify.app/web/quiz/29)

### गेम डेव्हलपमेंटमधील इनहेरिटन्स आणि कंपोझिशन

मागील धड्यांमध्ये, तुम्ही तयार केलेल्या अॅप्सच्या डिझाइन आर्किटेक्चरबद्दल फारसा विचार करण्याची गरज नव्हती, कारण प्रकल्पांचा आवाका खूपच लहान होता. मात्र, जेव्हा तुमचे अॅप्लिकेशन्स आकाराने आणि आवाक्याने मोठे होतात, तेव्हा आर्किटेक्चरल निर्णय महत्त्वाचे ठरतात. जावास्क्रिप्टमध्ये मोठ्या अॅप्लिकेशन्स तयार करण्यासाठी दोन प्रमुख दृष्टिकोन आहेत: *कंपोझिशन* किंवा *इनहेरिटन्स*. दोन्हींचे फायदे आणि तोटे आहेत, पण चला त्यांना गेमच्या संदर्भात समजून घेऊया.

✅ सर्वात प्रसिद्ध प्रोग्रामिंग पुस्तकांपैकी एक [डिझाइन पॅटर्न्स](https://en.wikipedia.org/wiki/Design_Patterns) यावर आधारित आहे.

एका गेममध्ये `गेम ऑब्जेक्ट्स` असतात, जे स्क्रीनवर असलेले ऑब्जेक्ट्स असतात. याचा अर्थ त्यांना कार्टेशियन कोऑर्डिनेट सिस्टमवर स्थान असते, ज्यामध्ये `x` आणि `y` कोऑर्डिनेट्स असतात. गेम विकसित करताना तुम्हाला लक्षात येईल की तुमच्या सर्व गेम ऑब्जेक्ट्समध्ये काही प्रमाणित गुणधर्म असतात, जे प्रत्येक गेमसाठी समान असतात. हे घटक खालीलप्रमाणे असतात:

- **स्थान-आधारित**: बहुतेक, किंवा सर्वच गेम घटक स्थान-आधारित असतात. याचा अर्थ त्यांना `x` आणि `y` स्थान असते.
- **हालचालक्षम**: हे असे ऑब्जेक्ट्स असतात जे नवीन ठिकाणी हलू शकतात. हे सहसा नायक, राक्षस किंवा NPC (नॉन-प्लेअर कॅरेक्टर) असतात, पण उदाहरणार्थ, झाडासारखे स्थिर ऑब्जेक्ट्स नसतात.
- **स्वत: नष्ट होणारे**: हे ऑब्जेक्ट्स फक्त एका ठराविक कालावधीसाठी अस्तित्वात असतात आणि नंतर स्वत:ला हटवण्यासाठी तयार करतात. सहसा हे `dead` किंवा `destroyed` नावाच्या बूलियनने दर्शवले जाते, जे गेम इंजिनला सूचित करते की हे ऑब्जेक्ट पुन्हा रेंडर केले जाऊ नये.
- **कूल-डाउन**: 'कूल-डाउन' हा अल्पायुषी ऑब्जेक्ट्समध्ये एक सामान्य गुणधर्म आहे. याचे एक सामान्य उदाहरण म्हणजे मजकूराचा तुकडा किंवा स्फोटासारखा ग्राफिकल इफेक्ट, जो फक्त काही मिलीसेकंदांसाठी दिसायला हवा.

✅ पॅक-मॅनसारख्या गेमचा विचार करा. तुम्ही या गेममध्ये वरील चार ऑब्जेक्ट प्रकार ओळखू शकता का?

### वर्तन व्यक्त करणे

वरील वर्णन केलेले सर्व वर्तन हे गेम ऑब्जेक्ट्सकडे असू शकते. मग आपण ते कसे कोड करतो? आपण हे वर्तन `क्लासेस` किंवा `ऑब्जेक्ट्स`शी संबंधित पद्धतींनी व्यक्त करू शकतो.

**क्लासेस**

`क्लासेस`चा वापर `इनहेरिटन्स`सह करून विशिष्ट वर्तन एका क्लासमध्ये जोडण्याची कल्पना आहे.

✅ इनहेरिटन्स समजून घेणे महत्त्वाचे आहे. [MDN च्या इनहेरिटन्सवरील लेख](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) वाचा.

कोडद्वारे व्यक्त केल्यास, एक गेम ऑब्जेक्ट सहसा असे दिसते:

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

✅ पॅक-मॅनचा नायक (उदा. इनकी, पिंकी किंवा ब्लिंकी) पुन्हा कसा लिहिता येईल याचा विचार करण्यासाठी काही मिनिटे घ्या.

**कंपोझिशन**

ऑब्जेक्ट इनहेरिटन्स हाताळण्याचा एक वेगळा मार्ग म्हणजे *कंपोझिशन* वापरणे. यामध्ये, ऑब्जेक्ट्स त्यांचे वर्तन खालीलप्रमाणे व्यक्त करतात:

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

**मला कोणता पॅटर्न वापरावा?**

तुम्ही कोणता पॅटर्न निवडायचा हे तुमच्यावर अवलंबून आहे. जावास्क्रिप्ट दोन्ही पॅराडाइम्सला समर्थन देते.

--

गेम डेव्हलपमेंटमध्ये आणखी एक सामान्य पॅटर्न म्हणजे गेमचा युजर अनुभव आणि कार्यक्षमता हाताळण्याचा प्रश्न सोडवतो.

## पब/सब पॅटर्न

✅ पब/सब म्हणजे 'पब्लिश-सबस्क्राइब'

हा पॅटर्न तुमच्या अॅप्लिकेशनच्या वेगवेगळ्या भागांनी एकमेकांबद्दल माहिती नसावी या कल्पनेला संबोधित करतो. का? कारण वेगवेगळे भाग वेगळे असल्यास एकूण काय चालले आहे हे समजणे सोपे होते. तसेच, जर गरज भासली तर वर्तन अचानक बदलणे सोपे होते. आपण हे कसे साध्य करतो? यासाठी काही संकल्पना तयार करतो:

- **संदेश**: संदेश हा सहसा मजकूर स्ट्रिंग असतो, ज्यासह एक पर्यायी पेलोड (डेटाचा तुकडा जो संदेशाबद्दल स्पष्टता देतो) असतो. गेममधील एक सामान्य संदेश म्हणजे `KEY_PRESSED_ENTER`.
- **प्रकाशक**: हा घटक संदेश *प्रकाशित* करतो आणि सर्व सबस्क्राइबर्सना पाठवतो.
- **सबस्क्राइबर**: हा घटक विशिष्ट संदेश *ऐकतो* आणि तो संदेश प्राप्त झाल्यामुळे काही कार्य करतो, जसे की लेझर फायर करणे.

या पॅटर्नची अंमलबजावणी आकाराने खूप लहान असते, पण हा एक खूप शक्तिशाली पॅटर्न आहे. याची अंमलबजावणी कशी करता येईल:

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

वरील कोड वापरण्यासाठी आपण एक खूप लहान अंमलबजावणी तयार करू शकतो:

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

वरील उदाहरणात आपण कीबोर्ड इव्हेंट `ArrowLeft` कनेक्ट करतो आणि `HERO_MOVE_LEFT` संदेश पाठवतो. आपण तो संदेश ऐकतो आणि त्याचा परिणाम म्हणून `hero` हलवतो. या पॅटर्नची ताकद अशी आहे की इव्हेंट लिसनर आणि नायक एकमेकांबद्दल काहीही जाणत नाहीत. तुम्ही `ArrowLeft` ला `A` कीवर रीमॅप करू शकता. याशिवाय, `ArrowLeft` वर काहीतरी पूर्णपणे वेगळे करण्याची शक्यता आहे, फक्त इव्हेंटएमिटरच्या `on` फंक्शनमध्ये काही संपादने करून:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

तुमचा गेम मोठा होत असताना गोष्टी अधिक गुंतागुंतीच्या होतात, पण हा पॅटर्न त्याच गुंतागुंतीत राहतो आणि तुमचा कोड स्वच्छ राहतो. हा पॅटर्न स्वीकारण्याची शिफारस केली जाते.

---

## 🚀 आव्हान

पब-सब पॅटर्न गेमला कसा सुधारू शकतो याचा विचार करा. कोणते भाग इव्हेंट्स उत्सर्जित करावेत, आणि गेमने त्यावर कसे प्रतिक्रिया द्यावी? आता नवीन गेमचा विचार करण्याची आणि त्याचे भाग कसे वागतील याबद्दल सर्जनशील होण्याची तुमची संधी आहे.

## व्याख्यानानंतरची प्रश्नमंजुषा

[व्याख्यानानंतरची प्रश्नमंजुषा](https://ff-quizzes.netlify.app/web/quiz/30)

## पुनरावलोकन आणि स्व-अभ्यास

पब/सब बद्दल अधिक जाणून घ्या [याबद्दल वाचून](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon).

## असाइनमेंट

[गेमची रूपरेषा तयार करा](assignment.md)

---

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) चा वापर करून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी कृपया लक्षात ठेवा की स्वयंचलित भाषांतरे त्रुटी किंवा अचूकतेच्या अभावाने युक्त असू शकतात. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून निर्माण होणाऱ्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.