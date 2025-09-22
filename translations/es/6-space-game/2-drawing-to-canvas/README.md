<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "056641280211e52fd0adb81b6058ec55",
  "translation_date": "2025-08-29T13:55:32+00:00",
  "source_file": "6-space-game/2-drawing-to-canvas/README.md",
  "language_code": "es"
}
-->
# Construye un Juego Espacial Parte 2: Dibuja al Héroe y a los Monstruos en el Lienzo

## Cuestionario Previo a la Clase

[Cuestionario previo a la clase](https://ff-quizzes.netlify.app/web/quiz/31)

## El Lienzo

El lienzo es un elemento HTML que, por defecto, no tiene contenido; es como una hoja en blanco. Necesitas agregarle contenido dibujando sobre él.

✅ Lee [más sobre la API de Canvas](https://developer.mozilla.org/docs/Web/API/Canvas_API) en MDN.

Así es como normalmente se declara, como parte del cuerpo de la página:

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

Arriba estamos configurando el `id`, `width` y `height`.

- `id`: establece esto para poder obtener una referencia cuando necesites interactuar con él.
- `width`: este es el ancho del elemento.
- `height`: esta es la altura del elemento.

## Dibujando geometría simple

El lienzo utiliza un sistema de coordenadas cartesianas para dibujar cosas. Por lo tanto, usa un eje x y un eje y para expresar dónde se encuentra algo. La ubicación `0,0` es la esquina superior izquierda, y la esquina inferior derecha corresponde al ANCHO y ALTO que definiste para el lienzo.

![la cuadrícula del lienzo](../../../../translated_images/canvas_grid.5f209da785ded492a01ece440e3032afe51efa500cc2308e5ea4252487ceaf0b.es.png)  
> Imagen de [MDN](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes)

Para dibujar en el elemento lienzo, necesitas seguir los siguientes pasos:

1. **Obtener una referencia** al elemento Canvas.
2. **Obtener una referencia** al elemento Context que está en el lienzo.
3. **Realizar una operación de dibujo** usando el elemento Context.

El código para los pasos anteriores usualmente se ve así:

```javascript
// draws a red rectangle
//1. get the canvas reference
canvas = document.getElementById("myCanvas");

//2. set the context to 2D to draw basic shapes
ctx = canvas.getContext("2d");

//3. fill it with the color red
ctx.fillStyle = 'red';

//4. and draw a rectangle with these parameters, setting location and size
ctx.fillRect(0,0, 200, 200) // x,y,width, height
```

✅ La API de Canvas se centra principalmente en formas 2D, pero también puedes dibujar elementos 3D en un sitio web; para esto, podrías usar la [API de WebGL](https://developer.mozilla.org/docs/Web/API/WebGL_API).

Con la API de Canvas puedes dibujar todo tipo de cosas, como:

- **Formas geométricas**, ya mostramos cómo dibujar un rectángulo, pero hay mucho más que puedes dibujar.
- **Texto**, puedes dibujar texto con cualquier fuente y color que desees.
- **Imágenes**, puedes dibujar una imagen basada en un recurso gráfico como un archivo .jpg o .png, por ejemplo.

✅ ¡Inténtalo! Ya sabes cómo dibujar un rectángulo, ¿puedes dibujar un círculo en una página? Echa un vistazo a algunos dibujos interesantes hechos con Canvas en CodePen. Aquí tienes un [ejemplo particularmente impresionante](https://codepen.io/dissimulate/pen/KrAwx).

## Cargar y dibujar un recurso gráfico

Cargas un recurso gráfico creando un objeto `Image` y configurando su propiedad `src`. Luego escuchas el evento `load` para saber cuándo está listo para ser usado. El código se ve así:

### Cargar recurso

```javascript
const img = new Image();
img.src = 'path/to/my/image.png';
img.onload = () => {
  // image loaded and ready to be used
}
```

### Patrón para cargar recursos

Se recomienda envolver lo anterior en una estructura como esta, para que sea más fácil de usar y solo intentes manipularlo cuando esté completamente cargado:

```javascript
function loadAsset(path) {
  return new Promise((resolve) => {
    const img = new Image();
    img.src = path;
    img.onload = () => {
      // image loaded and ready to be used
      resolve(img);
    }
  })
}

// use like so

async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')
}

```

Para dibujar recursos gráficos del juego en una pantalla, tu código se vería así:

```javascript
async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')

  canvas = document.getElementById("myCanvas");
  ctx = canvas.getContext("2d");
  ctx.drawImage(heroImg, canvas.width/2,canvas.height/2);
  ctx.drawImage(monsterImg, 0,0);
}
```

## Ahora es momento de empezar a construir tu juego

### Qué construir

Construirás una página web con un elemento Canvas. Debería renderizar una pantalla negra de `1024*768`. Te hemos proporcionado dos imágenes:

- Nave del héroe

   ![Nave del héroe](../../../../translated_images/player.dd24c1afa8c71e9b82b2958946d4bad13308681392d4b5ddcc61a0e818ef8088.es.png)

- Monstruo 5*5

   ![Nave del monstruo](../../../../translated_images/enemyShip.5df2a822c16650c2fb3c06652e8ec8120cdb9122a6de46b9a1a56d54db22657f.es.png)

### Pasos recomendados para comenzar el desarrollo

Ubica los archivos que se han creado para ti en la subcarpeta `your-work`. Debería contener lo siguiente:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

Abre la copia de esta carpeta en Visual Studio Code. Necesitas tener configurado un entorno de desarrollo local, preferiblemente con Visual Studio Code, NPM y Node instalados. Si no tienes `npm` configurado en tu computadora, [aquí te mostramos cómo hacerlo](https://www.npmjs.com/get-npm).

Inicia tu proyecto navegando a la carpeta `your_work`:

```bash
cd your-work
npm start
```

Lo anterior iniciará un servidor HTTP en la dirección `http://localhost:5000`. Abre un navegador e ingresa esa dirección. Ahora mismo es una página en blanco, pero eso cambiará.

> Nota: para ver los cambios en tu pantalla, actualiza tu navegador.

### Agregar código

Agrega el código necesario en `your-work/app.js` para resolver lo siguiente:

1. **Dibuja** un lienzo con fondo negro  
   > consejo: agrega dos líneas bajo el TODO correspondiente en `/app.js`, configurando el elemento `ctx` para que sea negro y las coordenadas superior/izquierda en 0,0, con la altura y el ancho iguales a los del lienzo.
2. **Carga** texturas  
   > consejo: agrega las imágenes del jugador y del enemigo usando `await loadTexture` y pasando la ruta de la imagen. ¡Aún no las verás en la pantalla!
3. **Dibuja** al héroe en el centro de la pantalla en la mitad inferior  
   > consejo: usa la API `drawImage` para dibujar `heroImg` en la pantalla, configurando `canvas.width / 2 - 45` y `canvas.height - canvas.height / 4)`.
4. **Dibuja** 5*5 monstruos  
   > consejo: ahora puedes descomentar el código para dibujar enemigos en la pantalla. Luego, ve a la función `createEnemies` y complétala.

   Primero, configura algunas constantes:

    ```javascript
    const MONSTER_TOTAL = 5;
    const MONSTER_WIDTH = MONSTER_TOTAL * 98;
    const START_X = (canvas.width - MONSTER_WIDTH) / 2;
    const STOP_X = START_X + MONSTER_WIDTH;
    ```

   Luego, crea un bucle para dibujar el array de monstruos en la pantalla:

    ```javascript
    for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          ctx.drawImage(enemyImg, x, y);
        }
      }
    ```

## Resultado

El resultado final debería verse así:

![Pantalla negra con un héroe y 5*5 monstruos](../../../../translated_images/partI-solution.36c53b48c9ffae2a5e15496b23b604ba5393433e4bf91608a7a0a020eb7a2691.es.png)

## Solución

Por favor, intenta resolverlo tú mismo primero, pero si te quedas atascado, revisa una [solución](../../../../6-space-game/2-drawing-to-canvas/solution/app.js).

---

## 🚀 Desafío

Has aprendido sobre cómo dibujar con la API de Canvas enfocada en 2D; echa un vistazo a la [API de WebGL](https://developer.mozilla.org/docs/Web/API/WebGL_API) e intenta dibujar un objeto 3D.

## Cuestionario Posterior a la Clase

[Cuestionario posterior a la clase](https://ff-quizzes.netlify.app/web/quiz/32)

## Repaso y Estudio Personal

Aprende más sobre la API de Canvas [leyendo sobre ella](https://developer.mozilla.org/docs/Web/API/Canvas_API).

## Tarea

[Experimenta con la API de Canvas](assignment.md)

---

**Descargo de responsabilidad**:  
Este documento ha sido traducido utilizando el servicio de traducción automática [Co-op Translator](https://github.com/Azure/co-op-translator). Si bien nos esforzamos por lograr precisión, tenga en cuenta que las traducciones automáticas pueden contener errores o imprecisiones. El documento original en su idioma nativo debe considerarse como la fuente autorizada. Para información crítica, se recomienda una traducción profesional realizada por humanos. No nos hacemos responsables de malentendidos o interpretaciones erróneas que puedan surgir del uso de esta traducción.