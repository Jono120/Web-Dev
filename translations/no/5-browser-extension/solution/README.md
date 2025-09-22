<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "fab4e6b4f0efcd587a9029d82991f597",
  "translation_date": "2025-08-26T22:46:42+00:00",
  "source_file": "5-browser-extension/solution/README.md",
  "language_code": "no"
}
-->
# Karbonutløser Nettleserutvidelse: Fullført Kode

Ved å bruke tmrow sin CO2 Signal API for å spore strømforbruk, kan du lage en nettleserutvidelse som gir deg en påminnelse direkte i nettleseren om hvor tungt strømforbruket er i din region. Å bruke denne utvidelsen sporadisk kan hjelpe deg med å ta bedre vurderinger av aktivitetene dine basert på denne informasjonen.

![utvidelse skjermbilde](../../../../translated_images/extension-screenshot.0e7f5bfa110e92e3875e1bc9405edd45a3d2e02963e48900adb91926a62a5807.no.png)

## Komme i gang

Du må ha [npm](https://npmjs.com) installert. Last ned en kopi av denne koden til en mappe på datamaskinen din.

Installer alle nødvendige pakker:

```
npm install
```

Bygg utvidelsen med webpack:

```
npm run build
```

For å installere på Edge, bruk menyen med 'tre prikker' øverst til høyre i nettleseren for å finne Utvidelser-panelet. Derfra velger du 'Last inn pakket utvidelse' for å laste inn en ny utvidelse. Åpne 'dist'-mappen når du blir bedt om det, og utvidelsen vil lastes inn. For å bruke den, trenger du en API-nøkkel for CO2 Signal API ([få en her via e-post](https://www.co2signal.com/) – skriv inn e-posten din i boksen på denne siden) og koden for din region ([finn den her](http://api.electricitymap.org/v3/zones)) som tilsvarer [Electricity Map](https://www.electricitymap.org/map) (for eksempel bruker jeg 'US-NEISO' i Boston).

![installasjon](../../../../translated_images/install-on-edge.78634f02842c48283726c531998679a6f03a45556b2ee99d8ff231fe41446324.no.png)

Når API-nøkkelen og regionen er lagt inn i utvidelsesgrensesnittet, bør den fargede prikken i nettleserens utvidelseslinje endre seg for å gjenspeile energiforbruket i din region og gi deg en pekepinn på hvilke energikrevende aktiviteter som kan være passende å utføre. Konseptet bak dette 'prikk'-systemet ble inspirert av [Energy Lollipop-utvidelsen](https://energylollipop.com/) for utslipp i California.

---

**Ansvarsfraskrivelse**:  
Dette dokumentet er oversatt ved hjelp av AI-oversettelsestjenesten [Co-op Translator](https://github.com/Azure/co-op-translator). Selv om vi streber etter nøyaktighet, vær oppmerksom på at automatiserte oversettelser kan inneholde feil eller unøyaktigheter. Det originale dokumentet på sitt opprinnelige språk bør anses som den autoritative kilden. For kritisk informasjon anbefales profesjonell menneskelig oversettelse. Vi er ikke ansvarlige for misforståelser eller feiltolkninger som oppstår ved bruk av denne oversettelsen.