<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-28T16:16:46+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "mr"
}
-->
# स्पेस गेम तयार करा भाग ६: शेवट आणि पुन्हा सुरू करा

## प्री-लेक्चर क्विझ

[प्री-लेक्चर क्विझ](https://ff-quizzes.netlify.app/web/quiz/39)

गेममध्ये *शेवटाची अट* व्यक्त करण्याचे वेगवेगळे मार्ग असतात. गेम तयार करणाऱ्या व्यक्तीवर हे अवलंबून असते की गेम का संपला आहे हे सांगणे. जर आपण आतापर्यंत तयार केलेल्या स्पेस गेमबद्दल बोलत असू, तर खालील कारणे असू शकतात:

- **`N` शत्रू जहाजे नष्ट झाली आहेत**: जर तुम्ही गेम वेगवेगळ्या स्तरांमध्ये विभागला असेल तर `N` शत्रू जहाजे नष्ट करणे आवश्यक असते जेणेकरून स्तर पूर्ण होईल.
- **तुमचे जहाज नष्ट झाले आहे**: असे अनेक गेम्स आहेत जिथे तुमचे जहाज नष्ट झाल्यास तुम्ही गेम हरता. आणखी एक सामान्य पद्धत म्हणजे "जीव" ही संकल्पना असते. प्रत्येक वेळी तुमचे जहाज नष्ट झाले की एक जीव कमी होतो. सर्व जीव संपल्यावर तुम्ही गेम हरता.
- **तुम्ही `N` गुण मिळवले आहेत**: आणखी एक सामान्य शेवटाची अट म्हणजे तुम्ही गुण गोळा करणे. तुम्ही गुण कसे मिळवता हे तुमच्यावर अवलंबून असते, परंतु शत्रू जहाज नष्ट करणे किंवा नष्ट झाल्यावर वस्तू गोळा करणे यासारख्या क्रियाकलापांना गुण देणे सामान्य आहे.
- **स्तर पूर्ण करा**: यामध्ये अनेक अटी असू शकतात जसे की `X` शत्रू जहाजे नष्ट करणे, `Y` गुण गोळा करणे किंवा विशिष्ट वस्तू गोळा करणे.

## पुन्हा सुरू करणे

जर लोकांना तुमचा गेम आवडला तर ते तो पुन्हा खेळण्याची शक्यता आहे. गेम कोणत्याही कारणाने संपल्यावर तुम्ही पुन्हा सुरू करण्याचा पर्याय द्यायला हवा.

✅ विचार करा की कोणत्या अटींवर तुम्हाला गेम संपतो असे वाटते आणि तुम्हाला पुन्हा सुरू करण्यासाठी कसे प्रोत्साहित केले जाते.

## काय तयार करायचे

तुम्ही तुमच्या गेममध्ये खालील नियम जोडणार आहात:

1. **गेम जिंकणे**. सर्व शत्रू जहाजे नष्ट झाल्यावर तुम्ही गेम जिंकता. याशिवाय विजयाचा संदेश दाखवा.
1. **पुन्हा सुरू करा**. सर्व जीव संपल्यावर किंवा गेम जिंकल्यावर तुम्ही गेम पुन्हा सुरू करण्याचा पर्याय द्यायला हवा. लक्षात ठेवा! तुम्हाला गेम पुन्हा सुरू करावा लागेल आणि मागील गेमची स्थिती साफ करावी लागेल.

## शिफारस केलेली पावले

`your-work` सब फोल्डरमध्ये तयार केलेल्या फाइल्स शोधा. त्यामध्ये खालील असावे:

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

तुमचा प्रोजेक्ट `your_work` फोल्डरमध्ये सुरू करण्यासाठी टाइप करा:

```bash
cd your-work
npm start
```

वरील आदेश `http://localhost:5000` या पत्त्यावर HTTP सर्व्हर सुरू करेल. ब्राउझर उघडा आणि तो पत्ता टाका. तुमचा गेम खेळण्यायोग्य स्थितीत असावा.

> टिप: व्हिज्युअल स्टुडिओ कोडमध्ये चेतावणी टाळण्यासाठी, `window.onload` फंक्शन संपादित करा आणि `gameLoopId` कॉल करा (त्याशिवाय `let`), आणि फाइलच्या शीर्षस्थानी स्वतंत्रपणे `let gameLoopId;` घोषित करा.

### कोड जोडा

1. **शेवटाची अट ट्रॅक करा**. शत्रूंची संख्या किंवा हिरो जहाज नष्ट झाले आहे का हे ट्रॅक करण्यासाठी खालील दोन फंक्शन्स जोडा:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **संदेश हँडलर्समध्ये लॉजिक जोडा**. `eventEmitter` संपादित करा आणि या अटी हाताळा:

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

1. **नवीन संदेश प्रकार जोडा**. या संदेशांना constants ऑब्जेक्टमध्ये जोडा:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **पुन्हा सुरू करण्याचा कोड जोडा**. निवडलेल्या बटणाच्या प्रेसवर गेम पुन्हा सुरू करण्याचा कोड जोडा.

   1. **की प्रेस `Enter` ऐका**. तुमच्या विंडोच्या eventListener मध्ये ही प्रेस ऐकण्यासाठी संपादन करा:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **पुन्हा सुरू करण्याचा संदेश जोडा**. Messages constant मध्ये हा संदेश जोडा:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **गेम नियम अंमलात आणा**. खालील गेम नियम अंमलात आणा:

   1. **प्लेयर जिंकण्याची अट**. सर्व शत्रू जहाजे नष्ट झाल्यावर विजयाचा संदेश दाखवा.

      1. प्रथम, `displayMessage()` फंक्शन तयार करा:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. `endGame()` फंक्शन तयार करा:

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

   1. **पुन्हा सुरू करण्याचे लॉजिक**. सर्व जीव संपल्यावर किंवा खेळाडूने गेम जिंकल्यावर, गेम पुन्हा सुरू करता येईल असे दाखवा. याशिवाय *पुन्हा सुरू* की दाबल्यावर गेम पुन्हा सुरू करा (तुम्ही कोणती की मॅप करायची ते ठरवू शकता).

      1. `resetGame()` फंक्शन तयार करा:

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

     1. `initGame()` मध्ये गेम रीसेट करण्यासाठी `eventEmitter` कॉल जोडा:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. EventEmitter मध्ये `clear()` फंक्शन जोडा:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 अभिनंदन, कॅप्टन! तुमचा गेम पूर्ण झाला आहे! खूप छान काम केले! 🚀 💥 👽

---

## 🚀 आव्हान

आवाज जोडा! तुम्ही गेमप्ले सुधारण्यासाठी आवाज जोडू शकता का, जसे की लेझर हिट झाल्यावर, हिरो मरण पावल्यावर किंवा जिंकल्यावर? जावास्क्रिप्ट वापरून आवाज कसा प्ले करायचा हे शिकण्यासाठी [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) पहा.

## पोस्ट-लेक्चर क्विझ

[पोस्ट-लेक्चर क्विझ](https://ff-quizzes.netlify.app/web/quiz/40)

## पुनरावलोकन आणि स्व-अभ्यास

तुमचे काम एक नवीन नमुना गेम तयार करणे आहे, त्यामुळे तुम्ही तयार करू शकणाऱ्या गेमच्या प्रकारांबद्दल जाणून घेण्यासाठी काही मनोरंजक गेम्स एक्सप्लोर करा.

## असाइनमेंट

[नमुना गेम तयार करा](assignment.md)

---

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी, कृपया लक्षात घ्या की स्वयंचलित भाषांतरांमध्ये त्रुटी किंवा अचूकतेचा अभाव असू शकतो. मूळ भाषेतील मूळ दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी, व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून उद्भवणाऱ्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.