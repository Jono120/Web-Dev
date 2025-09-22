<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-28T22:59:47+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "bn"
}
-->
# মহাকাশ গেম তৈরি করুন পর্ব ৬: শেষ এবং পুনরায় শুরু

## প্রাক-লেকচার কুইজ

[প্রাক-লেকচার কুইজ](https://ff-quizzes.netlify.app/web/quiz/39)

গেমে *শেষের শর্ত* প্রকাশ করার বিভিন্ন উপায় রয়েছে। গেমের স্রষ্টা হিসেবে, গেমটি কেন শেষ হয়েছে তা নির্ধারণ করা আপনার উপর নির্ভর করে। এখানে কিছু কারণ উল্লেখ করা হলো, যদি আমরা ধরে নিই যে আপনি এখন পর্যন্ত যে মহাকাশ গেমটি তৈরি করছেন তা নিয়ে কথা বলছি:

- **`N` শত্রু জাহাজ ধ্বংস হয়েছে**: এটি বেশ সাধারণ, যদি আপনি গেমটিকে বিভিন্ন স্তরে ভাগ করেন, যেখানে একটি স্তর সম্পন্ন করতে `N` শত্রু জাহাজ ধ্বংস করতে হবে।
- **আপনার জাহাজ ধ্বংস হয়েছে**: এমন অনেক গেম রয়েছে যেখানে আপনার জাহাজ ধ্বংস হলে আপনি গেমটি হারান। আরেকটি সাধারণ পদ্ধতি হলো জীবন ধারণার ব্যবহার। প্রতিবার আপনার জাহাজ ধ্বংস হলে একটি জীবন কমে যায়। যখন সব জীবন শেষ হয়ে যায়, তখন আপনি গেমটি হারান।
- **আপনি `N` পয়েন্ট সংগ্রহ করেছেন**: আরেকটি সাধারণ শেষের শর্ত হলো পয়েন্ট সংগ্রহ করা। আপনি কীভাবে পয়েন্ট পাবেন তা আপনার উপর নির্ভর করে, তবে শত্রু জাহাজ ধ্বংস করা বা ধ্বংস হওয়া আইটেম সংগ্রহ করার মতো বিভিন্ন কার্যকলাপে পয়েন্ট দেওয়া সাধারণ।
- **একটি স্তর সম্পন্ন করুন**: এটি বিভিন্ন শর্ত জড়িত থাকতে পারে, যেমন `X` শত্রু জাহাজ ধ্বংস, `Y` পয়েন্ট সংগ্রহ, অথবা একটি নির্দিষ্ট আইটেম সংগ্রহ করা।

## পুনরায় শুরু

যদি মানুষ আপনার গেমটি উপভোগ করে, তবে তারা এটি পুনরায় খেলতে চাইবে। যেকোনো কারণে গেমটি শেষ হলে, আপনাকে পুনরায় শুরু করার একটি বিকল্প দেওয়া উচিত।

✅ একটু চিন্তা করুন, কোন শর্তে আপনি মনে করেন গেমটি শেষ হয় এবং তারপর কীভাবে আপনাকে পুনরায় শুরু করার জন্য প্ররোচিত করা হয়।

## কী তৈরি করবেন

আপনার গেমে এই নিয়মগুলো যোগ করবেন:

1. **গেম জেতা**। যখন সব শত্রু জাহাজ ধ্বংস হয়ে যায়, তখন আপনি গেমটি জিতে যান। এছাড়াও একটি বিজয়ের বার্তা প্রদর্শন করুন।
1. **পুনরায় শুরু**। যখন আপনার সব জীবন শেষ হয়ে যায় বা গেমটি জিতে যান, তখন গেমটি পুনরায় শুরু করার একটি উপায় দেওয়া উচিত। মনে রাখবেন! আপনাকে গেমটি পুনরায় আরম্ভ করতে হবে এবং পূর্ববর্তী গেমের অবস্থা মুছে ফেলতে হবে।

## প্রস্তাবিত ধাপসমূহ

`your-work` সাব ফোল্ডারে আপনার জন্য তৈরি করা ফাইলগুলো খুঁজে বের করুন। এতে নিম্নলিখিত ফাইলগুলো থাকা উচিত:

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

আপনার প্রকল্পটি `your_work` ফোল্ডারে শুরু করুন এই কমান্ডটি টাইপ করে:

```bash
cd your-work
npm start
```

উপরের কমান্ডটি `http://localhost:5000` ঠিকানায় একটি HTTP সার্ভার চালু করবে। একটি ব্রাউজার খুলুন এবং এই ঠিকানাটি প্রবেশ করান। আপনার গেমটি খেলার উপযোগী অবস্থায় থাকা উচিত।

> টিপ: Visual Studio Code-এ সতর্কতা এড়াতে, `window.onload` ফাংশনটি সম্পাদনা করে `gameLoopId` কল করুন যেমনটি আছে (কোনো `let` ছাড়া), এবং ফাইলের শীর্ষে আলাদাভাবে `let gameLoopId;` ঘোষণা করুন।

### কোড যোগ করুন

1. **শেষের শর্ত ট্র্যাক করুন**। শত্রুদের সংখ্যা বা হিরো জাহাজ ধ্বংস হয়েছে কিনা তা ট্র্যাক করার জন্য এই দুটি ফাংশন যোগ করুন:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **বার্তা হ্যান্ডলারগুলিতে লজিক যোগ করুন**। এই শর্তগুলো পরিচালনা করার জন্য `eventEmitter` সম্পাদনা করুন:

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

1. **নতুন বার্তার ধরন যোগ করুন**। এই বার্তাগুলো Constants অবজেক্টে যোগ করুন:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **পুনরায় শুরু করার কোড যোগ করুন**। একটি নির্দিষ্ট বোতাম চাপলে গেমটি পুনরায় শুরু করার কোড যোগ করুন।

   1. **`Enter` কী প্রেস শোনার জন্য**। আপনার উইন্ডোর eventListener সম্পাদনা করুন যাতে এটি এই প্রেস শোনে:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **পুনরায় শুরু বার্তা যোগ করুন**। এই বার্তাটি আপনার Messages constant-এ যোগ করুন:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **গেমের নিয়ম বাস্তবায়ন করুন**। নিম্নলিখিত গেমের নিয়মগুলো বাস্তবায়ন করুন:

   1. **প্লেয়ার জয়ের শর্ত**। যখন সব শত্রু জাহাজ ধ্বংস হয়ে যায়, তখন একটি বিজয়ের বার্তা প্রদর্শন করুন।

      1. প্রথমে একটি `displayMessage()` ফাংশন তৈরি করুন:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. একটি `endGame()` ফাংশন তৈরি করুন:

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

   1. **পুনরায় শুরু লজিক**। যখন সব জীবন শেষ হয়ে যায় বা প্লেয়ার গেমটি জিতে যায়, তখন দেখান যে গেমটি পুনরায় শুরু করা যেতে পারে। এছাড়াও, *পুনরায় শুরু* কী চাপলে গেমটি পুনরায় শুরু করুন (আপনি সিদ্ধান্ত নিতে পারেন কোন কী পুনরায় শুরুতে ম্যাপ করা হবে)।

      1. `resetGame()` ফাংশন তৈরি করুন:

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

     1. `initGame()`-এ গেম রিসেট করার জন্য `eventEmitter`-এ একটি কল যোগ করুন:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. EventEmitter-এ একটি `clear()` ফাংশন যোগ করুন:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 অভিনন্দন, ক্যাপ্টেন! আপনার গেমটি সম্পূর্ণ হয়েছে! খুব ভালো কাজ করেছেন! 🚀 💥 👽

---

## 🚀 চ্যালেঞ্জ

একটি শব্দ যোগ করুন! আপনি কি গেমপ্লে উন্নত করতে একটি শব্দ যোগ করতে পারেন, যেমন লেজার আঘাতের সময়, বা হিরো মারা গেলে বা জিতলে? এই [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) দেখুন, যেখানে JavaScript ব্যবহার করে শব্দ বাজানোর পদ্ধতি শেখানো হয়েছে।

## পোস্ট-লেকচার কুইজ

[পোস্ট-লেকচার কুইজ](https://ff-quizzes.netlify.app/web/quiz/40)

## পুনরালোচনা ও স্ব-অধ্যয়ন

আপনার কাজ হলো একটি নতুন নমুনা গেম তৈরি করা, তাই কিছু আকর্ষণীয় গেম অন্বেষণ করুন এবং দেখুন আপনি কী ধরনের গেম তৈরি করতে পারেন।

## অ্যাসাইনমেন্ট

[একটি নমুনা গেম তৈরি করুন](assignment.md)

---

**অস্বীকৃতি**:  
এই নথিটি AI অনুবাদ পরিষেবা [Co-op Translator](https://github.com/Azure/co-op-translator) ব্যবহার করে অনুবাদ করা হয়েছে। আমরা যথাসম্ভব সঠিক অনুবাদের চেষ্টা করি, তবে অনুগ্রহ করে মনে রাখবেন যে স্বয়ংক্রিয় অনুবাদে ত্রুটি বা অসঙ্গতি থাকতে পারে। নথিটির মূল ভাষায় লেখা সংস্করণটিকেই প্রামাণিক উৎস হিসেবে বিবেচনা করা উচিত। গুরুত্বপূর্ণ তথ্যের জন্য, পেশাদার মানব অনুবাদ ব্যবহার করার পরামর্শ দেওয়া হচ্ছে। এই অনুবাদ ব্যবহারের ফলে সৃষ্ট কোনো ভুল বোঝাবুঝি বা ভুল ব্যাখ্যার জন্য আমরা দায়ী নই।