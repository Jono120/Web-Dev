<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1b0aeccb600f83c603cd70cb42df594d",
  "translation_date": "2025-08-28T18:21:23+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "uk"
}
-->
# Створення гри за допомогою подій

## Тест перед лекцією

[Тест перед лекцією](https://ff-quizzes.netlify.app/web/quiz/21)

## Програмування, кероване подіями

Коли ми створюємо браузерний додаток, ми надаємо графічний інтерфейс користувача (GUI), щоб користувач міг взаємодіяти з тим, що ми створили. Найпоширеніший спосіб взаємодії з браузером — це кліки та введення тексту в різні елементи. Виклик для нас, як розробників, полягає в тому, що ми не знаємо, коли користувач виконає ці дії!

[Програмування, кероване подіями](https://uk.wikipedia.org/wiki/Програмування,_кероване_подіями) — це назва типу програмування, який нам потрібно використовувати для створення нашого GUI. Якщо розібрати цю фразу, то основним словом тут є **подія**. [Подія](https://www.merriam-webster.com/dictionary/event), за визначенням Merriam-Webster, — це "щось, що відбувається". Це ідеально описує нашу ситуацію. Ми знаємо, що щось відбудеться, і ми хочемо виконати певний код у відповідь, але ми не знаємо, коли це станеться.

Спосіб, яким ми позначаємо частину коду, яку хочемо виконати, — це створення функції. Якщо ми говоримо про [процедурне програмування](https://uk.wikipedia.org/wiki/Процедурне_програмування), функції викликаються у певному порядку. Те ж саме стосується програмування, керованого подіями. Різниця лише в тому, **як** викликаються функції.

Для обробки подій (натискання кнопок, введення тексту тощо) ми реєструємо **обробники подій**. Обробник подій — це функція, яка "слухає" подію та виконується у відповідь. Обробники подій можуть оновлювати інтерфейс користувача, викликати сервер або виконувати будь-які інші дії у відповідь на дії користувача. Ми додаємо обробник подій за допомогою [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) і передаємо функцію для виконання.

> **NOTE:** Варто зазначити, що існує багато способів створення обробників подій. Ви можете використовувати анонімні функції або створювати іменовані. Ви можете використовувати різні скорочення, наприклад, встановлювати властивість `click` або використовувати `addEventListener`. У нашій вправі ми зосередимося на `addEventListener` та анонімних функціях, оскільки це, мабуть, найпоширеніший підхід, який використовують веброзробники. Це також найгнучкіший спосіб, оскільки `addEventListener` працює для всіх подій, а ім'я події можна передати як параметр.

### Поширені події

Існує [безліч подій](https://developer.mozilla.org/docs/Web/Events), які ви можете використовувати у своїх додатках. Практично будь-яка дія користувача на сторінці викликає подію, що дає вам багато можливостей для створення бажаного досвіду. На щастя, зазвичай вам знадобиться лише кілька основних подій. Ось кілька поширених (включаючи ті, які ми будемо використовувати для створення нашої гри):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): Користувач натиснув на щось, зазвичай кнопку або гіперпосилання
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): Користувач натиснув праву кнопку миші
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): Користувач виділив текст
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): Користувач ввів текст

## Створення гри

Ми створимо гру, щоб дослідити, як працюють події в JavaScript. Наша гра перевірятиме навички друку гравця, що є однією з найбільш недооцінених навичок, які повинен мати кожен розробник. Ми всі повинні практикувати друк! Загальний хід гри виглядатиме так:

- Гравець натискає кнопку "Почати" і отримує цитату для друку
- Гравець друкує цитату якомога швидше у текстовому полі
  - Коли кожне слово завершено, наступне виділяється
  - Якщо гравець робить помилку, текстове поле стає червоним
  - Коли гравець завершує цитату, відображається повідомлення про успіх із витраченим часом

Давайте створимо нашу гру та дізнаємося про події!

### Структура файлів

Нам знадобиться три файли: **index.html**, **script.js** і **style.css**. Почнемо з їх створення, щоб полегшити собі життя.

- Створіть нову папку для своєї роботи, відкривши консоль або термінал і виконавши наступну команду:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- Відкрийте Visual Studio Code

```bash
code .
```

- Додайте три файли до папки у Visual Studio Code з такими іменами:
  - index.html
  - script.js
  - style.css

## Створення інтерфейсу користувача

Якщо ми розглянемо вимоги, то зрозуміємо, що нам знадобиться кілька елементів на нашій HTML-сторінці. Це схоже на рецепт, де нам потрібні інгредієнти:

- Місце для відображення цитати, яку користувач має надрукувати
- Місце для відображення повідомлень, наприклад, повідомлення про успіх
- Текстове поле для введення тексту
- Кнопка "Почати"

Кожен із цих елементів потребуватиме ідентифікаторів, щоб ми могли працювати з ними у нашому JavaScript. Ми також додамо посилання на файли CSS і JavaScript, які ми створимо.

Створіть новий файл із назвою **index.html**. Додайте наступний HTML:

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

### Запуск додатка

Завжди краще розробляти ітеративно, щоб бачити, як усе виглядає. Давайте запустимо наш додаток. У Visual Studio Code є чудове розширення під назвою [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon), яке дозволяє локально хостити ваш додаток і автоматично оновлювати браузер після збереження.

- Встановіть [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon), перейшовши за посиланням і натиснувши **Install**
  - Браузер запропонує відкрити Visual Studio Code, а потім Visual Studio Code запропонує виконати встановлення
  - Перезапустіть Visual Studio Code, якщо буде запропоновано
- Після встановлення у Visual Studio Code натисніть Ctrl-Shift-P (або Cmd-Shift-P), щоб відкрити командний палітру
- Введіть **Live Server: Open with Live Server**
  - Live Server почне хостити ваш додаток
- Відкрийте браузер і перейдіть за адресою **https://localhost:5500**
- Тепер ви повинні побачити створену сторінку!

Додамо трохи функціональності.

## Додавання CSS

Після створення HTML додамо CSS для основного стилю. Нам потрібно виділити слово, яке гравець має друкувати, і змінити колір текстового поля, якщо введено неправильний текст. Ми зробимо це за допомогою двох класів.

Створіть новий файл із назвою **style.css** і додайте наступний синтаксис.

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

✅ Що стосується CSS, ви можете оформити сторінку на свій смак. Приділіть трохи часу, щоб зробити сторінку більш привабливою:

- Виберіть інший шрифт
- Змініть кольори заголовків
- Змініть розміри елементів

## JavaScript

Після створення інтерфейсу користувача настав час зосередитися на JavaScript, який забезпечить логіку. Ми розділимо це на кілька кроків:

- [Створення констант](../../../../4-typing-game/typing-game)
- [Обробник подій для початку гри](../../../../4-typing-game/typing-game)
- [Обробник подій для введення тексту](../../../../4-typing-game/typing-game)

Але спочатку створіть новий файл із назвою **script.js**.

### Додавання констант

Нам знадобиться кілька елементів, щоб полегшити програмування. Знову ж таки, як у рецепті, ось що нам потрібно:

- Масив із переліком усіх цитат
- Порожній масив для зберігання слів поточної цитати
- Місце для зберігання індексу слова, яке гравець зараз друкує
- Час, коли гравець натиснув "Почати"

Нам також знадобляться посилання на елементи інтерфейсу:

- Текстове поле (**typed-value**)
- Відображення цитати (**quote**)
- Повідомлення (**message**)

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

✅ Додайте більше цитат до вашої гри

> **NOTE:** Ми можемо отримувати елементи в будь-який момент у коді за допомогою `document.getElementById`. Оскільки ми будемо часто звертатися до цих елементів, ми уникнемо помилок у рядкових літералах, використовуючи константи. Фреймворки, такі як [Vue.js](https://vuejs.org/) або [React](https://reactjs.org/), можуть допомогти вам краще централізувати ваш код.

Перегляньте відео про використання `const`, `let` і `var`

[![Типи змінних](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Типи змінних")

> 🎥 Натисніть на зображення вище, щоб переглянути відео про змінні.

### Додавання логіки початку гри

Щоб почати гру, гравець натискає "Почати". Звісно, ми не знаємо, коли він це зробить. Тут у гру вступає [обробник подій](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener). Обробник подій дозволяє нам слухати певну подію та виконувати код у відповідь. У нашому випадку ми хочемо виконати код, коли користувач натискає "Почати".

Коли користувач натискає **Почати**, нам потрібно вибрати цитату, налаштувати інтерфейс користувача та відстеження поточного слова й часу. Нижче наведено JavaScript, який вам потрібно додати; ми обговоримо його після блоку коду.

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

Розберемо код!

- Налаштування відстеження слів
  - Використання [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) і [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) дозволяє нам випадково вибрати цитату з масиву `quotes`
  - Ми перетворюємо `quote` на масив `words`, щоб відстежувати слово, яке гравець зараз друкує
  - `wordIndex` встановлюється на 0, оскільки гравець починає з першого слова
- Налаштування інтерфейсу користувача
  - Створюється масив `spanWords`, який містить кожне слово всередині елемента `span`
    - Це дозволяє нам виділяти слово на екрані
  - `join` масиву створює рядок, який ми можемо використати для оновлення `innerHTML` у `quoteElement`
    - Це відображає цитату для гравця
  - Встановлюється `className` першого елемента `span` на `highlight`, щоб виділити його жовтим
  - Очищається `messageElement`, встановлюючи `innerText` у `''`
- Налаштування текстового поля
  - Очищається поточне `value` у `typedValueElement`
  - Встановлюється `focus` на `typedValueElement`
- Запускається таймер, викликаючи `getTime`

### Додавання логіки введення тексту

Коли гравець друкує, викликається подія `input`. Цей обробник подій перевіряє, чи правильно гравець друкує слово, і обробляє поточний стан гри. Поверніться до **script.js** і додайте наступний код у кінець. Ми розберемо його після блоку коду.

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

Розберемо код! Ми починаємо з отримання поточного слова та значення, яке гравець ввів на цей момент. Потім ми використовуємо каскадну логіку, де перевіряємо, чи завершена цитата, чи завершене слово, чи слово правильне, або (нарешті), чи є помилка.

- Цитата завершена, якщо `typedValue` дорівнює `currentWord`, а `wordIndex` дорівнює довжині `words` мінус один
  - Обчислюється `elapsedTime`, віднімаючи `startTime` від поточного часу
  - `elapsedTime` ділиться на 1,000, щоб перетворити мілісекунди на секунди
  - Відображається повідомлення про успіх
- Слово завершене, якщо `typedValue` закінчується пробілом (кінець слова) і `typedValue` дорівнює `currentWord`
  - Встановлюється `value` у `typedElement` на `''`, щоб дозволити друкувати наступне слово
  - Збільшується `wordIndex`, щоб перейти до наступного слова
  - Проходиться по всіх `childNodes` у `quoteElement`, щоб встановити `className` у `''`, повертаючи до стандартного вигляду
  - Встановлюється `className` поточного слова на `highlight`, щоб позначити його як наступне для друку
- Слово наразі друкується правильно (але не завершене), якщо `currentWord` починається з `typedValue`
  - Забезпечується відображення `typedValueElement` у стандартному вигляді, очищаючи `className`
- Якщо ми дійшли до цього моменту, є помилка
  - Встановлюється `className` у `typedValueElement` на `error`

## Тестування додатка

Ви дійшли до кінця! Останній крок — переконатися, що наш додаток працює. Спробуйте! Не хвилюйтеся, якщо виникнуть помилки; **усі розробники** стикаються з помилками. Перегляньте повідомлення та налагоджуйте за потреби.

Натисніть **Почати** і починайте друкувати! Це має виглядати приблизно так, як на анімації, яку ми бачили раніше.

![Анімація гри в дії](../../../../4-typing-game/images/demo.gif)

---

## 🚀 Виклик

Додайте більше функціональності

- Вимикайте обробник подій `input` після завершення гри та знову вмикайте його, коли натискається кнопка
- Вимикайте текстове поле, коли гравець завершує цитату
- Відображайте модальне діалогове вікно з повідомленням про успіх
- Зберігайте найкращі результати за допомогою [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)
## Тест після лекції

[Тест після лекції](https://ff-quizzes.netlify.app/web/quiz/22)

## Огляд та самостійне навчання

Ознайомтеся з [усіма доступними подіями](https://developer.mozilla.org/docs/Web/Events), які веб-браузер надає розробнику, і подумайте про сценарії, в яких ви б використовували кожну з них.

## Завдання

[Створіть нову гру з клавіатурою](assignment.md)

---

**Відмова від відповідальності**:  
Цей документ був перекладений за допомогою сервісу автоматичного перекладу [Co-op Translator](https://github.com/Azure/co-op-translator). Хоча ми прагнемо до точності, будь ласка, майте на увазі, що автоматичні переклади можуть містити помилки або неточності. Оригінальний документ на його рідній мові слід вважати авторитетним джерелом. Для критичної інформації рекомендується професійний людський переклад. Ми не несемо відповідальності за будь-які непорозуміння або неправильні тлумачення, що виникають внаслідок використання цього перекладу.