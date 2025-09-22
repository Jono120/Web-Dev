<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-29T15:56:45+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "hi"
}
-->
# अंतरिक्ष खेल बनाएं भाग 6: समाप्ति और पुनः प्रारंभ

## व्याख्यान पूर्व प्रश्नोत्तरी

[व्याख्यान पूर्व प्रश्नोत्तरी](https://ff-quizzes.netlify.app/web/quiz/39)

खेल में *समाप्ति की स्थिति* व्यक्त करने के कई तरीके होते हैं। यह आपके ऊपर है, जो खेल के निर्माता हैं, यह तय करने के लिए कि खेल क्यों समाप्त हुआ। यदि हम अब तक बनाए गए अंतरिक्ष खेल की बात कर रहे हैं, तो यहां कुछ कारण दिए गए हैं:

- **`N` दुश्मन जहाज नष्ट हो गए हैं**: यह काफी सामान्य है कि यदि आप खेल को विभिन्न स्तरों में विभाजित करते हैं, तो आपको एक स्तर पूरा करने के लिए `N` दुश्मन जहाजों को नष्ट करना होगा।
- **आपका जहाज नष्ट हो गया है**: ऐसे कई खेल हैं जहां यदि आपका जहाज नष्ट हो जाता है तो आप खेल हार जाते हैं। एक और सामान्य तरीका यह है कि आपके पास "जीवन" की अवधारणा हो। हर बार जब आपका जहाज नष्ट होता है, तो एक जीवन कम हो जाता है। जब सभी जीवन समाप्त हो जाते हैं, तो आप खेल हार जाते हैं।
- **आपने `N` अंक एकत्र किए हैं**: एक और सामान्य समाप्ति की स्थिति यह है कि आप अंक एकत्र करें। अंक कैसे प्राप्त होते हैं, यह आपके ऊपर है, लेकिन यह काफी सामान्य है कि विभिन्न गतिविधियों जैसे दुश्मन जहाज को नष्ट करना या वस्तुओं को एकत्र करना (जो वस्तुएं नष्ट होने पर गिरती हैं) पर अंक दिए जाएं।
- **एक स्तर पूरा करें**: इसमें कई स्थितियां शामिल हो सकती हैं जैसे `X` दुश्मन जहाज नष्ट करना, `Y` अंक एकत्र करना, या शायद एक विशिष्ट वस्तु को एकत्र करना।

## पुनः प्रारंभ करना

यदि लोग आपके खेल का आनंद लेते हैं, तो वे इसे फिर से खेलना चाहेंगे। जब भी खेल किसी कारण से समाप्त हो, तो आपको पुनः प्रारंभ करने का विकल्प देना चाहिए।

✅ सोचें कि किन स्थितियों में आपको लगता है कि खेल समाप्त होता है, और फिर आपको पुनः प्रारंभ करने के लिए कैसे प्रेरित किया जाता है।

## क्या बनाना है

आपको अपने खेल में ये नियम जोड़ने होंगे:

1. **खेल जीतना**। जब सभी दुश्मन जहाज नष्ट हो जाते हैं, तो आप खेल जीत जाते हैं। इसके अतिरिक्त, किसी प्रकार का विजय संदेश प्रदर्शित करें।
1. **पुनः प्रारंभ**। जब आपके सभी जीवन समाप्त हो जाते हैं या खेल जीत लिया जाता है, तो आपको खेल को पुनः प्रारंभ करने का विकल्प देना चाहिए। याद रखें! आपको खेल को पुनः प्रारंभ करना होगा और पिछले खेल की स्थिति को साफ़ करना होगा।

## अनुशंसित चरण

`your-work` सब फोल्डर में आपके लिए बनाए गए फाइलों को ढूंढें। इसमें निम्नलिखित शामिल होना चाहिए:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
  -| life.png
-| index.html
-| app.js
-| package.json
```

आप अपने प्रोजेक्ट को `your_work` फोल्डर में निम्नलिखित टाइप करके शुरू करें:

```bash
cd your-work
npm start
```

उपरोक्त कमांड `http://localhost:5000` पते पर एक HTTP सर्वर शुरू करेगा। एक ब्राउज़र खोलें और उस पते को दर्ज करें। आपका खेल खेलने योग्य स्थिति में होना चाहिए।

> सुझाव: Visual Studio Code में चेतावनियों से बचने के लिए, `window.onload` फ़ंक्शन को `gameLoopId` को वैसे ही कॉल करने के लिए संपादित करें (बिना `let` के), और फ़ाइल के शीर्ष पर स्वतंत्र रूप से `let gameLoopId;` घोषित करें।

### कोड जोड़ें

1. **समाप्ति की स्थिति को ट्रैक करें**। कोड जोड़ें जो दुश्मनों की संख्या को ट्रैक करता है, या यदि हीरो जहाज नष्ट हो गया है, तो इन दो फ़ंक्शनों को जोड़ें:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **संदेश हैंडलर्स में लॉजिक जोड़ें**। `eventEmitter` को इन स्थितियों को संभालने के लिए संपादित करें:

    ```javascript
    eventEmitter.on(Messages.COLLISION_ENEMY_LASER, (_, { first, second }) => {
        first.dead = true;
        second.dead = true;
        hero.incrementPoints();

        if (isEnemiesDead()) {
          eventEmitter.emit(Messages.GAME_END_WIN);
        }
    });

    eventEmitter.on(Messages.COLLISION_ENEMY_HERO, (_, { enemy }) => {
        enemy.dead = true;
        hero.decrementLife();
        if (isHeroDead())  {
          eventEmitter.emit(Messages.GAME_END_LOSS);
          return; // loss before victory
        }
        if (isEnemiesDead()) {
          eventEmitter.emit(Messages.GAME_END_WIN);
        }
    });
    
    eventEmitter.on(Messages.GAME_END_WIN, () => {
        endGame(true);
    });
      
    eventEmitter.on(Messages.GAME_END_LOSS, () => {
      endGame(false);
    });
    ```

1. **नए संदेश प्रकार जोड़ें**। इन संदेशों को constants ऑब्जेक्ट में जोड़ें:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **पुनः प्रारंभ कोड जोड़ें**। ऐसा कोड जोड़ें जो चयनित बटन दबाने पर खेल को पुनः प्रारंभ करता है।

   1. **कुंजी दबाव `Enter` सुनें**। अपने विंडो के eventListener को इस दबाव को सुनने के लिए संपादित करें:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **पुनः प्रारंभ संदेश जोड़ें**। इस संदेश को अपने Messages constant में जोड़ें:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **खेल के नियम लागू करें**। निम्नलिखित खेल नियम लागू करें:

   1. **खिलाड़ी जीतने की स्थिति**। जब सभी दुश्मन जहाज नष्ट हो जाते हैं, तो एक विजय संदेश प्रदर्शित करें।

      1. पहले, एक `displayMessage()` फ़ंक्शन बनाएं:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. एक `endGame()` फ़ंक्शन बनाएं:

        ```javascript
        function endGame(win) {
          clearInterval(gameLoopId);
        
          // set a delay so we are sure any paints have finished
          setTimeout(() => {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = "black";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            if (win) {
              displayMessage(
                "Victory!!! Pew Pew... - Press [Enter] to start a new game Captain Pew Pew",
                "green"
              );
            } else {
              displayMessage(
                "You died !!! Press [Enter] to start a new game Captain Pew Pew"
              );
            }
          }, 200)  
        }
        ```

   1. **पुनः प्रारंभ लॉजिक**। जब सभी जीवन समाप्त हो जाते हैं या खिलाड़ी खेल जीत जाता है, तो प्रदर्शित करें कि खेल को पुनः प्रारंभ किया जा सकता है। इसके अतिरिक्त, जब *पुनः प्रारंभ* कुंजी दबाई जाती है, तो खेल को पुनः प्रारंभ करें (आप तय कर सकते हैं कि किस कुंजी को पुनः प्रारंभ के लिए मैप किया जाना चाहिए)।

      1. `resetGame()` फ़ंक्शन बनाएं:

        ```javascript
        function resetGame() {
          if (gameLoopId) {
            clearInterval(gameLoopId);
            eventEmitter.clear();
            initGame();
            gameLoopId = setInterval(() => {
              ctx.clearRect(0, 0, canvas.width, canvas.height);
              ctx.fillStyle = "black";
              ctx.fillRect(0, 0, canvas.width, canvas.height);
              drawPoints();
              drawLife();
              updateGameObjects();
              drawGameObjects(ctx);
            }, 100);
          }
        }
        ```

     1. `initGame()` में खेल को रीसेट करने के लिए `eventEmitter` को कॉल जोड़ें:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. EventEmitter में एक `clear()` फ़ंक्शन जोड़ें:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 बधाई हो, कप्तान! आपका खेल पूरा हो गया है! बहुत बढ़िया! 🚀 💥 👽

---

## 🚀 चुनौती

एक ध्वनि जोड़ें! क्या आप अपने खेल को बेहतर बनाने के लिए ध्वनि जोड़ सकते हैं, जैसे लेज़र हिट होने पर, या हीरो के मरने या जीतने पर? यह जानने के लिए कि जावास्क्रिप्ट का उपयोग करके ध्वनि कैसे चलाई जाती है, इस [सैंडबॉक्स](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) को देखें।

## व्याख्यान पश्चात प्रश्नोत्तरी

[व्याख्यान पश्चात प्रश्नोत्तरी](https://ff-quizzes.netlify.app/web/quiz/40)

## समीक्षा और स्व-अध्ययन

आपका असाइनमेंट एक नया नमूना खेल बनाना है, इसलिए वहां के कुछ दिलचस्प खेलों का अन्वेषण करें और देखें कि आप किस प्रकार का खेल बना सकते हैं।

## असाइनमेंट

[नमूना खेल बनाएं](assignment.md)

---

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता सुनिश्चित करने का प्रयास करते हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को प्रामाणिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम उत्तरदायी नहीं हैं।