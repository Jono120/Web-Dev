<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1b0aeccb600f83c603cd70cb42df594d",
  "translation_date": "2025-08-29T01:20:26+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "he"
}
-->
# יצירת משחק באמצעות אירועים

## חידון לפני ההרצאה

[חידון לפני ההרצאה](https://ff-quizzes.netlify.app/web/quiz/21)

## תכנות מונחה אירועים

כאשר אנו יוצרים אפליקציה מבוססת דפדפן, אנו מספקים ממשק משתמש גרפי (GUI) למשתמש כדי שיוכל לתקשר עם מה שבנינו. הדרך הנפוצה ביותר לתקשר עם הדפדפן היא באמצעות לחיצה והקלדה על אלמנטים שונים. האתגר שלנו כמפתחים הוא שאיננו יודעים מתי המשתמש יבצע את הפעולות הללו!

[תכנות מונחה אירועים](https://en.wikipedia.org/wiki/Event-driven_programming) הוא השם לסוג התכנות שאנו צריכים לבצע כדי ליצור את ה-GUI שלנו. אם נפרק את הביטוי הזה, נראה שהמילה המרכזית כאן היא **אירוע**. [אירוע](https://www.merriam-webster.com/dictionary/event), לפי Merriam-Webster, מוגדר כ"משהו שקורה". זה מתאר את המצב שלנו בצורה מושלמת. אנו יודעים שמשהו הולך לקרות, עבורו נרצה להפעיל קוד בתגובה, אך איננו יודעים מתי זה יקרה.

הדרך שבה אנו מסמנים קטע קוד שאנו רוצים להפעיל היא על ידי יצירת פונקציה. כשאנו חושבים על [תכנות פרוצדורלי](https://en.wikipedia.org/wiki/Procedural_programming), פונקציות נקראות בסדר מסוים. אותו דבר נכון גם בתכנות מונחה אירועים. ההבדל הוא **איך** הפונקציות ייקראו.

כדי לטפל באירועים (לחיצה על כפתור, הקלדה וכו'), אנו רושמים **מאזיני אירועים**. מאזין אירועים הוא פונקציה שמאזינה לאירוע שמתרחש ומופעלת בתגובה. מאזיני אירועים יכולים לעדכן את ממשק המשתמש, לבצע קריאות לשרת, או כל דבר אחר שצריך לעשות בתגובה לפעולת המשתמש. אנו מוסיפים מאזין אירועים באמצעות [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) ומספקים פונקציה לביצוע.

> **NOTE:** כדאי לציין שיש דרכים רבות ליצור מאזיני אירועים. ניתן להשתמש בפונקציות אנונימיות או ליצור פונקציות עם שם. ניתן להשתמש בקיצורי דרך שונים, כמו הגדרת המאפיין `click` או שימוש ב-`addEventListener`. בתרגיל שלנו נתמקד ב-`addEventListener` ובפונקציות אנונימיות, מכיוון שזה כנראה הטכניקה הנפוצה ביותר שמפתחים משתמשים בה. זה גם הכי גמיש, מכיוון ש-`addEventListener` עובד עבור כל האירועים, ושם האירוע יכול להינתן כפרמטר.

### אירועים נפוצים

ישנם [עשרות אירועים](https://developer.mozilla.org/docs/Web/Events) שניתן להאזין להם בעת יצירת אפליקציה. למעשה, כל דבר שמשתמש עושה בדף מעלה אירוע, מה שנותן לך הרבה כוח לוודא שהוא מקבל את החוויה הרצויה. למרבה המזל, בדרך כלל תצטרך רק קומץ קטן של אירועים. הנה כמה נפוצים (כולל שניים שנשתמש בהם ביצירת המשחק שלנו):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): המשתמש לחץ על משהו, בדרך כלל כפתור או קישור
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): המשתמש לחץ על כפתור העכבר הימני
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): המשתמש סימן טקסט
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): המשתמש הזין טקסט

## יצירת המשחק

אנו הולכים ליצור משחק כדי לחקור כיצד אירועים עובדים ב-JavaScript. המשחק שלנו יבדוק את מיומנות ההקלדה של השחקן, שהיא אחת המיומנויות הכי פחות מוערכות שכל מפתח צריך. כולנו צריכים לתרגל את ההקלדה שלנו! הזרימה הכללית של המשחק תיראה כך:

- השחקן לוחץ על כפתור ההתחלה ומוצגת לו ציטוט להקלדה
- השחקן מקליד את הציטוט במהירות האפשרית בתיבת טקסט
  - בכל פעם שמילה מושלמת, המילה הבאה מודגשת
  - אם לשחקן יש שגיאת הקלדה, תיבת הטקסט מתעדכנת לאדום
  - כאשר השחקן משלים את הציטוט, מוצגת הודעת הצלחה עם הזמן שחלף

בואו נבנה את המשחק שלנו ונלמד על אירועים!

### מבנה הקבצים

נזדקק לשלושה קבצים בסך הכול: **index.html**, **script.js** ו-**style.css**. בואו נתחיל בהגדרתם כדי להקל עלינו.

- צרו תיקייה חדשה לעבודה שלכם על ידי פתיחת חלון קונסול או טרמינל והקלדת הפקודה הבאה:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- פתחו את Visual Studio Code

```bash
code .
```

- הוסיפו שלושה קבצים לתיקייה ב-Visual Studio Code עם השמות הבאים:
  - index.html
  - script.js
  - style.css

## יצירת ממשק המשתמש

אם נבחן את הדרישות, אנו יודעים שנצטרך כמה אלמנטים בדף ה-HTML שלנו. זה קצת כמו מתכון, שבו אנו צריכים כמה מרכיבים:

- מקום להציג את הציטוט שהמשתמש צריך להקליד
- מקום להציג הודעות, כמו הודעת הצלחה
- תיבת טקסט להקלדה
- כפתור התחלה

לכל אחד מהם נצטרך להוסיף מזהים (IDs) כדי שנוכל לעבוד איתם ב-JavaScript שלנו. נוסיף גם הפניות לקבצי ה-CSS וה-JavaScript שניצור.

צרו קובץ חדש בשם **index.html**. הוסיפו את ה-HTML הבא:

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

### הפעלת האפליקציה

תמיד עדיף לפתח באופן איטרטיבי כדי לראות איך הדברים נראים. בואו נפעיל את האפליקציה שלנו. יש תוסף נהדר ל-Visual Studio Code בשם [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) שיארח את האפליקציה שלכם מקומית וירענן את הדפדפן בכל פעם שתשמרו.

- התקינו את [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) על ידי לחיצה על הקישור ולחיצה על **Install**
  - הדפדפן יבקש מכם לפתוח את Visual Studio Code, ואז Visual Studio Code יבקש מכם לבצע את ההתקנה
  - אתחלו את Visual Studio Code אם תתבקשו
- לאחר ההתקנה, ב-Visual Studio Code, לחצו על Ctrl-Shift-P (או Cmd-Shift-P) כדי לפתוח את לוח הפקודות
- הקלידו **Live Server: Open with Live Server**
  - Live Server יתחיל לארח את האפליקציה שלכם
- פתחו דפדפן ונווטו לכתובת **https://localhost:5500**
- כעת אמור להופיע הדף שיצרתם!

בואו נוסיף קצת פונקציונליות.

## הוספת ה-CSS

עם יצירת ה-HTML שלנו, נוסיף את ה-CSS לעיצוב הבסיסי. נצטרך להדגיש את המילה שהשחקן צריך להקליד ולצבוע את תיבת הטקסט אם מה שהוקלד שגוי. נעשה זאת באמצעות שתי מחלקות.

צרו קובץ חדש בשם **style.css** והוסיפו את התחביר הבא.

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

✅ כשמדובר ב-CSS, אתם יכולים לעצב את הדף שלכם איך שתרצו. קחו קצת זמן ותעשו את הדף יותר מושך:

- בחרו גופן שונה
- צבעו את הכותרות
- שנו את גודל האלמנטים

## JavaScript

עם יצירת ממשק המשתמש שלנו, הגיע הזמן להתמקד ב-JavaScript שיספק את הלוגיקה. נחלק את זה לכמה שלבים:

- [יצירת הקבועים](../../../../4-typing-game/typing-game)
- [מאזין אירועים להתחלת המשחק](../../../../4-typing-game/typing-game)
- [מאזין אירועים להקלדה](../../../../4-typing-game/typing-game)

אבל קודם, צרו קובץ חדש בשם **script.js**.

### יצירת הקבועים

נזדקק לכמה פריטים כדי להקל עלינו בתכנות. שוב, בדומה למתכון, הנה מה שנצטרך:

- מערך עם רשימת כל הציטוטים
- מערך ריק לאחסון כל המילים של הציטוט הנוכחי
- מקום לאחסון האינדקס של המילה שהשחקן מקליד כרגע
- הזמן שבו השחקן לחץ על התחלה

נרצה גם הפניות לאלמנטים בממשק המשתמש:

- תיבת הטקסט (**typed-value**)
- תצוגת הציטוט (**quote**)
- ההודעה (**message**)

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

✅ הוסיפו עוד ציטוטים למשחק שלכם

> **NOTE:** אנו יכולים לאחזר את האלמנטים בכל פעם שנרצה בקוד באמצעות `document.getElementById`. מכיוון שנפנה לאלמנטים הללו באופן קבוע, נשתמש בקבועים כדי להימנע משגיאות הקלדה במחרוזות. מסגרות כמו [Vue.js](https://vuejs.org/) או [React](https://reactjs.org/) יכולות לעזור לכם לנהל טוב יותר את ריכוז הקוד שלכם.

קחו רגע לצפות בסרטון על שימוש ב-`const`, `let` ו-`var`

[![סוגי משתנים](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "סוגי משתנים")

> 🎥 לחצו על התמונה למעלה לצפייה בסרטון על משתנים.

### הוספת לוגיקת התחלה

כדי להתחיל את המשחק, השחקן ילחץ על התחלה. כמובן, איננו יודעים מתי הוא ילחץ על התחלה. כאן נכנס לתמונה [מאזין אירועים](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener). מאזין אירועים יאפשר לנו להאזין למשהו שמתרחש (אירוע) ולהפעיל קוד בתגובה. במקרה שלנו, נרצה להפעיל קוד כאשר המשתמש לוחץ על התחלה.

כאשר המשתמש לוחץ על **start**, נצטרך לבחור ציטוט, להגדיר את ממשק המשתמש ולהגדיר מעקב אחר המילה הנוכחית והזמן. להלן ה-JavaScript שתצטרכו להוסיף; נדון בו מיד לאחר קטע הקוד.

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

בואו נפרק את הקוד!

- הגדרת מעקב המילים
  - שימוש ב-[Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) וב-[Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) מאפשר לנו לבחור באופן אקראי ציטוט מתוך המערך `quotes`
  - אנו ממירים את ה-`quote` למערך של `words` כדי שנוכל לעקוב אחר המילה שהשחקן מקליד כרגע
  - `wordIndex` מוגדר ל-0, מכיוון שהשחקן יתחיל במילה הראשונה
- הגדרת ממשק המשתמש
  - יצירת מערך של `spanWords`, שמכיל כל מילה בתוך אלמנט `span`
    - זה יאפשר לנו להדגיש את המילה בתצוגה
  - שימוש ב-`join` ליצירת מחרוזת שנוכל להשתמש בה כדי לעדכן את ה-`innerHTML` של `quoteElement`
    - זה יציג את הציטוט לשחקן
  - הגדרת `className` של אלמנט ה-`span` הראשון ל-`highlight` כדי להדגיש אותו בצהוב
  - ניקוי `messageElement` על ידי הגדרת `innerText` ל-`''`
- הגדרת תיבת הטקסט
  - ניקוי ה-`value` הנוכחי של `typedValueElement`
  - הגדרת ה-`focus` ל-`typedValueElement`
- התחלת הטיימר על ידי קריאה ל-`getTime`

### הוספת לוגיקת הקלדה

כאשר השחקן מקליד, יופעל אירוע `input`. מאזין האירועים הזה יבדוק שהשחקן מקליד את המילה בצורה נכונה ויטפל במצב הנוכחי של המשחק. חזרו ל-**script.js** והוסיפו את הקוד הבא בסוף. נפרק אותו לאחר מכן.

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

בואו נפרק את הקוד! אנו מתחילים באחזור המילה הנוכחית והערך שהשחקן הקליד עד כה. לאחר מכן יש לנו לוגיקה מדורגת, שבה אנו בודקים אם הציטוט הושלם, המילה הושלמה, המילה נכונה, או (לבסוף), אם יש שגיאה.

- הציטוט הושלם, מצוין על ידי כך ש-`typedValue` שווה ל-`currentWord`, ו-`wordIndex` שווה לאחד פחות מ-`length` של `words`
  - חישוב `elapsedTime` על ידי חיסור `startTime` מהזמן הנוכחי
  - חלוקת `elapsedTime` ב-1,000 כדי להמיר ממילישניות לשניות
  - הצגת הודעת הצלחה
- המילה הושלמה, מצוין על ידי כך ש-`typedValue` מסתיים ברווח (סוף מילה) ו-`typedValue` שווה ל-`currentWord`
  - הגדרת `value` של `typedElement` ל-`''` כדי לאפשר הקלדת המילה הבאה
  - הגדלת `wordIndex` כדי לעבור למילה הבאה
  - מעבר על כל ה-`childNodes` של `quoteElement` כדי להגדיר `className` ל-`''` כדי להחזיר לתצוגה ברירת מחדל
  - הגדרת `className` של המילה הנוכחית ל-`highlight` כדי לסמן אותה כמילה הבאה להקלדה
- המילה מוקלדת נכון (אך לא הושלמה), מצוין על ידי כך ש-`currentWord` מתחיל ב-`typedValue`
  - הבטחת תצוגת `typedValueElement` כברירת מחדל על ידי ניקוי `className`
- אם הגענו עד כאן, יש שגיאה
  - הגדרת `className` של `typedValueElement` ל-`error`

## בדיקת האפליקציה

הגעתם לסוף! השלב האחרון הוא לוודא שהאפליקציה שלנו עובדת. נסו אותה! אל תדאגו אם יש שגיאות; **לכל המפתחים** יש שגיאות. בדקו את ההודעות ותקנו לפי הצורך.

לחצו על **start**, והתחילו להקליד! זה אמור להיראות קצת כמו האנימציה שראינו קודם.

![אנימציה של המשחק בפעולה](../../../../4-typing-game/images/demo.gif)

---

## 🚀 אתגר

הוסיפו עוד פונקציונליות

- השבתת מאזין אירועי `input` בסיום המשחק, והפעלתו מחדש כאשר לוחצים על הכפתור
- השבתת תיבת הטקסט כאשר השחקן משלים את הציטוט
- הצגת תיבת דיאלוג מודאלית עם הודעת ההצלחה
- שמירת תוצאות גבוהות באמצעות [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)
## חידון לאחר ההרצאה

[חידון לאחר ההרצאה](https://ff-quizzes.netlify.app/web/quiz/22)

## סקירה ולמידה עצמית

קראו על [כל האירועים הזמינים](https://developer.mozilla.org/docs/Web/Events) למפתח דרך דפדפן האינטרנט, ושקלו את התרחישים שבהם הייתם משתמשים בכל אחד מהם.

## משימה

[צרו משחק מקלדת חדש](assignment.md)

---

**כתב ויתור**:  
מסמך זה תורגם באמצעות שירות תרגום מבוסס בינה מלאכותית [Co-op Translator](https://github.com/Azure/co-op-translator). למרות שאנו שואפים לדיוק, יש לקחת בחשבון שתרגומים אוטומטיים עשויים להכיל שגיאות או אי-דיוקים. המסמך המקורי בשפתו המקורית נחשב למקור הסמכותי. למידע קריטי, מומלץ להשתמש בתרגום מקצועי על ידי מתרגם אנושי. איננו נושאים באחריות לכל אי-הבנה או פרשנות שגויה הנובעת משימוש בתרגום זה.