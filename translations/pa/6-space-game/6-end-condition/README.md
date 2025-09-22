<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-28T17:04:31+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "pa"
}
-->
# ਸਪੇਸ ਗੇਮ ਬਣਾਓ ਭਾਗ 6: ਖੇਡ ਦਾ ਅੰਤ ਅਤੇ ਮੁੜ ਸ਼ੁਰੂ ਕਰੋ

## ਪ੍ਰੀ-ਲੈਕਚਰ ਕਵਿਜ਼

[ਪ੍ਰੀ-ਲੈਕਚਰ ਕਵਿਜ਼](https://ff-quizzes.netlify.app/web/quiz/39)

ਖੇਡ ਵਿੱਚ *ਅੰਤ ਦੀ ਸਥਿਤੀ* ਦਰਸਾਉਣ ਦੇ ਕਈ ਤਰੀਕੇ ਹਨ। ਇਹ ਤੁਹਾਡੇ ਉੱਤੇ ਨਿਰਭਰ ਕਰਦਾ ਹੈ ਕਿ ਤੁਸੀਂ ਖੇਡ ਦੇ ਰਚਨਾਕਾਰ ਵਜੋਂ ਇਹ ਕਿਉਂ ਦੱਸਦੇ ਹੋ ਕਿ ਖੇਡ ਖਤਮ ਹੋ ਗਈ ਹੈ। ਹੇਠਾਂ ਕੁਝ ਕਾਰਨ ਦਿੱਤੇ ਗਏ ਹਨ, ਜੇ ਅਸੀਂ ਮੰਨ ਲਈਏ ਕਿ ਅਸੀਂ ਉਸ ਸਪੇਸ ਗੇਮ ਬਾਰੇ ਗੱਲ ਕਰ ਰਹੇ ਹਾਂ ਜੋ ਤੁਸੀਂ ਹੁਣ ਤੱਕ ਬਣਾਈ ਹੈ:

- **`N` ਦੁਸ਼ਮਨ ਜਹਾਜ਼ ਤਬਾਹ ਹੋ ਗਏ ਹਨ**: ਇਹ ਕਾਫੀ ਆਮ ਹੈ ਜੇ ਤੁਸੀਂ ਖੇਡ ਨੂੰ ਵੱਖ-ਵੱਖ ਪੱਧਰਾਂ ਵਿੱਚ ਵੰਡਦੇ ਹੋ, ਤਾਂ ਤੁਹਾਨੂੰ ਇੱਕ ਪੱਧਰ ਪੂਰਾ ਕਰਨ ਲਈ `N` ਦੁਸ਼ਮਨ ਜਹਾਜ਼ ਤਬਾਹ ਕਰਨੇ ਪੈਂਦੇ ਹਨ।
- **ਤੁਹਾਡਾ ਜਹਾਜ਼ ਤਬਾਹ ਹੋ ਗਿਆ ਹੈ**: ਕਈ ਖੇਡਾਂ ਵਿੱਚ ਇਹ ਹੁੰਦਾ ਹੈ ਕਿ ਜੇ ਤੁਹਾਡਾ ਜਹਾਜ਼ ਤਬਾਹ ਹੋ ਜਾਂਦਾ ਹੈ ਤਾਂ ਤੁਸੀਂ ਖੇਡ ਹਾਰ ਜਾਂਦੇ ਹੋ। ਇੱਕ ਹੋਰ ਆਮ ਤਰੀਕਾ ਇਹ ਹੈ ਕਿ ਤੁਹਾਡੇ ਕੋਲ ਜ਼ਿੰਦਗੀਆਂ ਦੀ ਸੰਕਲਪਨਾ ਹੁੰਦੀ ਹੈ। ਹਰ ਵਾਰ ਜਦੋਂ ਤੁਹਾਡਾ ਜਹਾਜ਼ ਤਬਾਹ ਹੁੰਦਾ ਹੈ, ਇੱਕ ਜ਼ਿੰਦਗੀ ਘਟ ਜਾਂਦੀ ਹੈ। ਜਦੋਂ ਸਾਰੀਆਂ ਜ਼ਿੰਦਗੀਆਂ ਖਤਮ ਹੋ ਜਾਂਦੀਆਂ ਹਨ, ਤਾਂ ਤੁਸੀਂ ਖੇਡ ਹਾਰ ਜਾਂਦੇ ਹੋ।
- **ਤੁਸੀਂ `N` ਅੰਕ ਪ੍ਰਾਪਤ ਕੀਤੇ ਹਨ**: ਇੱਕ ਹੋਰ ਆਮ ਅੰਤ ਦੀ ਸਥਿਤੀ ਇਹ ਹੈ ਕਿ ਤੁਸੀਂ ਅੰਕ ਪ੍ਰਾਪਤ ਕਰੋ। ਤੁਸੀਂ ਅੰਕ ਕਿਵੇਂ ਪ੍ਰਾਪਤ ਕਰਦੇ ਹੋ ਇਹ ਤੁਹਾਡੇ ਉੱਤੇ ਨਿਰਭਰ ਕਰਦਾ ਹੈ, ਪਰ ਇਹ ਕਾਫੀ ਆਮ ਹੈ ਕਿ ਵੱਖ-ਵੱਖ ਗਤੀਵਿਧੀਆਂ ਲਈ ਅੰਕ ਦਿੱਤੇ ਜਾਂਦੇ ਹਨ, ਜਿਵੇਂ ਕਿ ਦੁਸ਼ਮਨ ਜਹਾਜ਼ ਤਬਾਹ ਕਰਨਾ ਜਾਂ ਉਹ ਚੀਜ਼ਾਂ ਇਕੱਠੀਆਂ ਕਰਨਾ ਜੋ ਤਬਾਹ ਹੋਣ 'ਤੇ ਡਰੌਪ ਹੁੰਦੀਆਂ ਹਨ।
- **ਇੱਕ ਪੱਧਰ ਪੂਰਾ ਕਰੋ**: ਇਸ ਵਿੱਚ ਕਈ ਸਥਿਤੀਆਂ ਸ਼ਾਮਲ ਹੋ ਸਕਦੀਆਂ ਹਨ ਜਿਵੇਂ ਕਿ `X` ਦੁਸ਼ਮਨ ਜਹਾਜ਼ ਤਬਾਹ ਹੋਏ, `Y` ਅੰਕ ਪ੍ਰਾਪਤ ਕੀਤੇ ਜਾਂ ਸ਼ਾਇਦ ਕੋਈ ਖਾਸ ਚੀਜ਼ ਇਕੱਠੀ ਕੀਤੀ ਗਈ।

## ਮੁੜ ਸ਼ੁਰੂ ਕਰਨਾ

ਜੇ ਲੋਕ ਤੁਹਾਡੀ ਖੇਡ ਦਾ ਆਨੰਦ ਲੈਂਦੇ ਹਨ, ਤਾਂ ਉਹ ਇਸਨੂੰ ਮੁੜ ਖੇਡਣਾ ਚਾਹੁੰਦੇ ਹਨ। ਜਦੋਂ ਖੇਡ ਕਿਸੇ ਵੀ ਕਾਰਨ ਕਰਕੇ ਖਤਮ ਹੁੰਦੀ ਹੈ, ਤਾਂ ਤੁਹਾਨੂੰ ਮੁੜ ਸ਼ੁਰੂ ਕਰਨ ਦਾ ਵਿਕਲਪ ਦੇਣਾ ਚਾਹੀਦਾ ਹੈ।

✅ ਸੋਚੋ ਕਿ ਕਿਸ ਸਥਿਤੀ ਵਿੱਚ ਤੁਹਾਨੂੰ ਲੱਗਦਾ ਹੈ ਕਿ ਖੇਡ ਖਤਮ ਹੋ ਗਈ ਹੈ, ਅਤੇ ਫਿਰ ਤੁਹਾਨੂੰ ਮੁੜ ਸ਼ੁਰੂ ਕਰਨ ਲਈ ਕਿਵੇਂ ਪ੍ਰੇਰਿਤ ਕੀਤਾ ਜਾਂਦਾ ਹੈ।

## ਕੀ ਬਣਾਉਣਾ ਹੈ

ਤੁਸੀਂ ਆਪਣੀ ਖੇਡ ਵਿੱਚ ਇਹ ਨਿਯਮ ਸ਼ਾਮਲ ਕਰੋਗੇ:

1. **ਖੇਡ ਜਿੱਤਣਾ**। ਜਦੋਂ ਸਾਰੇ ਦੁਸ਼ਮਨ ਜਹਾਜ਼ ਤਬਾਹ ਹੋ ਜਾਂਦੇ ਹਨ, ਤਾਂ ਤੁਸੀਂ ਖੇਡ ਜਿੱਤ ਲੈਂਦੇ ਹੋ। ਇਸਦੇ ਨਾਲ ਹੀ ਕਿਸੇ ਤਰ੍ਹਾਂ ਦਾ ਜਿੱਤ ਦਾ ਸੁਨੇਹਾ ਦਿਖਾਓ।
1. **ਮੁੜ ਸ਼ੁਰੂ ਕਰੋ**। ਜਦੋਂ ਸਾਰੀਆਂ ਜ਼ਿੰਦਗੀਆਂ ਖਤਮ ਹੋ ਜਾਂਦੀਆਂ ਹਨ ਜਾਂ ਖੇਡ ਜਿੱਤੀ ਜਾਂਦੀ ਹੈ, ਤਾਂ ਤੁਹਾਨੂੰ ਖੇਡ ਮੁੜ ਸ਼ੁਰੂ ਕਰਨ ਦਾ ਤਰੀਕਾ ਦੇਣਾ ਚਾਹੀਦਾ ਹੈ। ਯਾਦ ਰੱਖੋ! ਤੁਹਾਨੂੰ ਖੇਡ ਨੂੰ ਮੁੜ ਸ਼ੁਰੂ ਕਰਨਾ ਹੋਵੇਗਾ ਅਤੇ ਪਿਛਲੇ ਖੇਡ ਦੀ ਸਥਿਤੀ ਨੂੰ ਸਾਫ਼ ਕਰਨਾ ਹੋਵੇਗਾ।

## ਸਿਫਾਰਸ਼ੀ ਕਦਮ

`your-work` ਸਬ ਫੋਲਡਰ ਵਿੱਚ ਬਣਾਈਆਂ ਗਈਆਂ ਫਾਈਲਾਂ ਨੂੰ ਲੱਭੋ। ਇਸ ਵਿੱਚ ਹੇਠਾਂ ਦਿੱਤੇ ਗਏ ਹੋਣੇ ਚਾਹੀਦੇ ਹਨ:

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

ਤੁਸੀਂ ਆਪਣਾ ਪ੍ਰੋਜੈਕਟ `your_work` ਫੋਲਡਰ ਵਿੱਚ ਇਸ ਤਰੀਕੇ ਨਾਲ ਸ਼ੁਰੂ ਕਰੋ:

```bash
cd your-work
npm start
```

ਉਪਰੋਕਤ HTTP ਸਰਵਰ ਪਤਾ `http://localhost:5000` 'ਤੇ ਸ਼ੁਰੂ ਕਰੇਗਾ। ਇੱਕ ਬ੍ਰਾਊਜ਼ਰ ਖੋਲ੍ਹੋ ਅਤੇ ਇਸ ਪਤੇ ਨੂੰ ਦਰਜ ਕਰੋ। ਤੁਹਾਡੀ ਖੇਡ ਖੇਡਣ ਯੋਗ ਹੋਣੀ ਚਾਹੀਦੀ ਹੈ।

> ਟਿਪ: Visual Studio Code ਵਿੱਚ ਚੇਤਾਵਨੀਆਂ ਤੋਂ ਬਚਣ ਲਈ, `window.onload` ਫੰਕਸ਼ਨ ਨੂੰ `gameLoopId` ਨੂੰ ਬਿਨਾਂ `let` ਦੇ ਕਾਲ ਕਰਨ ਲਈ ਸੋਧੋ, ਅਤੇ ਫਾਈਲ ਦੇ ਸਿਰੇ 'ਤੇ `let gameLoopId;` ਨੂੰ ਅਲੱਗ-ਅਲੱਗ ਘੋਸ਼ਿਤ ਕਰੋ।

### ਕੋਡ ਸ਼ਾਮਲ ਕਰੋ

1. **ਅੰਤ ਦੀ ਸਥਿਤੀ ਟ੍ਰੈਕ ਕਰੋ**। ਕੋਡ ਸ਼ਾਮਲ ਕਰੋ ਜੋ ਦੁਸ਼ਮਨਾਂ ਦੀ ਗਿਣਤੀ ਜਾਂ ਹੀਰੋ ਜਹਾਜ਼ ਦੇ ਤਬਾਹ ਹੋਣ ਨੂੰ ਟ੍ਰੈਕ ਕਰਦਾ ਹੈ, ਇਹ ਦੋ ਫੰਕਸ਼ਨ ਸ਼ਾਮਲ ਕਰਕੇ:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **ਸੁਨੇਹਾ ਹੈਂਡਲਰ ਵਿੱਚ ਤਰਕ ਸ਼ਾਮਲ ਕਰੋ**। `eventEmitter` ਨੂੰ ਸੋਧੋ ਤਾਂ ਜੋ ਇਹ ਸਥਿਤੀਆਂ ਹੈਂਡਲ ਕਰ ਸਕੇ:

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

1. **ਨਵੇਂ ਸੁਨੇਹਾ ਪ੍ਰਕਾਰ ਸ਼ਾਮਲ ਕਰੋ**। ਇਹ ਸੁਨੇਹੇ constants ਆਬਜੈਕਟ ਵਿੱਚ ਸ਼ਾਮਲ ਕਰੋ:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **ਮੁੜ ਸ਼ੁਰੂ ਕਰਨ ਦਾ ਕੋਡ ਸ਼ਾਮਲ ਕਰੋ**। ਖਾਸ ਬਟਨ ਦਬਾਉਣ 'ਤੇ ਖੇਡ ਮੁੜ ਸ਼ੁਰੂ ਕਰਨ ਦਾ ਕੋਡ ਸ਼ਾਮਲ ਕਰੋ।

   1. **ਕੀ ਦਬਾਉਣ `Enter` ਨੂੰ ਸੁਣੋ**। ਆਪਣੇ ਵਿੰਡੋ ਦੇ eventListener ਨੂੰ ਇਸ ਦਬਾਅ ਨੂੰ ਸੁਣਨ ਲਈ ਸੋਧੋ:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **ਮੁੜ ਸ਼ੁਰੂ ਕਰਨ ਦਾ ਸੁਨੇਹਾ ਸ਼ਾਮਲ ਕਰੋ**। ਇਹ ਸੁਨੇਹਾ ਆਪਣੇ Messages constant ਵਿੱਚ ਸ਼ਾਮਲ ਕਰੋ:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **ਖੇਡ ਦੇ ਨਿਯਮ ਲਾਗੂ ਕਰੋ**। ਹੇਠਾਂ ਦਿੱਤੇ ਖੇਡ ਦੇ ਨਿਯਮ ਲਾਗੂ ਕਰੋ:

   1. **ਪਲੇਅਰ ਜਿੱਤ ਦੀ ਸਥਿਤੀ**। ਜਦੋਂ ਸਾਰੇ ਦੁਸ਼ਮਨ ਜਹਾਜ਼ ਤਬਾਹ ਹੋ ਜਾਂਦੇ ਹਨ, ਤਾਂ ਜਿੱਤ ਦਾ ਸੁਨੇਹਾ ਦਿਖਾਓ।

      1. ਪਹਿਲਾਂ, ਇੱਕ `displayMessage()` ਫੰਕਸ਼ਨ ਬਣਾਓ:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. ਇੱਕ `endGame()` ਫੰਕਸ਼ਨ ਬਣਾਓ:

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

   1. **ਮੁੜ ਸ਼ੁਰੂ ਕਰਨ ਦੀ ਤਰਕ**। ਜਦੋਂ ਸਾਰੀਆਂ ਜ਼ਿੰਦਗੀਆਂ ਖਤਮ ਹੋ ਜਾਂਦੀਆਂ ਹਨ ਜਾਂ ਖਿਡਾਰੀ ਨੇ ਖੇਡ ਜਿੱਤ ਲਈ ਹੈ, ਤਾਂ ਦਿਖਾਓ ਕਿ ਖੇਡ ਮੁੜ ਸ਼ੁਰੂ ਕੀਤੀ ਜਾ ਸਕਦੀ ਹੈ। ਇਸਦੇ ਨਾਲ ਹੀ, ਜਦੋਂ *ਮੁੜ ਸ਼ੁਰੂ ਕਰਨ* ਦੀ ਕੁੰਜੀ ਦਬਾਈ ਜਾਂਦੀ ਹੈ, ਤਾਂ ਖੇਡ ਮੁੜ ਸ਼ੁਰੂ ਕਰੋ (ਤੁਸੀਂ ਫੈਸਲਾ ਕਰ ਸਕਦੇ ਹੋ ਕਿ ਕਿਹੜੀ ਕੁੰਜੀ ਮੁੜ ਸ਼ੁਰੂ ਕਰਨ ਲਈ ਨਕਸ਼ਾ ਕੀਤੀ ਜਾਵੇ)।

      1. `resetGame()` ਫੰਕਸ਼ਨ ਬਣਾਓ:

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

     1. `initGame()` ਵਿੱਚ ਖੇਡ ਨੂੰ ਰੀਸੈਟ ਕਰਨ ਲਈ `eventEmitter` ਨੂੰ ਕਾਲ ਸ਼ਾਮਲ ਕਰੋ:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. EventEmitter ਵਿੱਚ ਇੱਕ `clear()` ਫੰਕਸ਼ਨ ਸ਼ਾਮਲ ਕਰੋ:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 ਮੁਬਾਰਕਾਂ, ਕੈਪਟਨ! ਤੁਹਾਡੀ ਖੇਡ ਪੂਰੀ ਹੋ ਗਈ ਹੈ! ਸ਼ਾਬਾਸ਼! 🚀 💥 👽

---

## 🚀 ਚੁਣੌਤੀ

ਆਵਾਜ਼ ਸ਼ਾਮਲ ਕਰੋ! ਕੀ ਤੁਸੀਂ ਖੇਡ ਦੇ ਖੇਡਣ ਦੇ ਤਜਰਬੇ ਨੂੰ ਵਧਾਉਣ ਲਈ ਕੋਈ ਆਵਾਜ਼ ਸ਼ਾਮਲ ਕਰ ਸਕਦੇ ਹੋ, ਜਿਵੇਂ ਕਿ ਜਦੋਂ ਲੇਜ਼ਰ ਹਿੱਟ ਕਰਦਾ ਹੈ, ਜਾਂ ਹੀਰੋ ਮਰ ਜਾਂਦਾ ਹੈ ਜਾਂ ਜਿੱਤਦਾ ਹੈ? ਇਸ [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) ਨੂੰ ਵੇਖੋ ਕਿ ਜਾਵਾਸਕ੍ਰਿਪਟ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਆਵਾਜ਼ ਕਿਵੇਂ ਚਲਾਈ ਜਾ ਸਕਦੀ ਹੈ।

## ਪੋਸਟ-ਲੈਕਚਰ ਕਵਿਜ਼

[ਪੋਸਟ-ਲੈਕਚਰ ਕਵਿਜ਼](https://ff-quizzes.netlify.app/web/quiz/40)

## ਸਮੀਖਿਆ ਅਤੇ ਸਵੈ ਅਧਿਐਨ

ਤੁਹਾਡਾ ਕੰਮ ਇੱਕ ਨਵੀਂ ਨਮੂਨਾ ਖੇਡ ਬਣਾਉਣਾ ਹੈ, ਇਸ ਲਈ ਕੁਝ ਦਿਲਚਸਪ ਖੇਡਾਂ ਦੀ ਖੋਜ ਕਰੋ ਤਾਂ ਜੋ ਤੁਸੀਂ ਦੇਖ ਸਕੋ ਕਿ ਤੁਸੀਂ ਕਿਸ ਤਰ੍ਹਾਂ ਦੀ ਖੇਡ ਬਣਾਉਣਾ ਚਾਹੁੰਦੇ ਹੋ।

## ਅਸਾਈਨਮੈਂਟ

[ਨਮੂਨਾ ਖੇਡ ਬਣਾਓ](assignment.md)

---

**ਅਸਵੀਕਰਤੀ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀ ਹੋਣ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰਦੇ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚਤਤਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼ ਨੂੰ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤ ਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।