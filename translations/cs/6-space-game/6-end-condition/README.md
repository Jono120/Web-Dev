<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-29T10:52:21+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "cs"
}
-->
# Vytvořte vesmírnou hru, část 6: Konec a restart

## Kvíz před přednáškou

[Kvíz před přednáškou](https://ff-quizzes.netlify.app/web/quiz/39)

Existuje několik způsobů, jak vyjádřit *konečný stav* ve hře. Je na vás jako na tvůrci hry, abyste určili, proč hra skončila. Zde jsou některé důvody, pokud předpokládáme, že mluvíme o vesmírné hře, kterou jste dosud vytvářeli:

- **Bylo zničeno `N` nepřátelských lodí**: Je běžné, že pokud rozdělíte hru na různé úrovně, musíte zničit `N` nepřátelských lodí, abyste úroveň dokončili.
- **Vaše loď byla zničena**: Existují hry, kde prohrajete, pokud je vaše loď zničena. Dalším běžným přístupem je koncept životů. Pokaždé, když je vaše loď zničena, odečte se jeden život. Jakmile ztratíte všechny životy, hra končí.
- **Nasbírali jste `N` bodů**: Další běžný konečný stav je, že nasbíráte body. Jak body získáváte, je na vás, ale je běžné přiřadit body různým aktivitám, jako je zničení nepřátelské lodi nebo sbírání předmětů, které se objeví, když jsou zničeny.
- **Dokončení úrovně**: To může zahrnovat několik podmínek, jako je zničení `X` nepřátelských lodí, nasbírání `Y` bodů nebo třeba získání konkrétního předmětu.

## Restartování

Pokud se lidem vaše hra líbí, pravděpodobně ji budou chtít hrát znovu. Jakmile hra skončí z jakéhokoliv důvodu, měli byste nabídnout možnost restartu.

✅ Zamyslete se nad tím, za jakých podmínek podle vás hra končí, a jak jste vyzváni k restartu.

## Co vytvořit

Do své hry přidáte tyto pravidla:

1. **Výhra ve hře**. Jakmile budou zničeny všechny nepřátelské lodě, vyhráváte hru. Navíc zobrazte nějakou zprávu o vítězství.
1. **Restart**. Jakmile ztratíte všechny životy nebo vyhrajete hru, měli byste nabídnout možnost restartu hry. Pamatujte! Budete muset hru znovu inicializovat a předchozí stav hry by měl být vymazán.

## Doporučené kroky

Najděte soubory, které byly vytvořeny pro vás ve složce `your-work`. Měly by obsahovat následující:

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

Spusťte svůj projekt ve složce `your_work` zadáním:

```bash
cd your-work
npm start
```

Výše uvedené spustí HTTP server na adrese `http://localhost:5000`. Otevřete prohlížeč a zadejte tuto adresu. Vaše hra by měla být v hratelném stavu.

> tip: abyste se vyhnuli varováním ve Visual Studio Code, upravte funkci `window.onload`, aby volala `gameLoopId` tak, jak je (bez `let`), a deklarujte `gameLoopId` na začátku souboru samostatně: `let gameLoopId;`

### Přidání kódu

1. **Sledování konečného stavu**. Přidejte kód, který sleduje počet nepřátel nebo zda byla hrdinská loď zničena, přidáním těchto dvou funkcí:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **Přidání logiky do zpracování zpráv**. Upravte `eventEmitter`, aby zpracovával tyto podmínky:

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

1. **Přidání nových typů zpráv**. Přidejte tyto zprávy do objektu constants:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **Přidání restartovacího kódu**. Přidejte kód, který restartuje hru po stisknutí vybraného tlačítka.

   1. **Poslouchejte stisk klávesy `Enter`**. Upravte eventListener okna, aby poslouchal tento stisk:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **Přidejte restartovací zprávu**. Přidejte tuto zprávu do constants Messages:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **Implementace pravidel hry**. Implementujte následující pravidla hry:

   1. **Podmínka výhry hráče**. Když jsou zničeny všechny nepřátelské lodě, zobrazte zprávu o vítězství.

      1. Nejprve vytvořte funkci `displayMessage()`:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. Vytvořte funkci `endGame()`:

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

   1. **Logika restartu**. Když jsou ztraceny všechny životy nebo hráč vyhrál hru, zobrazte, že hru lze restartovat. Navíc restartujte hru, když je stisknuta klávesa *restart* (můžete rozhodnout, která klávesa bude mapována na restart).

      1. Vytvořte funkci `resetGame()`:

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

     1. Přidejte volání `eventEmitter` pro resetování hry v `initGame()`:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. Přidejte funkci `clear()` do EventEmitter:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 Gratulujeme, kapitáne! Vaše hra je hotová! Skvělá práce! 🚀 💥 👽

---

## 🚀 Výzva

Přidejte zvuk! Dokážete přidat zvuk, který zlepší herní zážitek, třeba při zásahu laserem, smrti hrdiny nebo vítězství? Podívejte se na tento [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play), abyste se naučili, jak přehrávat zvuk pomocí JavaScriptu.

## Kvíz po přednášce

[Kvíz po přednášce](https://ff-quizzes.netlify.app/web/quiz/40)

## Přehled a samostudium

Vaším úkolem je vytvořit nový vzorový příklad hry, takže prozkoumejte některé zajímavé hry, abyste zjistili, jaký typ hry byste mohli vytvořit.

## Úkol

[Vytvořte vzorovou hru](assignment.md)

---

**Prohlášení**:  
Tento dokument byl přeložen pomocí služby pro automatický překlad [Co-op Translator](https://github.com/Azure/co-op-translator). I když se snažíme o co největší přesnost, mějte prosím na paměti, že automatické překlady mohou obsahovat chyby nebo nepřesnosti. Původní dokument v jeho původním jazyce by měl být považován za závazný zdroj. Pro důležité informace doporučujeme profesionální lidský překlad. Neodpovídáme za žádná nedorozumění nebo nesprávné výklady vyplývající z použití tohoto překladu.