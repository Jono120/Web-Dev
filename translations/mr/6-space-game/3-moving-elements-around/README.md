<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a9a161871de7706cb0e23b1bd0c74559",
  "translation_date": "2025-08-28T16:15:03+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "mr"
}
-->
# स्पेस गेम तयार करा भाग ३: गती जोडणे

## पूर्व-व्याख्यान प्रश्नमंजुषा

[पूर्व-व्याख्यान प्रश्नमंजुषा](https://ff-quizzes.netlify.app/web/quiz/33)

गेम्स मजेदार होतात जेव्हा स्क्रीनवर एलियन्स फिरायला लागतात! या गेममध्ये आपण दोन प्रकारच्या हालचालींचा वापर करू:

- **कीबोर्ड/माऊस हालचाल**: जेव्हा वापरकर्ता कीबोर्ड किंवा माऊस वापरून स्क्रीनवरील वस्तू हलवतो.
- **गेम-प्रेरित हालचाल**: जेव्हा गेम विशिष्ट वेळेच्या अंतराने वस्तू हलवतो.

तर स्क्रीनवर वस्तू कशा हलवायच्या? हे सर्व कार्टेशियन कोऑर्डिनेट्सवर आधारित आहे: आपण वस्तूचे स्थान (x, y) बदलतो आणि नंतर स्क्रीन पुन्हा रेखाटतो.

स्क्रीनवर *हालचाल* साध्य करण्यासाठी आपल्याला सामान्यतः खालील चरणांची आवश्यकता असते:

1. **नवीन स्थान सेट करा**: वस्तू हलवलेली असल्याचे जाणवण्यासाठी हे आवश्यक आहे.
2. **स्क्रीन साफ करा**: स्क्रीन पुन्हा रेखाटण्याच्या दरम्यान साफ ​​करणे आवश्यक आहे. आपण पार्श्वभूमी रंगाने भरलेला आयत रेखाटून स्क्रीन साफ ​​करू शकतो.
3. **नवीन स्थानावर वस्तू पुन्हा रेखाटणे**: असे केल्याने आपण वस्तू एका स्थानावरून दुसऱ्या स्थानावर हलवणे साध्य करतो.

कोडमध्ये हे असे दिसू शकते:

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

✅ तुम्ही विचार करू शकता का की तुमच्या हिरोला सेकंदाला अनेक फ्रेम्समध्ये पुन्हा रेखाटल्यामुळे कार्यक्षमतेवर काही परिणाम होऊ शकतो? [या पद्धतीचे पर्याय](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas) वाचा.

## कीबोर्ड इव्हेंट्स हाताळा

तुम्ही इव्हेंट्स हाताळता तेव्हा विशिष्ट इव्हेंट्स कोडशी जोडता. कीबोर्ड इव्हेंट्स संपूर्ण विंडोवर ट्रिगर होतात, तर माऊस इव्हेंट्स जसे की `click` विशिष्ट घटकावर क्लिक करण्याशी जोडले जाऊ शकतात. आपण या प्रकल्पात कीबोर्ड इव्हेंट्स वापरणार आहोत.

इव्हेंट हाताळण्यासाठी तुम्हाला विंडोच्या `addEventListener()` पद्धतीचा वापर करावा लागतो आणि त्याला दोन इनपुट पॅरामीटर्स द्यावे लागतात. पहिला पॅरामीटर इव्हेंटचे नाव आहे, उदाहरणार्थ `keyup`. दुसरा पॅरामीटर म्हणजे इव्हेंट घडल्यामुळे कॉल होणारी फंक्शन.

उदाहरण येथे आहे:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

की इव्हेंट्ससाठी इव्हेंटवर दोन प्रॉपर्टीज असतात ज्याचा वापर तुम्ही कोणती की दाबली आहे हे पाहण्यासाठी करू शकता:

- `key`: ही दाबलेल्या कीची स्ट्रिंग प्रतिनिधित्व आहे, उदाहरणार्थ `ArrowUp`.
- `keyCode`: ही संख्यात्मक प्रतिनिधित्व आहे, उदाहरणार्थ `37`, जे `ArrowLeft` शी संबंधित आहे.

✅ की इव्हेंट्सचे हेरफेर गेम डेव्हलपमेंटच्या बाहेर उपयुक्त आहे. या तंत्राचा आणखी कोणत्या उपयोगासाठी विचार करू शकता?

### विशेष की: एक सावधगिरी

काही *विशेष* की विंडोवर परिणाम करतात. याचा अर्थ असा की जर तुम्ही `keyup` इव्हेंट ऐकत असाल आणि तुम्ही तुमच्या हिरोला हलवण्यासाठी या विशेष की वापरत असाल तर ते क्षैतिज स्क्रोलिंग देखील करेल. त्यामुळे तुम्हाला तुमचा गेम तयार करताना हे अंगभूत ब्राउझर वर्तन *बंद* करायचे असेल. तुम्हाला अशा प्रकारचा कोड आवश्यक आहे:

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

वरील कोड सुनिश्चित करेल की अॅरो-की आणि स्पेस कीचे *डिफॉल्ट* वर्तन बंद केले जाईल. *बंद* यंत्रणा `e.preventDefault()` कॉल केल्यावर होते.

## गेम-प्रेरित हालचाल

आपण `setTimeout()` किंवा `setInterval()` सारख्या टाइमर्सचा वापर करून वस्तू स्वतःच हलवू शकतो, जे प्रत्येक टिक किंवा वेळेच्या अंतराने वस्तूचे स्थान अपडेट करतात. हे कोडमध्ये असे दिसू शकते:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## गेम लूप

गेम लूप ही एक संकल्पना आहे जी मूलतः नियमित अंतराने कॉल होणारी फंक्शन आहे. याला गेम लूप म्हणतात कारण वापरकर्त्याला दिसणारे सर्व काही लूपमध्ये रेखाटले जाते. गेम लूप गेमचा भाग असलेल्या सर्व गेम ऑब्जेक्ट्सचा वापर करते, त्यापैकी सर्व रेखाटते, जोपर्यंत काही कारणास्तव गेमचा भाग राहू नये. उदाहरणार्थ, जर एखादी वस्तू शत्रू असेल जी लेसरने हिट झाली आणि फुटली, तर ती सध्याच्या गेम लूपचा भाग राहणार नाही (याबद्दल तुम्ही पुढील धड्यांमध्ये अधिक शिकाल).

गेम लूप कोडमध्ये सामान्यतः असे दिसते:

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

वरील लूप प्रत्येक `200` मिलिसेकंदाला कॅनव्हास पुन्हा रेखाटण्यासाठी कॉल केला जातो. तुमच्या गेमसाठी योग्य वाटणारे सर्वोत्तम अंतर निवडण्याची क्षमता तुमच्याकडे आहे.

## स्पेस गेम सुरू ठेवणे

तुम्ही विद्यमान कोड घेऊन त्याचा विस्तार कराल. भाग I मध्ये पूर्ण केलेल्या कोडसह प्रारंभ करा किंवा [भाग II- स्टार्टर](../../../../6-space-game/3-moving-elements-around/your-work) मधील कोड वापरा.

- **हिरो हलवणे**: तुम्ही अॅरो की वापरून हिरो हलवण्यासाठी कोड जोडाल.
- **शत्रू हलवणे**: तुम्हाला शत्रू वरून खाली दिलेल्या दराने हलवण्यासाठी कोड जोडणे आवश्यक आहे.

## शिफारस केलेली पावले

`your-work` सब फोल्डरमध्ये तयार केलेल्या फाइल्स शोधा. त्यात खालील गोष्टी असाव्यात:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

तुमचा प्रकल्प `your_work` फोल्डरमध्ये सुरू करण्यासाठी टाइप करा:

```bash
cd your-work
npm start
```

वरील HTTP सर्व्हर `http://localhost:5000` पत्त्यावर सुरू करेल. ब्राउझर उघडा आणि तो पत्ता इनपुट करा, सध्या ते हिरो आणि सर्व शत्रूंना रेंडर करेल; काहीही हलत नाही - अजून!

### कोड जोडा

1. **`hero`, `enemy` आणि `game object` साठी समर्पित ऑब्जेक्ट्स जोडा**, त्यांच्याकडे `x` आणि `y` प्रॉपर्टीज असाव्यात. ([Inheritance किंवा composition](../README.md) याबद्दलच्या भागाची आठवण ठेवा).

   *सूचना*: `game object` हा `x` आणि `y` असलेला आणि स्वतःला कॅनव्हासवर रेखाटण्याची क्षमता असलेला असावा.

   >सूचना: खाली दिलेल्या प्रकारे त्याचा कन्स्ट्रक्टर असलेला नवीन GameObject क्लास जोडा आणि नंतर कॅनव्हासवर रेखाट:

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

    आता, या GameObject चा विस्तार करून हिरो आणि शत्रू तयार करा.

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

2. **की-इव्हेंट हँडलर्स जोडा** की नेव्हिगेशन हाताळण्यासाठी (हिरो वर/खाली डाव्या/उजवीकडे हलवा).

   *लक्षात ठेवा*: हे एक कार्टेशियन सिस्टम आहे, टॉप-लेफ्ट `0,0` आहे. तसेच *डिफॉल्ट वर्तन* थांबवण्यासाठी कोड जोडण्याची आठवण ठेवा.

   >सूचना: तुमची onKeyDown फंक्शन तयार करा आणि ती विंडोशी जोडा:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   या टप्प्यावर तुमच्या ब्राउझर कन्सोलमध्ये तपासा आणि की दाबल्यावर लॉगिंग पहा.

3. **[Pub sub pattern](../README.md) लागू करा**, यामुळे तुम्ही उर्वरित भागांचे अनुसरण करत असताना तुमचा कोड स्वच्छ राहील.

   हे शेवटचे भाग करण्यासाठी, तुम्ही:

   1. **विंडोवर इव्हेंट लिसनर जोडा**:

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

    1. **EventEmitter क्लास तयार करा** संदेश प्रकाशित आणि सबस्क्राइब करण्यासाठी:

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

    1. **Constants जोडा** आणि EventEmitter सेट करा:

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

    1. **गेम प्रारंभ करा**:

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

1. **गेम लूप सेट करा**

   विंडो.onload फंक्शनला रिफॅक्टर करा, गेम प्रारंभ करा आणि चांगल्या अंतरावर गेम लूप सेट करा. तुम्ही लेसर बीम देखील जोडाल:

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

5. **शत्रूंना विशिष्ट अंतरावर हलवण्यासाठी कोड जोडा**

    `createEnemies()` फंक्शनला रिफॅक्टर करा, शत्रू तयार करा आणि त्यांना नवीन gameObjects क्लासमध्ये पुश करा:

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
    
    आणि हिरोसाठी समान प्रक्रिया करण्यासाठी `createHero()` फंक्शन जोडा.

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

    आणि शेवटी, रेखाटणे सुरू करण्यासाठी `drawGameObjects()` फंक्शन जोडा:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    तुमचे शत्रू तुमच्या हिरो स्पेसशिपवर हल्ला करण्यास सुरुवात करतील!

---

## 🚀 आव्हान

जसे तुम्ही पाहू शकता, तुमचा कोड 'स्पॅगेटी कोड' मध्ये बदलू शकतो जेव्हा तुम्ही फंक्शन्स, व्हेरिएबल्स आणि क्लासेस जोडायला सुरुवात करता. तुमचा कोड अधिक वाचनीय होण्यासाठी तुम्ही तो कसा चांगल्या प्रकारे आयोजित करू शकता? तुमचा कोड आयोजित करण्यासाठी एक प्रणाली तयार करा, जरी तो अजूनही एका फाइलमध्ये असला तरी.

## व्याख्यानानंतरची प्रश्नमंजुषा

[व्याख्यानानंतरची प्रश्नमंजुषा](https://ff-quizzes.netlify.app/web/quiz/34)

## पुनरावलोकन आणि स्व-अभ्यास

जरी आपण फ्रेमवर्कशिवाय आपला गेम लिहित आहोत, तरी गेम डेव्हलपमेंटसाठी अनेक जावास्क्रिप्ट-आधारित कॅनव्हास फ्रेमवर्क आहेत. याबद्दल [वाचन करा](https://github.com/collections/javascript-game-engines).

## असाइनमेंट

[तुमच्या कोडवर टिप्पणी द्या](assignment.md)

---

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी, कृपया लक्षात ठेवा की स्वयंचलित भाषांतरे त्रुटी किंवा अचूकतेच्या अभावाने युक्त असू शकतात. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी, व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून उद्भवलेल्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.