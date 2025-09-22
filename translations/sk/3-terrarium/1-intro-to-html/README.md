<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "89f7f9f800ce7c9f149e98baaae8491a",
  "translation_date": "2025-08-29T11:14:54+00:00",
  "source_file": "3-terrarium/1-intro-to-html/README.md",
  "language_code": "sk"
}
-->
# Projekt Terrárium Časť 1: Úvod do HTML

![Úvod do HTML](../../../../translated_images/webdev101-html.4389c2067af68e98280c1bde52b6c6269f399eaae3659b7c846018d8a7b0bbd9.sk.png)
> Sketchnote od [Tomomi Imura](https://twitter.com/girlie_mac)

## Kvíz pred prednáškou

[Kvíz pred prednáškou](https://ff-quizzes.netlify.app/web/quiz/15)

> Pozrite si video

> 
> [![Video o základoch Git a GitHub](https://img.youtube.com/vi/1TvxJKBzhyQ/0.jpg)](https://www.youtube.com/watch?v=1TvxJKBzhyQ)

### Úvod

HTML, alebo HyperText Markup Language, je „kostra“ webu. Ak CSS „obliekne“ váš HTML a JavaScript mu vdýchne život, HTML je telom vašej webovej aplikácie. Syntax HTML dokonca odráža túto myšlienku, pretože obsahuje značky ako „head“, „body“ a „footer“.

V tejto lekcii použijeme HTML na vytvorenie „kostry“ rozhrania nášho virtuálneho terária. Bude obsahovať názov a tri stĺpce: pravý a ľavý stĺpec, kde budú umiestnené ťahateľné rastliny, a strednú oblasť, ktorá bude predstavovať sklenené terárium. Na konci tejto lekcie budete môcť vidieť rastliny v stĺpcoch, ale rozhranie bude vyzerať trochu zvláštne; nebojte sa, v ďalšej časti pridáte do rozhrania štýly CSS, aby vyzeralo lepšie.

### Úloha

Na svojom počítači vytvorte priečinok s názvom „terrarium“ a v ňom súbor s názvom „index.html“. Môžete to urobiť vo Visual Studio Code po vytvorení priečinka terrarium tak, že otvoríte nové okno VS Code, kliknete na „open folder“ a prejdete do svojho nového priečinka. Kliknite na malé tlačidlo „file“ v paneli Explorer a vytvorte nový súbor:

![explorer vo VS Code](../../../../translated_images/vs-code-index.e2986cf919471eb984a0afef231380c8b132b000635105f2397bd2754d1b689c.sk.png)

Alebo

Použite tieto príkazy vo vašom git bash:
* `mkdir terrarium`
* `cd terrarium`
* `touch index.html`
* `code index.html` alebo `nano index.html`

> Súbory index.html naznačujú prehliadaču, že ide o predvolený súbor v priečinku; URL ako `https://anysite.com/test` môžu byť vytvorené pomocou štruktúry priečinkov vrátane priečinka s názvom `test` s `index.html` vo vnútri; `index.html` sa nemusí zobrazovať v URL.

---

## DocType a značky html

Prvý riadok súboru HTML je jeho doctype. Je trochu prekvapujúce, že tento riadok musí byť na úplnom vrchu súboru, ale hovorí starším prehliadačom, že stránka sa má vykresliť v štandardnom režime podľa aktuálnej špecifikácie HTML.

> Tip: vo VS Code môžete prejsť kurzorom na značku a získať informácie o jej použití z referenčných príručiek MDN.

Druhý riadok by mal byť otváracou značkou `<html>`, nasledovanou zatiaľ zatváracou značkou `</html>`. Tieto značky sú koreňovými prvkami vášho rozhrania.

### Úloha

Pridajte tieto riadky na začiatok vášho súboru `index.html`:

```HTML
<!DOCTYPE html>
<html></html>
```

✅ Existuje niekoľko rôznych režimov, ktoré je možné určiť nastavením DocType pomocou reťazca dopytu: [Quirks Mode a Standards Mode](https://developer.mozilla.org/docs/Web/HTML/Quirks_Mode_and_Standards_Mode). Tieto režimy slúžili na podporu veľmi starých prehliadačov, ktoré sa dnes bežne nepoužívajú (Netscape Navigator 4 a Internet Explorer 5). Držte sa štandardného vyhlásenia doctype.

---

## 'Head' dokumentu

Oblasť 'head' dokumentu HTML obsahuje kľúčové informácie o vašej webovej stránke, známe aj ako [metadata](https://developer.mozilla.org/docs/Web/HTML/Element/meta). V našom prípade hovoríme webovému serveru, na ktorý bude táto stránka odoslaná na vykreslenie, tieto štyri veci:

-   názov stránky
-   metadáta stránky vrátane:
    -   'character set', ktorý informuje o tom, aké kódovanie znakov sa používa na stránke
    -   informácie o prehliadači, vrátane `x-ua-compatible`, čo naznačuje, že je podporovaný prehliadač IE=edge
    -   informácie o tom, ako by sa mal viewport správať pri načítaní. Nastavenie viewportu na počiatočné zväčšenie 1 kontroluje úroveň priblíženia pri prvom načítaní stránky.

### Úloha

Pridajte blok 'head' do vášho dokumentu medzi otváracie a zatváracie značky `<html>`.

```html
<head>
	<title>Welcome to my Virtual Terrarium</title>
	<meta charset="utf-8" />
	<meta http-equiv="X-UA-Compatible" content="IE=edge" />
	<meta name="viewport" content="width=device-width, initial-scale=1" />
</head>
```

✅ Čo by sa stalo, keby ste nastavili meta značku viewport takto: `<meta name="viewport" content="width=600">`? Prečítajte si viac o [viewporte](https://developer.mozilla.org/docs/Web/HTML/Viewport_meta_tag).

---

## 'Body' dokumentu

### HTML značky

V HTML pridávate značky do vášho .html súboru na vytváranie prvkov webovej stránky. Každá značka má zvyčajne otváraciu a zatváraciu značku, napríklad: `<p>ahoj</p>` na označenie odseku. Vytvorte telo vášho rozhrania pridaním sady značiek `<body>` do páru značiek `<html>`; váš kód teraz vyzerá takto:

### Úloha

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

Teraz môžete začať budovať svoju stránku. Zvyčajne používate značky `<div>` na vytváranie samostatných prvkov na stránke. Vytvoríme sériu prvkov `<div>`, ktoré budú obsahovať obrázky.

### Obrázky

Jedna HTML značka, ktorá nepotrebuje zatváraciu značku, je `<img>`, pretože obsahuje atribút `src`, ktorý obsahuje všetky informácie potrebné na vykreslenie položky na stránke.

Vytvorte priečinok vo vašej aplikácii s názvom `images` a do neho pridajte všetky obrázky z [priečinka so zdrojovým kódom](../../../../3-terrarium/solution/images); (je tam 14 obrázkov rastlín).

### Úloha

Pridajte tieto obrázky rastlín do dvoch stĺpcov medzi značky `<body></body>`:

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

> Poznámka: Spany vs. Divy. Divy sa považujú za „blokové“ prvky a Spany za „riadkové“. Čo by sa stalo, keby ste tieto divy zmenili na spany?

S týmto kódom sa rastliny teraz zobrazia na obrazovke. Vyzerá to dosť zle, pretože ešte nie sú naštýlované pomocou CSS, čo urobíme v ďalšej lekcii.

Každý obrázok má alternatívny text, ktorý sa zobrazí, aj keď obrázok nemôžete vidieť alebo vykresliť. Toto je dôležitý atribút pre prístupnosť. Viac o prístupnosti sa dozviete v budúcich lekciách; zatiaľ si zapamätajte, že atribút alt poskytuje alternatívne informácie o obrázku, ak ho používateľ z nejakého dôvodu nemôže zobraziť (kvôli pomalému pripojeniu, chybe v atribúte src alebo ak používateľ používa čítačku obrazovky).

✅ Všimli ste si, že každý obrázok má rovnaký alt text? Je to dobrá prax? Prečo áno alebo nie? Môžete tento kód vylepšiť?

---

## Sémantické značkovanie

Vo všeobecnosti je vhodnejšie používať zmysluplné „sémantiky“ pri písaní HTML. Čo to znamená? Znamená to, že používate HTML značky na reprezentáciu typu údajov alebo interakcie, na ktoré boli navrhnuté. Napríklad hlavný názov textu na stránke by mal používať značku `<h1>`.

Pridajte nasledujúci riadok hneď pod otváraciu značku `<body>`:

```html
<h1>My Terrarium</h1>
```

Používanie sémantického značkovania, ako je napríklad použitie hlavičiek `<h1>` a neriadených zoznamov `<ul>`, pomáha čítačkám obrazovky navigovať na stránke. Vo všeobecnosti by tlačidlá mali byť napísané ako `<button>` a zoznamy ako `<li>`. Aj keď je _možné_ použiť špeciálne naštýlované `<span>` prvky s obsluhou kliknutí na napodobnenie tlačidiel, je lepšie pre používateľov so zdravotným postihnutím, aby technológie určili, kde sa na stránke nachádza tlačidlo, a aby s ním mohli interagovať, ak sa prvok zobrazuje ako tlačidlo. Z tohto dôvodu sa snažte používať sémantické značkovanie čo najviac.

✅ Pozrite si čítačku obrazovky a [ako interaguje s webovou stránkou](https://www.youtube.com/watch?v=OUDV1gqs9GA). Vidíte, prečo by nesémantické značkovanie mohlo používateľa frustrovať?

## Terárium

Posledná časť tohto rozhrania zahŕňa vytvorenie značkovania, ktoré bude naštýlované na vytvorenie terária.

### Úloha:

Pridajte toto značkovanie nad poslednú značku `</div>`:

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

✅ Aj keď ste pridali toto značkovanie na obrazovku, nič sa nezobrazí. Prečo?

---

## 🚀Výzva

Existujú niektoré „staršie“ značky v HTML, ktoré sú stále zábavné na hranie, aj keď by ste nemali používať zastarané značky, ako sú [tieto značky](https://developer.mozilla.org/docs/Web/HTML/Element#Obsolete_and_deprecated_elements) vo vašom značkovaní. Napriek tomu, môžete použiť starú značku `<marquee>` na to, aby sa názov h1 posúval horizontálne? (ak to urobíte, nezabudnite ju potom odstrániť)

## Kvíz po prednáške

[Kvíz po prednáške](https://ff-quizzes.netlify.app/web/quiz/16)

## Prehľad a samoštúdium

HTML je „osvedčený a spoľahlivý“ stavebný systém, ktorý pomohol vybudovať web do podoby, akú má dnes. Zistite niečo o jeho histórii štúdiom starých a nových značiek. Dokážete zistiť, prečo boli niektoré značky zastarané a iné pridané? Aké značky by mohli byť zavedené v budúcnosti?

Dozviete sa viac o vytváraní stránok pre web a mobilné zariadenia na [Microsoft Learn](https://docs.microsoft.com/learn/modules/build-simple-website/?WT.mc_id=academic-77807-sagibbon).

## Zadanie

[Precvičte si HTML: Vytvorte maketu blogu](assignment.md)

---

**Upozornenie**:  
Tento dokument bol preložený pomocou služby na automatický preklad [Co-op Translator](https://github.com/Azure/co-op-translator). Aj keď sa snažíme o presnosť, upozorňujeme, že automatické preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho pôvodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre dôležité informácie sa odporúča profesionálny ľudský preklad. Nezodpovedáme za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.