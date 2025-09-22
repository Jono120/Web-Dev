<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "056641280211e52fd0adb81b6058ec55",
  "translation_date": "2025-08-28T23:18:24+00:00",
  "source_file": "6-space-game/2-drawing-to-canvas/README.md",
  "language_code": "ru"
}
-->
# Создание космической игры, часть 2: Рисуем героя и монстров на Canvas

## Викторина перед лекцией

[Викторина перед лекцией](https://ff-quizzes.netlify.app/web/quiz/31)

## Canvas

Canvas — это HTML-элемент, который по умолчанию не содержит контента; это чистый холст. Чтобы добавить на него что-то, нужно рисовать.

✅ Прочитайте [больше о Canvas API](https://developer.mozilla.org/docs/Web/API/Canvas_API) на MDN.

Обычно он объявляется следующим образом, как часть тела страницы:

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

В приведенном выше примере мы устанавливаем `id`, `width` и `height`.

- `id`: задается для получения ссылки, когда нужно взаимодействовать с элементом.
- `width`: ширина элемента.
- `height`: высота элемента.

## Рисование простой геометрии

Canvas использует декартову систему координат для рисования. Таким образом, он использует оси x и y для определения местоположения объекта. Точка `0,0` находится в верхнем левом углу, а нижний правый угол соответствует заданным значениям WIDTH и HEIGHT холста.

![Сетка Canvas](../../../../translated_images/canvas_grid.5f209da785ded492a01ece440e3032afe51efa500cc2308e5ea4252487ceaf0b.ru.png)  
> Изображение с [MDN](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes)

Чтобы рисовать на элементе Canvas, нужно выполнить следующие шаги:

1. **Получить ссылку** на элемент Canvas.
2. **Получить ссылку** на элемент Context, который находится на Canvas.
3. **Выполнить операцию рисования** с использованием элемента Context.

Код для выполнения этих шагов обычно выглядит так:

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

✅ Canvas API в основном ориентирован на 2D-формы, но вы также можете рисовать 3D-элементы на веб-странице, используя [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API).

С помощью Canvas API можно рисовать множество вещей, таких как:

- **Геометрические фигуры**. Мы уже показали, как нарисовать прямоугольник, но можно нарисовать гораздо больше.
- **Текст**. Вы можете рисовать текст с любым шрифтом и цветом.
- **Изображения**. Можно рисовать изображения, используя такие ресурсы, как .jpg или .png.

✅ Попробуйте! Вы знаете, как нарисовать прямоугольник, сможете ли вы нарисовать круг на странице? Посмотрите интересные примеры рисунков на Canvas на CodePen. Вот [особенно впечатляющий пример](https://codepen.io/dissimulate/pen/KrAwx).

## Загрузка и рисование изображения

Чтобы загрузить изображение, нужно создать объект `Image` и установить его свойство `src`. Затем нужно слушать событие `load`, чтобы узнать, когда изображение готово к использованию. Код выглядит так:

### Загрузка ресурса

```javascript
const img = new Image();
img.src = 'path/to/my/image.png';
img.onload = () => {
  // image loaded and ready to be used
}
```

### Шаблон загрузки ресурса

Рекомендуется обернуть приведенный выше код в конструкцию, чтобы было проще использовать и манипулировать изображением только после его полной загрузки:

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

Чтобы нарисовать игровые ресурсы на экране, ваш код будет выглядеть так:

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

## Теперь пора начинать создавать вашу игру

### Что нужно создать

Вы создадите веб-страницу с элементом Canvas. На ней должен отображаться черный экран размером `1024*768`. Мы предоставили вам два изображения:

- Корабль героя

   ![Корабль героя](../../../../translated_images/player.dd24c1afa8c71e9b82b2958946d4bad13308681392d4b5ddcc61a0e818ef8088.ru.png)

- 5*5 монстров

   ![Корабль монстра](../../../../translated_images/enemyShip.5df2a822c16650c2fb3c06652e8ec8120cdb9122a6de46b9a1a56d54db22657f.ru.png)

### Рекомендуемые шаги для начала разработки

Найдите файлы, которые были созданы для вас в папке `your-work`. Она должна содержать следующее:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

Откройте копию этой папки в Visual Studio Code. Убедитесь, что у вас настроена локальная среда разработки, желательно с Visual Studio Code, NPM и Node. Если у вас не установлен `npm`, [вот как это сделать](https://www.npmjs.com/get-npm).

Начните проект, перейдя в папку `your_work`:

```bash
cd your-work
npm start
```

Этот код запустит HTTP-сервер по адресу `http://localhost:5000`. Откройте браузер и введите этот адрес. Сейчас это пустая страница, но скоро она изменится.

> Примечание: чтобы увидеть изменения на экране, обновите браузер.

### Добавьте код

Добавьте необходимый код в `your-work/app.js`, чтобы выполнить следующие задачи:

1. **Нарисуйте** Canvas с черным фоном  
   > совет: добавьте две строки под соответствующим TODO в `/app.js`, установив элемент `ctx` черным, а координаты верхнего левого угла — 0,0, высоту и ширину равными размерам Canvas.
2. **Загрузите** текстуры  
   > совет: добавьте изображения игрока и врага, используя `await loadTexture` и передав путь к изображению. Пока вы их не увидите на экране!
3. **Нарисуйте** героя в центре экрана в нижней половине  
   > совет: используйте API `drawImage`, чтобы нарисовать heroImg на экране, установив `canvas.width / 2 - 45` и `canvas.height - canvas.height / 4)`.
4. **Нарисуйте** 5*5 монстров  
   > совет: теперь можно раскомментировать код для рисования врагов на экране. Затем перейдите к функции `createEnemies` и завершите ее.

   Сначала задайте несколько констант:

    ```javascript
    const MONSTER_TOTAL = 5;
    const MONSTER_WIDTH = MONSTER_TOTAL * 98;
    const START_X = (canvas.width - MONSTER_WIDTH) / 2;
    const STOP_X = START_X + MONSTER_WIDTH;
    ```

    затем создайте цикл для рисования массива монстров на экране:

    ```javascript
    for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          ctx.drawImage(enemyImg, x, y);
        }
      }
    ```

## Результат

Готовый результат должен выглядеть так:

![Черный экран с героем и 5*5 монстрами](../../../../translated_images/partI-solution.36c53b48c9ffae2a5e15496b23b604ba5393433e4bf91608a7a0a020eb7a2691.ru.png)

## Решение

Попробуйте сначала решить задачу самостоятельно, но если вы застряли, посмотрите [решение](../../../../6-space-game/2-drawing-to-canvas/solution/app.js).

---

## 🚀 Задание

Вы узнали о рисовании с помощью Canvas API, ориентированного на 2D. Ознакомьтесь с [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API) и попробуйте нарисовать 3D-объект.

## Викторина после лекции

[Викторина после лекции](https://ff-quizzes.netlify.app/web/quiz/32)

## Обзор и самостоятельное изучение

Узнайте больше о Canvas API, [прочитав о нем](https://developer.mozilla.org/docs/Web/API/Canvas_API).

## Задание

[Попробуйте Canvas API](assignment.md)

---

**Отказ от ответственности**:  
Этот документ был переведен с помощью сервиса автоматического перевода [Co-op Translator](https://github.com/Azure/co-op-translator). Несмотря на наши усилия по обеспечению точности, пожалуйста, учитывайте, что автоматические переводы могут содержать ошибки или неточности. Оригинальный документ на его родном языке следует считать авторитетным источником. Для получения критически важной информации рекомендуется профессиональный перевод человеком. Мы не несем ответственности за любые недоразумения или неправильные интерпретации, возникшие в результате использования данного перевода.