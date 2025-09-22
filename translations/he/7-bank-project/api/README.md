<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "9884f8c8a61cf56214450f8b16a094ce",
  "translation_date": "2025-08-27T20:55:23+00:00",
  "source_file": "7-bank-project/api/README.md",
  "language_code": "he"
}
-->
# API של בנק

> API של בנק שנבנה באמצעות [Node.js](https://nodejs.org) + [Express](https://expressjs.com/).

ה-API כבר נבנה עבורכם ואינו חלק מהתרגיל.

עם זאת, אם אתם מעוניינים ללמוד כיצד לבנות API כזה, תוכלו לעקוב אחר סדרת הסרטונים הזו: https://aka.ms/NodeBeginner (סרטונים 17 עד 21 מכסים בדיוק את ה-API הזה).

תוכלו גם להסתכל על מדריך אינטראקטיבי זה: https://aka.ms/learn/express-api

## הפעלת השרת

ודאו ש-[Node.js](https://nodejs.org) מותקן אצלכם.

1. בצעו Git clone לריפו הזה [The Web-Dev-For-Beginners](https://github.com/microsoft/Web-Dev-For-Beginners).
2. פתחו את הטרמינל שלכם ונווטו לתיקיית `Web-Dev-For-Beginners/7-bank-project/api`.
3. הריצו `npm install` והמתינו עד שכל החבילות יותקנו (יכול לקחת זמן בהתאם לאיכות חיבור האינטרנט שלכם).
4. כשההתקנה מסתיימת, הריצו `npm start` ואתם מוכנים להתחיל.

השרת אמור להתחיל להאזין על פורט `5000`.
*שרת זה ירוץ יחד עם הטרמינל של שרת האפליקציה הראשי של הבנק (מאזין על פורט `3000`), אל תסגרו אותו.*

> הערה: כל הרשומות נשמרות בזיכרון ואינן נשמרות באופן קבוע, כך שכאשר השרת נעצר כל הנתונים נמחקים.

## פרטי ה-API

נתיב                                        | תיאור
---------------------------------------------|------------------------------------
GET    /api/                                 | קבלת מידע על השרת
POST   /api/accounts/                        | יצירת חשבון, לדוגמה: `{ user: 'Yohan', description: 'My budget', currency: 'EUR', balance: 100 }`
GET    /api/accounts/:user                   | קבלת כל הנתונים עבור החשבון שצוין
DELETE /api/accounts/:user                   | מחיקת החשבון שצוין
POST   /api/accounts/:user/transactions      | הוספת טרנזקציה, לדוגמה: `{ date: '2020-07-23T18:25:43.511Z', object: 'Bought a book', amount: -20 }`
DELETE  /api/accounts/:user/transactions/:id | מחיקת טרנזקציה שצוינה

---

**כתב ויתור**:  
מסמך זה תורגם באמצעות שירות תרגום מבוסס בינה מלאכותית [Co-op Translator](https://github.com/Azure/co-op-translator). למרות שאנו שואפים לדיוק, יש לקחת בחשבון שתרגומים אוטומטיים עשויים להכיל שגיאות או אי דיוקים. המסמך המקורי בשפתו המקורית צריך להיחשב כמקור סמכותי. עבור מידע קריטי, מומלץ להשתמש בתרגום מקצועי על ידי אדם. איננו נושאים באחריות לאי הבנות או לפרשנויות שגויות הנובעות משימוש בתרגום זה.