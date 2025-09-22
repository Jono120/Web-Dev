<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2dcbb9259dee4f20a4f08d9a1aa2bd4c",
  "translation_date": "2025-08-29T08:41:44+00:00",
  "source_file": "1-getting-started-lessons/1-intro-to-programming-languages/README.md",
  "language_code": "no"
}
-->
# Introduksjon til programmeringsspråk og verktøyene i faget

Denne leksjonen dekker det grunnleggende om programmeringsspråk. Temaene som dekkes her gjelder for de fleste moderne programmeringsspråk i dag. I delen "Verktøyene i faget" vil du lære om nyttig programvare som hjelper deg som utvikler.

![Intro Programmering](../../../../translated_images/webdev101-programming.d6e3f98e61ac4bff0b27dcbf1c3f16c8ed46984866f2d29988929678b0058fde.no.png)
> Sketchnote av [Tomomi Imura](https://twitter.com/girlie_mac)

## Quiz før forelesning
[Quiz før forelesning](https://forms.office.com/r/dru4TE0U9n?origin=lprLink)

## Introduksjon

I denne leksjonen skal vi dekke:

- Hva er programmering?
- Typer programmeringsspråk
- Grunnleggende elementer i et program
- Nyttig programvare og verktøy for profesjonelle utviklere

> Du kan ta denne leksjonen på [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101/introduction-programming/?WT.mc_id=academic-77807-sagibbon)!

## Hva er programmering?

Programmering (også kjent som koding) er prosessen med å skrive instruksjoner for en enhet som en datamaskin eller mobiltelefon. Vi skriver disse instruksjonene med et programmeringsspråk, som deretter tolkes av enheten. Disse instruksjonene kan ha ulike navn, men *program*, *dataprogram*, *applikasjon (app)* og *kjørbar fil* er noen vanlige betegnelser.

Et *program* kan være hva som helst som er skrevet med kode; nettsider, spill og mobilapper er programmer. Selv om det er mulig å lage et program uten å skrive kode, tolkes den underliggende logikken av enheten, og denne logikken er mest sannsynlig skrevet med kode. Et program som *kjører* eller *utfører* kode, følger instruksjonene. Enheten du leser denne leksjonen på, kjører et program for å vise den på skjermen din.

✅ Gjør litt research: Hvem regnes som verdens første dataprogrammerer?

## Programmeringsspråk

Programmeringsspråk gjør det mulig for utviklere å skrive instruksjoner for en enhet. Enheter kan kun forstå binærkode (1 og 0), og for *de fleste* utviklere er ikke det en særlig effektiv måte å kommunisere på. Programmeringsspråk er verktøyet som gjør kommunikasjon mellom mennesker og datamaskiner mulig.

Programmeringsspråk finnes i ulike formater og kan tjene forskjellige formål. For eksempel brukes JavaScript primært til webapplikasjoner, mens Bash brukes hovedsakelig til operativsystemer.

*Lavnivåspråk* krever vanligvis færre steg enn *høynivåspråk* for at en enhet skal tolke instruksjonene. Det som imidlertid gjør høynivåspråk populære, er deres lesbarhet og støtte. JavaScript regnes som et høynivåspråk.

Følgende kode viser forskjellen mellom et høynivåspråk med JavaScript og et lavnivåspråk med ARM-assemblerkode.

```javascript
let number = 10
let n1 = 0, n2 = 1, nextTerm;

for (let i = 1; i <= number; i++) {
    console.log(n1);
    nextTerm = n1 + n2;
    n1 = n2;
    n2 = nextTerm;
}
```

```c
 area ascen,code,readonly
 entry
 code32
 adr r0,thumb+1
 bx r0
 code16
thumb
 mov r0,#00
 sub r0,r0,#01
 mov r1,#01
 mov r4,#10
 ldr r2,=0x40000000
back add r0,r1
 str r0,[r2]
 add r2,#04
 mov r3,r0
 mov r0,r1
 mov r1,r3
 sub r4,#01
 cmp r4,#00
 bne back
 end
```

Tro det eller ei, *de gjør akkurat det samme*: skriver ut en Fibonacci-sekvens opp til 10.

✅ En Fibonacci-sekvens er [definert](https://en.wikipedia.org/wiki/Fibonacci_number) som en rekke tall der hvert tall er summen av de to foregående, med start fra 0 og 1. De første 10 tallene i Fibonacci-sekvensen er 0, 1, 1, 2, 3, 5, 8, 13, 21 og 34.

## Elementer i et program

En enkelt instruksjon i et program kalles en *setning* og vil vanligvis ha et tegn eller linjeskift som markerer hvor instruksjonen slutter, eller *terminerer*. Hvordan en setning termineres, varierer mellom språk.

Setninger i et program kan være avhengige av data som gis av en bruker eller hentes fra andre steder for å utføre instruksjoner. Data kan endre hvordan et program oppfører seg, så programmeringsspråk har en måte å midlertidig lagre data på slik at det kan brukes senere. Disse kalles *variabler*. Variabler er setninger som instruerer en enhet om å lagre data i minnet sitt. Variabler i programmering ligner på variabler i algebra, der de har et unikt navn og verdien deres kan endres over tid.

Det er en sjanse for at noen setninger ikke blir utført av en enhet. Dette er vanligvis med vilje når det er skrevet av utvikleren, eller ved en feiltakelse når en uventet feil oppstår. Denne typen kontroll over et program gjør det mer robust og vedlikeholdbart. Typisk skjer disse endringene i kontroll når visse betingelser er oppfylt. En vanlig setning som brukes i moderne programmering for å kontrollere hvordan et program kjører, er `if..else`-setningen.

✅ Du vil lære mer om denne typen setning i senere leksjoner.

## Verktøyene i faget

[![Verktøyene i faget](https://img.youtube.com/vi/69WJeXGBdxg/0.jpg)](https://youtube.com/watch?v=69WJeXGBdxg "Verktøyene i faget")

> 🎥 Klikk på bildet over for en video om verktøy

I denne delen vil du lære om noe programvare som kan være svært nyttig når du starter din profesjonelle utviklingsreise.

Et **utviklingsmiljø** er et unikt sett med verktøy og funksjoner som en utvikler ofte bruker når de skriver programvare. Noen av disse verktøyene er tilpasset en utviklers spesifikke behov og kan endres over tid hvis utvikleren endrer prioriteringer i arbeid, personlige prosjekter eller når de bruker et annet programmeringsspråk. Utviklingsmiljøer er like unike som utviklerne som bruker dem.

### Redaktører

Et av de mest avgjørende verktøyene for programvareutvikling er redaktøren. Redaktører er der du skriver koden din og noen ganger der du kjører koden din.

Utviklere stoler på redaktører av flere grunner:

- *Feilsøking* hjelper med å avdekke feil og problemer ved å gå gjennom koden, linje for linje. Noen redaktører har innebygde feilsøkingsfunksjoner som kan tilpasses for spesifikke programmeringsspråk.
- *Syntaksutheving* legger til farger og tekstformatering i koden, noe som gjør den lettere å lese. De fleste redaktører tillater tilpasset syntaksutheving.
- *Utvidelser og integrasjoner* er spesialiserte verktøy laget av og for utviklere. Disse verktøyene er ikke innebygd i selve redaktøren. For eksempel dokumenterer mange utviklere koden sin for å forklare hvordan den fungerer. De kan installere en stavekontrollutvidelse for å finne skrivefeil i dokumentasjonen. De fleste utvidelser er laget for spesifikke redaktører, og de fleste redaktører har en måte å søke etter tilgjengelige utvidelser på.
- *Tilpasning* gjør det mulig for utviklere å skape et unikt utviklingsmiljø som passer deres behov. De fleste redaktører er svært tilpassbare og kan også tillate utviklere å lage egne utvidelser.

#### Populære redaktører og utvidelser for webutvikling

- [Visual Studio Code](https://code.visualstudio.com/?WT.mc_id=academic-77807-sagibbon)
  - [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
  - [Live Share](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare)
  - [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
- [Atom](https://atom.io/)
  - [spell-check](https://atom.io/packages/spell-check)
  - [teletype](https://atom.io/packages/teletype)
  - [atom-beautify](https://atom.io/packages/atom-beautify)
  
- [Sublimetext](https://www.sublimetext.com/)
  - [emmet](https://emmet.io/)
  - [SublimeLinter](http://www.sublimelinter.com/en/stable/)

### Nettlesere

Et annet viktig verktøy er nettleseren. Webutviklere stoler på nettleseren for å se hvordan koden deres kjører på nettet. Den brukes også til å vise de visuelle elementene på en nettside som er skrevet i redaktøren, som HTML.

Mange nettlesere har *utviklerverktøy* (DevTools) som inneholder et sett med nyttige funksjoner og informasjon for å hjelpe utviklere med å samle og fange opp viktig informasjon om applikasjonen deres. For eksempel: Hvis en nettside har feil, kan det være nyttig å vite når de oppsto. DevTools i en nettleser kan konfigureres til å fange opp denne informasjonen.

#### Populære nettlesere og DevTools

- [Edge](https://docs.microsoft.com/microsoft-edge/devtools-guide-chromium/?WT.mc_id=academic-77807-sagibbon)
- [Chrome](https://developers.google.com/web/tools/chrome-devtools/)
- [Firefox](https://developer.mozilla.org/docs/Tools)

### Kommandolinjeverktøy

Noen utviklere foretrekker en mindre grafisk tilnærming til daglige oppgaver og stoler på kommandolinjen for dette. Å skrive kode krever mye skriving, og noen utviklere foretrekker å ikke avbryte flyten sin på tastaturet. De bruker hurtigtaster for å bytte mellom vinduer, jobbe med forskjellige filer og bruke verktøy. De fleste oppgaver kan utføres med en mus, men en fordel med kommandolinjen er at mye kan gjøres uten å bytte mellom mus og tastatur. En annen fordel med kommandolinjen er at den kan konfigureres, og du kan lagre en tilpasset konfigurasjon, endre den senere og importere den til andre utviklingsmaskiner. Fordi utviklingsmiljøer er så unike for hver utvikler, vil noen unngå å bruke kommandolinjen, noen vil stole helt på den, og andre foretrekker en blanding av begge.

### Populære alternativer for kommandolinjen

Alternativene for kommandolinjen varierer avhengig av operativsystemet du bruker.

*💻 = forhåndsinstallert på operativsystemet.*

#### Windows

- [Powershell](https://docs.microsoft.com/powershell/scripting/overview?view=powershell-7/?WT.mc_id=academic-77807-sagibbon) 💻
- [Kommandolinje](https://docs.microsoft.com/windows-server/administration/windows-commands/windows-commands/?WT.mc_id=academic-77807-sagibbon) (også kjent som CMD) 💻
- [Windows Terminal](https://docs.microsoft.com/windows/terminal/?WT.mc_id=academic-77807-sagibbon)
- [mintty](https://mintty.github.io/)
  
#### MacOS

- [Terminal](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac) 💻
- [iTerm](https://iterm2.com/)
- [Powershell](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-7/?WT.mc_id=academic-77807-sagibbon)

#### Linux

- [Bash](https://www.gnu.org/software/bash/manual/html_node/index.html) 💻
- [KDE Konsole](https://docs.kde.org/trunk5/en/konsole/konsole/index.html)
- [Powershell](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-7/?WT.mc_id=academic-77807-sagibbon)

#### Populære kommandolinjeverktøy

- [Git](https://git-scm.com/) (💻 på de fleste operativsystemer)
- [NPM](https://www.npmjs.com/)
- [Yarn](https://classic.yarnpkg.com/en/docs/cli/)

### Dokumentasjon

Når en utvikler ønsker å lære noe nytt, vil de mest sannsynlig vende seg til dokumentasjon for å lære hvordan de skal bruke det. Utviklere stoler ofte på dokumentasjon for å veilede dem i hvordan de bruker verktøy og språk riktig, og også for å få dypere kunnskap om hvordan det fungerer.

#### Populær dokumentasjon om webutvikling

- [Mozilla Developer Network (MDN)](https://developer.mozilla.org/docs/Web), fra Mozilla, utgiverne av [Firefox](https://www.mozilla.org/firefox/) nettleseren
- [Frontend Masters](https://frontendmasters.com/learn/)
- [Web.dev](https://web.dev), fra Google, utgiverne av [Chrome](https://www.google.com/chrome/)
- [Microsofts egne utviklerdokumenter](https://docs.microsoft.com/microsoft-edge/#microsoft-edge-for-developers), for [Microsoft Edge](https://www.microsoft.com/edge)
- [W3 Schools](https://www.w3schools.com/where_to_start.asp)

✅ Gjør litt research: Nå som du kjenner det grunnleggende om et webutviklingsmiljø, sammenlign det med et webdesignmiljø.

---

## 🚀 Utfordring

Sammenlign noen programmeringsspråk. Hva er noen av de unike egenskapene til JavaScript vs. Java? Hva med COBOL vs. Go?

## Quiz etter forelesning
[Quiz etter forelesning](https://ff-quizzes.netlify.app/web/)

## Gjennomgang og selvstudium

Studer litt om de forskjellige språkene som er tilgjengelige for programmerere. Prøv å skrive en linje i ett språk, og skriv den deretter om i to andre. Hva lærte du?

## Oppgave

[Les dokumentasjonen](assignment.md)

---

**Ansvarsfraskrivelse**:  
Dette dokumentet er oversatt ved hjelp av AI-oversettelsestjenesten [Co-op Translator](https://github.com/Azure/co-op-translator). Selv om vi tilstreber nøyaktighet, vennligst vær oppmerksom på at automatiske oversettelser kan inneholde feil eller unøyaktigheter. Det originale dokumentet på sitt opprinnelige språk bør anses som den autoritative kilden. For kritisk informasjon anbefales profesjonell menneskelig oversettelse. Vi er ikke ansvarlige for eventuelle misforståelser eller feiltolkninger som oppstår ved bruk av denne oversettelsen.