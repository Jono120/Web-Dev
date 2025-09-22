<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-29T16:31:40+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "pl"
}
-->
# Stwórz grę kosmiczną, część 6: Zakończenie i restart

## Quiz przed wykładem

[Quiz przed wykładem](https://ff-quizzes.netlify.app/web/quiz/39)

Istnieje wiele sposobów na określenie *warunku zakończenia* w grze. To od Ciebie, jako twórcy gry, zależy, dlaczego gra się kończy. Oto kilka powodów, zakładając, że mówimy o grze kosmicznej, którą budujesz do tej pory:

- **Zniszczono `N` wrogich statków**: Jest to dość powszechne, jeśli dzielisz grę na różne poziomy, gdzie musisz zniszczyć `N` wrogich statków, aby ukończyć poziom.
- **Twój statek został zniszczony**: W wielu grach przegrywasz, jeśli Twój statek zostanie zniszczony. Innym popularnym podejściem jest wprowadzenie koncepcji żyć. Za każdym razem, gdy Twój statek zostaje zniszczony, tracisz jedno życie. Gdy wszystkie życia zostaną utracone, przegrywasz grę.
- **Zebrałeś `N` punktów**: Kolejnym częstym warunkiem zakończenia jest zebranie określonej liczby punktów. To, jak zdobywasz punkty, zależy od Ciebie, ale często przypisuje się je do różnych działań, takich jak niszczenie wrogich statków lub zbieranie przedmiotów, które wypadają po ich zniszczeniu.
- **Ukończenie poziomu**: Może to obejmować kilka warunków, takich jak zniszczenie `X` wrogich statków, zebranie `Y` punktów lub zdobycie konkretnego przedmiotu.

## Restartowanie

Jeśli ludzie polubią Twoją grę, prawdopodobnie będą chcieli zagrać ponownie. Gdy gra się kończy z jakiegokolwiek powodu, powinieneś zaoferować możliwość jej restartu.

✅ Zastanów się, w jakich warunkach gra się kończy, a następnie jak gracz jest zachęcany do jej ponownego uruchomienia.

## Co zbudować

Dodasz te zasady do swojej gry:

1. **Wygranie gry**. Gdy wszystkie wrogie statki zostaną zniszczone, wygrywasz grę. Dodatkowo wyświetl jakąś wiadomość o zwycięstwie.
1. **Restart**. Gdy wszystkie życia zostaną utracone lub gra zostanie wygrana, powinieneś umożliwić ponowne uruchomienie gry. Pamiętaj! Musisz zainicjalizować grę od nowa, a poprzedni stan gry powinien zostać wyczyszczony.

## Zalecane kroki

Znajdź pliki, które zostały dla Ciebie utworzone w podfolderze `your-work`. Powinny zawierać następujące:

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

Uruchom swój projekt w folderze `your_work`, wpisując:

```bash
cd your-work
npm start
```

Powyższe polecenie uruchomi serwer HTTP pod adresem `http://localhost:5000`. Otwórz przeglądarkę i wpisz ten adres. Twoja gra powinna być w stanie grywalnym.

> wskazówka: aby uniknąć ostrzeżeń w Visual Studio Code, edytuj funkcję `window.onload`, aby wywoływała `gameLoopId` tak, jak jest (bez `let`), i zadeklaruj `gameLoopId` na początku pliku, niezależnie: `let gameLoopId;`

### Dodaj kod

1. **Śledzenie warunku zakończenia**. Dodaj kod, który śledzi liczbę wrogów lub czy statek bohatera został zniszczony, dodając te dwie funkcje:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **Dodaj logikę do obsługi komunikatów**. Edytuj `eventEmitter`, aby obsługiwał te warunki:

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

1. **Dodaj nowe typy komunikatów**. Dodaj te komunikaty do obiektu constants:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **Dodaj kod restartu**. Dodaj kod, który restartuje grę po naciśnięciu wybranego przycisku.

   1. **Nasłuchuj naciśnięcia klawisza `Enter`**. Edytuj eventListener okna, aby nasłuchiwał tego naciśnięcia:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **Dodaj komunikat restartu**. Dodaj ten komunikat do constants Messages:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **Zaimplementuj zasady gry**. Zaimplementuj następujące zasady gry:

   1. **Warunek wygranej gracza**. Gdy wszystkie wrogie statki zostaną zniszczone, wyświetl wiadomość o zwycięstwie.

      1. Najpierw utwórz funkcję `displayMessage()`:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. Utwórz funkcję `endGame()`:

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

   1. **Logika restartu**. Gdy wszystkie życia zostaną utracone lub gracz wygra grę, wyświetl informację, że grę można zrestartować. Dodatkowo zrestartuj grę po naciśnięciu klawisza *restart* (możesz zdecydować, który klawisz będzie przypisany do restartu).

      1. Utwórz funkcję `resetGame()`:

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

     1. Dodaj wywołanie do `eventEmitter`, aby zresetować grę w `initGame()`:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. Dodaj funkcję `clear()` do EventEmitter:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 Gratulacje, Kapitanie! Twoja gra jest gotowa! Dobra robota! 🚀 💥 👽

---

## 🚀 Wyzwanie

Dodaj dźwięk! Czy możesz dodać dźwięk, aby poprawić rozgrywkę, na przykład gdy laser trafia, bohater ginie lub wygrywa? Sprawdź ten [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play), aby dowiedzieć się, jak odtwarzać dźwięk za pomocą JavaScript.

## Quiz po wykładzie

[Quiz po wykładzie](https://ff-quizzes.netlify.app/web/quiz/40)

## Przegląd i samodzielna nauka

Twoim zadaniem jest stworzenie nowej przykładowej gry, więc eksploruj ciekawe gry, aby zobaczyć, jaki rodzaj gry możesz zbudować.

## Zadanie

[Stwórz przykładową grę](assignment.md)

---

**Zastrzeżenie**:  
Ten dokument został przetłumaczony za pomocą usługi tłumaczenia AI [Co-op Translator](https://github.com/Azure/co-op-translator). Chociaż dokładamy wszelkich starań, aby tłumaczenie było precyzyjne, prosimy pamiętać, że automatyczne tłumaczenia mogą zawierać błędy lub nieścisłości. Oryginalny dokument w jego rodzimym języku powinien być uznawany za wiarygodne źródło. W przypadku informacji o kluczowym znaczeniu zaleca się skorzystanie z profesjonalnego tłumaczenia przez człowieka. Nie ponosimy odpowiedzialności za jakiekolwiek nieporozumienia lub błędne interpretacje wynikające z użycia tego tłumaczenia.