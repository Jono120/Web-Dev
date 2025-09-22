<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1b0aeccb600f83c603cd70cb42df594d",
  "translation_date": "2025-08-29T12:20:09+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "sr"
}
-->
# Прављење игре коришћењем догађаја

## Квиз пре предавања

[Квиз пре предавања](https://ff-quizzes.netlify.app/web/quiz/21)

## Програмирање вођено догађајима

Када правимо апликацију за прегледач, обезбеђујемо графички кориснички интерфејс (GUI) који корисник користи за интеракцију са оним што смо направили. Најчешћи начин интеракције са прегледачем је кликање и куцање у различитим елементима. Изазов са којим се суочавамо као програмери је то што не знамо када ће корисник извршити ове операције!

[Програмирање вођено догађајима](https://en.wikipedia.org/wiki/Event-driven_programming) је назив за врсту програмирања коју треба да користимо да бисмо направили наш GUI. Ако мало разложимо овај израз, видимо да је кључна реч овде **догађај**. [Догађај](https://www.merriam-webster.com/dictionary/event), према Merriam-Webster-у, дефинише се као "нешто што се дешава". Ово савршено описује нашу ситуацију. Знамо да ће се нешто догодити за шта желимо да извршимо неки код као одговор, али не знамо када ће се то десити.

Начин на који означавамо део кода који желимо да извршимо је креирањем функције. Када размишљамо о [процедуралном програмирању](https://en.wikipedia.org/wiki/Procedural_programming), функције се позивају у одређеном редоследу. Исто важи и за програмирање вођено догађајима. Разлика је у томе **како** ће функције бити позване.

Да бисмо обрадили догађаје (кликове на дугмад, куцање итд.), региструјемо **слушаче догађаја**. Слушач догађаја је функција која "ослушкује" да ли ће се догађај десити и извршава се као одговор. Слушачи догађаја могу ажурирати кориснички интерфејс, позивати сервер или радити било шта друго што је потребно као одговор на корисничку акцију. Слушача догађаја додајемо коришћењем [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) и пружањем функције за извршавање.

> **NOTE:** Вреди нагласити да постоји много начина за креирање слушача догађаја. Можете користити анонимне функције или креирати именоване. Можете користити разне пречице, као што је подешавање својства `click`, или коришћење `addEventListener`. У нашем примеру ћемо се фокусирати на `addEventListener` и анонимне функције, јер је то вероватно најчешћа техника коју веб програмери користе. Такође је најфлексибилнија, јер `addEventListener` ради за све догађаје, а име догађаја може бити прослеђено као параметар.

### Уобичајени догађаји

Постоје [десетине догађаја](https://developer.mozilla.org/docs/Web/Events) које можете слушати приликом креирања апликације. Практично све што корисник уради на страници покреће догађај, што вам даје велику моћ да осигурате да добију искуство које желите. Срећом, обично ће вам требати само неколико догађаја. Ево неколико уобичајених (укључујући два која ћемо користити приликом креирања наше игре):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): Корисник је кликнуо на нешто, обично дугме или хипервезу
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): Корисник је кликнуо десним тастером миша
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): Корисник је означио неки текст
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): Корисник је унео неки текст

## Прављење игре

Направићемо игру како бисмо истражили како догађаји функционишу у JavaScript-у. Наша игра ће тестирати вештину куцања играча, што је једна од најпотцењенијих вештина коју сви програмери треба да имају. Сви бисмо требали да вежбамо куцање! Општи ток игре изгледаће овако:

- Играчу се приказује цитат за куцање након што кликне на дугме за почетак
- Играчу се мери време док куца цитат у текстуалном пољу
  - Како заврши сваку реч, следећа се истиче
  - Ако играч направи грешку, текстуално поље постаје црвено
  - Када играч заврши цитат, приказује се порука о успеху са протеклим временом

Хајде да направимо нашу игру и научимо о догађајима!

### Структура фајлова

Биће нам потребна три фајла: **index.html**, **script.js** и **style.css**. Почнимо тако што ћемо их подесити како бисмо себи олакшали посао.

- Направите нови фолдер за свој рад отварањем конзоле или терминала и извршавањем следеће команде:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- Отворите Visual Studio Code

```bash
code .
```

- Додајте три фајла у фолдер у Visual Studio Code-у са следећим именима:
  - index.html
  - script.js
  - style.css

## Креирање корисничког интерфејса

Ако анализирамо захтеве, знамо да ће нам бити потребно неколико елемената на нашој HTML страници. Ово је као рецепт, где су нам потребни састојци:

- Место за приказивање цитата који корисник треба да откуца
- Место за приказивање порука, као што је порука о успеху
- Текстуално поље за куцање
- Дугме за почетак

Сваки од ових елемената ће морати да има ID како бисмо могли да радимо са њима у нашем JavaScript-у. Такође ћемо додати референце на CSS и JavaScript фајлове које ћемо креирати.

Направите нови фајл под именом **index.html**. Додајте следећи HTML:

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

### Покретање апликације

Увек је најбоље развијати итеративно како бисмо видели како ствари изгледају. Покренимо нашу апликацију. Постоји одличан додатак за Visual Studio Code под називом [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) који ће хостовати вашу апликацију локално и освежавати прегледач сваки пут када сачувате.

- Инсталирајте [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) пратећи линк и кликом на **Install**
  - Прегледач ће вас упитати да отворите Visual Studio Code, а затим ће вас Visual Studio Code упитати да извршите инсталацију
  - Поново покрените Visual Studio Code ако буде затражено
- Када је инсталиран, у Visual Studio Code-у притисните Ctrl-Shift-P (или Cmd-Shift-P) да отворите палету команди
- Укуцајте **Live Server: Open with Live Server**
  - Live Server ће почети да хостује вашу апликацију
- Отворите прегледач и идите на **https://localhost:5500**
- Сада би требало да видите страницу коју сте креирали!

Хајде да додамо неку функционалност.

## Додавање CSS-а

Са нашим HTML-ом креираним, додајмо CSS за основно стилизовање. Требаће нам да истакнемо реч коју играч треба да куца и да обојимо текстуално поље ако оно што је укуцано није тачно. Ово ћемо урадити са две класе.

Направите нови фајл под именом **style.css** и додајте следећу синтаксу.

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

✅ Када је у питању CSS, можете распоредити своју страницу како год желите. Одвојите мало времена и учините страницу привлачнијом:

- Изаберите другачији фонт
- Обојите наслове
- Промените величину елемената

## JavaScript

Са нашим корисничким интерфејсом креираним, време је да се фокусирамо на JavaScript који ће обезбедити логику. Ово ћемо поделити на неколико корака:

- [Креирање константи](../../../../4-typing-game/typing-game)
- [Слушач догађаја за почетак игре](../../../../4-typing-game/typing-game)
- [Слушач догађаја за куцање](../../../../4-typing-game/typing-game)

Али прво, направите нови фајл под именом **script.js**.

### Додавање константи

Требаће нам неколико ставки како бисмо себи олакшали програмирање. Опет, слично рецепту, ево шта ће нам требати:

- Низ са списком свих цитата
- Празан низ за чување свих речи тренутног цитата
- Простор за чување индекса речи коју играч тренутно куца
- Време када је играч кликнуо на почетак

Такође ћемо желети референце на елементе корисничког интерфејса:

- Текстуално поље (**typed-value**)
- Приказ цитата (**quote**)
- Порука (**message**)

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

✅ Додајте још цитата у своју игру

> **NOTE:** Елементе можемо дохватити кад год желимо у коду коришћењем `document.getElementById`. Због чињенице да ћемо се често позивати на ове елементе, избећи ћемо грешке са стринг литералима коришћењем константи. Оквири као што су [Vue.js](https://vuejs.org/) или [React](https://reactjs.org/) могу вам помоћи да боље управљате централизацијом вашег кода.

Одвојите минут да погледате видео о коришћењу `const`, `let` и `var`

[![Врсте променљивих](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Врсте променљивих")

> 🎥 Кликните на слику изнад за видео о променљивама.

### Додавање логике за почетак

Да би започео игру, играч ће кликнути на дугме за почетак. Наравно, не знамо када ће кликнути на почетак. Овде на сцену ступа [слушач догађаја](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener). Слушач догађаја ће нам омогућити да слушамо да ли ће се нешто десити (догађај) и извршавамо код као одговор. У нашем случају, желимо да извршимо код када корисник кликне на почетак.

Када корисник кликне на **почетак**, треба да изаберемо цитат, подесимо кориснички интерфејс и подесимо праћење тренутне речи и времена. Испод је JavaScript који треба да додате; објаснићемо га одмах након блока кода.

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

Хајде да разложимо код!

- Подешавање праћења речи
  - Коришћењем [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) и [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) омогућавамо насумичан избор цитата из низа `quotes`
  - Конвертујемо `quote` у низ `words` како бисмо пратили реч коју играч тренутно куца
  - `wordIndex` постављамо на 0, јер играч почиње од прве речи
- Подешавање корисничког интерфејса
  - Креирамо низ `spanWords`, који садржи сваку реч унутар `span` елемента
    - Ово нам омогућава да истакнемо реч на приказу
  - `join` низ како бисмо креирали стринг који можемо користити за ажурирање `innerHTML` на `quoteElement`
    - Ово ће приказати цитат играчу
  - Постављамо `className` првог `span` елемента на `highlight` како бисмо га истакли жутом бојом
  - Чистимо `messageElement` постављањем `innerText` на `''`
- Подешавање текстуалног поља
  - Чистимо тренутну `value` на `typedValueElement`
  - Постављамо `focus` на `typedValueElement`
- Покрећемо тајмер позивањем `getTime`

### Додавање логике за куцање

Док играч куца, подиже се `input` догађај. Овај слушач догађаја проверава да ли играч исправно куца реч и управља тренутним статусом игре. Вратите се на **script.js** и додајте следећи код на крај. Објаснићемо га након тога.

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

Хајде да разложимо код! Почињемо тако што дохватамо тренутну реч и вредност коју је играч до сада укуцао. Затим имамо логику у низу, где проверавамо да ли је цитат завршен, реч завршена, реч тачна или (на крају) да ли постоји грешка.

- Цитат је завршен, што је означено тиме да је `typedValue` једнако `currentWord`, и да је `wordIndex` једнак један мање од `length` низа `words`
  - Израчунавамо `elapsedTime` одузимањем `startTime` од тренутног времена
  - Делимо `elapsedTime` са 1.000 како бисмо конвертовали из милисекунди у секунде
  - Приказујемо поруку о успеху
- Реч је завршена, што је означено тиме да `typedValue` завршава са размаком (крај речи) и да је `typedValue` једнако `currentWord`
  - Постављамо `value` на `typedElement` на `''` како бисмо омогућили куцање следеће речи
  - Инкрементирамо `wordIndex` како бисмо прешли на следећу реч
  - Пролазимо кроз све `childNodes` елемента `quoteElement` како бисмо поставили `className` на `''` и вратили подразумевани приказ
  - Постављамо `className` тренутне речи на `highlight` како бисмо је означили као следећу реч за куцање
- Реч је тренутно исправно укуцана (али није завршена), што је означено тиме да `currentWord` почиње са `typedValue`
  - Осигуравамо да је `typedValueElement` приказан као подразумеван тако што чистимо `className`
- Ако смо стигли до овде, имамо грешку
  - Постављамо `className` на `typedValueElement` на `error`

## Тестирајте своју апликацију

Стигли сте до краја! Последњи корак је да осигурате да ваша апликација ради. Испробајте је! Не брините ако постоје грешке; **сви програмери** праве грешке. Испитајте поруке и дебагујте по потреби.

Кликните на **почетак** и почните да куцате! Требало би да изгледа отприлике као анимација коју смо видели раније.

![Анимација
## Квиз након предавања

[Квиз након предавања](https://ff-quizzes.netlify.app/web/quiz/22)

## Преглед и самостално учење

Прочитајте о [свим доступним догађајима](https://developer.mozilla.org/docs/Web/Events) које веб прегледач пружа програмеру и размислите о ситуацијама у којима бисте користили сваки од њих.

## Задатак

[Направите нову игру на тастатури](assignment.md)

---

**Одрицање од одговорности**:  
Овај документ је преведен коришћењем услуге за превођење помоћу вештачке интелигенције [Co-op Translator](https://github.com/Azure/co-op-translator). Иако настојимо да обезбедимо тачност, молимо вас да имате у виду да аутоматски преводи могу садржати грешке или нетачности. Оригинални документ на изворном језику треба сматрати ауторитативним извором. За критичне информације препоручује се професионални превод од стране људи. Не сносимо одговорност за било каква погрешна тумачења или неспоразуме који могу произаћи из коришћења овог превода.