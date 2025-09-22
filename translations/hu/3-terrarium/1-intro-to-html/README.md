<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "89f7f9f800ce7c9f149e98baaae8491a",
  "translation_date": "2025-08-29T10:32:47+00:00",
  "source_file": "3-terrarium/1-intro-to-html/README.md",
  "language_code": "hu"
}
-->
# Terrárium Projekt 1. rész: Bevezetés a HTML-be

![Bevezetés a HTML-be](../../../../translated_images/webdev101-html.4389c2067af68e98280c1bde52b6c6269f399eaae3659b7c846018d8a7b0bbd9.hu.png)
> Sketchnote készítette: [Tomomi Imura](https://twitter.com/girlie_mac)

## Előadás előtti kvíz

[Előadás előtti kvíz](https://ff-quizzes.netlify.app/web/quiz/15)


> Nézd meg a videót

> 
> [![Git és GitHub alapok videó](https://img.youtube.com/vi/1TvxJKBzhyQ/0.jpg)](https://www.youtube.com/watch?v=1TvxJKBzhyQ)

### Bevezetés

A HTML, vagyis a HyperText Markup Language, a web 'csontváza'. Ha a CSS 'felöltözteti' a HTML-t, és a JavaScript életre kelti, akkor a HTML a webalkalmazás teste. A HTML szintaxisa is tükrözi ezt az elképzelést, mivel tartalmaz "head", "body" és "footer" tageket.

Ebben a leckében a HTML-t fogjuk használni, hogy megalkossuk virtuális terráriumunk felületének 'csontvázát'. Lesz egy címe és három oszlopa: egy jobb és egy bal oszlop, ahol a húzható növények találhatók, valamint egy középső terület, amely maga az üvegszerű terrárium lesz. A lecke végére látni fogod a növényeket az oszlopokban, de a felület kissé furcsán fog kinézni; ne aggódj, a következő részben CSS stílusokat adsz hozzá, hogy jobban nézzen ki.

### Feladat

A számítógépeden hozz létre egy 'terrarium' nevű mappát, és azon belül egy 'index.html' nevű fájlt. Ezt megteheted a Visual Studio Code-ban, miután létrehoztad a terrarium mappát, egy új VS Code ablak megnyitásával, a 'mappa megnyitása' opcióra kattintva, és az új mappádhoz navigálva. Az Explorer panelen kattints a kis 'fájl' gombra, és hozd létre az új fájlt:

![explorer a VS Code-ban](../../../../translated_images/vs-code-index.e2986cf919471eb984a0afef231380c8b132b000635105f2397bd2754d1b689c.hu.png)

Vagy

Használd ezeket a parancsokat a git bash-ben:
* `mkdir terrarium`
* `cd terrarium`
* `touch index.html`
* `code index.html` vagy `nano index.html`

> Az index.html fájlok jelzik a böngészőnek, hogy ez az alapértelmezett fájl egy mappában; az olyan URL-ek, mint például `https://anysite.com/test`, egy olyan mappastruktúrából épülhetnek fel, amely tartalmaz egy `test` nevű mappát, benne egy `index.html` fájllal; az `index.html` nem feltétlenül jelenik meg az URL-ben.

---

## A DocType és a html tagek

A HTML fájl első sora a doctype. Kicsit meglepő, hogy ennek a sornak a fájl legfelső részén kell lennie, de ez azt mondja a régebbi böngészőknek, hogy az oldal megjelenítését szabványos módban kell végezni, a jelenlegi HTML specifikációt követve.

> Tipp: a VS Code-ban egy tag fölé húzva az egeret információkat kaphatsz annak használatáról az MDN Reference útmutatók alapján.

A második sornak a `<html>` tag nyitó tagjának kell lennie, amelyet most azonnal követ a záró tag `</html>`. Ezek a tagek az interfész gyökérelemei.

### Feladat

Add hozzá ezeket a sorokat az `index.html` fájlod tetejére:

```HTML
<!DOCTYPE html>
<html></html>
```

✅ A DocType beállításával néhány különböző módot lehet meghatározni egy lekérdezési karakterlánc segítségével: [Quirks Mode és Standards Mode](https://developer.mozilla.org/docs/Web/HTML/Quirks_Mode_and_Standards_Mode). Ezek a módok nagyon régi böngészők támogatására szolgáltak, amelyeket manapság már nem igazán használnak (például Netscape Navigator 4 és Internet Explorer 5). Maradj a szabványos doctype deklarációnál.

---

## A dokumentum 'head' része

A HTML dokumentum 'head' része tartalmazza a weboldalról szóló alapvető információkat, más néven [metaadatokat](https://developer.mozilla.org/docs/Web/HTML/Element/meta). Esetünkben a következő négy dolgot adjuk meg a webkiszolgálónak, amelyhez ezt az oldalt küldjük megjelenítésre:

-   az oldal címe
-   metaadatok, beleértve:
    -   a 'karakterkészletet', amely megadja, hogy milyen karakterkódolást használ az oldal
    -   böngészőinformációk, beleértve az `x-ua-compatible`-t, amely jelzi, hogy az IE=edge böngésző támogatott
    -   információk arról, hogyan viselkedjen a viewport az oldal betöltésekor. A viewport kezdeti méretezésének 1-re állítása szabályozza a nagyítási szintet az oldal első betöltésekor.

### Feladat

Adj hozzá egy 'head' blokkot a dokumentumodhoz a `<html>` nyitó és záró tagek közé.

```html
<head>
	<title>Welcome to my Virtual Terrarium</title>
	<meta charset="utf-8" />
	<meta http-equiv="X-UA-Compatible" content="IE=edge" />
	<meta name="viewport" content="width=device-width, initial-scale=1" />
</head>
```

✅ Mi történne, ha egy ilyen viewport meta tag-et állítanál be: `<meta name="viewport" content="width=600">`? Olvass többet a [viewport](https://developer.mozilla.org/docs/Web/HTML/Viewport_meta_tag) témájáról.

---

## A dokumentum `body` része

### HTML tagek

A HTML-ben tageket adsz hozzá a .html fájlodhoz, hogy létrehozd a weboldal elemeit. Minden tag általában egy nyitó és egy záró tagból áll, például: `<p>hello</p>` egy bekezdés jelölésére. Hozd létre az interfész 'body' részét úgy, hogy egy `<body>` tagpárt adsz hozzá a `<html>` tagpár belsejébe; a jelölésed most így néz ki:

### Feladat

```html
<!DOCTYPE html>
<html>
	<head>
		<title>Welcome to my Virtual Terrarium</title>
		<meta charset="utf-8" />
		<meta http-equiv="X-UA-Compatible" content="IE=edge" />
		<meta name="viewport" content="width=device-width, initial-scale=1" />
	</head>
	<body></body>
</html>
```

Most elkezdheted az oldal felépítését. Általában `<div>` tageket használsz az oldal különálló elemeinek létrehozásához. Hozz létre egy sor `<div>` elemet, amelyek képeket fognak tartalmazni.

### Képek

Egy HTML tag, amelynek nincs szüksége záró tagra, az `<img>` tag, mert van egy `src` eleme, amely tartalmazza az összes információt, amely az elem megjelenítéséhez szükséges.

Hozz létre egy `images` nevű mappát az alkalmazásodban, és abba helyezd el az összes képet a [forráskód mappából](../../../../3-terrarium/solution/images); (14 növény képe van).

### Feladat

Add hozzá ezeket a növényképeket két oszlopba a `<body></body>` tagek közé:

```html
<div id="page">
	<div id="left-container" class="container">
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant1" src="./images/plant1.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant2" src="./images/plant2.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant3" src="./images/plant3.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant4" src="./images/plant4.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant5" src="./images/plant5.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant6" src="./images/plant6.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant7" src="./images/plant7.png" />
		</div>
	</div>
	<div id="right-container" class="container">
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant8" src="./images/plant8.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant9" src="./images/plant9.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant10" src="./images/plant10.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant11" src="./images/plant11.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant12" src="./images/plant12.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant13" src="./images/plant13.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant14" src="./images/plant14.png" />
		</div>
	</div>
</div>
```

> Megjegyzés: Spans vs. Divs. A Div-ek 'blokk' elemeknek számítanak, míg a Spans 'soros' elemek. Mi történne, ha ezeket a div-eket span-ekké alakítanád?

Ezzel a jelöléssel a növények most megjelennek a képernyőn. Elég rosszul néz ki, mert még nincsenek CSS-sel formázva, de ezt a következő leckében fogjuk megtenni.

Minden képnek van alternatív szövege, amely akkor is megjelenik, ha nem tudod látni vagy megjeleníteni a képet. Ez egy fontos attribútum a hozzáférhetőség érdekében. A hozzáférhetőségről a későbbi leckékben tanulhatsz többet; egyelőre jegyezd meg, hogy az alt attribútum alternatív információt nyújt egy képről, ha a felhasználó valamilyen okból nem tudja megtekinteni azt (például lassú kapcsolat, hiba a src attribútumban, vagy ha a felhasználó képernyőolvasót használ).

✅ Észrevetted, hogy minden képnek ugyanaz az alt tag-je? Ez jó gyakorlat? Miért igen vagy miért nem? Tudod javítani ezt a kódot?

---

## Szemantikus jelölés

Általánosságban előnyösebb, ha jelentést hordozó 'szemantikát' használsz a HTML írásakor. Mit jelent ez? Azt, hogy a HTML tageket arra a típusú adatra vagy interakcióra használod, amelyre tervezték őket. Például az oldal főcímének `<h1>` tag-et kell használnia.

Add hozzá a következő sort közvetlenül a nyitó `<body>` tag alá:

```html
<h1>My Terrarium</h1>
```

A szemantikus jelölés, például a címek `<h1>`-ként való megadása és a rendezetlen listák `<ul>`-ként való megjelenítése segíti a képernyőolvasókat az oldal navigálásában. Általánosságban a gombokat `<button>`-ként kell írni, a listákat pedig `<li>`-ként. Bár _lehetséges_ speciálisan formázott `<span>` elemeket használni kattintáskezelőkkel, hogy gombokat utánozzanak, jobb a fogyatékkal élő felhasználók számára, ha a technológiák meghatározhatják, hogy az oldalon hol található egy gomb, és interakcióba léphetnek vele, ha az elem gombként jelenik meg. Emiatt próbálj meg minél több szemantikus jelölést használni.

✅ Nézd meg, hogyan működik egy képernyőolvasó, és [hogyan lép kapcsolatba egy weboldallal](https://www.youtube.com/watch?v=OUDV1gqs9GA). Látod, miért lehet frusztráló a nem szemantikus jelölés a felhasználó számára?

## A terrárium

Az interfész utolsó része olyan jelölés létrehozását foglalja magában, amelyet úgy fogunk formázni, hogy terráriumot hozzon létre.

### Feladat:

Add hozzá ezt a jelölést az utolsó `</div>` tag fölé:

```html
<div id="terrarium">
	<div class="jar-top"></div>
	<div class="jar-walls">
		<div class="jar-glossy-long"></div>
		<div class="jar-glossy-short"></div>
	</div>
	<div class="dirt"></div>
	<div class="jar-bottom"></div>
</div>
```

✅ Bár hozzáadtad ezt a jelölést a képernyőhöz, semmi sem jelenik meg. Miért?

---

## 🚀Kihívás

Vannak néhány 'régi' HTML tag, amelyekkel még mindig szórakoztató játszani, bár nem szabad elavult tageket, például [ezeket a tageket](https://developer.mozilla.org/docs/Web/HTML/Element#Obsolete_and_deprecated_elements) használni a jelölésedben. Mégis, tudod használni a régi `<marquee>` tag-et, hogy az h1 cím vízszintesen görögjön? (ha megteszed, ne felejtsd el utána eltávolítani)

## Előadás utáni kvíz

[Előadás utáni kvíz](https://ff-quizzes.netlify.app/web/quiz/16)

## Áttekintés és önálló tanulás

A HTML az a 'kipróbált és bevált' építőkocka-rendszer, amely segített a webet azzá alakítani, ami ma. Tanulj egy kicsit a történelméről, tanulmányozva néhány régi és új tag-et. Ki tudod találni, miért vontak vissza néhány tag-et, és miért adtak hozzá újakat? Milyen tagek jelenhetnek meg a jövőben?

Tudj meg többet a web- és mobiloldalak készítéséről a [Microsoft Learn](https://docs.microsoft.com/learn/modules/build-simple-website/?WT.mc_id=academic-77807-sagibbon) oldalon.

## Feladat

[Gyakorold a HTML-t: Készíts egy blog makettet](assignment.md)

---

**Felelősségkizárás**:  
Ez a dokumentum az [Co-op Translator](https://github.com/Azure/co-op-translator) AI fordítási szolgáltatás segítségével lett lefordítva. Bár törekszünk a pontosságra, kérjük, vegye figyelembe, hogy az automatikus fordítások hibákat vagy pontatlanságokat tartalmazhatnak. Az eredeti dokumentum az eredeti nyelvén tekintendő hiteles forrásnak. Kritikus információk esetén javasolt a professzionális, emberi fordítás igénybevétele. Nem vállalunk felelősséget a fordítás használatából eredő félreértésekért vagy téves értelmezésekért.