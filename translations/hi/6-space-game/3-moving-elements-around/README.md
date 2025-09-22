<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a9a161871de7706cb0e23b1bd0c74559",
  "translation_date": "2025-08-29T15:54:45+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "hi"
}
-->
# स्पेस गेम बनाएं भाग 3: गति जोड़ना

## प्री-लेक्चर क्विज़

[प्री-लेक्चर क्विज़](https://ff-quizzes.netlify.app/web/quiz/33)

गेम्स तब तक मज़ेदार नहीं होते जब तक स्क्रीन पर एलियंस इधर-उधर न भागें! इस गेम में, हम दो प्रकार की गतियों का उपयोग करेंगे:

- **कीबोर्ड/माउस मूवमेंट**: जब उपयोगकर्ता कीबोर्ड या माउस के साथ स्क्रीन पर किसी ऑब्जेक्ट को हिलाता है।
- **गेम-प्रेरित मूवमेंट**: जब गेम किसी ऑब्जेक्ट को एक निश्चित समय अंतराल पर हिलाता है।

तो स्क्रीन पर चीजों को कैसे हिलाया जाए? यह सब कार्टेशियन निर्देशांक पर आधारित है: हम ऑब्जेक्ट के स्थान (x, y) को बदलते हैं और फिर स्क्रीन को फिर से ड्रॉ करते हैं।

आमतौर पर स्क्रीन पर *मूवमेंट* को पूरा करने के लिए आपको निम्नलिखित चरणों की आवश्यकता होती है:

1. **नया स्थान सेट करें**: किसी ऑब्जेक्ट के लिए एक नया स्थान सेट करना आवश्यक है ताकि ऐसा लगे कि वह हिल रहा है।
2. **स्क्रीन साफ़ करें**: ड्रॉ के बीच स्क्रीन को साफ़ करना आवश्यक है। हम इसे एक आयत बनाकर साफ़ कर सकते हैं जिसे हम बैकग्राउंड रंग से भरते हैं।
3. **ऑब्जेक्ट को नए स्थान पर फिर से ड्रॉ करें**: ऐसा करके हम अंततः ऑब्जेक्ट को एक स्थान से दूसरे स्थान पर ले जाने में सफल होते हैं।

कोड में यह कुछ इस तरह दिख सकता है:

```javascript
//set the hero's location
hero.x += 5;
// clear the rectangle that hosts the hero
ctx.clearRect(0, 0, canvas.width, canvas.height);
// redraw the game background and hero
ctx.fillRect(0, 0, canvas.width, canvas.height)
ctx.fillStyle = "black";
ctx.drawImage(heroImg, hero.x, hero.y);
```

✅ क्या आप सोच सकते हैं कि आपके हीरो को प्रति सेकंड कई फ्रेम्स पर फिर से ड्रॉ करने से प्रदर्शन लागत क्यों बढ़ सकती है? [इस पैटर्न के विकल्पों](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas) के बारे में पढ़ें।

## कीबोर्ड इवेंट्स को हैंडल करें

आप इवेंट्स को कोड से जोड़कर हैंडल करते हैं। कीबोर्ड इवेंट्स पूरे विंडो पर ट्रिगर होते हैं, जबकि माउस इवेंट्स जैसे `क्लिक` को किसी विशेष एलिमेंट पर क्लिक करने से जोड़ा जा सकता है। इस प्रोजेक्ट में हम कीबोर्ड इवेंट्स का उपयोग करेंगे।

इवेंट को हैंडल करने के लिए, आपको विंडो के `addEventListener()` मेथड का उपयोग करना होगा और इसे दो इनपुट पैरामीटर देने होंगे। पहला पैरामीटर इवेंट का नाम है, जैसे `keyup`। दूसरा पैरामीटर वह फंक्शन है जिसे इवेंट होने पर कॉल किया जाना चाहिए।

यहां एक उदाहरण है:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

की इवेंट्स के लिए, इवेंट पर दो प्रॉपर्टीज़ होती हैं जिनका उपयोग यह देखने के लिए किया जा सकता है कि कौन सी कुंजी दबाई गई थी:

- `key`: यह दबाई गई कुंजी का स्ट्रिंग प्रतिनिधित्व है, जैसे `ArrowUp`।
- `keyCode`: यह एक नंबर प्रतिनिधित्व है, जैसे `37`, जो `ArrowLeft` के अनुरूप है।

✅ की इवेंट मैनिपुलेशन गेम डेवलपमेंट के बाहर भी उपयोगी है। इस तकनीक के अन्य उपयोग क्या हो सकते हैं?

### विशेष कुंजियाँ: एक चेतावनी

कुछ *विशेष* कुंजियाँ विंडो को प्रभावित करती हैं। इसका मतलब है कि यदि आप `keyup` इवेंट को सुन रहे हैं और इन विशेष कुंजियों का उपयोग करके अपने हीरो को हिलाते हैं, तो यह क्षैतिज स्क्रॉलिंग भी करेगा। इस कारण से, आप अपने गेम को बनाते समय इस अंतर्निहित ब्राउज़र व्यवहार को *बंद* करना चाह सकते हैं। इसके लिए आपको इस तरह का कोड चाहिए:

```javascript
let onKeyDown = function (e) {
  console.log(e.keyCode);
  switch (e.keyCode) {
    case 37:
    case 39:
    case 38:
    case 40: // Arrow keys
    case 32:
      e.preventDefault();
      break; // Space
    default:
      break; // do not block other keys
  }
};

window.addEventListener('keydown', onKeyDown);
```

ऊपर दिया गया कोड सुनिश्चित करेगा कि एरो-की और स्पेस की का *डिफ़ॉल्ट* व्यवहार बंद हो जाए। *बंद* करने की प्रक्रिया तब होती है जब हम `e.preventDefault()` को कॉल करते हैं।

## गेम-प्रेरित मूवमेंट

हम `setTimeout()` या `setInterval()` जैसे टाइमर्स का उपयोग करके चीजों को अपने आप हिला सकते हैं, जो प्रत्येक टिक या समय अंतराल पर ऑब्जेक्ट के स्थान को अपडेट करते हैं। यह कुछ इस तरह दिख सकता है:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## गेम लूप

गेम लूप एक अवधारणा है, जो मूल रूप से एक फंक्शन है जिसे नियमित अंतराल पर कॉल किया जाता है। इसे गेम लूप कहा जाता है क्योंकि जो कुछ भी उपयोगकर्ता को दिखाई देना चाहिए, वह लूप में ड्रॉ किया जाता है। गेम लूप गेम के सभी ऑब्जेक्ट्स का उपयोग करता है, उन्हें ड्रॉ करता है जब तक कि किसी कारणवश वे गेम का हिस्सा न हों। उदाहरण के लिए, यदि कोई ऑब्जेक्ट एक दुश्मन है जिसे लेज़र ने मारा और वह फट गया, तो वह अब वर्तमान गेम लूप का हिस्सा नहीं है (आप इसके बारे में बाद के पाठों में और जानेंगे)।

गेम लूप आमतौर पर कोड में इस तरह दिख सकता है:

```javascript
let gameLoopId = setInterval(() =>
  function gameLoop() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = "black";
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    drawHero();
    drawEnemies();
    drawStaticObjects();
}, 200);
```

ऊपर दिया गया लूप हर `200` मिलीसेकंड में कैनवास को फिर से ड्रॉ करने के लिए कॉल किया जाता है। आप अपने गेम के लिए उपयुक्त सबसे अच्छा अंतराल चुन सकते हैं।

## स्पेस गेम जारी रखें

आप मौजूदा कोड को लें और इसे बढ़ाएं। या तो उस कोड से शुरू करें जिसे आपने भाग I के दौरान पूरा किया था या [भाग II-स्टार्टर](../../../../6-space-game/3-moving-elements-around/your-work) में दिए गए कोड का उपयोग करें।

- **हीरो को हिलाना**: आप कोड जोड़ेंगे ताकि आप एरो कीज़ का उपयोग करके हीरो को हिला सकें।
- **दुश्मनों को हिलाना**: आपको यह सुनिश्चित करने के लिए कोड भी जोड़ना होगा कि दुश्मन एक निश्चित दर पर ऊपर से नीचे की ओर बढ़ें।

## अनुशंसित चरण

`your-work` सब फोल्डर में बनाए गए फाइलों का पता लगाएं। इसमें निम्नलिखित शामिल होना चाहिए:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

आप अपने प्रोजेक्ट को `your_work` फोल्डर में इस प्रकार शुरू करें:

```bash
cd your-work
npm start
```

ऊपर दिया गया कमांड `http://localhost:5000` पते पर एक HTTP सर्वर शुरू करेगा। एक ब्राउज़र खोलें और उस पते को दर्ज करें, अभी यह हीरो और सभी दुश्मनों को रेंडर करना चाहिए; अभी कुछ भी हिल नहीं रहा है!

### कोड जोड़ें

1. **हीरो**, **दुश्मन**, और **गेम ऑब्जेक्ट** के लिए समर्पित ऑब्जेक्ट्स जोड़ें, जिनमें `x` और `y` प्रॉपर्टीज़ होनी चाहिए। ([विरासत या संरचना](../README.md) पर अनुभाग को याद रखें)।

   *संकेत*: `गेम ऑब्जेक्ट` वह होना चाहिए जिसमें `x` और `y` और खुद को कैनवास पर ड्रॉ करने की क्षमता हो।

   > सुझाव: नीचे दिए गए कंस्ट्रक्टर के साथ एक नया GameObject क्लास जोड़कर शुरू करें, और फिर इसे कैनवास पर ड्रॉ करें:
  
    ```javascript
        
    class GameObject {
      constructor(x, y) {
        this.x = x;
        this.y = y;
        this.dead = false;
        this.type = "";
        this.width = 0;
        this.height = 0;
        this.img = undefined;
      }
    
      draw(ctx) {
        ctx.drawImage(this.img, this.x, this.y, this.width, this.height);
      }
    }
    ```

    अब, इस GameObject को बढ़ाकर Hero और Enemy बनाएं।
    
    ```javascript
    class Hero extends GameObject {
      constructor(x, y) {
        ...it needs an x, y, type, and speed
      }
    }
    ```

    ```javascript
    class Enemy extends GameObject {
      constructor(x, y) {
        super(x, y);
        (this.width = 98), (this.height = 50);
        this.type = "Enemy";
        let id = setInterval(() => {
          if (this.y < canvas.height - this.height) {
            this.y += 5;
          } else {
            console.log('Stopped at', this.y)
            clearInterval(id);
          }
        }, 300)
      }
    }
    ```

2. **की-इवेंट हैंडलर्स जोड़ें** ताकि की नेविगेशन (हीरो को ऊपर/नीचे, बाएं/दाएं हिलाना) को हैंडल किया जा सके।

   *याद रखें*: यह एक कार्टेशियन सिस्टम है, टॉप-लेफ्ट `0,0` है। डिफ़ॉल्ट व्यवहार को रोकने के लिए कोड जोड़ना भी याद रखें।

   > सुझाव: अपना onKeyDown फंक्शन बनाएं और इसे विंडो से जोड़ें:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   इस बिंदु पर अपने ब्राउज़र कंसोल की जांच करें, और कीस्ट्रोक्स को लॉग होते हुए देखें।

3. **[पब सब पैटर्न](../README.md) लागू करें**, यह आपके कोड को साफ़ रखेगा क्योंकि आप शेष भागों का अनुसरण करेंगे।

   ऐसा करने के लिए, आप:

   1. **विंडो पर एक इवेंट लिसनर जोड़ें**:

       ```javascript
        window.addEventListener("keyup", (evt) => {
          if (evt.key === "ArrowUp") {
            eventEmitter.emit(Messages.KEY_EVENT_UP);
          } else if (evt.key === "ArrowDown") {
            eventEmitter.emit(Messages.KEY_EVENT_DOWN);
          } else if (evt.key === "ArrowLeft") {
            eventEmitter.emit(Messages.KEY_EVENT_LEFT);
          } else if (evt.key === "ArrowRight") {
            eventEmitter.emit(Messages.KEY_EVENT_RIGHT);
          }
        });
        ```

    1. **एक EventEmitter क्लास बनाएं** ताकि संदेशों को प्रकाशित और सब्सक्राइब किया जा सके:

        ```javascript
        class EventEmitter {
          constructor() {
            this.listeners = {};
          }
        
          on(message, listener) {
            if (!this.listeners[message]) {
              this.listeners[message] = [];
            }
            this.listeners[message].push(listener);
          }
        
          emit(message, payload = null) {
            if (this.listeners[message]) {
              this.listeners[message].forEach((l) => l(message, payload));
            }
          }
        }
        ```

    1. **कॉन्स्टेंट्स जोड़ें** और EventEmitter सेट करें:

        ```javascript
        const Messages = {
          KEY_EVENT_UP: "KEY_EVENT_UP",
          KEY_EVENT_DOWN: "KEY_EVENT_DOWN",
          KEY_EVENT_LEFT: "KEY_EVENT_LEFT",
          KEY_EVENT_RIGHT: "KEY_EVENT_RIGHT",
        };
        
        let heroImg, 
            enemyImg, 
            laserImg,
            canvas, ctx, 
            gameObjects = [], 
            hero, 
            eventEmitter = new EventEmitter();
        ```

    1. **गेम को प्रारंभ करें**:

    ```javascript
    function initGame() {
      gameObjects = [];
      createEnemies();
      createHero();
    
      eventEmitter.on(Messages.KEY_EVENT_UP, () => {
        hero.y -=5 ;
      })
    
      eventEmitter.on(Messages.KEY_EVENT_DOWN, () => {
        hero.y += 5;
      });
    
      eventEmitter.on(Messages.KEY_EVENT_LEFT, () => {
        hero.x -= 5;
      });
    
      eventEmitter.on(Messages.KEY_EVENT_RIGHT, () => {
        hero.x += 5;
      });
    }
    ```

1. **गेम लूप सेट करें**

   विंडो.onload फंक्शन को रिफैक्टर करें ताकि गेम को प्रारंभ किया जा सके और एक अच्छे अंतराल पर गेम लूप सेट किया जा सके। आप एक लेज़र बीम भी जोड़ेंगे:

    ```javascript
    window.onload = async () => {
      canvas = document.getElementById("canvas");
      ctx = canvas.getContext("2d");
      heroImg = await loadTexture("assets/player.png");
      enemyImg = await loadTexture("assets/enemyShip.png");
      laserImg = await loadTexture("assets/laserRed.png");
    
      initGame();
      let gameLoopId = setInterval(() => {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = "black";
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        drawGameObjects(ctx);
      }, 100)
      
    };
    ```

5. **दुश्मनों को एक निश्चित अंतराल पर हिलाने के लिए कोड जोड़ें**

    `createEnemies()` फंक्शन को रिफैक्टर करें ताकि दुश्मनों को बनाया जा सके और उन्हें नए gameObjects क्लास में पुश किया जा सके:

    ```javascript
    function createEnemies() {
      const MONSTER_TOTAL = 5;
      const MONSTER_WIDTH = MONSTER_TOTAL * 98;
      const START_X = (canvas.width - MONSTER_WIDTH) / 2;
      const STOP_X = START_X + MONSTER_WIDTH;
    
      for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          const enemy = new Enemy(x, y);
          enemy.img = enemyImg;
          gameObjects.push(enemy);
        }
      }
    }
    ```
    
    और हीरो के लिए एक `createHero()` फंक्शन जोड़ें ताकि इसी प्रक्रिया को दोहराया जा सके।
    
    ```javascript
    function createHero() {
      hero = new Hero(
        canvas.width / 2 - 45,
        canvas.height - canvas.height / 4
      );
      hero.img = heroImg;
      gameObjects.push(hero);
    }
    ```

    और अंत में, एक `drawGameObjects()` फंक्शन जोड़ें ताकि ड्रॉइंग शुरू हो सके:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    आपके दुश्मन आपके हीरो स्पेसशिप पर हमला करना शुरू कर देंगे!

---

## 🚀 चुनौती

जैसा कि आप देख सकते हैं, जब आप फंक्शन्स, वेरिएबल्स और क्लासेस जोड़ना शुरू करते हैं, तो आपका कोड 'स्पेगेटी कोड' में बदल सकता है। आप अपने कोड को बेहतर तरीके से व्यवस्थित करने के लिए क्या कर सकते हैं ताकि यह अधिक पठनीय हो? एक सिस्टम का खाका तैयार करें ताकि आपका कोड व्यवस्थित हो, भले ही यह अभी भी एक ही फाइल में हो।

## पोस्ट-लेक्चर क्विज़

[पोस्ट-लेक्चर क्विज़](https://ff-quizzes.netlify.app/web/quiz/34)

## समीक्षा और स्व-अध्ययन

हालांकि हम अपने गेम को फ्रेमवर्क्स का उपयोग किए बिना लिख रहे हैं, गेम डेवलपमेंट के लिए कई जावास्क्रिप्ट-आधारित कैनवास फ्रेमवर्क हैं। इनके बारे में [पढ़ने के लिए समय निकालें](https://github.com/collections/javascript-game-engines)।

## असाइनमेंट

[अपने कोड पर टिप्पणी करें](assignment.md)

---

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता सुनिश्चित करने का प्रयास करते हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को प्रामाणिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम जिम्मेदार नहीं हैं।