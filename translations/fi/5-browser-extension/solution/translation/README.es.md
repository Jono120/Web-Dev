<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "cbaf73f94a9ab4c680a10ef871e92948",
  "translation_date": "2025-08-27T20:51:54+00:00",
  "source_file": "5-browser-extension/solution/translation/README.es.md",
  "language_code": "fi"
}
-->
# Carbon Trigger -selaimen laajennus: Täydellinen koodi

Käyttämällä tmrow'n CO2 Signal -API:ta sähkönkulutuksen seuraamiseen, luo selaimen laajennus, joka tarjoaa suoraan selaimessasi muistutuksen alueesi sähkönkulutuksesta. Tämän ad hoc -laajennuksen käyttö auttaa sinua tekemään päätöksiä toimistasi perustuen tähän tietoon.

![laajennuksen kuvakaappaus](../../../../../translated_images/extension-screenshot.352c4c3ba54e4041ad2f6af749d562cc5705f527b5826efd53d11c3528f5ae45.fi.png)

## Aloittaminen

Sinulla tulee olla [npm](https://npmjs.com) asennettuna. Lataa kopio tästä koodista tietokoneesi kansioon.

Asenna kaikki tarvittavat paketit:

```
npm install
```

Rakenna laajennus webpackilla:

```
npm run build
```

Asentaaksesi Edge-selaimeen, käytä selaimen oikeassa yläkulmassa olevaa 'kolmen pisteen' valikkoa löytääksesi Laajennukset-paneelin. Valitse sieltä 'Lataa purkamaton' ladataksesi uuden laajennuksen. Avaa 'dist'-kansio, kun sitä pyydetään, ja laajennus ladataan. Käyttääksesi sitä tarvitset API-avaimen CO2 Signal -API:lle ([hanki avain sähköpostitse täältä](https://www.co2signal.com/) - syötä sähköpostiosoitteesi tämän sivun laatikkoon) sekä [sähköaluekoodin](http://api.electricitymap.org/v3/zones), joka vastaa [Electricity Map](https://www.electricitymap.org/map) -karttaa (esimerkiksi Bostonissa käytän 'US-NEISO').

![asennus](../../../../../translated_images/install-on-edge.8bd0ee3ca7dcda1c5334b5195603a43c864e3b38d088b03d57376d25e77b9459.fi.png)

Kun API-avain ja alue on syötetty laajennuksen käyttöliittymään, väripiste selaimen laajennuspalkissa muuttuu heijastamaan alueesi energiankulutusta ja antaa sinulle indikaattorin siitä, mitkä korkean energiankulutuksen toiminnot olisivat sinulle sopivia. Tämän "pistejärjestelmän" konseptin sain [Energy Lollipop -laajennuksesta](https://energylollipop.com/) Kalifornian päästöille.

---

**Vastuuvapauslauseke**:  
Tämä asiakirja on käännetty käyttämällä tekoälypohjaista käännöspalvelua [Co-op Translator](https://github.com/Azure/co-op-translator). Vaikka pyrimme tarkkuuteen, huomioithan, että automaattiset käännökset voivat sisältää virheitä tai epätarkkuuksia. Alkuperäistä asiakirjaa sen alkuperäisellä kielellä tulisi pitää ensisijaisena lähteenä. Kriittisen tiedon osalta suositellaan ammattimaista ihmiskäännöstä. Emme ole vastuussa väärinkäsityksistä tai virhetulkinnoista, jotka johtuvat tämän käännöksen käytöstä.