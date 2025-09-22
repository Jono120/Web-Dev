<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "8a07db14e75ac62f013b7de5df05981d",
  "translation_date": "2025-08-29T10:23:40+00:00",
  "source_file": "7-bank-project/1-template-route/README.md",
  "language_code": "hu"
}
-->
# Banki Alkalmazás Készítése 1. rész: HTML sablonok és útvonalak egy webalkalmazásban

## Előadás előtti kvíz

[Előadás előtti kvíz](https://ff-quizzes.netlify.app/web/quiz/41)

### Bevezetés

A JavaScript böngészőkben való megjelenése óta a weboldalak interaktívabbak és összetettebbek, mint valaha. A webes technológiákat ma már gyakran használják teljes funkcionalitású alkalmazások létrehozására, amelyek közvetlenül a böngészőben futnak, és amelyeket [webalkalmazásoknak](https://en.wikipedia.org/wiki/Web_application) nevezünk. Mivel a webalkalmazások rendkívül interaktívak, a felhasználók nem szeretnének minden művelet végrehajtásakor teljes oldalfrissítést várni. Ezért használják a JavaScriptet az HTML közvetlen frissítésére a DOM segítségével, hogy zökkenőmentesebb felhasználói élményt nyújtsanak.

Ebben a leckében lefektetjük egy banki webalkalmazás alapjait, HTML sablonokat használva több képernyő létrehozásához, amelyeket frissítés nélkül lehet megjeleníteni és frissíteni.

### Előfeltétel

Szükséged lesz egy helyi webszerverre, hogy tesztelhesd a webalkalmazást, amelyet ebben a leckében készítünk. Ha még nincs ilyen, telepítsd a [Node.js](https://nodejs.org) alkalmazást, és használd az `npx lite-server` parancsot a projektmappádból. Ez létrehoz egy helyi webszervert, és megnyitja az alkalmazásodat egy böngészőben.

### Előkészületek

A számítógépeden hozz létre egy `bank` nevű mappát, benne egy `index.html` nevű fájllal. Kezdjük ezzel a HTML [boilerplate](https://en.wikipedia.org/wiki/Boilerplate_code) kóddal:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bank App</title>
  </head>
  <body>
    <!-- This is where you'll work -->
  </body>
</html>
```

---

## HTML sablonok

Ha egy weboldalhoz több képernyőt szeretnél létrehozni, az egyik megoldás az lehet, hogy minden megjeleníteni kívánt képernyőhöz külön HTML fájlt készítesz. Ez a megoldás azonban néhány kényelmetlenséggel jár:

- Az egész HTML-t újra kell tölteni képernyőváltáskor, ami lassú lehet.
- Nehéz adatokat megosztani a különböző képernyők között.

Egy másik megközelítés az, hogy csak egy HTML fájlt használunk, és több [HTML sablont](https://developer.mozilla.org/docs/Web/HTML/Element/template) definiálunk a `<template>` elem segítségével. A sablon egy újrahasznosítható HTML blokk, amelyet a böngésző nem jelenít meg, és amelyet futásidőben kell példányosítani JavaScript segítségével.

### Feladat

Készítsünk egy banki alkalmazást két képernyővel: a bejelentkezési oldallal és a vezérlőpulttal. Először adjunk hozzá egy helyőrző elemet a HTML törzséhez, amelyet az alkalmazás különböző képernyőinek példányosítására fogunk használni:

```html
<div id="app">Loading...</div>
```

Egy `id` attribútumot adunk neki, hogy később könnyebben megtaláljuk JavaScript segítségével.

> Tipp: Mivel ennek az elemnek a tartalma cserélődni fog, elhelyezhetünk benne egy betöltési üzenetet vagy jelzőt, amely az alkalmazás betöltése közben jelenik meg.

Ezután adjuk hozzá a bejelentkezési oldal HTML sablonját. Egyelőre csak egy címet és egy szekciót helyezünk el benne, amely egy navigációs linket tartalmaz.

```html
<template id="login">
  <h1>Bank App</h1>
  <section>
    <a href="/dashboard">Login</a>
  </section>
</template>
```

Ezután adjunk hozzá egy másik HTML sablont a vezérlőpult oldalhoz. Ez az oldal különböző szekciókat tartalmaz:

- Egy fejlécet címmel és kijelentkezési linkkel
- A bankszámla aktuális egyenlegét
- Egy tranzakciós listát, amely egy táblázatban jelenik meg

```html
<template id="dashboard">
  <header>
    <h1>Bank App</h1>
    <a href="/login">Logout</a>
  </header>
  <section>
    Balance: 100$
  </section>
  <section>
    <h2>Transactions</h2>
    <table>
      <thead>
        <tr>
          <th>Date</th>
          <th>Object</th>
          <th>Amount</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
  </section>
</template>
```

> Tipp: HTML sablonok létrehozásakor, ha meg szeretnéd nézni, hogyan fog kinézni, a `<template>` és `</template>` sorokat kikommentelheted, például `<!-- -->` közé helyezve.

✅ Miért használunk `id` attribútumokat a sablonokon? Használhatnánk valami mást, például osztályokat?

## Sablonok megjelenítése JavaScript segítségével

Ha a jelenlegi HTML fájlt megnyitod egy böngészőben, azt fogod látni, hogy a `Loading...` üzenetnél elakad. Ez azért van, mert hozzá kell adnunk némi JavaScript kódot a HTML sablonok példányosításához és megjelenítéséhez.

A sablon példányosítása általában 3 lépésben történik:

1. A sablonelem lekérése a DOM-ban, például a [`document.getElementById`](https://developer.mozilla.org/docs/Web/API/Document/getElementById) használatával.
2. A sablonelem klónozása a [`cloneNode`](https://developer.mozilla.org/docs/Web/API/Node/cloneNode) segítségével.
3. A klónozott elem hozzáadása a DOM-hoz egy látható elem alá, például az [`appendChild`](https://developer.mozilla.org/docs/Web/API/Node/appendChild) használatával.

✅ Miért kell klónoznunk a sablont, mielőtt hozzáadnánk a DOM-hoz? Mi történne, ha kihagynánk ezt a lépést?

### Feladat

Hozz létre egy új fájlt `app.js` néven a projektmappádban, és importáld ezt a fájlt a HTML `<head>` szekciójába:

```html
<script src="app.js" defer></script>
```

Most az `app.js` fájlban hozzunk létre egy új `updateRoute` nevű függvényt:

```js
function updateRoute(templateId) {
  const template = document.getElementById(templateId);
  const view = template.content.cloneNode(true);
  const app = document.getElementById('app');
  app.innerHTML = '';
  app.appendChild(view);
}
```

Itt pontosan az előzőleg leírt 3 lépést hajtjuk végre. A `templateId` azonosítójú sablont példányosítjuk, és annak klónozott tartalmát az alkalmazás helyőrzőjébe helyezzük. Figyeljünk arra, hogy a `cloneNode(true)` metódust használjuk, hogy a sablon teljes alstruktúráját lemásoljuk.

Most hívd meg ezt a függvényt az egyik sablonnal, és nézd meg az eredményt.

```js
updateRoute('login');
```

✅ Mi a célja ennek a kódnak: `app.innerHTML = '';`? Mi történik nélküle?

## Útvonalak létrehozása

Egy webalkalmazás esetében az *útvonalkezelés* azt jelenti, hogy a **URL-eket** meghatározott képernyőkhöz rendeljük, amelyeket meg kell jeleníteni. Egy több HTML fájlt tartalmazó weboldal esetében ez automatikusan történik, mivel a fájlútvonalak tükröződnek az URL-ben. Például, ha ezek a fájlok vannak a projektmappádban:

```
mywebsite/index.html
mywebsite/login.html
mywebsite/admin/index.html
```

Ha létrehozol egy webszervert a `mywebsite` gyökérrel, az URL-leképezés a következő lesz:

```
https://site.com            --> mywebsite/index.html
https://site.com/login.html --> mywebsite/login.html
https://site.com/admin/     --> mywebsite/admin/index.html
```

Azonban a webalkalmazásunk esetében egyetlen HTML fájlt használunk, amely az összes képernyőt tartalmazza, így ez az alapértelmezett viselkedés nem segít nekünk. Ezt a leképezést manuálisan kell létrehoznunk, és JavaScript segítségével kell frissítenünk a megjelenített sablont.

### Feladat

Egy egyszerű objektumot fogunk használni, hogy megvalósítsunk egy [leképezést](https://en.wikipedia.org/wiki/Associative_array) az URL-útvonalak és a sablonjaink között. Add hozzá ezt az objektumot az `app.js` fájl tetejére.

```js
const routes = {
  '/login': { templateId: 'login' },
  '/dashboard': { templateId: 'dashboard' },
};
```

Most módosítsuk egy kicsit az `updateRoute` függvényt. Ahelyett, hogy közvetlenül a `templateId`-t adnánk át argumentumként, először az aktuális URL-t nézzük meg, majd a leképezésünket használjuk a megfelelő sablonazonosító értékének lekérésére. A [`window.location.pathname`](https://developer.mozilla.org/docs/Web/API/Location/pathname) segítségével csak az URL útvonal szakaszát kapjuk meg.

```js
function updateRoute() {
  const path = window.location.pathname;
  const route = routes[path];

  const template = document.getElementById(route.templateId);
  const view = template.content.cloneNode(true);
  const app = document.getElementById('app');
  app.innerHTML = '';
  app.appendChild(view);
}
```

Itt leképeztük a meghatározott útvonalakat a megfelelő sablonokra. Próbáld ki, hogy helyesen működik-e, ha manuálisan megváltoztatod az URL-t a böngésződben.

✅ Mi történik, ha egy ismeretlen útvonalat írsz be az URL-be? Hogyan oldhatnánk meg ezt?

## Navigáció hozzáadása

Az alkalmazás következő lépése, hogy lehetővé tegyük az oldalak közötti navigációt anélkül, hogy manuálisan kellene megváltoztatni az URL-t. Ez két dolgot jelent:

1. Az aktuális URL frissítése
2. A megjelenített sablon frissítése az új URL alapján

A második részről már gondoskodtunk az `updateRoute` függvénnyel, így most ki kell találnunk, hogyan frissítsük az aktuális URL-t.

Ehhez JavaScriptet kell használnunk, pontosabban a [`history.pushState`](https://developer.mozilla.org/docs/Web/API/History/pushState) metódust, amely lehetővé teszi az URL frissítését és egy új bejegyzés létrehozását a böngészési előzményekben, anélkül, hogy újratöltenénk az HTML-t.

> Megjegyzés: Bár a HTML horgonyelem [`<a href>`](https://developer.mozilla.org/docs/Web/HTML/Element/a) önmagában is használható különböző URL-ekre mutató hiperhivatkozások létrehozására, alapértelmezés szerint a böngésző újratölti az HTML-t. Ezt a viselkedést meg kell akadályoznunk, ha egyedi JavaScript-alapú útvonalkezelést használunk, a `preventDefault()` függvény használatával a kattintási eseményen.

### Feladat

Hozzunk létre egy új függvényt, amelyet az alkalmazásban navigációra használhatunk:

```js
function navigate(path) {
  window.history.pushState({}, path, path);
  updateRoute();
}
```

Ez a metódus először frissíti az aktuális URL-t az adott útvonal alapján, majd frissíti a sablont. A `window.location.origin` tulajdonság az URL gyökerét adja vissza, lehetővé téve számunkra, hogy egy adott útvonalból teljes URL-t állítsunk össze.

Most, hogy megvan ez a függvény, foglalkozzunk azzal a problémával, amely akkor merül fel, ha egy útvonal nem egyezik egyetlen meghatározott útvonallal sem. Módosítsuk az `updateRoute` függvényt úgy, hogy hozzáadunk egy visszaesési lehetőséget egy meglévő útvonalhoz, ha nem találunk egyezést.

```js
function updateRoute() {
  const path = window.location.pathname;
  const route = routes[path];

  if (!route) {
    return navigate('/login');
  }

  ...
```

Ha egy útvonal nem található, mostantól a `login` oldalra irányítunk.

Most hozzunk létre egy függvényt, amely az URL-t kapja meg, amikor egy linkre kattintanak, és megakadályozza a böngésző alapértelmezett linkviselkedését:

```js
function onLinkClick(event) {
  event.preventDefault();
  navigate(event.target.href);
}
```

Egészítsük ki a navigációs rendszert azzal, hogy kötéseket adunk a HTML-ben található *Bejelentkezés* és *Kijelentkezés* linkekhez.

```html
<a href="/dashboard" onclick="onLinkClick(event)">Login</a>
...
<a href="/login" onclick="onLinkClick(event)">Logout</a>
```

A fenti `event` objektum rögzíti a `click` eseményt, és továbbítja azt az `onLinkClick` függvényünknek.

A [`onclick`](https://developer.mozilla.org/docs/Web/API/GlobalEventHandlers/onclick) attribútum használatával kösd a `click` eseményt JavaScript kódhoz, itt a `navigate()` függvény hívásához.

Próbálj meg ezekre a linkekre kattintani, most már képesnek kell lenned navigálni az alkalmazás különböző képernyői között.

✅ A `history.pushState` metódus az HTML5 szabvány része, és [minden modern böngészőben](https://caniuse.com/?search=pushState) implementálva van. Ha egy webalkalmazást régebbi böngészőkhöz készítesz, van egy trükk, amelyet használhatsz ennek az API-nak a helyettesítésére: egy [hash (`#`)](https://en.wikipedia.org/wiki/URI_fragment) használatával az útvonal előtt olyan útvonalkezelést valósíthatsz meg, amely a szokásos horgonynavigációval működik, és nem tölti újra az oldalt, mivel eredetileg belső linkek létrehozására szolgált egy oldalon belül.

## A böngésző vissza- és előre gombjainak kezelése

A `history.pushState` használata új bejegyzéseket hoz létre a böngésző navigációs előzményeiben. Ezt úgy ellenőrizheted, hogy lenyomva tartod a böngésződ *vissza gombját*, amelynek valami ilyesmit kell megjelenítenie:

![Navigációs előzmények képernyőkép](../../../../translated_images/history.7fdabbafa521e06455b738d3dafa3ff41d3071deae60ead8c7e0844b9ed987d8.hu.png)

Ha néhányszor rákattintasz a vissza gombra, látni fogod, hogy az aktuális URL megváltozik, és az előzmények frissülnek, de ugyanaz a sablon marad megjelenítve.

Ez azért van, mert az alkalmazás nem tudja, hogy minden alkalommal, amikor az előzmények változnak, meg kell hívnunk az `updateRoute()` függvényt. Ha megnézed a [`history.pushState` dokumentációját](https://developer.mozilla.org/docs/Web/API/History/pushState), láthatod, hogy ha az állapot megváltozik - vagyis egy másik URL-re léptünk -, a [`popstate`](https://developer.mozilla.org/docs/Web/API/Window/popstate_event) esemény aktiválódik. Ezt fogjuk használni a probléma megoldására.

### Feladat

Annak biztosítása érdekében, hogy a megjelenített sablon frissüljön, amikor a böngésző előzményei változnak, csatoljunk egy új függvényt, amely meghívja az `updateRoute()` függvényt. Ezt az `app.js` fájl alján végezzük el:

```js
window.onpopstate = () => updateRoute();
updateRoute();
```

> Megjegyzés: Az `updateRoute` eseménykezelő deklarálásához itt egy [nyílfüggvényt](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Functions/Arrow_functions) használtunk a tömörség érdekében, de egy hagyományos függvény is ugyanúgy működne.

Itt egy frissítő videó a nyílfüggvényekről:

[![Nyílfüggvények](https://img.youtube.com/vi/OP6eEbOj2sc/0.jpg)](https://youtube.com/watch?v=OP6eEbOj2sc "Nyílfüggvények")

> 🎥 Kattints a fenti képre egy videóért a nyílfüggvényekről.

Most próbáld meg használni a böngésződ vissza- és előre gombjait, és ellenőrizd, hogy a megjelenített útvonal helyesen frissül-e ezúttal.

---

## 🚀 Kihívás

Adj hozzá egy új sablont és útvonalat egy harmadik oldalhoz, amely az alkalmazás készítőit mutatja be.

## Előadás utáni kvíz

[Előadás utáni kvíz](https://ff-quizzes.netlify.app/web/quiz/42)

## Áttekintés és önálló tanulás

Az útvonalkezelés a webfejlesztés egyik meglepően trükkös része, különösen, ahogy a web a teljes oldalfrissítési viselkedésekről az Egylapos Alkalmazások oldalfrissítéseire vált. Olvass egy kicsit arról, hogy az [Azure Static Web App szolgáltatás](https://docs.microsoft.com/azure/static-web-apps/routes/?WT.mc_id=academic-77807-sagibbon) hogyan kezeli az útvonalakat. Meg tudod magyarázni, miért szükségesek az ott leírt döntések?

## Feladat

[Fejleszd az útvonalkezelést](assignment.md)

---

**Felelősségkizárás**:  
Ez a dokumentum az [Co-op Translator](https://github.com/Azure/co-op-translator) AI fordítási szolgáltatás segítségével készült. Bár törekszünk a pontosságra, kérjük, vegye figyelembe, hogy az automatikus fordítások hibákat vagy pontatlanságokat tartalmazhatnak. Az eredeti dokumentum az eredeti nyelvén tekintendő hiteles forrásnak. Kritikus információk esetén javasolt a professzionális, emberi fordítás igénybevétele. Nem vállalunk felelősséget a fordítás használatából eredő félreértésekért vagy téves értelmezésekért.