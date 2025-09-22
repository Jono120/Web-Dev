<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a9a161871de7706cb0e23b1bd0c74559",
  "translation_date": "2025-08-29T00:23:51+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "tr"
}
-->
# Uzay Oyunu Bölüm 3: Hareket Eklemek

## Ders Öncesi Test

[Ders öncesi test](https://ff-quizzes.netlify.app/web/quiz/33)

Oyunlar, ekranda uzaylılar dolaşmadıkça pek eğlenceli olmaz! Bu oyunda iki tür hareket kullanacağız:

- **Klavye/Fare hareketi**: Kullanıcı, klavye veya fare ile ekrandaki bir nesneyi hareket ettirdiğinde.
- **Oyun kaynaklı hareket**: Oyun, belirli bir zaman aralığında bir nesneyi hareket ettirdiğinde.

Peki, ekrandaki nesneleri nasıl hareket ettiririz? Her şey kartezyen koordinatlarla ilgilidir: nesnenin konumunu (x, y) değiştiririz ve ardından ekranı yeniden çizeriz.

Ekranda *hareket* gerçekleştirmek için genellikle şu adımlara ihtiyacınız olur:

1. **Yeni bir konum belirleyin**: Nesnenin hareket ettiğini algılamak için bu gereklidir.
2. **Ekranı temizleyin**: Çizimler arasında ekranın temizlenmesi gerekir. Bunu, arka plan rengiyle doldurduğumuz bir dikdörtgen çizerek yapabiliriz.
3. **Nesneyi yeni konumda yeniden çizin**: Bunu yaparak, nesneyi bir konumdan diğerine taşımayı başarırız.

Kodda bunun nasıl görünebileceği aşağıda verilmiştir:

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

✅ Kahramanınızı saniyede birçok kez yeniden çizmenin performans maliyetlerini artırabileceği bir neden düşünebilir misiniz? [Bu desene alternatifler](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas) hakkında okuyun.

## Klavye olaylarını yönetmek

Olayları yönetmek için belirli olayları koda bağlamanız gerekir. Klavye olayları tüm pencere üzerinde tetiklenirken, fare olayları (örneğin `click`) belirli bir öğeye tıklamaya bağlanabilir. Bu projede klavye olaylarını kullanacağız.

Bir olayı yönetmek için pencerenin `addEventListener()` metodunu kullanmanız ve ona iki giriş parametresi sağlamanız gerekir. İlk parametre olayın adıdır, örneğin `keyup`. İkinci parametre ise olay gerçekleştiğinde çağrılması gereken fonksiyondur.

Bir örnek:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

Klavye olayları için, hangi tuşa basıldığını görmek için olay üzerinde kullanabileceğiniz iki özellik vardır:

- `key`: Basılan tuşun string temsili, örneğin `ArrowUp`.
- `keyCode`: Sayısal temsili, örneğin `37`, bu `ArrowLeft` ile eşleşir.

✅ Klavye olaylarını manipüle etmek oyun geliştirme dışında da faydalıdır. Bu tekniğin başka hangi kullanım alanlarını düşünebilirsiniz?

### Özel tuşlar: bir uyarı

Bazı *özel* tuşlar pencereyi etkiler. Bu, bir `keyup` olayını dinliyorsanız ve kahramanınızı hareket ettirmek için bu özel tuşları kullanıyorsanız, aynı zamanda yatay kaydırma işlemi de gerçekleştireceği anlamına gelir. Bu nedenle, oyununuzu geliştirirken bu yerleşik tarayıcı davranışını *kapatmak* isteyebilirsiniz. Bunun için şu tür bir koda ihtiyacınız var:

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

Yukarıdaki kod, ok tuşlarının ve boşluk tuşunun *varsayılan* davranışını kapatacaktır. *Kapatma* mekanizması, `e.preventDefault()` çağrıldığında gerçekleşir.

## Oyun kaynaklı hareket

Nesneleri kendiliğinden hareket ettirebiliriz, bunu `setTimeout()` veya `setInterval()` gibi zamanlayıcılar kullanarak yaparız. Bu fonksiyonlar, her zaman aralığında nesnenin konumunu günceller. Bunun kodda nasıl görünebileceği aşağıda verilmiştir:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## Oyun döngüsü

Oyun döngüsü, düzenli aralıklarla çağrılan bir fonksiyon kavramıdır. Oyun döngüsü, kullanıcıya görünmesi gereken her şeyi döngüye çizer. Oyun döngüsü, oyunun bir parçası olan tüm oyun nesnelerini kullanır ve bir şekilde artık oyunun bir parçası olmaması gereken nesneleri çizmez. Örneğin, bir nesne bir düşmansa ve bir lazer tarafından vurulup patlıyorsa, artık mevcut oyun döngüsünün bir parçası değildir (bunun hakkında daha fazla bilgiyi sonraki derslerde öğreneceksiniz).

Bir oyun döngüsünün kodda tipik olarak nasıl görünebileceği aşağıda verilmiştir:

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

Yukarıdaki döngü, her `200` milisaniyede bir tuvali yeniden çizer. Oyununuz için en uygun aralığı seçme özgürlüğüne sahipsiniz.

## Uzay Oyununa Devam Etmek

Mevcut kodu alıp genişleteceksiniz. Ya Bölüm I sırasında tamamladığınız kodla başlayın ya da [Bölüm II - başlangıç](../../../../6-space-game/3-moving-elements-around/your-work) kodunu kullanın.

- **Kahramanı hareket ettirme**: Ok tuşlarını kullanarak kahramanı hareket ettirebilmeniz için kod ekleyeceksiniz.
- **Düşmanları hareket ettirme**: Düşmanların belirli bir hızda yukarıdan aşağıya hareket etmesini sağlamak için kod eklemeniz gerekecek.

## Önerilen adımlar

`your-work` alt klasöründe sizin için oluşturulmuş dosyaları bulun. Şunları içermelidir:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

Projenizi `your_work` klasöründe başlatmak için şu komutu yazın:

```bash
cd your-work
npm start
```

Yukarıdaki komut, `http://localhost:5000` adresinde bir HTTP Sunucusu başlatacaktır. Bir tarayıcı açın ve bu adresi girin, şu anda kahramanı ve tüm düşmanları göstermesi gerekir; henüz hiçbir şey hareket etmiyor!

### Kod ekleme

1. **Kahraman**, **düşman** ve **oyun nesnesi** için özel nesneler ekleyin, bunlar `x` ve `y` özelliklerine sahip olmalıdır. ([Kalıtım veya bileşim](../README.md) bölümünü hatırlayın).

   *İPUCU*: `oyun nesnesi`, `x` ve `y` özelliklerine ve kendini bir tuvale çizebilme yeteneğine sahip olan nesne olmalıdır.

   >ipucu: aşağıda belirtilen şekilde bir yapıcıya sahip yeni bir GameObject sınıfı ekleyerek başlayın ve ardından bunu tuvale çizin:
  
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

    Şimdi bu GameObject'i genişleterek Kahraman ve Düşman oluşturun.
    
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

2. **Tuş olay işleyicileri ekleyin**: Kahramanı yukarı/aşağı, sola/sağa hareket ettirmek için tuş navigasyonunu yönetin.

   *UNUTMAYIN*: Bu bir kartezyen sistemdir, sol üst köşe `0,0`'dır. Ayrıca *varsayılan davranışı* durdurmak için kod eklemeyi unutmayın.

   >ipucu: onKeyDown fonksiyonunuzu oluşturun ve pencereye bağlayın:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   Bu noktada tarayıcı konsolunuzu kontrol edin ve tuş vuruşlarının kaydedildiğini izleyin.

3. **[Pub sub desenini](../README.md) uygulayın**, bu kodunuzu temiz tutmanıza yardımcı olacaktır.

   Bunu yapmak için:

   1. **Pencereye bir olay dinleyici ekleyin**:

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

    1. **Mesajları yayınlamak ve abone olmak için bir EventEmitter sınıfı oluşturun**:

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

    1. **Sabitler ekleyin** ve EventEmitter'ı ayarlayın:

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

    1. **Oyunu başlatın**

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

1. **Oyun döngüsünü ayarlayın**

   window.onload fonksiyonunu yeniden düzenleyerek oyunu başlatın ve uygun bir aralıkta bir oyun döngüsü ayarlayın. Ayrıca bir lazer ışını ekleyeceksiniz:

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

5. **Düşmanları belirli bir aralıkta hareket ettirmek için kod ekleyin**

    `createEnemies()` fonksiyonunu yeniden düzenleyerek düşmanları oluşturun ve bunları yeni gameObjects sınıfına ekleyin:

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
    
    ve kahraman için benzer bir işlem yapmak üzere bir `createHero()` fonksiyonu ekleyin.
    
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

    ve son olarak, çizimi başlatmak için bir `drawGameObjects()` fonksiyonu ekleyin:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    Düşmanlarınız kahraman uzay geminize doğru ilerlemeye başlamalı!

---

## 🚀 Meydan Okuma

Gördüğünüz gibi, fonksiyonlar, değişkenler ve sınıflar eklemeye başladığınızda kodunuz 'spagetti koduna' dönüşebilir. Kodunuzu daha okunabilir hale getirmek için nasıl daha iyi organize edebilirsiniz? Kodunuzu organize etmek için bir sistem tasarlayın, hatta hala tek bir dosyada olsa bile.

## Ders Sonrası Test

[Ders sonrası test](https://ff-quizzes.netlify.app/web/quiz/34)

## Gözden Geçirme ve Kendi Kendine Çalışma

Oyunlarımızı framework kullanmadan yazıyor olsak da, oyun geliştirme için birçok JavaScript tabanlı tuval framework'ü bulunmaktadır. [Bunlar hakkında okumak](https://github.com/collections/javascript-game-engines) için biraz zaman ayırın.

## Ödev

[Kodunuzu yorumlayın](assignment.md)

---

**Feragatname**:  
Bu belge, AI çeviri hizmeti [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluk için çaba göstersek de, otomatik çevirilerin hata veya yanlışlık içerebileceğini lütfen unutmayın. Belgenin orijinal dili, yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımından kaynaklanan yanlış anlamalar veya yanlış yorumlamalar için sorumluluk kabul etmiyoruz.