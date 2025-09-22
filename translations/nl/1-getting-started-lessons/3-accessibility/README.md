<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f0c88c3e2cefa8952d356f802b1e47ca",
  "translation_date": "2025-08-29T01:04:57+00:00",
  "source_file": "1-getting-started-lessons/3-accessibility/README.md",
  "language_code": "nl"
}
-->
# Toegankelijke Webpagina's Maken

![Alles Over Toegankelijkheid](../../../../translated_images/webdev101-a11y.8ef3025c858d897a403a1a42c0897c76e11b724d9a8a0c0578dd4316f7507622.nl.png)
> Sketchnote door [Tomomi Imura](https://twitter.com/girlie_mac)

## Quiz Voor De Les
[Quiz voor de les](https://ff-quizzes.netlify.app/web/)

> De kracht van het web ligt in zijn universaliteit. Toegang voor iedereen, ongeacht een beperking, is een essentieel aspect.
>
> \- Sir Timothy Berners-Lee, W3C-directeur en uitvinder van het World Wide Web

Deze quote benadrukt perfect het belang van het maken van toegankelijke websites. Een applicatie die niet door iedereen kan worden gebruikt, is per definitie exclusief. Als webontwikkelaars moeten we altijd toegankelijkheid in gedachten houden. Door hier vanaf het begin op te focussen, ben je goed op weg om ervoor te zorgen dat iedereen toegang heeft tot de pagina's die je maakt. In deze les leer je over de tools die je kunnen helpen om ervoor te zorgen dat je webassets toegankelijk zijn en hoe je met toegankelijkheid in gedachten kunt bouwen.

> Je kunt deze les volgen op [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101/accessibility/?WT.mc_id=academic-77807-sagibbon)!

## Tools om te gebruiken

### Schermlezers

Een van de bekendste toegankelijkheidstools zijn schermlezers.

[Schermlezers](https://en.wikipedia.org/wiki/Screen_reader) worden vaak gebruikt door mensen met een visuele beperking. Terwijl we tijd besteden aan het zorgen dat een browser de informatie correct weergeeft, moeten we er ook voor zorgen dat een schermlezer dit doet.

In de meest eenvoudige vorm leest een schermlezer een pagina van boven naar beneden voor. Als je pagina alleen tekst bevat, zal de lezer de informatie op een vergelijkbare manier overbrengen als een browser. Natuurlijk zijn webpagina's zelden puur tekst; ze bevatten links, afbeeldingen, kleuren en andere visuele componenten. Er moet aandacht worden besteed aan het correct laten lezen van deze informatie door een schermlezer.

Elke webontwikkelaar zou zich vertrouwd moeten maken met een schermlezer. Zoals hierboven benadrukt, is het de client die je gebruikers zullen gebruiken. Net zoals je bekend bent met hoe een browser werkt, zou je moeten leren hoe een schermlezer werkt. Gelukkig zijn schermlezers ingebouwd in de meeste besturingssystemen.

Sommige browsers hebben ook ingebouwde tools en extensies die tekst kunnen voorlezen of zelfs enkele basisnavigatiefuncties bieden, zoals [deze toegankelijkheidsgerichte Edge-browsertools](https://support.microsoft.com/help/4000734/microsoft-edge-accessibility-features). Deze zijn ook belangrijke toegankelijkheidstools, maar werken heel anders dan schermlezers en mogen niet worden verward met schermlezer-testtools.

✅ Probeer een schermlezer en browsertekstlezer. Op Windows is [Verteller](https://support.microsoft.com/windows/complete-guide-to-narrator-e4397a0d-ef4f-b386-d8ae-c172f109bdb1/?WT.mc_id=academic-77807-sagibbon) standaard inbegrepen, en [JAWS](https://webaim.org/articles/jaws/) en [NVDA](https://www.nvaccess.org/about-nvda/) kunnen ook worden geïnstalleerd. Op macOS en iOS is [VoiceOver](https://support.apple.com/guide/voiceover/welcome/10) standaard geïnstalleerd.

### Zoomen

Een andere tool die vaak wordt gebruikt door mensen met een visuele beperking is zoomen. De meest basale vorm van zoomen is statisch zoomen, gecontroleerd via `Control + plusteken (+)` of door de schermresolutie te verlagen. Dit type zoomen zorgt ervoor dat de hele pagina wordt vergroot, dus het gebruik van [responsief ontwerp](https://developer.mozilla.org/docs/Learn/CSS/CSS_layout/Responsive_Design) is belangrijk om een goede gebruikerservaring te bieden bij verhoogde zoomniveaus.

Een ander type zoomen maakt gebruik van gespecialiseerde software om één gebied van het scherm te vergroten en te pannen, vergelijkbaar met het gebruik van een echte vergrootglas. Op Windows is [Vergrootglas](https://support.microsoft.com/windows/use-magnifier-to-make-things-on-the-screen-easier-to-see-414948ba-8b1c-d3bd-8615-0e5e32204198) ingebouwd, en [ZoomText](https://www.freedomscientific.com/training/zoomtext/getting-started/) is een software van derden met meer functies en een grotere gebruikersbasis. Zowel macOS als iOS hebben ingebouwde vergrootsoftware genaamd [Zoom](https://www.apple.com/accessibility/mac/vision/).

### Contrastcheckers

Kleuren op websites moeten zorgvuldig worden gekozen om te voldoen aan de behoeften van kleurenblinde gebruikers of mensen die moeite hebben met het zien van kleuren met weinig contrast.

✅ Test een website die je graag gebruikt op kleurgebruik met een browserextensie zoals [WCAG's kleurchecker](https://microsoftedge.microsoft.com/addons/detail/wcag-color-contrast-check/idahaggnlnekelhgplklhfpchbfdmkjp?hl=en-US&WT.mc_id=academic-77807-sagibbon). Wat leer je?

### Lighthouse

In het ontwikkelaarstoolgebied van je browser vind je de Lighthouse-tool. Deze tool is belangrijk om een eerste indruk te krijgen van de toegankelijkheid (en andere analyses) van een website. Hoewel het belangrijk is om niet uitsluitend op Lighthouse te vertrouwen, is een score van 100% zeer nuttig als basislijn.

✅ Zoek Lighthouse in het ontwikkelaarstoolpaneel van je browser en voer een analyse uit op een willekeurige site. Wat ontdek je?

## Ontwerpen voor toegankelijkheid

Toegankelijkheid is een relatief groot onderwerp. Om je te helpen zijn er tal van bronnen beschikbaar.

- [Accessible U - Universiteit van Minnesota](https://accessibility.umn.edu/your-role/web-developers)

Hoewel we niet elk aspect van het maken van toegankelijke sites kunnen behandelen, staan hieronder enkele kernprincipes die je wilt implementeren. Een toegankelijke pagina ontwerpen vanaf het begin is **altijd** gemakkelijker dan teruggaan naar een bestaande pagina om deze toegankelijk te maken.

## Goede weergaveprincipes

### Kleurenveilige paletten

Mensen zien de wereld op verschillende manieren, en dit geldt ook voor kleuren. Bij het selecteren van een kleurenpalet voor je site moet je ervoor zorgen dat het toegankelijk is voor iedereen. Een geweldige [tool voor het genereren van kleurenpaletten is Color Safe](http://colorsafe.co/).

✅ Identificeer een website die zeer problematisch is in het gebruik van kleuren. Waarom?

### Gebruik de juiste HTML

Met CSS en JavaScript is het mogelijk om elk element eruit te laten zien als elk type controle. `<span>` kan worden gebruikt om een `<button>` te maken, en `<b>` kan een hyperlink worden. Hoewel dit misschien gemakkelijker te stijlen lijkt, geeft het niets door aan een schermlezer. Gebruik de juiste HTML bij het maken van controles op een pagina. Als je een hyperlink wilt, gebruik dan `<a>`. Het gebruik van de juiste HTML voor de juiste controle wordt het gebruik van Semantische HTML genoemd.

✅ Ga naar een willekeurige website en kijk of de ontwerpers en ontwikkelaars HTML correct gebruiken. Kun je een knop vinden die een link zou moeten zijn? Tip: klik met de rechtermuisknop en kies 'Pagina Bron Bekijken' in je browser om de onderliggende code te bekijken.

### Maak een beschrijvende koppenhiërarchie

Schermlezergebruikers [vertrouwen sterk op koppen](https://webaim.org/projects/screenreadersurvey8/#finding) om informatie te vinden en door een pagina te navigeren. Beschrijvende koppen schrijven en semantische koppen-tags gebruiken zijn belangrijk voor het maken van een gemakkelijk navigeerbare site voor schermlezergebruikers.

### Gebruik goede visuele aanwijzingen

CSS biedt volledige controle over het uiterlijk van elk element op een pagina. Je kunt tekstvakken maken zonder een omlijning of hyperlinks zonder een onderstreping. Helaas kan het verwijderen van die aanwijzingen het moeilijker maken voor iemand die ervan afhankelijk is om het type controle te herkennen.

## Het belang van linktekst

Hyperlinks zijn essentieel voor het navigeren op het web. Daarom is het belangrijk dat een schermlezer links correct kan lezen, zodat alle gebruikers je site kunnen navigeren.

### Schermlezers en links

Zoals je zou verwachten, lezen schermlezers linktekst op dezelfde manier als andere tekst op de pagina. Met dit in gedachten lijkt de onderstaande tekst misschien perfect acceptabel.

> De kleine pinguïn, ook wel bekend als de feeënpinguïn, is de kleinste pinguïn ter wereld. [Klik hier](https://en.wikipedia.org/wiki/Little_penguin) voor meer informatie.

> De kleine pinguïn, ook wel bekend als de feeënpinguïn, is de kleinste pinguïn ter wereld. Bezoek https://en.wikipedia.org/wiki/Little_penguin voor meer informatie.

> **NOTE** Zoals je zo zult lezen, moet je **nooit** links maken die eruitzien zoals hierboven.

Onthoud dat schermlezers een andere interface zijn dan browsers met een andere set functies.

### Het probleem met het gebruik van de URL

Schermlezers lezen de tekst. Als een URL in de tekst verschijnt, zal de schermlezer de URL lezen. Over het algemeen geeft de URL geen betekenisvolle informatie en kan het vervelend klinken. Je hebt dit misschien ervaren als je telefoon ooit een tekstbericht met een URL hardop heeft voorgelezen.

### Het probleem met "klik hier"

Schermlezers hebben ook de mogelijkheid om alleen de hyperlinks op een pagina te lezen, net zoals een ziende persoon een pagina zou scannen op links. Als de linktekst altijd "klik hier" is, zal de gebruiker alleen "klik hier, klik hier, klik hier, klik hier, klik hier, ..." horen. Alle links zijn nu niet te onderscheiden van elkaar.

### Goede linktekst

Goede linktekst beschrijft kort wat er aan de andere kant van de link staat. In het bovenstaande voorbeeld over kleine pinguïns verwijst de link naar de Wikipedia-pagina over de soort. De term *kleine pinguïns* zou perfecte linktekst zijn, omdat het duidelijk maakt wat iemand zal leren als ze op de link klikken - kleine pinguïns.

> De [kleine pinguïn](https://en.wikipedia.org/wiki/Little_penguin), ook wel bekend als de feeënpinguïn, is de kleinste pinguïn ter wereld.

✅ Surf een paar minuten op het web om pagina's te vinden die obscure linkstrategieën gebruiken. Vergelijk ze met andere, beter gelinkte sites. Wat leer je?

#### Opmerkingen over zoekmachines

Als extra voordeel van het zorgen dat je site toegankelijk is voor iedereen, help je zoekmachines ook om je site te navigeren. Zoekmachines gebruiken linktekst om de onderwerpen van pagina's te leren. Dus het gebruik van goede linktekst helpt iedereen!

### ARIA

Stel je de volgende pagina voor:

| Product      | Beschrijving       | Bestellen    |
| ------------ | ------------------ | ------------ |
| Widget       | [Beschrijving](../../../../1-getting-started-lessons/3-accessibility/') | [Bestellen](../../../../1-getting-started-lessons/3-accessibility/') |
| Super widget | [Beschrijving](../../../../1-getting-started-lessons/3-accessibility/') | [Bestellen](../../../../1-getting-started-lessons/3-accessibility/') |

In dit voorbeeld lijkt het dupliceren van de tekst van beschrijving en bestellen logisch voor iemand die een browser gebruikt. Echter, iemand die een schermlezer gebruikt, zou alleen de woorden *beschrijving* en *bestellen* herhaald horen zonder context.

Om dit soort scenario's te ondersteunen, ondersteunt HTML een reeks attributen die bekend staan als [Accessible Rich Internet Applications (ARIA)](https://developer.mozilla.org/docs/Web/Accessibility/ARIA). Deze attributen stellen je in staat om extra informatie te geven aan schermlezers.

> **NOTE**: Zoals bij veel aspecten van HTML, kan de ondersteuning door browsers en schermlezers variëren. Echter, de meeste mainstream clients ondersteunen ARIA-attributen.

Je kunt `aria-label` gebruiken om de link te beschrijven wanneer het formaat van de pagina dit niet toestaat. De beschrijving voor widget kan worden ingesteld als

``` html
<a href="#" aria-label="Widget description">description</a>
```

✅ Over het algemeen heeft het gebruik van semantische markup zoals hierboven beschreven de voorkeur boven het gebruik van ARIA, maar soms is er geen semantisch equivalent voor verschillende HTML-widgets. Een goed voorbeeld is een boomstructuur. Er is geen HTML-equivalent voor een boomstructuur, dus je identificeert het generieke `<div>`-element voor dit onderdeel met een juiste rol en ARIA-waarden. De [MDN-documentatie over ARIA](https://developer.mozilla.org/docs/Web/Accessibility/ARIA) bevat meer nuttige informatie.

```html
<h2 id="tree-label">File Viewer</h2>
<div role="tree" aria-labelledby="tree-label">
  <div role="treeitem" aria-expanded="false" tabindex="0">Uploads</div>
</div>
```

## Afbeeldingen

Het spreekt voor zich dat schermlezers niet automatisch kunnen lezen wat er in een afbeelding staat. Het toegankelijk maken van afbeeldingen kost niet veel werk - dat is waar het `alt`-attribuut voor is. Alle betekenisvolle afbeeldingen moeten een `alt` hebben om te beschrijven wat ze zijn. 
Afbeeldingen die puur decoratief zijn, moeten hun `alt`-attribuut instellen op een lege string: `alt=""`. Dit voorkomt dat schermlezers onnodig de decoratieve afbeelding aankondigen.

✅ Zoals je zou verwachten, kunnen zoekmachines ook niet begrijpen wat er in een afbeelding staat. Ze gebruiken ook alt-tekst. Dus nogmaals, het zorgen dat je pagina toegankelijk is biedt extra voordelen!

## Het toetsenbord

Sommige gebruikers kunnen geen muis of trackpad gebruiken en vertrouwen in plaats daarvan op toetsenbordinteracties om van het ene element naar het andere te tabben. Het is belangrijk dat je website je inhoud in een logische volgorde presenteert, zodat een toetsenbordgebruiker elk interactief element kan bereiken terwijl ze door een document gaan. Als je je webpagina's bouwt met semantische markup en CSS gebruikt om hun visuele lay-out te stijlen, zou je site toetsenbordnavigeerbaar moeten zijn, maar het is belangrijk om dit aspect handmatig te testen. Leer meer over [toetsenbordnavigatiestrategieën](https://webaim.org/techniques/keyboard/).

✅ Ga naar een willekeurige website en probeer er doorheen te navigeren met alleen je toetsenbord. Wat werkt, wat werkt niet? Waarom?

## Samenvatting

Een web dat slechts voor sommigen toegankelijk is, is geen echt 'wereldwijd web'. De beste manier om ervoor te zorgen dat de sites die je maakt toegankelijk zijn, is door vanaf het begin toegankelijkheidsbest practices te integreren. Hoewel er extra stappen nodig zijn, betekent het opnemen van deze vaardigheden in je workflow nu dat alle pagina's die je maakt toegankelijk zullen zijn.

---

## 🚀 Uitdaging

Neem deze HTML en herschrijf deze om zo toegankelijk mogelijk te zijn, gegeven de strategieën die je hebt geleerd.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>
      Example
    </title>
    <link href='../assets/style.css' rel='stylesheet' type='text/css'>
  </head>
  <body>
    <div class="site-header">
      <p class="site-title">Turtle Ipsum</p>
      <p class="site-subtitle">The World's Premier Turtle Fan Club</p>
    </div>
    <div class="main-nav">
      <p class="nav-header">Resources</p>
      <div class="nav-list">
        <p class="nav-item nav-item-bull"><a href="https://www.youtube.com/watch?v=CMNry4PE93Y">"I like turtles"</a></p>
        <p class="nav-item nav-item-bull"><a href="https://en.wikipedia.org/wiki/Turtle">Basic Turtle Info</a></p>
        <p class="nav-item nav-item-bull"><a href="https://en.wikipedia.org/wiki/Turtles_(chocolate)">Chocolate Turtles</a></p>
      </div>
    </div>
    <div class="main-content">
      <div>
        <p class="page-title">Welcome to Turtle Ipsum. 
            <a href="">Click here</a> to learn more.
        </p>
        <p class="article-text">
          Turtle ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum
        </p>
      </div>
    </div>
    <div class="footer">
      <div class="footer-section">
        <span class="button">Sign up for turtle news</span>
      </div><div class="footer-section">
        <p class="nav-header footer-title">
          Internal Pages
        </p>
        <div class="nav-list">
          <p class="nav-item nav-item-bull"><a href="../">Index</a></p>
          <p class="nav-item nav-item-bull"><a href="../semantic">Semantic Example</a></p>
        </div>
      </div>
      <p class="footer-copyright">&copy; 2016 Instrument</p>
    </div>
  </body>
</html>
```

## Quiz Na De Les
[Quiz na de les](https://ff-quizzes.netlify.app/web/en/)

## Review & Zelfstudie
Veel overheden hebben wetten met betrekking tot toegankelijkheidseisen. Lees meer over de toegankelijkheidswetten in jouw eigen land. Wat wordt er gedekt, en wat niet? Een voorbeeld is [deze overheidswebsite](https://accessibility.blog.gov.uk/).

## Opdracht

[Analyseer een niet-toegankelijke website](assignment.md)

Credits: [Turtle Ipsum](https://github.com/Instrument/semantic-html-sample) door Instrument

---

**Disclaimer**:  
Dit document is vertaald met behulp van de AI-vertalingsservice [Co-op Translator](https://github.com/Azure/co-op-translator). Hoewel we streven naar nauwkeurigheid, dient u zich ervan bewust te zijn dat geautomatiseerde vertalingen fouten of onnauwkeurigheden kunnen bevatten. Het originele document in de oorspronkelijke taal moet worden beschouwd als de gezaghebbende bron. Voor kritieke informatie wordt professionele menselijke vertaling aanbevolen. Wij zijn niet aansprakelijk voor misverstanden of verkeerde interpretaties die voortvloeien uit het gebruik van deze vertaling.