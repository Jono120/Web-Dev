<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a9a161871de7706cb0e23b1bd0c74559",
  "translation_date": "2025-08-28T17:01:57+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "pa"
}
-->
# ਸਪੇਸ ਗੇਮ ਬਣਾਓ ਭਾਗ 3: ਮੋਸ਼ਨ ਸ਼ਾਮਲ ਕਰਨਾ

## ਪੂਰਵ-ਵਿਆਖਿਆ ਪ੍ਰਸ਼ਨਾਵਲੀ

[ਪੂਰਵ-ਵਿਆਖਿਆ ਪ੍ਰਸ਼ਨਾਵਲੀ](https://ff-quizzes.netlify.app/web/quiz/33)

ਗੇਮਾਂ ਤਦ ਤੱਕ ਮਜ਼ੇਦਾਰ ਨਹੀਂ ਹੁੰਦੀਆਂ ਜਦ ਤੱਕ ਸਕ੍ਰੀਨ 'ਤੇ ਐਲੀਅਨ ਦੌੜਦੇ ਨਹੀਂ। ਇਸ ਗੇਮ ਵਿੱਚ, ਅਸੀਂ ਦੋ ਕਿਸਮ ਦੇ ਮੋਸ਼ਨ ਦੀ ਵਰਤੋਂ ਕਰਾਂਗੇ:

- **ਕੀਬੋਰਡ/ਮਾਊਸ ਮੋਸ਼ਨ**: ਜਦੋਂ ਉਪਭੋਗਤਾ ਸਕ੍ਰੀਨ 'ਤੇ ਕਿਸੇ ਆਬਜੈਕਟ ਨੂੰ ਹਿਲਾਉਣ ਲਈ ਕੀਬੋਰਡ ਜਾਂ ਮਾਊਸ ਨਾਲ ਇੰਟਰੈਕਟ ਕਰਦਾ ਹੈ।
- **ਗੇਮ ਦੁਆਰਾ ਪ੍ਰੇਰਿਤ ਮੋਸ਼ਨ**: ਜਦੋਂ ਗੇਮ ਕਿਸੇ ਆਬਜੈਕਟ ਨੂੰ ਇੱਕ ਨਿਰਧਾਰਤ ਸਮੇਂ ਦੇ ਅੰਤਰਾਲ 'ਤੇ ਹਿਲਾਉਂਦਾ ਹੈ।

ਤਾਂ ਅਸੀਂ ਸਕ੍ਰੀਨ 'ਤੇ ਚੀਜ਼ਾਂ ਕਿਵੇਂ ਹਿਲਾਉਂਦੇ ਹਾਂ? ਇਹ ਸਾਰਾ ਕਾਰਟੀਸੀਅਨ ਕੋਆਰਡੀਨੇਟਸ ਬਾਰੇ ਹੈ: ਅਸੀਂ ਆਬਜੈਕਟ ਦੇ ਸਥਾਨ (x, y) ਨੂੰ ਬਦਲਦੇ ਹਾਂ ਅਤੇ ਫਿਰ ਸਕ੍ਰੀਨ ਨੂੰ ਦੁਬਾਰਾ ਡ੍ਰਾ ਕਰਦੇ ਹਾਂ।

ਆਮ ਤੌਰ 'ਤੇ, ਸਕ੍ਰੀਨ 'ਤੇ *ਮੋਸ਼ਨ* ਪੂਰਾ ਕਰਨ ਲਈ ਤੁਹਾਨੂੰ ਹੇਠਾਂ ਦਿੱਤੇ ਕਦਮਾਂ ਦੀ ਲੋੜ ਹੁੰਦੀ ਹੈ:

1. **ਨਵਾਂ ਸਥਾਨ ਸੈਟ ਕਰੋ** ਕਿਸੇ ਆਬਜੈਕਟ ਲਈ; ਇਹ ਆਬਜੈਕਟ ਨੂੰ ਹਿਲਿਆ ਹੋਇਆ ਮਹਿਸੂਸ ਕਰਨ ਲਈ ਜ਼ਰੂਰੀ ਹੈ।
2. **ਸਕ੍ਰੀਨ ਸਾਫ਼ ਕਰੋ**, ਡ੍ਰਾ ਕਰਨ ਦੇ ਵਿਚਕਾਰ ਸਕ੍ਰੀਨ ਨੂੰ ਸਾਫ਼ ਕਰਨ ਦੀ ਲੋੜ ਹੁੰਦੀ ਹੈ। ਅਸੀਂ ਇਸਨੂੰ ਇੱਕ ਰੈਕਟੈਂਗਲ ਡ੍ਰਾ ਕਰਕੇ ਸਾਫ਼ ਕਰ ਸਕਦੇ ਹਾਂ ਜਿਸਨੂੰ ਅਸੀਂ ਬੈਕਗ੍ਰਾਊਂਡ ਰੰਗ ਨਾਲ ਭਰਦੇ ਹਾਂ।
3. **ਨਵੇਂ ਸਥਾਨ 'ਤੇ ਆਬਜੈਕਟ ਨੂੰ ਦੁਬਾਰਾ ਡ੍ਰਾ ਕਰੋ**। ਇਸਨੂੰ ਕਰਨ ਨਾਲ ਅਸੀਂ ਆਖਿਰਕਾਰ ਆਬਜੈਕਟ ਨੂੰ ਇੱਕ ਸਥਾਨ ਤੋਂ ਦੂਜੇ ਸਥਾਨ 'ਤੇ ਹਿਲਾਉਣ ਵਿੱਚ ਸਫਲ ਹੁੰਦੇ ਹਾਂ।

ਇਹ ਕੋਡ ਵਿੱਚ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦੇ ਸਕਦਾ ਹੈ:

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

✅ ਕੀ ਤੁਸੀਂ ਸੋਚ ਸਕਦੇ ਹੋ ਕਿ ਕਿਉਂ ਆਪਣੇ ਹੀਰੋ ਨੂੰ ਹਰ ਸੈਕੰਡ ਵਿੱਚ ਕਈ ਫਰੇਮਾਂ 'ਤੇ ਦੁਬਾਰਾ ਡ੍ਰਾ ਕਰਨ ਨਾਲ ਪ੍ਰਦਰਸ਼ਨ ਦੀ ਲਾਗਤ ਵਧ ਸਕਦੀ ਹੈ? [ਇਸ ਪੈਟਰਨ ਦੇ ਵਿਕਲਪਾਂ](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas) ਬਾਰੇ ਪੜ੍ਹੋ।

## ਕੀਬੋਰਡ ਇਵੈਂਟਸ ਨੂੰ ਹੈਂਡਲ ਕਰੋ

ਤੁਸੀਂ ਇਵੈਂਟਸ ਨੂੰ ਕੋਡ ਨਾਲ ਜੁੜੇ ਵਿਸ਼ੇਸ਼ ਇਵੈਂਟਸ ਨੂੰ ਹੈਂਡਲ ਕਰਕੇ ਸੰਭਾਲਦੇ ਹੋ। ਕੀਬੋਰਡ ਇਵੈਂਟਸ ਪੂਰੀ ਵਿੰਡੋ 'ਤੇ ਟ੍ਰਿਗਰ ਹੁੰਦੇ ਹਨ ਜਦਕਿ ਮਾਊਸ ਇਵੈਂਟਸ ਜਿਵੇਂ ਕਿ `click` ਕਿਸੇ ਵਿਸ਼ੇਸ਼ ਐਲੀਮੈਂਟ 'ਤੇ ਕਲਿਕ ਕਰਨ ਨਾਲ ਜੁੜੇ ਹੋ ਸਕਦੇ ਹਨ। ਅਸੀਂ ਇਸ ਪ੍ਰੋਜੈਕਟ ਵਿੱਚ ਕੀਬੋਰਡ ਇਵੈਂਟਸ ਦੀ ਵਰਤੋਂ ਕਰਾਂਗੇ।

ਇਕ ਇਵੈਂਟ ਨੂੰ ਹੈਂਡਲ ਕਰਨ ਲਈ ਤੁਹਾਨੂੰ ਵਿੰਡੋ ਦੇ `addEventListener()` ਮੈਥਡ ਦੀ ਵਰਤੋਂ ਕਰਨੀ ਪਵੇਗੀ ਅਤੇ ਇਸਨੂੰ ਦੋ ਇਨਪੁਟ ਪੈਰਾਮੀਟਰ ਦੇਣੇ ਪੈਣਗੇ। ਪਹਿਲਾ ਪੈਰਾਮੀਟਰ ਇਵੈਂਟ ਦਾ ਨਾਮ ਹੈ, ਉਦਾਹਰਨ ਲਈ `keyup`। ਦੂਜਾ ਪੈਰਾਮੀਟਰ ਉਹ ਫੰਕਸ਼ਨ ਹੈ ਜੋ ਇਵੈਂਟ ਹੋਣ ਦੇ ਨਤੀਜੇ ਵਜੋਂ ਚਲਾਇਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ।

ਇਹ ਇੱਕ ਉਦਾਹਰਨ ਹੈ:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

ਕੀ ਇਵੈਂਟਸ ਲਈ ਇਵੈਂਟ 'ਤੇ ਦੋ ਪ੍ਰਾਪਰਟੀਜ਼ ਹੁੰਦੀਆਂ ਹਨ ਜੋ ਤੁਸੀਂ ਦੇਖ ਸਕਦੇ ਹੋ ਕਿ ਕਿਹੜੀ ਕੁੰਜੀ ਦਬਾਈ ਗਈ ਸੀ:

- `key`, ਇਹ ਦਬਾਈ ਗਈ ਕੁੰਜੀ ਦੀ ਸਤਰ ਰੂਪ ਰੂਪਰੇਖਾ ਹੈ, ਉਦਾਹਰਨ ਲਈ `ArrowUp`
- `keyCode`, ਇਹ ਇੱਕ ਨੰਬਰ ਰੂਪ ਰੂਪਰੇਖਾ ਹੈ, ਉਦਾਹਰਨ ਲਈ `37`, ਜੋ `ArrowLeft` ਦੇ ਅਨੁਕੂਲ ਹੈ।

✅ ਕੀ ਇਵੈਂਟ ਮੈਨਿਪੂਲੇਸ਼ਨ ਗੇਮ ਡਿਵੈਲਪਮੈਂਟ ਤੋਂ ਬਾਹਰ ਵੀ ਲਾਭਦਾਇਕ ਹੈ। ਇਸ ਤਕਨੀਕ ਲਈ ਹੋਰ ਕੀ ਉਪਯੋਗਤਾਵਾਂ ਤੁਸੀਂ ਸੋਚ ਸਕਦੇ ਹੋ?

### ਵਿਸ਼ੇਸ਼ ਕੁੰਜੀਆਂ: ਇੱਕ ਚੇਤਾਵਨੀ

ਕੁਝ *ਵਿਸ਼ੇਸ਼* ਕੁੰਜੀਆਂ ਵਿੰਡੋ ਨੂੰ ਪ੍ਰਭਾਵਿਤ ਕਰਦੀਆਂ ਹਨ। ਇਸਦਾ ਮਤਲਬ ਹੈ ਕਿ ਜੇ ਤੁਸੀਂ `keyup` ਇਵੈਂਟ ਨੂੰ ਸੁਣ ਰਹੇ ਹੋ ਅਤੇ ਤੁਸੀਂ ਆਪਣੇ ਹੀਰੋ ਨੂੰ ਹਿਲਾਉਣ ਲਈ ਇਹ ਵਿਸ਼ੇਸ਼ ਕੁੰਜੀਆਂ ਵਰਤਦੇ ਹੋ ਤਾਂ ਇਹ ਹੋਰਿਜ਼ਾਂਟਲ ਸਕ੍ਰੋਲਿੰਗ ਵੀ ਕਰੇਗਾ। ਇਸ ਕਾਰਨ, ਤੁਸੀਂ ਆਪਣੇ ਗੇਮ ਨੂੰ ਬਣਾਉਂਦੇ ਸਮੇਂ ਇਸ ਬਿਲਟ-ਇਨ ਬ੍ਰਾਊਜ਼ਰ ਵਿਵਹਾਰ ਨੂੰ *ਬੰਦ* ਕਰਨਾ ਚਾਹੁੰਦੇ ਹੋ। ਤੁਹਾਨੂੰ ਇਸ ਤਰ੍ਹਾਂ ਦਾ ਕੋਡ ਚਾਹੀਦਾ ਹੈ:

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

ਉਪਰੋਕਤ ਕੋਡ ਇਹ ਯਕੀਨੀ ਬਣਾਏਗਾ ਕਿ ਐਰੋ-ਕੀਜ਼ ਅਤੇ ਸਪੇਸ ਕੀ ਦੀ *ਡਿਫਾਲਟ* ਵਿਵਹਾਰ ਬੰਦ ਹੋ ਜਾਵੇ। *ਬੰਦ* ਮਕੈਨਿਜ਼ਮ ਤਦ ਹੁੰਦਾ ਹੈ ਜਦੋਂ ਅਸੀਂ `e.preventDefault()` ਨੂੰ ਕਾਲ ਕਰਦੇ ਹਾਂ।

## ਗੇਮ ਦੁਆਰਾ ਪ੍ਰੇਰਿਤ ਮੋਸ਼ਨ

ਅਸੀਂ ਚੀਜ਼ਾਂ ਨੂੰ ਆਪਣੇ ਆਪ ਹਿਲਾ ਸਕਦੇ ਹਾਂ ਜਦੋਂ ਅਸੀਂ `setTimeout()` ਜਾਂ `setInterval()` ਫੰਕਸ਼ਨ ਵਰਤਦੇ ਹਾਂ ਜੋ ਹਰ ਟਿਕ ਜਾਂ ਸਮੇਂ ਦੇ ਅੰਤਰਾਲ 'ਤੇ ਆਬਜੈਕਟ ਦੇ ਸਥਾਨ ਨੂੰ ਅਪਡੇਟ ਕਰਦੇ ਹਨ। ਇਹ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦੇ ਸਕਦਾ ਹੈ:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## ਗੇਮ ਲੂਪ

ਗੇਮ ਲੂਪ ਇੱਕ ਸੰਕਲਪ ਹੈ ਜੋ ਅਸਲ ਵਿੱਚ ਇੱਕ ਫੰਕਸ਼ਨ ਹੈ ਜੋ ਨਿਯਮਿਤ ਅੰਤਰਾਲ 'ਤੇ ਚਲਾਇਆ ਜਾਂਦਾ ਹੈ। ਇਸਨੂੰ ਗੇਮ ਲੂਪ ਕਿਹਾ ਜਾਂਦਾ ਹੈ ਕਿਉਂਕਿ ਜੋ ਕੁਝ ਵੀ ਉਪਭੋਗਤਾ ਨੂੰ ਦਿਖਾਈ ਦੇਣਾ ਚਾਹੀਦਾ ਹੈ ਉਹ ਲੂਪ ਵਿੱਚ ਡ੍ਰਾ ਕੀਤਾ ਜਾਂਦਾ ਹੈ। ਗੇਮ ਲੂਪ ਗੇਮ ਦੇ ਸਾਰੇ ਆਬਜੈਕਟਸ ਦੀ ਵਰਤੋਂ ਕਰਦਾ ਹੈ ਜੋ ਗੇਮ ਦਾ ਹਿੱਸਾ ਹਨ, ਸਾਰੇ ਨੂੰ ਡ੍ਰਾ ਕਰਦਾ ਹੈ ਜਦ ਤੱਕ ਕਿ ਕਿਸੇ ਕਾਰਨ ਕਰਕੇ ਉਹ ਹੁਣ ਗੇਮ ਦਾ ਹਿੱਸਾ ਨਹੀਂ ਰਹੇ। ਉਦਾਹਰਨ ਲਈ, ਜੇਕਰ ਕੋਈ ਆਬਜੈਕਟ ਇੱਕ ਦੁਸ਼ਮਨ ਹੈ ਜਿਸਨੂੰ ਲੇਜ਼ਰ ਨਾਲ ਮਾਰਿਆ ਗਿਆ ਅਤੇ ਉਹ ਫਟ ਜਾਂਦਾ ਹੈ, ਤਾਂ ਇਹ ਹੁਣ ਮੌਜੂਦਾ ਗੇਮ ਲੂਪ ਦਾ ਹਿੱਸਾ ਨਹੀਂ ਹੈ (ਤੁਸੀਂ ਇਸ ਬਾਰੇ ਹੋਰ ਅਗਲੇ ਪਾਠਾਂ ਵਿੱਚ ਸਿੱਖੋਗੇ)।

ਇਹ ਗੇਮ ਲੂਪ ਆਮ ਤੌਰ 'ਤੇ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦੇ ਸਕਦਾ ਹੈ, ਕੋਡ ਵਿੱਚ ਪ੍ਰਗਟ ਕੀਤਾ:

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

ਉਪਰੋਕਤ ਲੂਪ ਹਰ `200` ਮਿਲੀਸੈਕੰਡ ਵਿੱਚ ਕੈਨਵਾਸ ਨੂੰ ਦੁਬਾਰਾ ਡ੍ਰਾ ਕਰਨ ਲਈ ਚਲਾਇਆ ਜਾਂਦਾ ਹੈ। ਤੁਹਾਡੇ ਕੋਲ ਉਹ ਅੰਤਰਾਲ ਚੁਣਨ ਦੀ ਯੋਗਤਾ ਹੈ ਜੋ ਤੁਹਾਡੇ ਗੇਮ ਲਈ ਵਧੀਆ ਹੈ।

## ਸਪੇਸ ਗੇਮ ਜਾਰੀ ਰੱਖਣਾ

ਤੁਸੀਂ ਮੌਜੂਦਾ ਕੋਡ ਲੈ ਕੇ ਇਸਨੂੰ ਵਧਾਓਗੇ। ਜਾਂ ਤਾਂ ਉਸ ਕੋਡ ਨਾਲ ਸ਼ੁਰੂ ਕਰੋ ਜੋ ਤੁਸੀਂ ਭਾਗ I ਦੌਰਾਨ ਪੂਰਾ ਕੀਤਾ ਸੀ ਜਾਂ [ਭਾਗ II- ਸ਼ੁਰੂਆਤੀ](../../../../6-space-game/3-moving-elements-around/your-work) ਵਿੱਚ ਦਿੱਤੇ ਕੋਡ ਦੀ ਵਰਤੋਂ ਕਰੋ।

- **ਹੀਰੋ ਨੂੰ ਹਿਲਾਉਣਾ**: ਤੁਸੀਂ ਕੋਡ ਸ਼ਾਮਲ ਕਰੋਗੇ ਤਾਂ ਕਿ ਤੁਸੀਂ ਐਰੋ ਕੀਜ਼ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਹੀਰੋ ਨੂੰ ਹਿਲਾ ਸਕੋ।
- **ਦੁਸ਼ਮਨਾਂ ਨੂੰ ਹਿਲਾਉਣਾ**: ਤੁਸੀਂ ਇਹ ਵੀ ਕੋਡ ਸ਼ਾਮਲ ਕਰਨ ਦੀ ਲੋੜ ਹੋਵੇਗੀ ਤਾਂ ਕਿ ਦੁਸ਼ਮਨ ਇੱਕ ਨਿਰਧਾਰਤ ਦਰ 'ਤੇ ਉੱਪਰ ਤੋਂ ਹੇਠਾਂ ਹਿਲ ਸਕਣ।

## ਸਿਫਾਰਸ਼ੀ ਕਦਮ

`your-work` ਸਬ ਫੋਲਡਰ ਵਿੱਚ ਬਣਾਈ ਗਈ ਫਾਈਲਾਂ ਨੂੰ ਲੱਭੋ। ਇਸ ਵਿੱਚ ਹੇਠਾਂ ਦਿੱਤੇ ਹੋਣ ਚਾਹੀਦੇ ਹਨ:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

ਤੁਸੀਂ ਆਪਣਾ ਪ੍ਰੋਜੈਕਟ `your_work` ਫੋਲਡਰ ਵਿੱਚ ਸ਼ੁਰੂ ਕਰਦੇ ਹੋ ਇਸਨੂੰ ਟਾਈਪ ਕਰਕੇ:

```bash
cd your-work
npm start
```

ਉਪਰੋਕਤ HTTP ਸਰਵਰ ਪਤਾ `http://localhost:5000` 'ਤੇ ਸ਼ੁਰੂ ਕਰੇਗਾ। ਇੱਕ ਬ੍ਰਾਊਜ਼ਰ ਖੋਲ੍ਹੋ ਅਤੇ ਉਸ ਪਤੇ ਨੂੰ ਇਨਪੁਟ ਕਰੋ, ਇਸ ਸਮੇਂ ਇਹ ਹੀਰੋ ਅਤੇ ਸਾਰੇ ਦੁਸ਼ਮਨਾਂ ਨੂੰ ਰੈਂਡਰ ਕਰਨਾ ਚਾਹੀਦਾ ਹੈ; ਕੁਝ ਵੀ ਹਿਲ ਨਹੀਂ ਰਿਹਾ - ਅਜੇ ਤੱਕ!

### ਕੋਡ ਸ਼ਾਮਲ ਕਰੋ

1. **ਹੀਰੋ**, **ਦੁਸ਼ਮਨ**, ਅਤੇ **ਗੇਮ ਆਬਜੈਕਟ** ਲਈ ਸਮਰਪਿਤ ਆਬਜੈਕਟਸ ਸ਼ਾਮਲ ਕਰੋ, ਇਹਨਾਂ ਵਿੱਚ `x` ਅਤੇ `y` ਪ੍ਰਾਪਰਟੀਜ਼ ਹੋਣੀਆਂ ਚਾਹੀਦੀਆਂ ਹਨ। ([ਵਿਰਾਸਤ ਜਾਂ ਰਚਨਾ](../README.md) 'ਤੇ ਹਿੱਸੇ ਨੂੰ ਯਾਦ ਕਰੋ)। 

   *ਸੁਝਾਅ*: `ਗੇਮ ਆਬਜੈਕਟ` ਉਹ ਹੋਣਾ ਚਾਹੀਦਾ ਹੈ ਜਿਸ ਵਿੱਚ `x` ਅਤੇ `y` ਅਤੇ ਆਪਣੇ ਆਪ ਨੂੰ ਕੈਨਵਾਸ 'ਤੇ ਡ੍ਰਾ ਕਰਨ ਦੀ ਯੋਗਤਾ ਹੋਵੇ।

   >ਸੁਝਾਅ: ਇੱਕ ਨਵਾਂ GameObject ਕਲਾਸ ਸ਼ੁਰੂ ਕਰੋ ਜਿਸਦਾ ਕੰਸਟ੍ਰਕਟਰ ਹੇਠਾਂ ਦਿੱਤੇ ਤਰੀਕੇ ਨਾਲ ਬਣਾਇਆ ਗਿਆ ਹੈ, ਅਤੇ ਫਿਰ ਇਸਨੂੰ ਕੈਨਵਾਸ 'ਤੇ ਡ੍ਰਾ ਕਰੋ:
  
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

    ਹੁਣ, ਇਸ GameObject ਨੂੰ ਵਧਾਓ ਤਾਂ ਕਿ ਹੀਰੋ ਅਤੇ ਦੁਸ਼ਮਨ ਬਣ ਸਕਣ।
    
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

2. **ਕੀ-ਇਵੈਂਟ ਹੈਂਡਲਰਸ ਸ਼ਾਮਲ ਕਰੋ** ਤਾਂ ਕਿ ਕੀ ਨੈਵੀਗੇਸ਼ਨ (ਹੀਰੋ ਨੂੰ ਉੱਪਰ/ਹੇਠਾਂ, ਖੱਬੇ/ਸੱਜੇ ਹਿਲਾਉਣਾ) ਸੰਭਾਲਿਆ ਜਾ ਸਕੇ।

   *ਯਾਦ ਰੱਖੋ*: ਇਹ ਇੱਕ ਕਾਰਟੀਸੀਅਨ ਸਿਸਟਮ ਹੈ, ਟੌਪ-ਲੈਫਟ `0,0` ਹੈ। ਡਿਫਾਲਟ ਵਿਵਹਾਰ ਨੂੰ ਬੰਦ ਕਰਨ ਲਈ ਕੋਡ ਸ਼ਾਮਲ ਕਰਨਾ ਵੀ ਯਾਦ ਰੱਖੋ।

   >ਸੁਝਾਅ: ਆਪਣਾ onKeyDown ਫੰਕਸ਼ਨ ਬਣਾਓ ਅਤੇ ਇਸਨੂੰ ਵਿੰਡੋ ਨਾਲ ਜੁੜੋ:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   ਇਸ ਸਮੇਂ ਆਪਣੇ ਬ੍ਰਾਊਜ਼ਰ ਕਨਸੋਲ ਦੀ ਜਾਂਚ ਕਰੋ, ਅਤੇ ਦਬਾਈਆਂ ਕੁੰਜੀਆਂ ਨੂੰ ਲੌਗ ਹੋਣ ਦੇਖੋ। 

3. **[ਪਬ-ਸਬ ਪੈਟਰਨ](../README.md) ਨੂੰ ਲਾਗੂ ਕਰੋ**, ਇਹ ਤੁਹਾਡੇ ਕੋਡ ਨੂੰ ਸਾਫ਼ ਰੱਖੇਗਾ ਜਦੋਂ ਤੁਸੀਂ ਬਾਕੀ ਭਾਗਾਂ ਦੀ ਪਾਲਣਾ ਕਰਦੇ ਹੋ।

   ਇਸ ਆਖਰੀ ਭਾਗ ਨੂੰ ਕਰਨ ਲਈ, ਤੁਸੀਂ:

   1. **ਇਵੈਂਟ ਲਿਸਨਰ ਸ਼ਾਮਲ ਕਰੋ** ਵਿੰਡੋ 'ਤੇ:

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

    1. **ਇਵੈਂਟEmitter ਕਲਾਸ ਬਣਾਓ** ਤਾਂ ਕਿ ਸੁਨੇਹੇ ਪ੍ਰਕਾਸ਼ਿਤ ਅਤੇ ਸਬਸਕ੍ਰਾਈਬ ਕੀਤੇ ਜਾ ਸਕਣ:

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

    1. **ਕਾਂਸਟੈਂਟਸ ਸ਼ਾਮਲ ਕਰੋ** ਅਤੇ EventEmitter ਸੈਟ ਕਰੋ:

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

    1. **ਗੇਮ ਸ਼ੁਰੂ ਕਰੋ**

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

1. **ਗੇਮ ਲੂਪ ਸੈਟ ਕਰੋ**

   ਵਿੰਡੋ.onload ਫੰਕਸ਼ਨ ਨੂੰ ਰਿਫੈਕਟਰ ਕਰੋ ਤਾਂ ਕਿ ਗੇਮ ਸ਼ੁਰੂ ਕੀਤੀ ਜਾ ਸਕੇ ਅਤੇ ਇੱਕ ਵਧੀਆ ਅੰਤਰਾਲ 'ਤੇ ਗੇਮ ਲੂਪ ਸੈਟ ਕੀਤਾ ਜਾ ਸਕੇ। ਤੁਸੀਂ ਇੱਕ ਲੇਜ਼ਰ ਬੀਮ ਵੀ ਸ਼ਾਮਲ ਕਰੋਗੇ:

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

5. **ਕੋਡ ਸ਼ਾਮਲ ਕਰੋ** ਤਾਂ ਕਿ ਦੁਸ਼ਮਨ ਇੱਕ ਨਿਰਧਾਰਤ ਅੰਤਰਾਲ 'ਤੇ ਹਿਲ ਸਕਣ

    `createEnemies()` ਫੰਕਸ਼ਨ ਨੂੰ ਰਿਫੈਕਟਰ ਕਰੋ ਤਾਂ ਕਿ ਦੁਸ਼ਮਨ ਬਣਾਏ ਜਾ ਸਕਣ ਅਤੇ ਉਹਨਾਂ ਨੂੰ ਨਵੀਂ gameObjects ਕਲਾਸ ਵਿੱਚ ਧੱਕਿਆ ਜਾ ਸਕੇ:

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
    
    ਅਤੇ ਇੱਕ `createHero()` ਫੰਕਸ਼ਨ ਸ਼ਾਮਲ ਕਰੋ ਜੋ ਹੀਰੋ ਲਈ ਇੱਕ ਸਮਾਨ ਪ੍ਰਕਿਰਿਆ ਕਰੇ।

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

    ਅਤੇ ਆਖਿਰਕਾਰ, ਇੱਕ `drawGameObjects()` ਫੰਕਸ਼ਨ ਸ਼ਾਮਲ ਕਰੋ ਤਾਂ ਕਿ ਡ੍ਰਾਇੰਗ ਸ਼ੁਰੂ ਕੀਤੀ ਜਾ ਸਕੇ:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    ਤੁਹਾਡੇ ਦੁਸ਼ਮਨ ਤੁਹਾਡੇ ਹੀਰੋ ਸਪੇਸਸ਼ਿਪ 'ਤੇ ਅਗੇ ਵਧਣ ਸ਼ੁਰੂ ਕਰ ਦੇਣੇ ਚਾਹੀਦੇ ਹਨ!

---

## 🚀 ਚੁਣੌਤੀ

ਜਿਵੇਂ ਤੁਸੀਂ ਦੇਖ ਸਕਦੇ ਹੋ, ਜਦੋਂ ਤੁਸੀਂ ਫੰਕਸ਼ਨ, ਵੈਰੀਏਬਲ ਅਤੇ ਕਲਾਸਾਂ ਸ਼ਾਮਲ ਕਰਦੇ ਹੋ ਤਾਂ ਤੁਹਾਡਾ ਕੋਡ 'ਸਪੈਗੇਟੀ ਕੋਡ' ਵਿੱਚ ਬਦਲ ਸਕਦਾ ਹੈ। ਤੁਸੀਂ ਆਪਣੇ ਕੋਡ ਨੂੰ ਕਿਵੇਂ ਵਧੀਆ ਢੰਗ ਨਾਲ ਸੰਗਠਿਤ ਕਰ ਸਕਦੇ ਹੋ ਤਾਂ ਕਿ ਇਹ ਹੋਰ ਪੜ੍ਹਨਯੋਗ ਹੋਵੇ? ਇੱਕ ਸਿਸਟਮ ਦਾ ਖਾਕਾ ਬਣਾਓ ਤਾਂ ਕਿ ਤੁਹਾਡਾ ਕੋਡ ਸੰਗਠਿਤ ਹੋ ਸਕੇ, ਭਾਵੇਂ ਇਹ ਅਜੇ ਵੀ ਇੱਕ ਫਾਈਲ ਵਿੱਚ ਹੋਵੇ।

## ਪੋਸਟ-ਵਿਆਖਿਆ ਪ੍ਰਸ਼ਨਾਵਲੀ

[ਪੋਸਟ-ਵਿਆਖਿਆ ਪ੍ਰਸ਼ਨਾਵਲੀ](https://ff-quizzes.netlify.app/web/quiz/34)

## ਸਮੀਖਿਆ ਅਤੇ ਸਵੈ ਅਧਿਐਨ

ਜਦੋਂ ਕਿ ਅਸੀਂ ਆਪਣੇ ਗੇਮ ਨੂੰ ਫਰੇਮਵਰਕਸ ਦੀ ਵਰਤੋਂ ਕੀਤੇ ਬਿਨਾਂ ਲਿਖ ਰਹੇ ਹਾਂ, ਕੈਨਵਾਸ ਫਰੇਮਵਰਕਸ ਦੇ ਆਧਾਰ 'ਤੇ ਬਹੁਤ ਸਾਰੇ ਜਾਵਾਸਕ੍ਰਿਪਟ ਹਨ ਜੋ ਗੇਮ ਡਿਵੈਲਪਮੈਂਟ ਲਈ ਹਨ। [ਇਨ੍ਹਾਂ ਬਾਰੇ ਪੜ੍ਹਨ](https://github.com/collections/javascript-game-engines) ਲਈ ਕੁਝ ਸਮਾਂ ਲਓ।

## ਅਸਾਈਨਮੈਂਟ

[ਆਪਣੇ ਕੋਡ 'ਤੇ ਟਿੱਪਣੀ ਕਰੋ](assignment.md)

---

**ਅਸਵੀਕਾਰਨਾ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀਤਾ ਲਈ ਯਤਨਸ਼ੀਲ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਣੀਕਤਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼, ਜੋ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਹੈ, ਨੂੰ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤ ਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।