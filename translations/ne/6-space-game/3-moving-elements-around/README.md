<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a9a161871de7706cb0e23b1bd0c74559",
  "translation_date": "2025-08-28T16:35:32+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "ne"
}
-->
# स्पेस गेम बनाउनुहोस् भाग ३: गति थप्ने

## प्रि-लेक्चर क्विज

[प्रि-लेक्चर क्विज](https://ff-quizzes.netlify.app/web/quiz/33)

खेलहरू त्यति रमाइलो हुँदैनन् जबसम्म स्क्रिनमा एलियनहरू दौडिरहेका हुँदैनन्! यस खेलमा, हामी दुई प्रकारका गतिहरू प्रयोग गर्नेछौं:

- **किबोर्ड/माउस गति**: जब प्रयोगकर्ताले स्क्रिनमा वस्तु सार्न किबोर्ड वा माउससँग अन्तरक्रिया गर्छ।
- **खेलद्वारा प्रेरित गति**: जब खेलले निश्चित समय अन्तरालमा वस्तु सार्छ।

त्यसो भए स्क्रिनमा वस्तु कसरी सार्ने? यो सबै कार्टेसियन समन्वयको बारेमा हो: हामी वस्तुको स्थान (x, y) परिवर्तन गर्छौं र त्यसपछि स्क्रिन पुनःचित्रण गर्छौं।

सामान्यतया स्क्रिनमा *गति* हासिल गर्न निम्न चरणहरू आवश्यक हुन्छन्:

1. **नयाँ स्थान सेट गर्नुहोस्**: वस्तु सारिएको देख्नको लागि यो आवश्यक छ।
2. **स्क्रिन सफा गर्नुहोस्**: स्क्रिनलाई प्रत्येक ड्रको बीचमा सफा गर्न आवश्यक छ। हामी यसलाई पृष्ठभूमि रंगले भरिएको आयत चित्रण गरेर सफा गर्न सक्छौं।
3. **नयाँ स्थानमा वस्तु पुनःचित्रण गर्नुहोस्**: यसले वस्तुलाई एक स्थानबाट अर्को स्थानमा सार्न अन्ततः पूरा गर्छ।

यसले कोडमा यस्तो देखिन सक्छ:

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

✅ के तपाईं सोच्न सक्नुहुन्छ किन तपाईंको नायकलाई प्रति सेकेन्ड धेरै फ्रेमहरूमा पुनःचित्रण गर्दा प्रदर्शन लागत बढ्न सक्छ? [यस ढाँचाको विकल्पहरू](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas) बारे पढ्नुहोस्।

## किबोर्ड इभेन्टहरू ह्यान्डल गर्नुहोस्

तपाईंले इभेन्टहरू ह्यान्डल गर्न कोडमा विशिष्ट इभेन्टहरू संलग्न गर्नु पर्छ। किबोर्ड इभेन्टहरू सम्पूर्ण विन्डोमा ट्रिगर हुन्छन् भने माउस इभेन्टहरू जस्तै `click` विशिष्ट तत्वमा क्लिक गर्न जोड्न सकिन्छ। हामी यस परियोजनामा ​​किबोर्ड इभेन्टहरू प्रयोग गर्नेछौं।

इभेन्ट ह्यान्डल गर्न तपाईंले विन्डोको `addEventListener()` विधि प्रयोग गर्नुपर्छ र यसलाई दुई इनपुट प्यारामिटरहरू प्रदान गर्नुपर्छ। पहिलो प्यारामिटर इभेन्टको नाम हो, उदाहरणका लागि `keyup`। दोस्रो प्यारामिटर इभेन्ट हुँदा बोलाइनु पर्ने फङ्सन हो।

यहाँ एउटा उदाहरण छ:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

किबोर्ड इभेन्टहरूको लागि, इभेन्टमा दुई गुणहरू छन् जसले कुन कुञ्जी थिचिएको थियो भनेर हेर्न प्रयोग गर्न सकिन्छ:

- `key`, यो थिचिएको कुञ्जीको स्ट्रिङ प्रतिनिधित्व हो, उदाहरणका लागि `ArrowUp`
- `keyCode`, यो संख्यात्मक प्रतिनिधित्व हो, उदाहरणका लागि `37`, जुन `ArrowLeft` सँग मेल खान्छ।

✅ किबोर्ड इभेन्ट हेरफेर खेल विकास बाहिर उपयोगी छ। तपाईं यस प्रविधिको अन्य के उपयोग सोच्न सक्नुहुन्छ?

### विशेष कुञ्जीहरू: एक चेतावनी

केही *विशेष* कुञ्जीहरू छन् जसले विन्डोलाई असर गर्छ। यसको मतलब यदि तपाईं `keyup` इभेन्ट सुन्दै हुनुहुन्छ र तपाईंले आफ्नो नायकलाई सार्न यी विशेष कुञ्जीहरू प्रयोग गर्नुभयो भने यसले क्षैतिज स्क्रोलिंग पनि प्रदर्शन गर्नेछ। त्यस कारणले गर्दा तपाईंले आफ्नो खेल निर्माण गर्दा यो बिल्ट-इन ब्राउजर व्यवहार *बन्द* गर्न चाहनुहुन्छ। तपाईंलाई यस्तो कोड चाहिन्छ:

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

माथिको कोडले सुनिश्चित गर्नेछ कि एरो-कुञ्जीहरू र स्पेस कुञ्जीको *डिफल्ट* व्यवहार बन्द गरिएको छ। *बन्द* गर्ने मेकानिजम तब हुन्छ जब हामी `e.preventDefault()` कल गर्छौं।

## खेलद्वारा प्रेरित गति

हामीले `setTimeout()` वा `setInterval()` जस्ता टाइमरहरू प्रयोग गरेर वस्तुहरूलाई आफैंले सार्न सक्छौं जसले प्रत्येक टिक वा समय अन्तरालमा वस्तुको स्थान अपडेट गर्छ। यसले यस्तो देखिन सक्छ:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## खेल लूप

खेल लूप एक अवधारणा हो जुन नियमित अन्तरालमा बोलाइने फङ्सन हो। यसलाई खेल लूप भनिन्छ किनभने प्रयोगकर्तालाई देखिनु पर्ने सबै कुरा लूपमा चित्रण गरिन्छ। खेल लूपले खेलको सबै वस्तुहरू प्रयोग गर्दछ जुन खेलको भाग हो, तिनीहरूलाई चित्रण गर्दै जबसम्म कुनै कारणले खेलको भाग हुनु हुँदैन। उदाहरणका लागि, यदि कुनै वस्तु शत्रु हो जसलाई लेजरले हानेर विस्फोट गर्यो भने, यो अब वर्तमान खेल लूपको भाग हुँदैन (तपाईं यसबारे थप पाठहरूमा सिक्नुहुनेछ)।

खेल लूप सामान्यतया कोडमा यस्तो देखिन सक्छ:

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

माथिको लूप प्रत्येक `200` मिलिसेकेन्डमा क्यानभास पुनःचित्रण गर्न बोलाइन्छ। तपाईंले आफ्नो खेलको लागि उपयुक्त अन्तराल चयन गर्न सक्नुहुन्छ।

## स्पेस गेम जारी राख्दै

तपाईंले विद्यमान कोड लिनेछ र यसलाई विस्तार गर्नेछ। भाग I मा तपाईंले पूरा गरेको कोडबाट सुरु गर्नुहोस् वा [भाग II- स्टार्टर](../../../../6-space-game/3-moving-elements-around/your-work) मा कोड प्रयोग गर्नुहोस्।

- **नायकलाई सार्ने**: तपाईंले एरो कुञ्जीहरू प्रयोग गरेर नायकलाई सार्न कोड थप्नु पर्नेछ।
- **शत्रुहरूलाई सार्नुहोस्**: तपाईंले शत्रुहरूलाई निश्चित दरमा माथिबाट तल सार्न कोड थप्नु पर्नेछ।

## सिफारिस गरिएका चरणहरू

`your-work` सब फोल्डरमा सिर्जना गरिएका फाइलहरू पत्ता लगाउनुहोस्। यसले निम्न समावेश गर्नुपर्छ:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

तपाईं आफ्नो परियोजना `your_work` फोल्डरमा निम्न टाइप गरेर सुरु गर्नुहोस्:

```bash
cd your-work
npm start
```

माथिकोले `http://localhost:5000` ठेगानामा HTTP सर्भर सुरु गर्नेछ। ब्राउजर खोल्नुहोस् र उक्त ठेगाना इनपुट गर्नुहोस्, अहिले यसले नायक र सबै शत्रुहरूलाई प्रस्तुत गर्नुपर्छ; केही पनि सर्दैन - अझै!

### कोड थप्नुहोस्

1. **नायक**, **शत्रु**, र **खेल वस्तु** को लागि समर्पित वस्तुहरू थप्नुहोस्, तिनीहरूसँग `x` र `y` गुणहरू हुनुपर्छ। ([Inheritance or composition](../README.md) को भाग सम्झनुहोस्।)

   *सुझाव*: `खेल वस्तु` त्यो हुनुपर्छ जससँग `x` र `y` हुन्छ र क्यानभासमा आफैंलाई चित्रण गर्ने क्षमता हुन्छ।

   >सुझाव: नयाँ GameObject क्लास थप्नुहोस् र यसको कन्स्ट्रक्टर निम्नानुसार परिभाषित गर्नुहोस्, त्यसपछि यसलाई क्यानभासमा चित्रण गर्नुहोस्:
  
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

    अब, यस GameObject लाई विस्तार गरेर नायक र शत्रु सिर्जना गर्नुहोस्।
    
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

2. **किबोर्ड इभेन्ट ह्यान्डलरहरू थप्नुहोस्** नायकलाई माथि/तल, बायाँ/दायाँ सार्न ह्यान्डल गर्न।

   *स्मरण गर्नुहोस्*: यो कार्टेसियन प्रणाली हो, माथि-बायाँ `0,0` हो। *डिफल्ट व्यवहार* रोक्न कोड थप्न पनि सम्झनुहोस्।

   >सुझाव: आफ्नो onKeyDown फङ्सन सिर्जना गर्नुहोस् र यसलाई विन्डोमा संलग्न गर्नुहोस्:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   यस बिन्दुमा आफ्नो ब्राउजर कन्सोल जाँच गर्नुहोस्, र कुञ्जी थिचिएको हेर्नुहोस्।

3. **[Pub sub pattern](../README.md) कार्यान्वयन गर्नुहोस्**, यसले तपाईंको कोड सफा राख्नेछ जब तपाईं बाँकी भागहरू अनुसरण गर्नुहुन्छ।

   यस अन्तिम भाग गर्न, तपाईं:

   1. **विन्डोमा इभेन्ट लिस्नर थप्नुहोस्**:

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

    1. **EventEmitter क्लास सिर्जना गर्नुहोस्** सन्देशहरू प्रकाशित गर्न र सदस्यता लिन:

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

    1. **Constants थप्नुहोस्** र EventEmitter सेटअप गर्नुहोस्:

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

    1. **खेल प्रारम्भ गर्नुहोस्**

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

1. **खेल लूप सेटअप गर्नुहोस्**

   विन्डो.onload फङ्सनलाई पुनःसंरचना गरेर खेल प्रारम्भ गर्नुहोस् र राम्रो अन्तरालमा खेल लूप सेटअप गर्नुहोस्। तपाईंले लेजर बीम पनि थप्नु पर्नेछ:

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

5. **शत्रुहरूलाई निश्चित अन्तरालमा सार्न कोड थप्नुहोस्**

    `createEnemies()` फङ्सनलाई पुनःसंरचना गरेर शत्रुहरू सिर्जना गर्नुहोस् र तिनीहरूलाई नयाँ gameObjects क्लासमा धकेल्नुहोस्:

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
    
    र नायकको लागि समान प्रक्रिया गर्न `createHero()` फङ्सन थप्नुहोस्।
    
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

    अन्तमा, `drawGameObjects()` फङ्सन थपेर चित्रण सुरु गर्नुहोस्:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    तपाईंका शत्रुहरू तपाईंको नायक स्पेसशिपतर्फ अगाडि बढ्न सुरु गर्नेछन्!

---

## 🚀 चुनौती

जस्तो तपाईं देख्न सक्नुहुन्छ, तपाईंको कोड 'स्प्यागेटी कोड' मा परिणत हुन सक्छ जब तपाईं फङ्सनहरू, भेरिएबलहरू, र क्लासहरू थप्न सुरु गर्नुहुन्छ। तपाईंको कोडलाई कसरी राम्रोसँग व्यवस्थित गर्न सकिन्छ ताकि यो पढ्न सजिलो होस्? तपाईंको कोड व्यवस्थित गर्न प्रणालीको स्केच गर्नुहोस्, यद्यपि यो अझै एक फाइलमा रहन्छ।

## पोस्ट-लेक्चर क्विज

[पोस्ट-लेक्चर क्विज](https://ff-quizzes.netlify.app/web/quiz/34)

## समीक्षा र आत्म-अध्ययन

हामी फ्रेमवर्कहरू प्रयोग नगरी हाम्रो खेल लेख्दैछौं, तर खेल विकासका लागि धेरै जाभास्क्रिप्ट-आधारित क्यानभास फ्रेमवर्कहरू छन्। यीबारे केही [पढ्ने समय निकाल्नुहोस्](https://github.com/collections/javascript-game-engines)।

## असाइनमेन्ट

[तपाईंको कोडमा टिप्पणी गर्नुहोस्](assignment.md)

---

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरेर अनुवाद गरिएको छ। हामी शुद्धताको लागि प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छ। यसको मूल भाषा मा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीको लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।