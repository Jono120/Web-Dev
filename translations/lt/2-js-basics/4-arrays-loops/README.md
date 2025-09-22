<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "9029f96b0e034839c1799f4595e4bb66",
  "translation_date": "2025-08-29T16:54:42+00:00",
  "source_file": "2-js-basics/4-arrays-loops/README.md",
  "language_code": "lt"
}
-->
# JavaScript pagrindai: masyvai ir ciklai

![JavaScript Basics - Arrays](../../../../translated_images/webdev101-js-arrays.439d7528b8a294558d0e4302e448d193f8ad7495cc407539cc81f1afe904b470.lt.png)
> Sketchnote sukūrė [Tomomi Imura](https://twitter.com/girlie_mac)

## Klausimai prieš paskaitą
[Klausimai prieš paskaitą](https://ff-quizzes.netlify.app/web/quiz/13)

Ši pamoka apima JavaScript pagrindus – kalbą, kuri suteikia interaktyvumo internete. Šioje pamokoje sužinosite apie masyvus ir ciklus, kurie naudojami duomenims apdoroti.

[![Masyvai](https://img.youtube.com/vi/1U4qTyq02Xw/0.jpg)](https://youtube.com/watch?v=1U4qTyq02Xw "Masyvai")

[![Ciklai](https://img.youtube.com/vi/Eeh7pxtTZ3k/0.jpg)](https://www.youtube.com/watch?v=Eeh7pxtTZ3k "Ciklai")

> 🎥 Spustelėkite aukščiau esančius paveikslėlius, kad peržiūrėtumėte vaizdo įrašus apie masyvus ir ciklus.

> Šią pamoką galite rasti [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-arrays/?WT.mc_id=academic-77807-sagibbon)!

## Masyvai

Darbas su duomenimis yra dažna užduotis bet kurioje programavimo kalboje, ir tai tampa daug paprasčiau, kai duomenys organizuojami struktūriškai, pavyzdžiui, masyvuose. Masyvuose duomenys saugomi struktūroje, panašioje į sąrašą. Vienas iš pagrindinių masyvų privalumų yra tas, kad viename masyve galite saugoti skirtingų tipų duomenis.

✅ Masyvai yra visur aplink mus! Ar galite sugalvoti realaus gyvenimo pavyzdį, pavyzdžiui, saulės baterijų masyvą?

Masyvo sintaksė yra kvadratinių skliaustų pora.

```javascript
let myArray = [];
```

Tai yra tuščias masyvas, tačiau masyvai gali būti deklaruojami jau užpildyti duomenimis. Keli masyvo elementai atskiriami kableliu.

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
```

Masyvo elementams priskiriama unikali reikšmė, vadinama **indeksu**, kuris yra sveikasis skaičius, priskiriamas pagal jo atstumą nuo masyvo pradžios. Aukščiau pateiktame pavyzdyje eilutės reikšmė „Chocolate“ turi indeksą 0, o „Rocky Road“ indeksas yra 4. Naudokite indeksą su kvadratiniais skliaustais, kad gautumėte, pakeistumėte ar įterptumėte masyvo reikšmes.

✅ Ar jus stebina, kad masyvai prasideda nuo nulio indekso? Kai kuriose programavimo kalbose indeksai prasideda nuo 1. Apie tai yra įdomi istorija, kurią galite [perskaityti Vikipedijoje](https://en.wikipedia.org/wiki/Zero-based_numbering).

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors[2]; //"Vanilla"
```

Indeksą galite panaudoti reikšmei pakeisti, pavyzdžiui, taip:

```javascript
iceCreamFlavors[4] = "Butter Pecan"; //Changed "Rocky Road" to "Butter Pecan"
```

Taip pat galite įterpti naują reikšmę tam tikru indeksu:

```javascript
iceCreamFlavors[5] = "Cookie Dough"; //Added "Cookie Dough"
```

✅ Dažnesnis būdas pridėti reikšmes į masyvą yra naudojant masyvo operatorius, tokius kaip array.push()

Norėdami sužinoti, kiek elementų yra masyve, naudokite `length` savybę.

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors.length; //5
```

✅ Išbandykite patys! Naudokite savo naršyklės konsolę, kad sukurtumėte ir manipuliuotumėte savo sukurtu masyvu.

## Ciklai

Ciklai leidžia atlikti pasikartojančias arba **iteracines** užduotis ir gali sutaupyti daug laiko bei kodo. Kiekviena iteracija gali skirtis savo kintamaisiais, reikšmėmis ir sąlygomis. JavaScript yra įvairių tipų ciklų, kurie turi nedidelių skirtumų, tačiau iš esmės atlieka tą patį: kartoja duomenis.

### For ciklas

`for` ciklas reikalauja 3 dalių, kad galėtų iteruoti:
- `counter` Kintamasis, kuris paprastai inicializuojamas skaičiumi, skaičiuojančiu iteracijų skaičių
- `condition` Išraiška, naudojanti palyginimo operatorius, kad ciklas sustotų, kai reikšmė tampa `false`
- `iteration-expression` Vykdoma kiekvienos iteracijos pabaigoje, paprastai naudojama keisti skaitiklio reikšmę
  
```javascript
// Counting up to 10
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

✅ Paleiskite šį kodą naršyklės konsolėje. Kas nutinka, kai šiek tiek pakeičiate skaitiklį, sąlygą ar iteracijos išraišką? Ar galite priversti jį veikti atgal, sukuriant atgalinį skaičiavimą?

### While ciklas

Skirtingai nuo `for` ciklo sintaksės, `while` ciklai reikalauja tik sąlygos, kuri sustabdys ciklą, kai sąlyga taps `false`. Sąlygos cikluose paprastai remiasi kitomis reikšmėmis, tokiomis kaip skaitikliai, ir turi būti valdomos ciklo metu. Pradinės skaitiklių reikšmės turi būti sukurtos už ciklo ribų, o bet kokios išraiškos, atitinkančios sąlygą, įskaitant skaitiklio keitimą, turi būti palaikomos ciklo viduje.

```javascript
//Counting up to 10
let i = 0;
while (i < 10) {
 console.log(i);
 i++;
}
```

✅ Kodėl rinktumėtės for ciklą, o ne while ciklą? 17 tūkst. žiūrovų turėjo tą patį klausimą StackOverflow, ir kai kurios nuomonės [gali būti jums įdomios](https://stackoverflow.com/questions/39969145/while-loops-vs-for-loops-in-javascript).

## Ciklai ir masyvai

Masyvai dažnai naudojami su ciklais, nes dauguma sąlygų reikalauja masyvo ilgio, kad sustabdytų ciklą, o indeksas taip pat gali būti skaitiklio reikšmė.

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];

for (let i = 0; i < iceCreamFlavors.length; i++) {
  console.log(iceCreamFlavors[i]);
} //Ends when all flavors are printed
```

✅ Eksperimentuokite su ciklu per savo sukurtą masyvą naršyklės konsolėje.

---

## 🚀 Iššūkis

Yra ir kitų būdų iteruoti per masyvus, be for ir while ciklų. Yra [forEach](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach), [for-of](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/for...of) ir [map](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/map). Pakeiskite savo masyvo ciklą naudodami vieną iš šių metodų.

## Klausimai po paskaitos
[Klausimai po paskaitos](https://ff-quizzes.netlify.app/web/quiz/14)

## Apžvalga ir savarankiškas mokymasis

JavaScript masyvai turi daug metodų, kurie yra labai naudingi duomenų manipuliavimui. [Perskaitykite apie šiuos metodus](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array) ir išbandykite kai kuriuos iš jų (pvz., push, pop, slice ir splice) savo sukurtame masyve.

## Užduotis

[Iteruoti per masyvą](assignment.md)

---

**Atsakomybės apribojimas**:  
Šis dokumentas buvo išverstas naudojant AI vertimo paslaugą [Co-op Translator](https://github.com/Azure/co-op-translator). Nors siekiame tikslumo, prašome atkreipti dėmesį, kad automatiniai vertimai gali turėti klaidų ar netikslumų. Originalus dokumentas jo gimtąja kalba turėtų būti laikomas autoritetingu šaltiniu. Kritinei informacijai rekomenduojama profesionali žmogaus vertimo paslauga. Mes neprisiimame atsakomybės už nesusipratimus ar klaidingus interpretavimus, atsiradusius naudojant šį vertimą.