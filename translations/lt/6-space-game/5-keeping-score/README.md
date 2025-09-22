<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "adda95e02afa3fbee67b6e385b1109e1",
  "translation_date": "2025-08-29T16:51:02+00:00",
  "source_file": "6-space-game/5-keeping-score/README.md",
  "language_code": "lt"
}
-->
# Sukurkite kosminį žaidimą 5 dalis: Taškai ir gyvybės

## Klausimai prieš paskaitą

[Klausimai prieš paskaitą](https://ff-quizzes.netlify.app/web/quiz/37)

Šioje pamokoje sužinosite, kaip pridėti taškų skaičiavimą žaidime ir apskaičiuoti gyvybes.

## Teksto rodymas ekrane

Norėdami ekrane rodyti žaidimo taškus, turite žinoti, kaip pateikti tekstą ekrane. Atsakymas yra naudojant `fillText()` metodą ant drobės objekto. Taip pat galite valdyti kitus aspektus, pvz., kokį šriftą naudoti, teksto spalvą ir net jo lygiavimą (kairė, dešinė, centras). Žemiau pateiktas kodas, kuris piešia tekstą ekrane.

```javascript
ctx.font = "30px Arial";
ctx.fillStyle = "red";
ctx.textAlign = "right";
ctx.fillText("show this on the screen", 0, 0);
```

✅ Skaitykite daugiau apie [kaip pridėti tekstą prie drobės](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_text), ir drąsiai padarykite savo tekstą įdomesnį!

## Gyvybės kaip žaidimo koncepcija

Gyvybės koncepcija žaidime yra tik skaičius. Kosminio žaidimo kontekste įprasta priskirti tam tikrą gyvybių skaičių, kuris mažėja po vieną, kai jūsų laivas patiria žalą. Gražu, jei galite parodyti grafinę šio skaičiaus reprezentaciją, pvz., mažus laivelius ar širdeles, o ne tik skaičių.

## Ką sukurti

Pridėkime šiuos elementus į jūsų žaidimą:

- **Žaidimo taškai**: Už kiekvieną sunaikintą priešo laivą herojus turėtų gauti taškų, siūlome 100 taškų už laivą. Žaidimo taškai turėtų būti rodomi apatiniame kairiajame kampe.
- **Gyvybės**: Jūsų laivas turi tris gyvybes. Kiekvieną kartą, kai priešo laivas susiduria su jūsų laivu, prarandate vieną gyvybę. Gyvybių skaičius turėtų būti rodomas apatiniame dešiniajame kampe ir būti sudarytas iš šio grafinio elemento ![gyvybės vaizdas](../../../../translated_images/life.6fb9f50d53ee0413cd91aa411f7c296e10a1a6de5c4a4197c718b49bf7d63ebf.lt.png).

## Rekomenduojami žingsniai

Raskite failus, kurie buvo sukurti jums aplanke `your-work`. Jame turėtų būti šie elementai:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
-| index.html
-| app.js
-| package.json
```

Pradėkite savo projektą aplanke `your_work` įvesdami:

```bash
cd your-work
npm start
```

Aukščiau pateiktas kodas paleis HTTP serverį adresu `http://localhost:5000`. Atidarykite naršyklę ir įveskite šį adresą. Šiuo metu turėtumėte matyti herojų ir visus priešus, o paspaudę kairės ir dešinės rodykles, herojus judės ir galės šaudyti į priešus.

### Pridėkite kodą

1. **Nukopijuokite reikalingus elementus** iš aplanko `solution/assets/` į aplanką `your-work`; pridėsite `life.png` elementą. Pridėkite `lifeImg` į `window.onload` funkciją:

    ```javascript
    lifeImg = await loadTexture("assets/life.png");
    ```

1. Pridėkite `lifeImg` į elementų sąrašą:

    ```javascript
    let heroImg,
    ...
    lifeImg,
    ...
    eventEmitter = new EventEmitter();
    ```
  
2. **Pridėkite kintamuosius**. Pridėkite kodą, kuris atspindi jūsų bendrą taškų skaičių (0) ir likusias gyvybes (3), rodykite šiuos skaičius ekrane.

3. **Išplėskite `updateGameObjects()` funkciją**. Išplėskite `updateGameObjects()` funkciją, kad ji apdorotų priešų susidūrimus:

    ```javascript
    enemies.forEach(enemy => {
        const heroRect = hero.rectFromGameObject();
        if (intersectRect(heroRect, enemy.rectFromGameObject())) {
          eventEmitter.emit(Messages.COLLISION_ENEMY_HERO, { enemy });
        }
      })
    ```

4. **Pridėkite gyvybes ir taškus**. 
   1. **Inicializuokite kintamuosius**. Po `this.cooldown = 0` klasėje `Hero`, nustatykite gyvybes ir taškus:

        ```javascript
        this.life = 3;
        this.points = 0;
        ```

   1. **Pieškite kintamuosius ekrane**. Rodykite šias reikšmes ekrane:

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

   1. **Pridėkite metodus į žaidimo ciklą**. Įsitikinkite, kad pridėjote šias funkcijas į `window.onload` funkciją po `updateGameObjects()`:

        ```javascript
        drawPoints();
        drawLife();
        ```

1. **Įgyvendinkite žaidimo taisykles**. Įgyvendinkite šias žaidimo taisykles:

   1. **Už kiekvieną herojaus ir priešo susidūrimą** atimkite gyvybę.
   
      Išplėskite `Hero` klasę, kad atliktumėte šį atėmimą:

        ```javascript
        decrementLife() {
          this.life--;
          if (this.life === 0) {
            this.dead = true;
          }
        }
        ```

   2. **Už kiekvieną lazerį, kuris pataiko į priešą**, padidinkite žaidimo taškus 100 taškų.

      Išplėskite `Hero` klasę, kad atliktumėte šį padidinimą:
    
        ```javascript
          incrementPoints() {
            this.points += 100;
          }
        ```

        Pridėkite šias funkcijas į susidūrimo įvykių emitentus:

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

✅ Šiek tiek pasidomėkite, kokie kiti žaidimai yra sukurti naudojant JavaScript/Canvas. Kokie jų bendri bruožai?

Baigę šį darbą, turėtumėte matyti mažus „gyvybės“ laivelius apatiniame dešiniajame kampe, taškus apatiniame kairiajame kampe, ir turėtumėte matyti, kaip jūsų gyvybių skaičius mažėja susidūrus su priešais, o taškai didėja šaudant į priešus. Puiku! Jūsų žaidimas beveik baigtas.

---

## 🚀 Iššūkis

Jūsų kodas beveik baigtas. Ar galite įsivaizduoti kitus žingsnius?

## Klausimai po paskaitos

[Klausimai po paskaitos](https://ff-quizzes.netlify.app/web/quiz/38)

## Apžvalga ir savarankiškas mokymasis

Pasidomėkite būdais, kaip galite padidinti ir sumažinti žaidimo taškus bei gyvybes. Yra įdomių žaidimų variklių, tokių kaip [PlayFab](https://playfab.com). Kaip vieno iš jų naudojimas galėtų pagerinti jūsų žaidimą?

## Užduotis

[Sukurkite žaidimą su taškų skaičiavimu](assignment.md)

---

**Atsakomybės apribojimas**:  
Šis dokumentas buvo išverstas naudojant AI vertimo paslaugą [Co-op Translator](https://github.com/Azure/co-op-translator). Nors siekiame tikslumo, prašome atkreipti dėmesį, kad automatiniai vertimai gali turėti klaidų ar netikslumų. Originalus dokumentas jo gimtąja kalba turėtų būti laikomas autoritetingu šaltiniu. Kritinei informacijai rekomenduojama profesionali žmogaus vertimo paslauga. Mes neprisiimame atsakomybės už nesusipratimus ar klaidingus interpretavimus, atsiradusius naudojant šį vertimą.