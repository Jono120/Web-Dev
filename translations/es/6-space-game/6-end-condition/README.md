<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "05be6c37791668e3719c4fba94566367",
  "translation_date": "2025-08-29T13:55:57+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "es"
}
-->
# Construir un Juego Espacial Parte 6: Final y Reinicio

## Cuestionario Previo a la Clase

[Cuestionario previo a la clase](https://ff-quizzes.netlify.app/web/quiz/39)

Existen diferentes maneras de expresar una *condición de finalización* en un juego. Depende de ti, como creador del juego, decidir por qué el juego ha terminado. Aquí hay algunas razones, suponiendo que estamos hablando del juego espacial que has estado construyendo hasta ahora:

- **Se han destruido `N` naves enemigas**: Es bastante común, si divides un juego en diferentes niveles, que necesites destruir `N` naves enemigas para completar un nivel.
- **Tu nave ha sido destruida**: Definitivamente hay juegos en los que pierdes si tu nave es destruida. Otro enfoque común es tener el concepto de vidas. Cada vez que tu nave es destruida, se descuenta una vida. Una vez que todas las vidas se han perdido, pierdes el juego.
- **Has recolectado `N` puntos**: Otra condición común de finalización es recolectar puntos. Cómo obtienes puntos depende de ti, pero es bastante común asignar puntos a diversas actividades como destruir una nave enemiga o recolectar objetos que caen cuando son destruidos.
- **Completar un nivel**: Esto podría involucrar varias condiciones, como destruir `X` naves enemigas, recolectar `Y` puntos o tal vez recolectar un objeto específico.

## Reinicio

Si las personas disfrutan tu juego, es probable que quieran jugarlo nuevamente. Una vez que el juego termina por cualquier razón, deberías ofrecer una alternativa para reiniciarlo.

✅ Piensa un poco sobre las condiciones bajo las cuales encuentras que un juego termina, y luego cómo se te invita a reiniciarlo.

## Qué construir

Agregarás estas reglas a tu juego:

1. **Ganar el juego**. Una vez que todas las naves enemigas han sido destruidas, ganas el juego. Además, muestra algún tipo de mensaje de victoria.
1. **Reiniciar**. Una vez que todas tus vidas se pierden o el juego se gana, deberías ofrecer una forma de reiniciar el juego. ¡Recuerda! Necesitarás reinicializar el juego y borrar el estado anterior del juego.

## Pasos recomendados

Ubica los archivos que se han creado para ti en la subcarpeta `your-work`. Debería contener lo siguiente:

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

Inicia tu proyecto en la carpeta `your_work` escribiendo:

```bash
cd your-work
npm start
```

Lo anterior iniciará un servidor HTTP en la dirección `http://localhost:5000`. Abre un navegador e ingresa esa dirección. Tu juego debería estar en un estado jugable.

> consejo: para evitar advertencias en Visual Studio Code, edita la función `window.onload` para llamar a `gameLoopId` tal como está (sin `let`), y declara `gameLoopId` en la parte superior del archivo, de forma independiente: `let gameLoopId;`

### Agregar código

1. **Rastrear la condición de finalización**. Agrega código que haga un seguimiento del número de enemigos o si la nave del héroe ha sido destruida, añadiendo estas dos funciones:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **Agregar lógica a los manejadores de mensajes**. Edita el `eventEmitter` para manejar estas condiciones:

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

1. **Agregar nuevos tipos de mensajes**. Agrega estos mensajes al objeto de constantes:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **Agregar código de reinicio** que reinicie el juego al presionar un botón seleccionado.

   1. **Escuchar la tecla `Enter`**. Edita el eventListener de tu ventana para escuchar esta tecla:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **Agregar mensaje de reinicio**. Agrega este mensaje a tu constante de mensajes:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **Implementar reglas del juego**. Implementa las siguientes reglas del juego:

   1. **Condición de victoria del jugador**. Cuando todas las naves enemigas sean destruidas, muestra un mensaje de victoria.

      1. Primero, crea una función `displayMessage()`:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. Crea una función `endGame()`:

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

   1. **Lógica de reinicio**. Cuando todas las vidas se pierdan o el jugador gane el juego, muestra que el juego puede ser reiniciado. Además, reinicia el juego cuando se presione la tecla de *reinicio* (puedes decidir qué tecla se asignará para reiniciar).

      1. Crea la función `resetGame()`:

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

     1. Agrega una llamada al `eventEmitter` para reiniciar el juego en `initGame()`:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. Agrega una función `clear()` al EventEmitter:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 ¡Felicitaciones, Capitán! ¡Tu juego está completo! ¡Bien hecho! 🚀 💥 👽

---

## 🚀 Desafío

¡Agrega un sonido! ¿Puedes agregar un sonido para mejorar la experiencia de juego, tal vez cuando hay un impacto de láser, o cuando el héroe muere o gana? Echa un vistazo a este [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) para aprender cómo reproducir sonido usando JavaScript.

## Cuestionario Posterior a la Clase

[Cuestionario posterior a la clase](https://ff-quizzes.netlify.app/web/quiz/40)

## Revisión y Estudio Personal

Tu tarea es crear un nuevo juego de muestra, así que explora algunos de los juegos interesantes que existen para ver qué tipo de juego podrías construir.

## Tarea

[Construir un Juego de Muestra](assignment.md)

---

**Descargo de responsabilidad**:  
Este documento ha sido traducido utilizando el servicio de traducción automática [Co-op Translator](https://github.com/Azure/co-op-translator). Si bien nos esforzamos por garantizar la precisión, tenga en cuenta que las traducciones automatizadas pueden contener errores o imprecisiones. El documento original en su idioma nativo debe considerarse como la fuente autorizada. Para información crítica, se recomienda una traducción profesional realizada por humanos. No nos hacemos responsables de malentendidos o interpretaciones erróneas que puedan surgir del uso de esta traducción.