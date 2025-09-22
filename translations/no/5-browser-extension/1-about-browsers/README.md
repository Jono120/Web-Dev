<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2326d04e194a10aa760b51f5e5a1f61d",
  "translation_date": "2025-08-29T08:30:58+00:00",
  "source_file": "5-browser-extension/1-about-browsers/README.md",
  "language_code": "no"
}
-->
# Nettleserutvidelsesprosjekt Del 1: Alt om nettlesere

![Browser sketchnote](../../../../translated_images/browser.60317c9be8b7f84adce43e30bff8d47a1ae15793beab762317b2bc6b74337c1a.no.jpg)
> Sketchnote av [Wassim Chegham](https://dev.to/wassimchegham/ever-wondered-what-happens-when-you-type-in-a-url-in-an-address-bar-in-a-browser-3dob)

## Quiz før forelesning

[Quiz før forelesning](https://ff-quizzes.netlify.app/web/quiz/23)

### Introduksjon

Nettleserutvidelser legger til ekstra funksjonalitet i en nettleser. Men før du bygger en, bør du lære litt om hvordan nettlesere fungerer.

### Om nettleseren

I denne serien med leksjoner vil du lære hvordan du bygger en nettleserutvidelse som fungerer i Chrome, Firefox og Edge. I denne delen vil du oppdage hvordan nettlesere fungerer og sette opp elementene til nettleserutvidelsen.

Men hva er egentlig en nettleser? Det er et program som lar en sluttbruker få tilgang til innhold fra en server og vise det på nettsider.

✅ Litt historie: Den første nettleseren het 'WorldWideWeb' og ble laget av Sir Timothy Berners-Lee i 1990.

![tidlige nettlesere](../../../../translated_images/earlybrowsers.d984b711cdf3a42ddac919d46c4b5ca7232f68ccfbd81395e04e5a64c0015277.no.jpg)
> Noen tidlige nettlesere, via [Karen McGrane](https://www.slideshare.net/KMcGrane/week-4-ixd-history-personal-computing)

Når en bruker kobler seg til internett ved hjelp av en URL (Uniform Resource Locator)-adresse, vanligvis via Hypertext Transfer Protocol med en `http`- eller `https`-adresse, kommuniserer nettleseren med en webserver og henter en nettside.

På dette tidspunktet viser nettleserens renderingsmotor siden på brukerens enhet, som kan være en mobiltelefon, stasjonær PC eller bærbar datamaskin.

Nettlesere har også evnen til å mellomlagre innhold slik at det ikke trenger å hentes fra serveren hver gang. De kan registrere historikken til en brukers nettleseraktivitet, lagre 'cookies', som er små datastykker som inneholder informasjon brukt til å lagre en brukers aktivitet, og mer.

En veldig viktig ting å huske om nettlesere er at de ikke er like! Hver nettleser har sine styrker og svakheter, og en profesjonell webutvikler må forstå hvordan man får nettsider til å fungere godt på tvers av nettlesere. Dette inkluderer å håndtere små skjermstørrelser som en mobiltelefon, samt en bruker som er offline.

Et veldig nyttig nettsted som du sannsynligvis bør bokmerke i nettleseren du foretrekker å bruke, er [caniuse.com](https://www.caniuse.com). Når du bygger nettsider, er det veldig hjelpsomt å bruke caniuse sine lister over støttede teknologier slik at du best kan støtte brukerne dine.

✅ Hvordan kan du finne ut hvilke nettlesere som er mest populære blant brukerne av nettstedet ditt? Sjekk analysene dine – du kan installere ulike analyseverktøy som en del av webutviklingsprosessen, og de vil fortelle deg hvilke nettlesere som brukes mest av de ulike populære nettleserne.

## Nettleserutvidelser

Hvorfor vil du bygge en nettleserutvidelse? Det er en praktisk ting å legge til i nettleseren når du trenger rask tilgang til oppgaver du ofte gjentar. For eksempel, hvis du ofte trenger å sjekke farger på ulike nettsider du besøker, kan du installere en fargevelger-utvidelse. Hvis du har problemer med å huske passord, kan du bruke en passordhåndteringsutvidelse.

Nettleserutvidelser er også morsomme å utvikle. De har en tendens til å håndtere et begrenset antall oppgaver som de utfører godt.

✅ Hva er dine favorittutvidelser for nettlesere? Hvilke oppgaver utfører de?

### Installere utvidelser

Før du begynner å bygge, ta en titt på prosessen med å bygge og distribuere en nettleserutvidelse. Selv om hver nettleser varierer litt i hvordan de håndterer denne oppgaven, er prosessen lik i Chrome og Firefox som i dette eksempelet på Edge:

![skjermbilde av Edge-nettleseren som viser den åpne edge://extensions-siden og åpne innstillingsmenyen](../../../../translated_images/install-on-edge.d68781acaf0b3d3dada8b7507cde7a64bf74b7040d9818baaa9070668e819f90.no.png)

> Merk: Sørg for å slå på utviklermodus og tillate utvidelser fra andre butikker.

I hovedsak vil prosessen være:

- bygg utvidelsen din ved å bruke `npm run build` 
- naviger i nettleseren til utvidelsespanelet ved å bruke "Innstillinger og mer"-knappen (ikonet `...`) øverst til høyre
- hvis det er en ny installasjon, velg `load unpacked` for å laste opp en ny utvidelse fra bygge-mappen (i vårt tilfelle er det `/dist`) 
- eller, klikk `reload` hvis du laster inn en allerede installert utvidelse på nytt

✅ Disse instruksjonene gjelder for utvidelser du bygger selv; for å installere utvidelser som er utgitt i nettleserens utvidelsesbutikk, bør du navigere til disse [butikkene](https://microsoftedge.microsoft.com/addons/Microsoft-Edge-Extensions-Home) og installere utvidelsen du ønsker.

### Kom i gang

Du skal bygge en nettleserutvidelse som viser karbonavtrykket i din region, inkludert energiforbruket og kilden til energien. Utvidelsen vil ha et skjema som samler inn en API-nøkkel slik at du kan få tilgang til CO2 Signal sitt API.

**Du trenger:**

- [en API-nøkkel](https://www.co2signal.com/); skriv inn e-posten din i boksen på denne siden, så får du en nøkkel tilsendt
- [koden for din region](http://api.electricitymap.org/v3/zones) som tilsvarer [Electricity Map](https://www.electricitymap.org/map) (i Boston, for eksempel, bruker jeg 'US-NEISO').
- [startkoden](../../../../5-browser-extension/start). Last ned `start`-mappen; du vil fullføre koden i denne mappen.
- [NPM](https://www.npmjs.com) - NPM er et verktøy for pakkebehandling; installer det lokalt, og pakkene som er oppført i `package.json`-filen din vil bli installert for bruk i webprosjektet ditt

✅ Lær mer om pakkebehandling i denne [utmerkede læringsmodulen](https://docs.microsoft.com/learn/modules/create-nodejs-project-dependencies/?WT.mc_id=academic-77807-sagibbon)

Ta et øyeblikk til å se gjennom kodebasen:

dist
    -|manifest.json (standardinnstillinger her)
    -|index.html (HTML-markup for front-end her)
    -|background.js (bakgrunns-JS her)
    -|main.js (bygget JS)
src
    -|index.js (JS-koden din går her)

✅ Når du har API-nøkkelen og regionkoden klar, lagre dem et sted i en notat for fremtidig bruk.

### Bygg HTML for utvidelsen

Denne utvidelsen har to visninger. En for å samle inn API-nøkkelen og regionkoden:

![skjermbilde av den ferdige utvidelsen åpnet i en nettleser, som viser et skjema med felt for regionnavn og API-nøkkel.](../../../../translated_images/1.b6da8c1394b07491afeb6b2a8e5aca73ebd3cf478e27bcc9aeabb187e722648e.no.png)

Og den andre for å vise regionens karbonforbruk:

![skjermbilde av den ferdige utvidelsen som viser verdier for karbonforbruk og prosentandel fossilt brensel for regionen US-NEISO.](../../../../translated_images/2.1dae52ff0804224692cd648afbf2342955d7afe3b0101b617268130dfb427f55.no.png)

La oss starte med å bygge HTML for skjemaet og style det med CSS.

I `/dist`-mappen bygger du et skjema og et resultatområde. I `index.html`-filen fyller du ut det avgrensede skjemaområdet:

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
Dette er skjemaet der den lagrede informasjonen din vil bli lagt inn og lagret i lokal lagring.

Deretter oppretter du resultatområdet; under den siste skjema-tagen legger du til noen div-er:

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
På dette tidspunktet kan du prøve en bygging. Sørg for å installere pakkene som er nødvendige for denne utvidelsen:

```
npm install
```

Denne kommandoen bruker npm, Node Package Manager, til å installere webpack for byggeprosessen til utvidelsen din. Du kan se resultatet av denne prosessen ved å se i `/dist/main.js` - du ser at koden har blitt samlet.

For nå bør utvidelsen bygges, og hvis du distribuerer den i Edge som en utvidelse, vil du se et skjema pent vist.

Gratulerer, du har tatt de første stegene mot å bygge en nettleserutvidelse. I de neste leksjonene vil du gjøre den mer funksjonell og nyttig.

---

## 🚀 Utfordring

Ta en titt på en nettleserutvidelsesbutikk og installer en utvidelse i nettleseren din. Du kan undersøke filene dens på interessante måter. Hva oppdager du?

## Quiz etter forelesning

[Quiz etter forelesning](https://ff-quizzes.netlify.app/web/quiz/24)

## Gjennomgang og selvstudium

I denne leksjonen lærte du litt om historien til nettleseren; benytt anledningen til å lære om hvordan oppfinnerne av World Wide Web så for seg bruken av den ved å lese mer om dens historie. Noen nyttige nettsteder inkluderer:

[The History of Web Browsers](https://www.mozilla.org/firefox/browsers/browser-history/)

[History of the Web](https://webfoundation.org/about/vision/history-of-the-web/)

[Et intervju med Tim Berners-Lee](https://www.theguardian.com/technology/2019/mar/12/tim-berners-lee-on-30-years-of-the-web-if-we-dream-a-little-we-can-get-the-web-we-want)

## Oppgave 

[Restyle utvidelsen din](assignment.md)

---

**Ansvarsfraskrivelse**:  
Dette dokumentet er oversatt ved hjelp av AI-oversettelsestjenesten [Co-op Translator](https://github.com/Azure/co-op-translator). Selv om vi tilstreber nøyaktighet, vennligst vær oppmerksom på at automatiske oversettelser kan inneholde feil eller unøyaktigheter. Det originale dokumentet på sitt opprinnelige språk bør anses som den autoritative kilden. For kritisk informasjon anbefales profesjonell menneskelig oversettelse. Vi er ikke ansvarlige for eventuelle misforståelser eller feiltolkninger som oppstår ved bruk av denne oversettelsen.