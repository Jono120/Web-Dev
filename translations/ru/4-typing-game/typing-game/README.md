<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1b0aeccb600f83c603cd70cb42df594d",
  "translation_date": "2025-08-28T23:25:34+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "ru"
}
-->
# Создание игры с использованием событий

## Викторина перед лекцией

[Викторина перед лекцией](https://ff-quizzes.netlify.app/web/quiz/21)

## Программирование, управляемое событиями

При создании веб-приложения мы предоставляем графический интерфейс (GUI), чтобы пользователь мог взаимодействовать с тем, что мы разработали. Самый распространенный способ взаимодействия с браузером — это клики и ввод текста в различные элементы. Проблема, с которой мы сталкиваемся как разработчики, заключается в том, что мы не знаем, когда пользователь выполнит эти действия!

[Программирование, управляемое событиями](https://en.wikipedia.org/wiki/Event-driven_programming) — это подход, который мы используем для создания нашего GUI. Если разобрать эту фразу, ключевым словом здесь является **событие**. [Событие](https://www.merriam-webster.com/dictionary/event), согласно Merriam-Webster, определяется как "что-то, что происходит". Это идеально описывает нашу ситуацию. Мы знаем, что что-то произойдет, и хотим выполнить код в ответ на это, но не знаем, когда именно это случится.

Чтобы указать участок кода, который мы хотим выполнить, мы создаем функцию. Если говорить о [процедурном программировании](https://en.wikipedia.org/wiki/Procedural_programming), функции вызываются в определенном порядке. То же самое будет верно и для программирования, управляемого событиями. Разница заключается в том, **как** функции будут вызываться.

Для обработки событий (например, кликов мыши, ввода текста и т.д.) мы регистрируем **обработчики событий**. Обработчик события — это функция, которая "слушает" событие и выполняется в ответ на его возникновение. Обработчики событий могут обновлять интерфейс, отправлять запросы на сервер или выполнять любые другие действия в ответ на действия пользователя. Мы добавляем обработчик события с помощью [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener), передавая функцию для выполнения.

> **NOTE:** Стоит отметить, что существует множество способов создания обработчиков событий. Вы можете использовать анонимные функции или создавать именованные. Также есть различные сокращения, такие как установка свойства `click` или использование `addEventListener`. В нашем упражнении мы сосредоточимся на `addEventListener` и анонимных функциях, так как это, вероятно, самый распространенный метод, который используют веб-разработчики. Кроме того, `addEventListener` является наиболее гибким, так как он работает для всех событий, а имя события можно передать в качестве параметра.

### Распространенные события

Существует [множество событий](https://developer.mozilla.org/docs/Web/Events), которые вы можете использовать при создании приложения. Практически любое действие пользователя на странице вызывает событие, что дает вам огромные возможности для создания желаемого пользовательского опыта. К счастью, вам обычно понадобится лишь небольшое количество событий. Вот несколько распространенных (включая те, которые мы будем использовать при создании нашей игры):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): Пользователь кликнул на что-то, обычно на кнопку или гиперссылку
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): Пользователь кликнул правой кнопкой мыши
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): Пользователь выделил текст
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): Пользователь ввел текст

## Создание игры

Мы создадим игру, чтобы изучить, как работают события в JavaScript. Наша игра будет проверять навыки набора текста игрока, что является одним из самых недооцененных навыков, которыми должен обладать каждый разработчик. Мы все должны практиковаться в наборе текста! Общий процесс игры будет выглядеть следующим образом:

- Игрок нажимает кнопку "Старт" и видит цитату, которую нужно набрать
- Игрок набирает цитату как можно быстрее в текстовом поле
  - По мере завершения каждого слова следующее слово выделяется
  - Если игрок допустил опечатку, текстовое поле становится красным
  - Когда игрок завершает цитату, отображается сообщение об успехе с указанием затраченного времени

Давайте создадим нашу игру и изучим события!

### Структура файлов

Нам понадобятся три файла: **index.html**, **script.js** и **style.css**. Начнем с их создания, чтобы упростить себе задачу.

- Создайте новую папку для работы, открыв консоль или терминал и выполнив следующую команду:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- Откройте Visual Studio Code

```bash
code .
```

- Добавьте три файла в папку в Visual Studio Code с следующими именами:
  - index.html
  - script.js
  - style.css

## Создание пользовательского интерфейса

Если мы изучим требования, то поймем, что нам понадобится несколько элементов на нашей HTML-странице. Это похоже на рецепт, где нам нужны ингредиенты:

- Место для отображения цитаты, которую должен набрать пользователь
- Место для отображения сообщений, например, сообщения об успехе
- Текстовое поле для ввода текста
- Кнопка "Старт"

Каждому из этих элементов понадобятся идентификаторы, чтобы мы могли работать с ними в JavaScript. Мы также добавим ссылки на CSS и JavaScript файлы, которые мы создадим.

Создайте новый файл с именем **index.html**. Добавьте следующий HTML:

```html
<!-- inside index.html -->
<html>
<head>
  <title>Typing game</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Typing game!</h1>
  <p>Practice your typing skills with a quote from Sherlock Holmes. Click **start** to begin!</p>
  <p id="quote"></p> <!-- This will display our quote -->
  <p id="message"></p> <!-- This will display any status messages -->
  <div>
    <input type="text" aria-label="current word" id="typed-value" /> <!-- The textbox for typing -->
    <button type="button" id="start">Start</button> <!-- To start the game -->
  </div>
  <script src="script.js"></script>
</body>
</html>
```

### Запуск приложения

Лучше всего разрабатывать итеративно, чтобы видеть, как все выглядит. Давайте запустим наше приложение. В Visual Studio Code есть замечательное расширение [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon), которое будет локально хостить ваше приложение и обновлять браузер каждый раз, когда вы сохраняете изменения.

- Установите [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon), перейдя по ссылке и нажав **Install**
  - Браузер предложит вам открыть Visual Studio Code, а затем Visual Studio Code предложит выполнить установку
  - Перезапустите Visual Studio Code, если потребуется
- После установки в Visual Studio Code нажмите Ctrl-Shift-P (или Cmd-Shift-P), чтобы открыть палитру команд
- Введите **Live Server: Open with Live Server**
  - Live Server начнет хостить ваше приложение
- Откройте браузер и перейдите по адресу **https://localhost:5500**
- Теперь вы должны увидеть созданную вами страницу!

Давайте добавим немного функциональности.

## Добавление CSS

После создания HTML добавим CSS для базового оформления. Нам нужно выделить слово, которое должен набрать игрок, и изменить цвет текстового поля, если введенный текст неверен. Мы сделаем это с помощью двух классов.

Создайте новый файл с именем **style.css** и добавьте следующий синтаксис.

```css
/* inside style.css */
.highlight {
  background-color: yellow;
}

.error {
  background-color: lightcoral;
  border: red;
}
```

✅ Когда дело касается CSS, вы можете оформить вашу страницу так, как вам нравится. Потратьте немного времени, чтобы сделать страницу более привлекательной:

- Выберите другой шрифт
- Измените цвет заголовков
- Измените размеры элементов

## JavaScript

После создания интерфейса мы сосредоточимся на JavaScript, который обеспечит логику. Мы разобьем это на несколько шагов:

- [Создание констант](../../../../4-typing-game/typing-game)
- [Обработчик события для начала игры](../../../../4-typing-game/typing-game)
- [Обработчик события для ввода текста](../../../../4-typing-game/typing-game)

Но сначала создайте новый файл с именем **script.js**.

### Добавление констант

Нам понадобятся несколько элементов, чтобы упростить программирование. Опять же, как в рецепте, вот что нам нужно:

- Массив со списком всех цитат
- Пустой массив для хранения всех слов текущей цитаты
- Переменная для хранения индекса слова, которое игрок набирает в данный момент
- Время, когда игрок нажал "Старт"

Также нам понадобятся ссылки на элементы интерфейса:

- Текстовое поле (**typed-value**)
- Элемент для отображения цитаты (**quote**)
- Элемент для отображения сообщений (**message**)

```javascript
// inside script.js
// all of our quotes
const quotes = [
    'When you have eliminated the impossible, whatever remains, however improbable, must be the truth.',
    'There is nothing more deceptive than an obvious fact.',
    'I ought to know by this time that when a fact appears to be opposed to a long train of deductions it invariably proves to be capable of bearing some other interpretation.',
    'I never make exceptions. An exception disproves the rule.',
    'What one man can invent another can discover.',
    'Nothing clears up a case so much as stating it to another person.',
    'Education never ends, Watson. It is a series of lessons, with the greatest for the last.',
];
// store the list of words and the index of the word the player is currently typing
let words = [];
let wordIndex = 0;
// the starting time
let startTime = Date.now();
// page elements
const quoteElement = document.getElementById('quote');
const messageElement = document.getElementById('message');
const typedValueElement = document.getElementById('typed-value');
```

✅ Добавьте больше цитат в вашу игру

> **NOTE:** Мы можем получать элементы в коде, используя `document.getElementById`. Поскольку мы будем часто обращаться к этим элементам, мы избегаем опечаток в строковых литералах, используя константы. Фреймворки, такие как [Vue.js](https://vuejs.org/) или [React](https://reactjs.org/), могут помочь вам лучше централизовать ваш код.

Посмотрите видео о использовании `const`, `let` и `var`.

[![Типы переменных](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Типы переменных")

> 🎥 Нажмите на изображение выше, чтобы посмотреть видео о переменных.

### Добавление логики начала игры

Чтобы начать игру, игрок должен нажать "Старт". Конечно, мы не знаем, когда он это сделает. Здесь нам поможет [обработчик события](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener). Обработчик события позволит нам "слушать" событие и выполнять код в ответ на его возникновение. В нашем случае мы хотим выполнить код, когда пользователь нажимает "Старт".

Когда пользователь нажимает **Старт**, нам нужно выбрать цитату, настроить интерфейс и установить отслеживание текущего слова и времени. Ниже приведен JavaScript, который вам нужно добавить; мы обсудим его после блока кода.

```javascript
// at the end of script.js
document.getElementById('start').addEventListener('click', () => {
  // get a quote
  const quoteIndex = Math.floor(Math.random() * quotes.length);
  const quote = quotes[quoteIndex];
  // Put the quote into an array of words
  words = quote.split(' ');
  // reset the word index for tracking
  wordIndex = 0;

  // UI updates
  // Create an array of span elements so we can set a class
  const spanWords = words.map(function(word) { return `<span>${word} </span>`});
  // Convert into string and set as innerHTML on quote display
  quoteElement.innerHTML = spanWords.join('');
  // Highlight the first word
  quoteElement.childNodes[0].className = 'highlight';
  // Clear any prior messages
  messageElement.innerText = '';

  // Setup the textbox
  // Clear the textbox
  typedValueElement.value = '';
  // set focus
  typedValueElement.focus();
  // set the event handler

  // Start the timer
  startTime = new Date().getTime();
});
```

Разберем код!

- Настройка отслеживания слов
  - Использование [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) и [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) позволяет нам случайным образом выбрать цитату из массива `quotes`
  - Мы преобразуем `quote` в массив `words`, чтобы отслеживать слово, которое игрок набирает в данный момент
  - `wordIndex` устанавливается в 0, так как игрок начнет с первого слова
- Настройка интерфейса
  - Создаем массив `spanWords`, который содержит каждое слово внутри элемента `span`
    - Это позволит нам выделять слово на экране
  - Используем `join` для создания строки, которую можно использовать для обновления `innerHTML` элемента `quoteElement`
    - Это отобразит цитату для игрока
  - Устанавливаем `className` первого элемента `span` в `highlight`, чтобы выделить его желтым цветом
  - Очищаем `messageElement`, установив `innerText` в `''`
- Настройка текстового поля
  - Очищаем текущее значение `value` элемента `typedValueElement`
  - Устанавливаем фокус на `typedValueElement`
- Запускаем таймер, вызвав `getTime`

### Добавление логики ввода текста

Когда игрок вводит текст, возникает событие `input`. Этот обработчик события проверит, правильно ли игрок набирает слово, и обработает текущий статус игры. Вернитесь к **script.js** и добавьте следующий код в конец. Мы разберем его после блока кода.

```javascript
// at the end of script.js
typedValueElement.addEventListener('input', () => {
  // Get the current word
  const currentWord = words[wordIndex];
  // get the current value
  const typedValue = typedValueElement.value;

  if (typedValue === currentWord && wordIndex === words.length - 1) {
    // end of sentence
    // Display success
    const elapsedTime = new Date().getTime() - startTime;
    const message = `CONGRATULATIONS! You finished in ${elapsedTime / 1000} seconds.`;
    messageElement.innerText = message;
  } else if (typedValue.endsWith(' ') && typedValue.trim() === currentWord) {
    // end of word
    // clear the typedValueElement for the new word
    typedValueElement.value = '';
    // move to the next word
    wordIndex++;
    // reset the class name for all elements in quote
    for (const wordElement of quoteElement.childNodes) {
      wordElement.className = '';
    }
    // highlight the new word
    quoteElement.childNodes[wordIndex].className = 'highlight';
  } else if (currentWord.startsWith(typedValue)) {
    // currently correct
    // highlight the next word
    typedValueElement.className = '';
  } else {
    // error state
    typedValueElement.className = 'error';
  }
});
```

Разберем код! Мы начинаем с получения текущего слова и значения, которое игрок ввел до сих пор. Затем у нас идет каскадная логика, где мы проверяем, завершена ли цитата, завершено ли слово, правильно ли введено слово или (наконец) есть ли ошибка.

- Цитата завершена, если `typedValue` равно `currentWord`, а `wordIndex` равен длине массива `words` минус один
  - Вычисляем `elapsedTime`, вычитая `startTime` из текущего времени
  - Делим `elapsedTime` на 1,000, чтобы преобразовать миллисекунды в секунды
  - Отображаем сообщение об успехе
- Слово завершено, если `typedValue` заканчивается пробелом (конец слова) и `typedValue` равно `currentWord`
  - Устанавливаем `value` элемента `typedElement` в `''`, чтобы можно было набрать следующее слово
  - Увеличиваем `wordIndex`, чтобы перейти к следующему слову
  - Проходим по всем `childNodes` элемента `quoteElement`, устанавливая `className` в `''`, чтобы вернуть стандартное отображение
  - Устанавливаем `className` текущего слова в `highlight`, чтобы отметить его как следующее слово для набора
- Слово введено правильно (но не завершено), если `currentWord` начинается с `typedValue`
  - Убеждаемся, что `typedValueElement` отображается как стандартное, очищая `className`
- Если мы дошли до этого момента, значит, есть ошибка
  - Устанавливаем `className` элемента `typedValueElement` в `error`

## Тестирование приложения

Вы дошли до конца! Последний шаг — убедиться, что наше приложение работает. Попробуйте! Не переживайте, если возникнут ошибки; **все разработчики** сталкиваются с ошибками. Изучите сообщения и исправьте их по мере необходимости.

Нажмите **Старт** и начните вводить текст! Это должно выглядеть примерно как анимация, которую мы видели ранее.

![Анимация игры в действии](../../../../4-typing-game/images/demo.gif)

---

## 🚀 Задание

Добавьте больше функциональности:

- Отключите обработчик события `input` после завершения игры и включите его снова при нажатии кнопки
- Отключите текстовое поле, когда игрок завершает цитату
- Отобразите модальное окно с сообщением об успехе
- Сохраните лучшие результаты, используя [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)
## Викторина после лекции

[Викторина после лекции](https://ff-quizzes.netlify.app/web/quiz/22)

## Обзор и самостоятельное изучение

Изучите [все доступные события](https://developer.mozilla.org/docs/Web/Events), которые предоставляет веб-браузер разработчику, и подумайте о сценариях, в которых вы могли бы использовать каждое из них.

## Задание

[Создайте новую игру с использованием клавиатуры](assignment.md)

---

**Отказ от ответственности**:  
Этот документ был переведен с помощью сервиса автоматического перевода [Co-op Translator](https://github.com/Azure/co-op-translator). Хотя мы стремимся к точности, пожалуйста, имейте в виду, что автоматические переводы могут содержать ошибки или неточности. Оригинальный документ на его родном языке следует считать авторитетным источником. Для получения критически важной информации рекомендуется профессиональный перевод человеком. Мы не несем ответственности за любые недоразумения или неправильные интерпретации, возникшие в результате использования данного перевода.