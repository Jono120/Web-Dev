<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1b0aeccb600f83c603cd70cb42df594d",
  "translation_date": "2025-08-29T08:21:53+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "da"
}
-->
# Oprettelse af et spil ved hjælp af events

## Quiz før forelæsning

[Quiz før forelæsning](https://ff-quizzes.netlify.app/web/quiz/21)

## Event-drevet programmering

Når vi skaber en browserbaseret applikation, leverer vi en grafisk brugergrænseflade (GUI), som brugeren kan bruge til at interagere med det, vi har bygget. Den mest almindelige måde at interagere med browseren på er ved at klikke og skrive i forskellige elementer. Udfordringen som udvikler er, at vi ikke ved, hvornår de vil udføre disse handlinger!

[Event-drevet programmering](https://en.wikipedia.org/wiki/Event-driven_programming) er navnet på den type programmering, vi skal bruge for at skabe vores GUI. Hvis vi bryder denne sætning lidt ned, ser vi, at kerneordet her er **event**. [Event](https://www.merriam-webster.com/dictionary/event), ifølge Merriam-Webster, defineres som "noget, der sker". Dette beskriver vores situation perfekt. Vi ved, at noget vil ske, som vi ønsker at udføre kode som svar på, men vi ved ikke, hvornår det vil finde sted.

Måden, vi markerer en sektion af kode, vi ønsker at udføre, er ved at oprette en funktion. Når vi tænker på [procedureprogrammering](https://en.wikipedia.org/wiki/Procedural_programming), kaldes funktioner i en specifik rækkefølge. Det samme gælder for event-drevet programmering. Forskellen er **hvordan** funktionerne kaldes.

For at håndtere events (knapklik, indtastning osv.) registrerer vi **event listeners**. En event listener er en funktion, der lytter efter, at en event opstår, og udfører noget som svar. Event listeners kan opdatere UI, foretage kald til serveren eller hvad der ellers skal gøres som svar på brugerens handling. Vi tilføjer en event listener ved at bruge [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) og angive en funktion, der skal udføres.

> **NOTE:** Det er værd at fremhæve, at der er mange måder at oprette event listeners på. Du kan bruge anonyme funktioner eller oprette navngivne funktioner. Du kan bruge forskellige genveje, som at sætte `click`-egenskaben eller bruge `addEventListener`. I vores øvelse vil vi fokusere på `addEventListener` og anonyme funktioner, da det sandsynligvis er den mest almindelige teknik, webudviklere bruger. Det er også den mest fleksible, da `addEventListener` fungerer for alle events, og event-navnet kan angives som en parameter.

### Almindelige events

Der er [mange events](https://developer.mozilla.org/docs/Web/Events) tilgængelige, som du kan lytte til, når du opretter en applikation. Grundlæggende udløser alt, hvad en bruger gør på en side, en event, hvilket giver dig stor magt til at sikre, at de får den oplevelse, du ønsker. Heldigvis har du normalt kun brug for en lille håndfuld events. Her er nogle almindelige (inklusive de to, vi vil bruge, når vi opretter vores spil):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): Brugeren klikkede på noget, typisk en knap eller et hyperlink
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): Brugeren klikkede på højre museknap
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): Brugeren markerede noget tekst
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): Brugeren indtastede noget tekst

## Oprettelse af spillet

Vi skal oprette et spil for at udforske, hvordan events fungerer i JavaScript. Vores spil vil teste en spillers skrivefærdigheder, som er en af de mest undervurderede færdigheder, alle udviklere bør have. Vi bør alle øve os i at skrive! Den generelle spilflow vil se sådan ud:

- Spilleren klikker på startknappen og præsenteres for et citat, de skal skrive
- Spilleren skriver citatet så hurtigt som muligt i en tekstboks
  - Når hvert ord er færdiggjort, fremhæves det næste
  - Hvis spilleren laver en tastefejl, bliver tekstboksen rød
  - Når spilleren fuldfører citatet, vises en succesmeddelelse med den forløbne tid

Lad os bygge vores spil og lære om events!

### Filstruktur

Vi skal bruge i alt tre filer: **index.html**, **script.js** og **style.css**. Lad os starte med at sætte dem op for at gøre livet lidt lettere for os.

- Opret en ny mappe til dit arbejde ved at åbne en konsol eller terminal og udføre følgende kommando:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- Åbn Visual Studio Code

```bash
code .
```

- Tilføj tre filer til mappen i Visual Studio Code med følgende navne:
  - index.html
  - script.js
  - style.css

## Opret brugergrænsefladen

Hvis vi ser på kravene, ved vi, at vi skal bruge en håndfuld elementer på vores HTML-side. Dette er lidt som en opskrift, hvor vi har brug for nogle ingredienser:

- Et sted at vise citatet, som brugeren skal skrive
- Et sted at vise meddelelser, som en succesmeddelelse
- En tekstboks til indtastning
- En startknap

Hvert af disse elementer skal have ID'er, så vi kan arbejde med dem i vores JavaScript. Vi tilføjer også referencer til de CSS- og JavaScript-filer, vi skal oprette.

Opret en ny fil med navnet **index.html**. Tilføj følgende HTML:

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

### Start applikationen

Det er altid bedst at udvikle iterativt for at se, hvordan tingene ser ud. Lad os starte vores applikation. Der er en fantastisk udvidelse til Visual Studio Code kaldet [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon), som både hoster din applikation lokalt og opdaterer browseren, hver gang du gemmer.

- Installer [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) ved at følge linket og klikke på **Install**
  - Du vil blive bedt om at åbne Visual Studio Code via browseren og derefter udføre installationen i Visual Studio Code
  - Genstart Visual Studio Code, hvis det bliver bedt om det
- Når det er installeret, skal du i Visual Studio Code trykke på Ctrl-Shift-P (eller Cmd-Shift-P) for at åbne kommandopaletten
- Skriv **Live Server: Open with Live Server**
  - Live Server vil begynde at hoste din applikation
- Åbn en browser og naviger til **https://localhost:5500**
- Du skulle nu kunne se den side, du har oprettet!

Lad os tilføje noget funktionalitet.

## Tilføj CSS

Med vores HTML oprettet, lad os tilføje CSS til grundlæggende styling. Vi skal fremhæve det ord, spilleren skal skrive, og farve tekstboksen, hvis det, de har skrevet, er forkert. Vi gør dette med to klasser.

Opret en ny fil med navnet **style.css**, og tilføj følgende syntaks.

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

✅ Når det kommer til CSS, kan du designe din side, som du vil. Brug lidt tid på at gøre siden mere tiltalende:

- Vælg en anden skrifttype
- Farvelæg overskrifterne
- Tilpas størrelsen på elementerne

## JavaScript

Med vores UI oprettet er det tid til at fokusere på JavaScript, som vil levere logikken. Vi vil opdele dette i en håndfuld trin:

- [Opret konstanterne](../../../../4-typing-game/typing-game)
- [Event listener til at starte spillet](../../../../4-typing-game/typing-game)
- [Event listener til indtastning](../../../../4-typing-game/typing-game)

Men først skal du oprette en ny fil med navnet **script.js**.

### Tilføj konstanterne

Vi skal bruge nogle elementer for at gøre vores programmering lettere. Igen, ligesom en opskrift, her er hvad vi skal bruge:

- En array med listen over alle citater
- En tom array til at gemme alle ordene for det aktuelle citat
- Et sted til at gemme indekset for det ord, spilleren aktuelt skriver
- Tiden, hvor spilleren klikkede på start

Vi skal også have referencer til UI-elementerne:

- Tekstboksen (**typed-value**)
- Citatvisningen (**quote**)
- Meddelelsen (**message**)

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

✅ Tilføj flere citater til dit spil

> **NOTE:** Vi kan hente elementerne, når som helst vi vil i koden, ved at bruge `document.getElementById`. Fordi vi ofte vil referere til disse elementer, undgår vi tastefejl med strenglitteraler ved at bruge konstanter. Frameworks som [Vue.js](https://vuejs.org/) eller [React](https://reactjs.org/) kan hjælpe dig med bedre at centralisere din kode.

Tag et øjeblik til at se en video om brugen af `const`, `let` og `var`.

[![Typer af variabler](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Typer af variabler")

> 🎥 Klik på billedet ovenfor for en video om variabler.

### Tilføj startlogik

For at starte spillet vil spilleren klikke på start. Selvfølgelig ved vi ikke, hvornår de vil klikke på start. Dette er, hvor en [event listener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) kommer i spil. En event listener giver os mulighed for at lytte efter, at noget sker (en event), og udføre kode som svar. I vores tilfælde ønsker vi at udføre kode, når brugeren klikker på start.

Når brugeren klikker på **start**, skal vi vælge et citat, opsætte brugergrænsefladen og opsætte sporing for det aktuelle ord og tidtagning. Nedenfor er den JavaScript, du skal tilføje; vi diskuterer det lige efter scriptblokken.

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

Lad os bryde koden ned!

- Opsætning af ordsporing
  - Brug af [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) og [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) giver os mulighed for tilfældigt at vælge et citat fra `quotes`-arrayet
  - Vi konverterer `quote` til en array af `words`, så vi kan spore det ord, spilleren aktuelt skriver
  - `wordIndex` sættes til 0, da spilleren starter med det første ord
- Opsætning af UI
  - Opret en array af `spanWords`, som indeholder hvert ord inde i et `span`-element
    - Dette giver os mulighed for at fremhæve ordet på skærmen
  - `join` arrayet for at skabe en streng, som vi kan bruge til at opdatere `innerHTML` på `quoteElement`
    - Dette vil vise citatet til spilleren
  - Sæt `className` for det første `span`-element til `highlight` for at fremhæve det som gult
  - Rens `messageElement` ved at sætte `innerText` til `''`
- Opsætning af tekstboksen
  - Ryd den aktuelle `value` på `typedValueElement`
  - Sæt `focus` til `typedValueElement`
- Start timeren ved at kalde `getTime`

### Tilføj indtastningslogik

Når spilleren skriver, vil en `input`-event blive udløst. Denne event listener vil kontrollere, om spilleren skriver ordet korrekt, og håndtere spillets aktuelle status. Tilføj følgende kode til slutningen af **script.js**. Vi vil bryde det ned bagefter.

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

Lad os bryde koden ned! Vi starter med at hente det aktuelle ord og den værdi, spilleren har skrevet indtil videre. Derefter har vi en kaskadelogik, hvor vi tjekker, om citatet er fuldført, ordet er fuldført, ordet er korrekt, eller (endelig), om der er en fejl.

- Citatet er fuldført, angivet ved, at `typedValue` er lig med `currentWord`, og `wordIndex` er lig med en mindre end længden af `words`
  - Beregn `elapsedTime` ved at trække `startTime` fra den aktuelle tid
  - Divider `elapsedTime` med 1.000 for at konvertere fra millisekunder til sekunder
  - Vis en succesmeddelelse
- Ordet er fuldført, angivet ved, at `typedValue` slutter med et mellemrum (slutningen af et ord), og `typedValue` er lig med `currentWord`
  - Sæt `value` på `typedElement` til `''` for at tillade, at det næste ord kan skrives
  - Inkrementer `wordIndex` for at gå videre til det næste ord
  - Gennemgå alle `childNodes` af `quoteElement` for at sætte `className` til `''` for at vende tilbage til standardvisning
  - Sæt `className` for det aktuelle ord til `highlight` for at markere det som det næste ord, der skal skrives
- Ordet er aktuelt skrevet korrekt (men ikke fuldført), angivet ved, at `currentWord` starter med `typedValue`
  - Sørg for, at `typedValueElement` vises som standard ved at rydde `className`
- Hvis vi er nået hertil, har vi en fejl
  - Sæt `className` på `typedValueElement` til `error`

## Test din applikation

Du er nået til slutningen! Det sidste trin er at sikre, at vores applikation fungerer. Prøv det! Vær ikke bekymret, hvis der er fejl; **alle udviklere** oplever fejl. Undersøg meddelelserne og fejlret efter behov.

Klik på **start**, og begynd at skrive! Det skulle se lidt ud som animationen, vi så tidligere.

![Animation af spillet i aktion](../../../../4-typing-game/images/demo.gif)

---

## 🚀 Udfordring

Tilføj mere funktionalitet

- Deaktiver `input`-event listeneren ved fuldførelse, og aktiver den igen, når knappen klikkes
- Deaktiver tekstboksen, når spilleren fuldfører citatet
- Vis en modal dialogboks med succesmeddelelsen
- Gem high scores ved hjælp af [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)
## Quiz efter forelæsning

[Quiz efter forelæsning](https://ff-quizzes.netlify.app/web/quiz/22)

## Gennemgang & Selvstudie

Læs om [alle de tilgængelige hændelser](https://developer.mozilla.org/docs/Web/Events) for udviklere via webbrowseren, og overvej de scenarier, hvor du ville bruge hver enkelt.

## Opgave

[Skab et nyt tastaturspil](assignment.md)

---

**Ansvarsfraskrivelse**:  
Dette dokument er blevet oversat ved hjælp af AI-oversættelsestjenesten [Co-op Translator](https://github.com/Azure/co-op-translator). Selvom vi bestræber os på nøjagtighed, skal du være opmærksom på, at automatiserede oversættelser kan indeholde fejl eller unøjagtigheder. Det originale dokument på dets oprindelige sprog bør betragtes som den autoritative kilde. For kritisk information anbefales professionel menneskelig oversættelse. Vi påtager os intet ansvar for misforståelser eller fejltolkninger, der måtte opstå som følge af brugen af denne oversættelse.