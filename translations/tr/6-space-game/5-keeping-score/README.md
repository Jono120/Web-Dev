<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "adda95e02afa3fbee67b6e385b1109e1",
  "translation_date": "2025-08-29T00:24:17+00:00",
  "source_file": "6-space-game/5-keeping-score/README.md",
  "language_code": "tr"
}
-->
# Uzay Oyunu Yapımı Bölüm 5: Puanlama ve Canlar

## Ders Öncesi Test

[Ders öncesi testi](https://ff-quizzes.netlify.app/web/quiz/37)

Bu derste, bir oyuna nasıl puanlama ekleyeceğinizi ve canları nasıl hesaplayacağınızı öğreneceksiniz.

## Ekrana Metin Çizme

Ekranda bir oyun puanını gösterebilmek için, metni ekrana nasıl yerleştireceğinizi bilmeniz gerekir. Bunun cevabı, canvas nesnesi üzerinde `fillText()` yöntemini kullanmaktır. Ayrıca hangi yazı tipini kullanacağınızı, metnin rengini ve hizalamasını (sol, sağ, merkez) kontrol edebilirsiniz. Aşağıda ekrana metin çizen bir kod örneği bulunmaktadır.

```javascript
ctx.font = "30px Arial";
ctx.fillStyle = "red";
ctx.textAlign = "right";
ctx.fillText("show this on the screen", 0, 0);
```

✅ [Canvas'a nasıl metin eklenir](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_text) hakkında daha fazla bilgi edinin ve kendi tasarımınızı daha şık hale getirmekten çekinmeyin!

## Oyun Kavramı Olarak Can

Bir oyunda can sahibi olma kavramı sadece bir sayıdır. Uzay oyunu bağlamında, geminiz hasar aldığında birer birer eksilen belirli bir can sayısı atamak yaygındır. Bu sayıyı bir sayı yerine minyatür gemiler veya kalpler gibi grafiksel bir temsil ile göstermek güzel olur.

## Ne Yapacağız?

Oyununuza aşağıdakileri ekleyelim:

- **Oyun puanı**: Yok edilen her düşman gemisi için kahramana puan verilmelidir. Gemi başına 100 puan öneriyoruz. Oyun puanı ekranın sol alt köşesinde gösterilmelidir.
- **Can**: Geminizin üç canı vardır. Her düşman gemisiyle çarpıştığınızda bir can kaybedersiniz. Can puanı ekranın sağ alt köşesinde gösterilmeli ve aşağıdaki grafikle oluşturulmalıdır: ![can görseli](../../../../translated_images/life.6fb9f50d53ee0413cd91aa411f7c296e10a1a6de5c4a4197c718b49bf7d63ebf.tr.png).

## Önerilen Adımlar

`your-work` alt klasöründe sizin için oluşturulmuş dosyaları bulun. Şu dosyaları içermelidir:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
-| index.html
-| app.js
-| package.json
```

Projenizi `your_work` klasöründe başlatmak için şu komutu yazın:

```bash
cd your-work
npm start
```

Yukarıdaki komut, `http://localhost:5000` adresinde bir HTTP Sunucusu başlatacaktır. Bir tarayıcı açın ve bu adresi girin. Şu anda kahramanı ve tüm düşmanları görmelisiniz ve sol ve sağ ok tuşlarına bastığınızda kahraman hareket eder ve düşmanları vurabilir.

### Kod Ekleme

1. **Gerekli varlıkları kopyalayın**. `solution/assets/` klasöründen `your-work` klasörüne gerekli varlıkları kopyalayın; bir `life.png` varlığı ekleyeceksiniz. `lifeImg`'i window.onload fonksiyonuna ekleyin:

    ```javascript
    lifeImg = await loadTexture("assets/life.png");
    ```

1. `lifeImg`'i varlıklar listesine ekleyin:

    ```javascript
    let heroImg,
    ...
    lifeImg,
    ...
    eventEmitter = new EventEmitter();
    ```
  
2. **Değişkenler ekleyin**. Toplam puanınızı (0) ve kalan canlarınızı (3) temsil eden kod ekleyin, bu puanları ekranda gösterin.

3. **`updateGameObjects()` fonksiyonunu genişletin**. Düşman çarpışmalarını işlemek için `updateGameObjects()` fonksiyonunu genişletin:

    ```javascript
    enemies.forEach(enemy => {
        const heroRect = hero.rectFromGameObject();
        if (intersectRect(heroRect, enemy.rectFromGameObject())) {
          eventEmitter.emit(Messages.COLLISION_ENEMY_HERO, { enemy });
        }
      })
    ```

4. **Can ve puan ekleyin**. 
   1. **Değişkenleri başlatın**. `Hero` sınıfında `this.cooldown = 0` altına can ve puan değişkenlerini ekleyin:

        ```javascript
        this.life = 3;
        this.points = 0;
        ```

   1. **Değişkenleri ekrana çizin**. Bu değerleri ekrana çizin:

        ```javascript
        function drawLife() {
          // TODO, 35, 27
          const START_POS = canvas.width - 180;
          for(let i=0; i < hero.life; i++ ) {
            ctx.drawImage(
              lifeImg, 
              START_POS + (45 * (i+1) ), 
              canvas.height - 37);
          }
        }
        
        function drawPoints() {
          ctx.font = "30px Arial";
          ctx.fillStyle = "red";
          ctx.textAlign = "left";
          drawText("Points: " + hero.points, 10, canvas.height-20);
        }
        
        function drawText(message, x, y) {
          ctx.fillText(message, x, y);
        }

        ```

   1. **Oyun döngüsüne yöntemler ekleyin**. Bu fonksiyonları `updateGameObjects()` altında window.onload fonksiyonuna eklediğinizden emin olun:

        ```javascript
        drawPoints();
        drawLife();
        ```

1. **Oyun kurallarını uygulayın**. Şu oyun kurallarını uygulayın:

   1. **Her kahraman ve düşman çarpışması için**, bir can eksiltin.
   
      `Hero` sınıfını bu eksiltmeyi yapmak için genişletin:

        ```javascript
        decrementLife() {
          this.life--;
          if (this.life === 0) {
            this.dead = true;
          }
        }
        ```

   2. **Her lazer bir düşmana çarptığında**, oyun puanını 100 puan artırın.

      Kahraman sınıfını bu artırımı yapmak için genişletin:
    
        ```javascript
          incrementPoints() {
            this.points += 100;
          }
        ```

        Bu fonksiyonları Çarpışma Olayı Yayıcılarına ekleyin:

        ```javascript
        eventEmitter.on(Messages.COLLISION_ENEMY_LASER, (_, { first, second }) => {
           first.dead = true;
           second.dead = true;
           hero.incrementPoints();
        })

        eventEmitter.on(Messages.COLLISION_ENEMY_HERO, (_, { enemy }) => {
           enemy.dead = true;
           hero.decrementLife();
        });
        ```

✅ JavaScript/Canvas kullanılarak oluşturulan diğer oyunları keşfetmek için biraz araştırma yapın. Ortak özellikleri nelerdir?

Bu çalışmanın sonunda, sağ alt köşede küçük 'can' gemilerini, sol alt köşede puanları görebilmelisiniz ve düşmanlarla çarpıştıkça can sayınız azalmalı, düşmanları vurdukça puanlarınız artmalıdır. Harika iş çıkardınız! Oyununuz neredeyse tamamlandı.

---

## 🚀 Zorluk

Kodunuz neredeyse tamamlandı. Bir sonraki adımlarınızı hayal edebiliyor musunuz?

## Ders Sonrası Test

[Ders sonrası testi](https://ff-quizzes.netlify.app/web/quiz/38)

## Gözden Geçirme ve Kendi Kendine Çalışma

Oyun puanlarını ve canları artırmanın ve azaltmanın yollarını araştırın. [PlayFab](https://playfab.com) gibi ilginç oyun motorları vardır. Bunlardan birini kullanmak oyununuzu nasıl geliştirebilir?

## Ödev

[Puanlama Oyunu Yapın](assignment.md)

---

**Feragatname**:  
Bu belge, AI çeviri hizmeti [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluk için çaba göstersek de, otomatik çevirilerin hata veya yanlışlık içerebileceğini lütfen unutmayın. Belgenin orijinal dili, yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımından kaynaklanan yanlış anlamalar veya yanlış yorumlamalardan sorumlu değiliz.