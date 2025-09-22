<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "21b364c158c8e4f698de65eeac16c9fe",
  "translation_date": "2025-08-26T22:48:55+00:00",
  "source_file": "5-browser-extension/solution/translation/README.ms.md",
  "language_code": "da"
}
-->
# Carbon Trigger Browserudvidelse: Komplet Kode

Ved at bruge CO2 Signal API fra tmrow til at overvåge elforbrug, kan du bygge en browserudvidelse, der giver dig advarsler i din browser om, hvor belastet dit områdes elforbrug er. Denne udvidelse kan hjælpe dig med at tage beslutninger om dine aktiviteter baseret på disse oplysninger.

![skærmbillede af browserudvidelse](../../../../../translated_images/extension-screenshot.0e7f5bfa110e92e3875e1bc9405edd45a3d2e02963e48900adb91926a62a5807.da.png)

## Kom godt i gang

Du skal installere [npm](https://npmjs.com). Download en kopi af denne kode til en mappe på din computer.

Installer alle nødvendige pakker:

```
npm install
```

Byg udvidelsen med webpack:

```
npm run build
```

For at installere i Edge skal du bruge menuen med 'tre prikker' i øverste højre hjørne af browseren for at finde panelet Udvidelser. Derfra vælger du 'Load Unpacked' for at indlæse den nye udvidelse. Åbn mappen 'dist', når du bliver bedt om det, og udvidelsen vil blive indlæst. For at bruge den skal du have en API-nøgle til CO2 Signal API ([få en her via e-mail](https://www.co2signal.com/) - indtast din e-mail i boksen på denne side) og [koden for dit område](http://api.electricitymap.org/v3/zones), som svarer til [Electricity Map](https://www.electricitymap.org/map) (i Boston bruger jeg for eksempel 'US-NEISO').

![downloader](../../../../../translated_images/install-on-edge.78634f02842c48283726c531998679a6f03a45556b2ee99d8ff231fe41446324.da.png)

Når API-nøglen og området er indtastet i udvidelsens interface, vil en farvet prik i browserens udvidelsesbjælke ændre sig for at afspejle dit områdes energiforbrug og give dig anbefalinger om passende aktiviteter baseret på belastningen. Konceptet bag dette 'prik'-system blev inspireret af [Energy Lollipop browserudvidelsen](https://energylollipop.com/) for Californiens emissioner.

---

**Ansvarsfraskrivelse**:  
Dette dokument er blevet oversat ved hjælp af AI-oversættelsestjenesten [Co-op Translator](https://github.com/Azure/co-op-translator). Selvom vi bestræber os på at sikre nøjagtighed, skal det bemærkes, at automatiserede oversættelser kan indeholde fejl eller unøjagtigheder. Det originale dokument på dets oprindelige sprog bør betragtes som den autoritative kilde. For kritisk information anbefales professionel menneskelig oversættelse. Vi er ikke ansvarlige for eventuelle misforståelser eller fejltolkninger, der måtte opstå som følge af brugen af denne oversættelse.