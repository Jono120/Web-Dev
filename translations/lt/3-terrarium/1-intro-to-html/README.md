<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "89f7f9f800ce7c9f149e98baaae8491a",
  "translation_date": "2025-08-29T16:55:06+00:00",
  "source_file": "3-terrarium/1-intro-to-html/README.md",
  "language_code": "lt"
}
-->
# Terrarium Projektas 1 dalis: Įvadas į HTML

![Įvadas į HTML](../../../../translated_images/webdev101-html.4389c2067af68e98280c1bde52b6c6269f399eaae3659b7c846018d8a7b0bbd9.lt.png)
> Sketchnote sukūrė [Tomomi Imura](https://twitter.com/girlie_mac)

## Klausimai prieš paskaitą

[Klausimai prieš paskaitą](https://ff-quizzes.netlify.app/web/quiz/15)

> Peržiūrėkite vaizdo įrašą

> 
> [![Git ir GitHub pagrindai vaizdo įrašas](https://img.youtube.com/vi/1TvxJKBzhyQ/0.jpg)](https://www.youtube.com/watch?v=1TvxJKBzhyQ)

### Įvadas

HTML, arba HyperText Markup Language, yra interneto „skeletas“. Jei CSS „aprengia“ jūsų HTML, o JavaScript suteikia jam gyvybės, HTML yra jūsų interneto aplikacijos kūnas. HTML sintaksė netgi atspindi šią idėją, nes ji apima „head“, „body“ ir „footer“ žymes.

Šioje pamokoje naudosime HTML, kad sukurtume virtualaus terariumo sąsajos „skeletą“. Jame bus pavadinimas ir trys stulpeliai: dešinysis ir kairysis stulpeliai, kuriuose bus perkeliamieji augalai, ir centrinė zona, kuri bus stiklinis terariumas. Pamokos pabaigoje galėsite matyti augalus stulpeliuose, tačiau sąsaja atrodys šiek tiek keistai; nesijaudinkite, kitame skyriuje pridėsite CSS stilius, kad sąsaja atrodytų geriau.

### Užduotis

Savo kompiuteryje sukurkite aplanką pavadinimu „terrarium“, o jame – failą „index.html“. Tai galite padaryti Visual Studio Code programoje, atidarę naują VS Code langą, paspaudę „open folder“ ir pasirinkę naują aplanką. Explorer skydelyje paspauskite mažą „file“ mygtuką ir sukurkite naują failą:

![Explorer VS Code](../../../../translated_images/vs-code-index.e2986cf919471eb984a0afef231380c8b132b000635105f2397bd2754d1b689c.lt.png)

Arba

Naudokite šias komandas git bash programoje:
* `mkdir terrarium`
* `cd terrarium`
* `touch index.html`
* `code index.html` arba `nano index.html`

> index.html failai nurodo naršyklei, kad tai yra numatytasis failas aplanke; URL, pvz., `https://anysite.com/test`, gali būti sukurtas naudojant aplanko struktūrą, kurioje yra aplankas „test“ su „index.html“ viduje; „index.html“ nebūtinai turi būti rodomas URL.

---

## DocType ir html žymės

Pirmoji HTML failo eilutė yra jo doctype. Gali būti šiek tiek netikėta, kad ši eilutė turi būti pačiame failo viršuje, tačiau ji nurodo senesnėms naršyklėms, kad puslapis turi būti pateikiamas standartiniu režimu, laikantis dabartinės HTML specifikacijos.

> Patarimas: VS Code programoje galite užvesti pelės žymeklį ant žymės ir gauti informaciją apie jos naudojimą iš MDN Reference vadovų.

Antroji eilutė turėtų būti `<html>` žymės atidarymo žymė, o po jos – uždarymo žymė `</html>`. Šios žymės yra jūsų sąsajos šakniniai elementai.

### Užduotis

Pridėkite šias eilutes savo `index.html` failo viršuje:

```HTML
<!DOCTYPE html>
<html></html>
```

✅ Yra keletas skirtingų režimų, kuriuos galima nustatyti naudojant DocType su užklausos eilute: [Quirks Mode ir Standards Mode](https://developer.mozilla.org/docs/Web/HTML/Quirks_Mode_and_Standards_Mode). Šie režimai buvo naudojami palaikyti labai senas naršykles, kurios šiais laikais paprastai nebenaudojamos (pvz., Netscape Navigator 4 ir Internet Explorer 5). Galite laikytis standartinio doctype deklaracijos.

---

## Dokumento 'head'

HTML dokumento 'head' sritis apima svarbią informaciją apie jūsų tinklalapį, dar vadinamą [metaduomenimis](https://developer.mozilla.org/docs/Web/HTML/Element/meta). Mūsų atveju, mes nurodome interneto serveriui, kuriam šis puslapis bus siunčiamas, šiuos keturis dalykus:

-   puslapio pavadinimą
-   puslapio metaduomenis, įskaitant:
    -   'character set', nurodantį, kokia simbolių koduotė naudojama puslapyje
    -   naršyklės informaciją, įskaitant `x-ua-compatible`, kuris nurodo, kad palaikoma IE=edge naršyklė
    -   informaciją apie tai, kaip turėtų elgtis viewport, kai jis įkeliamas. Nustatant viewport pradinį mastelį 1, kontroliuojamas priartinimo lygis, kai puslapis pirmą kartą įkeliamas.

### Užduotis

Pridėkite 'head' bloką savo dokumente tarp `<html>` žymių.

```html
<head>
	<title>Welcome to my Virtual Terrarium</title>
	<meta charset="utf-8" />
	<meta http-equiv="X-UA-Compatible" content="IE=edge" />
	<meta name="viewport" content="width=device-width, initial-scale=1" />
</head>
```

✅ Kas nutiktų, jei nustatytumėte viewport meta žymę taip: `<meta name="viewport" content="width=600">`? Skaitykite daugiau apie [viewport](https://developer.mozilla.org/docs/Web/HTML/Viewport_meta_tag).

---

## Dokumento `body`

### HTML žymės

HTML faile pridedate žymes, kad sukurtumėte tinklalapio elementus. Kiekviena žymė paprastai turi atidarymo ir uždarymo žymę, pvz., `<p>hello</p>`, kad nurodytumėte pastraipą. Sukurkite savo sąsajos kūną, pridėdami `<body>` žymių rinkinį tarp `<html>` žymių; jūsų žymėjimas dabar atrodo taip:

### Užduotis

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

Dabar galite pradėti kurti savo puslapį. Paprastai naudojate `<div>` žymes, kad sukurtumėte atskirus puslapio elementus. Sukursime seriją `<div>` elementų, kuriuose bus vaizdai.

### Vaizdai

Viena HTML žymė, kuriai nereikia uždarymo žymės, yra `<img>` žymė, nes ji turi `src` elementą, kuriame yra visa informacija, reikalinga puslapiui, kad būtų pateiktas elementas.

Sukurkite aplanką savo aplikacijoje pavadinimu `images` ir jame pridėkite visus vaizdus iš [source code folder](../../../../3-terrarium/solution/images); (yra 14 augalų vaizdų).

### Užduotis

Pridėkite tuos augalų vaizdus į du stulpelius tarp `<body></body>` žymių:

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

> Pastaba: Spans vs. Divs. Divs laikomi 'blokų' elementais, o Spans – 'eilutės'. Kas nutiktų, jei šiuos divs pakeistumėte į spans?

Su šiuo žymėjimu augalai dabar rodomi ekrane. Tai atrodo gana prastai, nes jie dar nėra stilizuoti naudojant CSS, ir tai padarysime kitoje pamokoje.

Kiekvienas vaizdas turi alt tekstą, kuris pasirodys net jei negalite matyti ar pateikti vaizdo. Tai yra svarbus atributas, kurį reikia įtraukti dėl prieinamumo. Sužinokite daugiau apie prieinamumą būsimose pamokose; kol kas prisiminkite, kad alt atributas pateikia alternatyvią informaciją apie vaizdą, jei vartotojas dėl kokios nors priežasties negali jo matyti (dėl lėto ryšio, klaidos src attribute arba jei vartotojas naudoja ekrano skaitytuvą).

✅ Ar pastebėjote, kad kiekvienas vaizdas turi tą patį alt tekstą? Ar tai gera praktika? Kodėl arba kodėl ne? Ar galite patobulinti šį kodą?

---

## Semantinis žymėjimas

Apskritai, rašant HTML, geriau naudoti prasmingą 'semantiką'. Ką tai reiškia? Tai reiškia, kad naudojate HTML žymes, kad atspindėtumėte duomenų tipą ar sąveiką, kuriai jos buvo sukurtos. Pavyzdžiui, pagrindinis puslapio pavadinimo tekstas turėtų naudoti `<h1>` žymę.

Pridėkite šią eilutę tiesiai po atidarymo `<body>` žyme:

```html
<h1>My Terrarium</h1>
```

Naudojant semantinį žymėjimą, pvz., antraštėms `<h1>` ir nesutvarkytoms sąrašams `<ul>`, padedama ekrano skaitytuvams naršyti puslapyje. Apskritai, mygtukai turėtų būti rašomi kaip `<button>`, o sąrašai – kaip `<li>`. Nors _įmanoma_ naudoti specialiai stilizuotus `<span>` elementus su paspaudimo tvarkytojais, kad imituotumėte mygtukus, geriau neįgaliems vartotojams naudoti technologijas, kad nustatytų, kur puslapyje yra mygtukas, ir sąveikauti su juo, jei elementas atrodo kaip mygtukas. Dėl šios priežasties stenkitės kuo daugiau naudoti semantinį žymėjimą.

✅ Pažvelkite į ekrano skaitytuvą ir [kaip jis sąveikauja su tinklalapiu](https://www.youtube.com/watch?v=OUDV1gqs9GA). Ar matote, kodėl nesemantinis žymėjimas gali erzinti vartotoją?

## Terariumas

Paskutinė šios sąsajos dalis apima žymėjimo sukūrimą, kuris bus stilizuotas, kad sukurtų terariumą.

### Užduotis:

Pridėkite šį žymėjimą virš paskutinės `</div>` žymės:

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

✅ Nors pridėjote šį žymėjimą ekrane, nieko nematote. Kodėl?

---

## 🚀Iššūkis

HTML yra keletas senų 'laukinės' žymių, kurios vis dar smagu naudoti, nors neturėtumėte naudoti pasenusių žymių, tokių kaip [šios žymės](https://developer.mozilla.org/docs/Web/HTML/Element#Obsolete_and_deprecated_elements) savo žymėjime. Vis dėlto, ar galite naudoti seną `<marquee>` žymę, kad h1 pavadinimas slinktų horizontaliai? (jei tai padarysite, nepamirškite vėliau ją pašalinti)

## Klausimai po paskaitos

[Klausimai po paskaitos](https://ff-quizzes.netlify.app/web/quiz/16)

## Apžvalga ir savarankiškas mokymasis

HTML yra 'patikrinta ir patikima' blokų sistema, kuri padėjo sukurti internetą tokį, koks jis yra šiandien. Sužinokite šiek tiek apie jo istoriją, studijuodami senas ir naujas žymes. Ar galite suprasti, kodėl kai kurios žymės buvo pasenę, o kitos pridėtos? Kokios žymės galėtų būti įvestos ateityje?

Sužinokite daugiau apie svetainių kūrimą internetui ir mobiliesiems įrenginiams [Microsoft Learn](https://docs.microsoft.com/learn/modules/build-simple-website/?WT.mc_id=academic-77807-sagibbon).

## Užduotis

[Praktikuokite HTML: Sukurkite tinklaraščio maketą](assignment.md)

---

**Atsakomybės apribojimas**:  
Šis dokumentas buvo išverstas naudojant dirbtinio intelekto vertimo paslaugą [Co-op Translator](https://github.com/Azure/co-op-translator). Nors siekiame tikslumo, atkreipiame dėmesį, kad automatiniai vertimai gali turėti klaidų ar netikslumų. Originalus dokumentas jo gimtąja kalba turėtų būti laikomas autoritetingu šaltiniu. Kritinei informacijai rekomenduojama naudotis profesionalių vertėjų paslaugomis. Mes neprisiimame atsakomybės už nesusipratimus ar klaidingus aiškinimus, kylančius dėl šio vertimo naudojimo.