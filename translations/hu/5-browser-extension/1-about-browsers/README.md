<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2326d04e194a10aa760b51f5e5a1f61d",
  "translation_date": "2025-08-29T10:24:31+00:00",
  "source_file": "5-browser-extension/1-about-browsers/README.md",
  "language_code": "hu"
}
-->
# Böngészőbővítmény projekt 1. rész: Minden a böngészőkről

![Böngésző sketchnote](../../../../translated_images/browser.60317c9be8b7f84adce43e30bff8d47a1ae15793beab762317b2bc6b74337c1a.hu.jpg)
> Sketchnote készítette: [Wassim Chegham](https://dev.to/wassimchegham/ever-wondered-what-happens-when-you-type-in-a-url-in-an-address-bar-in-a-browser-3dob)

## Előadás előtti kvíz

[Előadás előtti kvíz](https://ff-quizzes.netlify.app/web/quiz/23)

### Bevezetés

A böngészőbővítmények további funkciókat adnak a böngészőhöz. De mielőtt elkezdenéd egyet készíteni, érdemes kicsit többet megtudni arról, hogyan működnek a böngészők.

### A böngészőről

Ebben a leckesorozatban megtanulod, hogyan készíts böngészőbővítményt, amely működik Chrome, Firefox és Edge böngészőkben. Ebben a részben felfedezed, hogyan működnek a böngészők, és felépíted a böngészőbővítmény elemeit.

De mi is pontosan a böngésző? Ez egy szoftveralkalmazás, amely lehetővé teszi a végfelhasználó számára, hogy tartalmat érjen el egy szerverről, és megjelenítse azt weboldalakon.

✅ Egy kis történelem: az első böngészőt 'WorldWideWeb'-nek hívták, és Sir Timothy Berners-Lee készítette 1990-ben.

![korai böngészők](../../../../translated_images/earlybrowsers.d984b711cdf3a42ddac919d46c4b5ca7232f68ccfbd81395e04e5a64c0015277.hu.jpg)
> Néhány korai böngésző, via [Karen McGrane](https://www.slideshare.net/KMcGrane/week-4-ixd-history-personal-computing)

Amikor egy felhasználó csatlakozik az internethez egy URL (Uniform Resource Locator) cím használatával, általában Hypertext Transfer Protocol segítségével, `http` vagy `https` címen keresztül, a böngésző kommunikál egy webszerverrel, és lekéri a weboldalt.

Ezen a ponton a böngésző renderelő motorja megjeleníti azt a felhasználó eszközén, amely lehet mobiltelefon, asztali számítógép vagy laptop.

A böngészők képesek a tartalmak gyorsítótárazására is, így nem kell minden alkalommal a szerverről lekérni azokat. Rögzíthetik a felhasználó böngészési előzményeit, tárolhatnak 'cookie'-kat, amelyek kis adatdarabok, és információkat tartalmaznak a felhasználó tevékenységéről, és még sok másra képesek.

Fontos megjegyezni, hogy a böngészők nem egyformák! Mindegyik böngészőnek megvannak az erősségei és gyengeségei, és egy profi webfejlesztőnek értenie kell, hogyan lehet a weboldalakat jól működtetni különböző böngészőkben. Ez magában foglalja a kis nézetablakok kezelését, például egy mobiltelefon képernyőjét, valamint az offline felhasználók támogatását.

Egy igazán hasznos weboldal, amelyet érdemes könyvjelzőzni a kedvenc böngésződben, a [caniuse.com](https://www.caniuse.com). Amikor weboldalakat készítesz, nagyon hasznos a caniuse által nyújtott támogatott technológiák listáját használni, hogy a lehető legjobban támogathasd a felhasználóidat.

✅ Hogyan tudhatod meg, mely böngészők a legnépszerűbbek a weboldalad felhasználói körében? Ellenőrizd az analitikát - különböző analitikai csomagokat telepíthetsz a webfejlesztési folyamat részeként, amelyek megmutatják, mely böngészőket használják leggyakrabban a felhasználók.

## Böngészőbővítmények

Miért érdemes böngészőbővítményt készíteni? Ez egy praktikus eszköz, amely gyors hozzáférést biztosít az ismétlődő feladatokhoz. Például, ha gyakran kell ellenőrizned a színeket az általad látogatott weboldalakon, telepíthetsz egy színválasztó böngészőbővítményt. Ha nehezen emlékszel a jelszavakra, használhatsz egy jelszókezelő böngészőbővítményt.

A böngészőbővítmények fejlesztése szórakoztató is. Általában egy meghatározott számú feladatot kezelnek, amelyeket hatékonyan végeznek el.

✅ Melyek a kedvenc böngészőbővítményeid? Milyen feladatokat látnak el?

### Bővítmények telepítése

Mielőtt elkezdenéd a fejlesztést, nézd meg, hogyan lehet böngészőbővítményt készíteni és telepíteni. Bár minden böngésző kicsit eltérően kezeli ezt a feladatot, a folyamat hasonló Chrome és Firefox esetében az Edge példájához:

![képernyőkép az Edge böngészőről, amely az edge://extensions oldalt és a beállítások menüt mutatja](../../../../translated_images/install-on-edge.d68781acaf0b3d3dada8b7507cde7a64bf74b7040d9818baaa9070668e819f90.hu.png)

> Megjegyzés: Kapcsold be a fejlesztői módot, és engedélyezd a bővítményeket más áruházakból.

Lényegében a folyamat így néz ki:

- készítsd el a bővítményt az `npm run build` parancs segítségével
- navigálj a böngészőben a bővítmények panelre a "Beállítások és továbbiak" gomb (a `...` ikon) segítségével a jobb felső sarokban
- ha új telepítésről van szó, válaszd a `load unpacked` opciót, hogy feltölts egy új bővítményt a build mappájából (esetünkben ez a `/dist`)
- vagy kattints a `reload` gombra, ha már telepített bővítményt frissítesz

✅ Ezek az utasítások az általad készített bővítményekre vonatkoznak; ha olyan bővítményt szeretnél telepíteni, amelyet már kiadtak a böngésző bővítményáruházában, navigálj az adott [áruházakba](https://microsoftedge.microsoft.com/addons/Microsoft-Edge-Extensions-Home), és telepítsd a választott bővítményt.

### Kezdj neki

Egy olyan böngészőbővítményt fogsz készíteni, amely megjeleníti a régiód szénlábnyomát, bemutatva az energiafelhasználást és az energiaforrást. A bővítmény tartalmazni fog egy űrlapot, amely API kulcsot gyűjt, hogy hozzáférhess a CO2 Signal API-jához.

**Szükséged lesz:**

- [egy API kulcsra](https://www.co2signal.com/); add meg az e-mail címedet az oldalon, és küldenek neked egyet
- a [régiód kódjára](http://api.electricitymap.org/v3/zones), amely megfelel az [Electricity Map](https://www.electricitymap.org/map) térképének (például Bostonban 'US-NEISO'-t használok).
- a [kezdő kódra](../../../../5-browser-extension/start). Töltsd le a `start` mappát; ebben a mappában fogod kiegészíteni a kódot.
- [NPM](https://www.npmjs.com) - Az NPM egy csomagkezelő eszköz; telepítsd helyileg, és a `package.json` fájlban felsorolt csomagok telepítve lesznek a webes eszközöd számára

✅ Tudj meg többet a csomagkezelésről ebben a [kiváló Learn modulban](https://docs.microsoft.com/learn/modules/create-nodejs-project-dependencies/?WT.mc_id=academic-77807-sagibbon)

Szánj egy percet a kódbázis átnézésére:

dist
    -|manifest.json (alapértelmezések itt)
    -|index.html (front-end HTML markup itt)
    -|background.js (háttér JS itt)
    -|main.js (összeállított JS)
src
    -|index.js (a JS kódod ide kerül)

✅ Miután megvan az API kulcsod és a régiókódod, tárold el őket valahol jegyzetként későbbi használatra.

### Készítsd el a bővítmény HTML-jét

Ez a bővítmény két nézetet tartalmaz. Az egyik az API kulcs és a régiókód begyűjtésére szolgál:

![képernyőkép a kész bővítményről, amely egy űrlapot mutat a régió neve és az API kulcs mezőkkel.](../../../../translated_images/1.b6da8c1394b07491afeb6b2a8e5aca73ebd3cf478e27bcc9aeabb187e722648e.hu.png)

A másik pedig a régió szénfelhasználását jeleníti meg:

![képernyőkép a kész bővítményről, amely az US-NEISO régió szénfelhasználási és fosszilis üzemanyag százalékos értékeit mutatja.](../../../../translated_images/2.1dae52ff0804224692cd648afbf2342955d7afe3b0101b617268130dfb427f55.hu.png)

Kezdjük azzal, hogy elkészítjük az űrlap HTML-jét, és CSS-sel formázzuk.

A `/dist` mappában készíts egy űrlapot és egy eredményterületet. Az `index.html` fájlban töltsd ki az űrlap területét:

```HTML
<form class="form-data" autocomplete="on">
	<div>
		<h2>New? Add your Information</h2>
	</div>
	<div>
		<label for="region">Region Name</label>
		<input type="text" id="region" required class="region-name" />
	</div>
	<div>
		<label for="api">Your API Key from tmrow</label>
		<input type="text" id="api" required class="api-key" />
	</div>
	<button class="search-btn">Submit</button>
</form>	
```
Ez az az űrlap, ahol a mentett információkat be lehet vinni és helyi tárolóba menteni.

Ezután készítsd el az eredményterületet; az utolsó űrlap címke alatt adj hozzá néhány div-et:

```HTML
<div class="result">
	<div class="loading">loading...</div>
	<div class="errors"></div>
	<div class="data"></div>
	<div class="result-container">
		<p><strong>Region: </strong><span class="my-region"></span></p>
		<p><strong>Carbon Usage: </strong><span class="carbon-usage"></span></p>
		<p><strong>Fossil Fuel Percentage: </strong><span class="fossil-fuel"></span></p>
	</div>
	<button class="clear-btn">Change region</button>
</div>
```
Ezen a ponton megpróbálhatod a buildet. Győződj meg róla, hogy telepítetted a bővítmény csomagfüggőségeit:

```
npm install
```

Ez a parancs az npm-et, a Node Package Manager-t használja, hogy telepítse a webpacket a bővítmény build folyamatához. A folyamat kimenetét a `/dist/main.js` fájlban láthatod - itt látható, hogy a kód össze lett csomagolva.

Egyelőre a bővítménynek épülnie kell, és ha Edge-be telepíted bővítményként, egy szépen megjelenített űrlapot fogsz látni.

Gratulálok, megtetted az első lépéseket egy böngészőbővítmény készítése felé. A következő leckékben még funkcionálisabbá és hasznosabbá teszed.

---

## 🚀 Kihívás

Nézz körül egy böngészőbővítmény áruházban, és telepíts egyet a böngésződbe. Érdekes módon megvizsgálhatod a fájljait. Mit fedezel fel?

## Előadás utáni kvíz

[Előadás utáni kvíz](https://ff-quizzes.netlify.app/web/quiz/24)

## Áttekintés és önálló tanulás

Ebben a leckében megtanultál egy kicsit a web böngésző történetéről; használd ki ezt az alkalmat, hogy többet megtudj a World Wide Web feltalálóinak elképzeléseiről, és olvass többet a történetéről. Néhány hasznos oldal:

[A web böngészők története](https://www.mozilla.org/firefox/browsers/browser-history/)

[A web története](https://webfoundation.org/about/vision/history-of-the-web/)

[Interjú Tim Berners-Lee-vel](https://www.theguardian.com/technology/2019/mar/12/tim-berners-lee-on-30-years-of-the-web-if-we-dream-a-little-we-can-get-the-web-we-want)

## Feladat 

[Stílusozd újra a bővítményedet](assignment.md)

---

**Felelősségkizárás**:  
Ez a dokumentum az [Co-op Translator](https://github.com/Azure/co-op-translator) AI fordítási szolgáltatás segítségével készült. Bár törekszünk a pontosságra, kérjük, vegye figyelembe, hogy az automatikus fordítások hibákat vagy pontatlanságokat tartalmazhatnak. Az eredeti dokumentum az eredeti nyelvén tekintendő hiteles forrásnak. Kritikus információk esetén javasolt a professzionális, emberi fordítás igénybevétele. Nem vállalunk felelősséget a fordítás használatából eredő félreértésekért vagy téves értelmezésekért.