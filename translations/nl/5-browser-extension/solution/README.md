<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "fab4e6b4f0efcd587a9029d82991f597",
  "translation_date": "2025-08-27T20:51:38+00:00",
  "source_file": "5-browser-extension/solution/README.md",
  "language_code": "nl"
}
-->
# Carbon Trigger Browser Extensie: Voltooide Code

Gebruik de CO2 Signal API van tmrow om het elektriciteitsverbruik bij te houden en bouw een browserextensie zodat je direct in je browser een herinnering hebt over hoe zwaar het elektriciteitsverbruik in jouw regio is. Door deze extensie ad hoc te gebruiken, kun je beter beslissingen nemen over je activiteiten op basis van deze informatie.

![extensie screenshot](../../../../translated_images/extension-screenshot.0e7f5bfa110e92e3875e1bc9405edd45a3d2e02963e48900adb91926a62a5807.nl.png)

## Aan de slag

Je moet [npm](https://npmjs.com) geïnstalleerd hebben. Download een kopie van deze code naar een map op je computer.

Installeer alle benodigde pakketten:

```
npm install
```

Bouw de extensie met webpack:

```
npm run build
```

Om de extensie op Edge te installeren, gebruik je het menu met de 'drie stippen' rechtsboven in de browser om het Extensies-paneel te vinden. Selecteer daar 'Load Unpacked' om een nieuwe extensie te laden. Open de 'dist'-map wanneer hierom wordt gevraagd en de extensie wordt geladen. Om het te gebruiken, heb je een API-sleutel nodig voor de CO2 Signal API ([hier via e-mail verkrijgen](https://www.co2signal.com/) - voer je e-mailadres in het veld op deze pagina in) en de [code voor jouw regio](http://api.electricitymap.org/v3/zones) die overeenkomt met de [Electricity Map](https://www.electricitymap.org/map) (in Boston gebruik ik bijvoorbeeld 'US-NEISO').

![installeren](../../../../translated_images/install-on-edge.78634f02842c48283726c531998679a6f03a45556b2ee99d8ff231fe41446324.nl.png)

Zodra de API-sleutel en regio zijn ingevoerd in de interface van de extensie, zou de gekleurde stip in de browserextensiebalk moeten veranderen om het energieverbruik in jouw regio weer te geven. Het geeft je een aanwijzing over welke energie-intensieve activiteiten geschikt zijn om uit te voeren. Het concept achter dit 'stip'-systeem is geïnspireerd door de [Energy Lollipop extensie](https://energylollipop.com/) voor emissies in Californië.

---

**Disclaimer**:  
Dit document is vertaald met behulp van de AI-vertalingsservice [Co-op Translator](https://github.com/Azure/co-op-translator). Hoewel we streven naar nauwkeurigheid, dient u zich ervan bewust te zijn dat geautomatiseerde vertalingen fouten of onnauwkeurigheden kunnen bevatten. Het originele document in zijn oorspronkelijke taal moet worden beschouwd als de gezaghebbende bron. Voor cruciale informatie wordt professionele menselijke vertaling aanbevolen. Wij zijn niet aansprakelijk voor misverstanden of verkeerde interpretaties die voortvloeien uit het gebruik van deze vertaling.