<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "adda95e02afa3fbee67b6e385b1109e1",
  "translation_date": "2025-08-29T08:34:16+00:00",
  "source_file": "6-space-game/5-keeping-score/README.md",
  "language_code": "no"
}
-->
# Bygg et Romspill Del 5: Poeng og Liv

## Quiz før forelesning

[Quiz før forelesning](https://ff-quizzes.netlify.app/web/quiz/37)

I denne leksjonen skal du lære hvordan du legger til poeng i et spill og beregner liv.

## Tegn tekst på skjermen

For å kunne vise poengsummen i spillet på skjermen, må du vite hvordan du plasserer tekst på skjermen. Svaret er å bruke metoden `fillText()` på canvas-objektet. Du kan også kontrollere andre aspekter som hvilken font som skal brukes, fargen på teksten og til og med justeringen (venstre, høyre, senter). Nedenfor er litt kode som tegner tekst på skjermen.

```javascript
ctx.font = "30px Arial";
ctx.fillStyle = "red";
ctx.textAlign = "right";
ctx.fillText("show this on the screen", 0, 0);
```

✅ Les mer om [hvordan legge til tekst på et canvas](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_text), og føl deg fri til å gjøre din versjon mer fancy!

## Liv som et spillkonsept

Konseptet med å ha liv i et spill er bare et tall. I konteksten av et romspill er det vanlig å tildele et sett med liv som reduseres ett etter ett når skipet ditt tar skade. Det er fint om du kan vise en grafisk representasjon av dette, som små skip eller hjerter, i stedet for bare et tall.

## Hva skal bygges

La oss legge til følgende i spillet ditt:

- **Poengsum i spillet**: For hvert fiendeskip som blir ødelagt, skal helten få poeng. Vi foreslår 100 poeng per skip. Poengsummen skal vises nederst til venstre.
- **Liv**: Skipet ditt har tre liv. Du mister ett liv hver gang et fiendeskip kolliderer med deg. Antall liv skal vises nederst til høyre og være laget av følgende grafikk ![livsbilde](../../../../translated_images/life.6fb9f50d53ee0413cd91aa411f7c296e10a1a6de5c4a4197c718b49bf7d63ebf.no.png).

## Anbefalte steg

Finn filene som er opprettet for deg i undermappen `your-work`. Den skal inneholde følgende:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
-| index.html
-| app.js
-| package.json
```

Start prosjektet ditt i `your_work`-mappen ved å skrive:

```bash
cd your-work
npm start
```

Dette vil starte en HTTP-server på adressen `http://localhost:5000`. Åpne en nettleser og skriv inn den adressen. Akkurat nå skal den vise helten og alle fiendene, og når du trykker på venstre- og høyrepilene, beveger helten seg og kan skyte ned fiender.

### Legg til kode

1. **Kopier over nødvendige ressurser** fra mappen `solution/assets/` til `your-work`-mappen; du skal legge til ressursen `life.png`. Legg til `lifeImg` i `window.onload`-funksjonen:

    ```javascript
    lifeImg = await loadTexture("assets/life.png");
    ```

1. Legg til `lifeImg` i listen over ressurser:

    ```javascript
    let heroImg,
    ...
    lifeImg,
    ...
    eventEmitter = new EventEmitter();
    ```
  
2. **Legg til variabler**. Legg til kode som representerer din totale poengsum (0) og antall gjenværende liv (3), og vis disse på skjermen.

3. **Utvid funksjonen `updateGameObjects()`**. Utvid funksjonen `updateGameObjects()` for å håndtere kollisjoner med fiender:

    ```javascript
    enemies.forEach(enemy => {
        const heroRect = hero.rectFromGameObject();
        if (intersectRect(heroRect, enemy.rectFromGameObject())) {
          eventEmitter.emit(Messages.COLLISION_ENEMY_HERO, { enemy });
        }
      })
    ```

4. **Legg til `liv` og `poeng`**. 
   1. **Initialiser variabler**. Under `this.cooldown = 0` i klassen `Hero`, sett liv og poeng:

        ```javascript
        this.life = 3;
        this.points = 0;
        ```

   1. **Tegn variabler på skjermen**. Tegn disse verdiene på skjermen:

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

   1. **Legg til metoder i spill-løkken**. Sørg for å legge til disse funksjonene i `window.onload`-funksjonen under `updateGameObjects()`:

        ```javascript
        drawPoints();
        drawLife();
        ```

1. **Implementer spillregler**. Implementer følgende spillregler:

   1. **For hver kollisjon mellom helten og en fiende**, trekk fra ett liv.
   
      Utvid klassen `Hero` for å gjøre dette fratrekket:

        ```javascript
        decrementLife() {
          this.life--;
          if (this.life === 0) {
            this.dead = true;
          }
        }
        ```

   2. **For hver laser som treffer en fiende**, øk poengsummen med 100 poeng.

      Utvid klassen `Hero` for å gjøre denne økningen:
    
        ```javascript
          incrementPoints() {
            this.points += 100;
          }
        ```

        Legg til disse funksjonene i dine Collision Event Emitters:

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

✅ Gjør litt research for å oppdage andre spill som er laget med JavaScript/Canvas. Hva er deres fellestrekk?

Når du er ferdig med dette arbeidet, skal du se små "liv"-skip nederst til høyre, poeng nederst til venstre, og du skal se at antall liv reduseres når du kolliderer med fiender, og poengene øker når du skyter fiender. Bra jobbet! Spillet ditt er nesten ferdig.

---

## 🚀 Utfordring

Koden din er nesten ferdig. Kan du se for deg neste steg?

## Quiz etter forelesning

[Quiz etter forelesning](https://ff-quizzes.netlify.app/web/quiz/38)

## Gjennomgang og selvstudium

Undersøk noen måter du kan øke og redusere poeng og liv i spill. Det finnes noen interessante spillmotorer som [PlayFab](https://playfab.com). Hvordan kunne bruk av en slik motor forbedret spillet ditt?

## Oppgave

[Bygg et poengspill](assignment.md)

---

**Ansvarsfraskrivelse**:  
Dette dokumentet er oversatt ved hjelp av AI-oversettelsestjenesten [Co-op Translator](https://github.com/Azure/co-op-translator). Selv om vi tilstreber nøyaktighet, vær oppmerksom på at automatiske oversettelser kan inneholde feil eller unøyaktigheter. Det originale dokumentet på sitt opprinnelige språk bør anses som den autoritative kilden. For kritisk informasjon anbefales profesjonell menneskelig oversettelse. Vi er ikke ansvarlige for eventuelle misforståelser eller feiltolkninger som oppstår ved bruk av denne oversettelsen.