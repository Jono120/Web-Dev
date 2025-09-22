<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "21b364c158c8e4f698de65eeac16c9fe",
  "translation_date": "2025-08-27T22:20:54+00:00",
  "source_file": "5-browser-extension/solution/translation/README.ms.md",
  "language_code": "sl"
}
-->
# Razširitev brskalnika Carbon Trigger: Celotna koda

Z uporabo API-ja CO2 Signal od tmrow za spremljanje porabe električne energije lahko ustvarite razširitev brskalnika, ki vas opozori na obremenjenost porabe električne energije v vaši regiji. Uporaba te razširitve vam bo pomagala sprejemati bolj premišljene odločitve glede vaših dejavnosti na podlagi teh informacij.

![posnetek zaslona razširitve brskalnika](../../../../../translated_images/extension-screenshot.0e7f5bfa110e92e3875e1bc9405edd45a3d2e02963e48900adb91926a62a5807.sl.png)

## Začetek

Najprej morate namestiti [npm](https://npmjs.com). Prenesite kopijo te kode v mapo na vašem računalniku.

Namestite vse potrebne pakete:

```
npm install
```

Sestavite razširitev z uporabo webpacka:

```
npm run build
```

Za namestitev v brskalnik Edge uporabite meni s 'tremi pikami' v zgornjem desnem kotu brskalnika, da odprete ploščo Razširitve. Tam izberite 'Naloži nepakirano' za dodajanje nove razširitve. Odprite mapo 'dist', ko vas sistem pozove, in razširitev bo naložena. Za uporabo boste potrebovali API ključ za CO2 Signal API ([pridobite ga tukaj prek e-pošte](https://www.co2signal.com/) - vnesite svoj e-poštni naslov v polje na tej strani) in [kodo za vašo regijo](http://api.electricitymap.org/v3/zones), ki ustreza [zemljevidu električne energije](https://www.electricitymap.org/map) (na primer, v Bostonu uporabljam 'US-NEISO').

![prenos](../../../../../translated_images/install-on-edge.78634f02842c48283726c531998679a6f03a45556b2ee99d8ff231fe41446324.sl.png)

Ko vmesnik razširitve vsebuje vaš API ključ in regijo, se bo barvna pika v vrstici razširitve brskalnika spremenila, da bo odražala porabo energije v vaši regiji, in vam dala namige o tem, katere dejavnosti so primerne za izvajanje. Koncept sistema 'pik' sem povzel po [razširitvi brskalnika Energy Lollipop](https://energylollipop.com/) za emisije v Kaliforniji.

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za strojno prevajanje [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da se zavedate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem izvirnem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo strokovno človeško prevajanje. Ne prevzemamo odgovornosti za morebitna nesporazumevanja ali napačne razlage, ki izhajajo iz uporabe tega prevoda.