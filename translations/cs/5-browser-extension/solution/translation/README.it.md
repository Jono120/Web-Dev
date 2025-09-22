<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "9a6b22a2eff0f499b66236be973b24ad",
  "translation_date": "2025-08-28T03:46:47+00:00",
  "source_file": "5-browser-extension/solution/translation/README.it.md",
  "language_code": "cs"
}
-->
# Rozšíření prohlížeče Carbon Trigger: kód pro začátek

Budeme používat API Signal CO2 od tmrow k monitorování spotřeby elektřiny a vytvoříme rozšíření pro prohlížeč, které vám umožní mít přímo v prohlížeči připomínku o tom, jak náročná je spotřeba elektřiny ve vaší oblasti. Používání tohoto rozšíření vám pomůže lépe hodnotit své aktivity na základě těchto informací.

![snímek obrazovky rozšíření](../../../../../translated_images/extension-screenshot.0e7f5bfa110e92e3875e1bc9405edd45a3d2e02963e48900adb91926a62a5807.cs.png)

## Začínáme

Je nutné mít nainstalovaný [npm](https://npmjs.com). Stáhněte si kopii tohoto kódu do složky na svém počítači.

Nainstalujte všechny potřebné balíčky:

```
npm install
```

Vytvořte rozšíření pomocí webpacku:

```
npm run build
```

Pro instalaci na Edge použijte nabídku "tři tečky" v pravém horním rohu prohlížeče a najděte panel Rozšíření. Pokud ještě není aktivní, zapněte režim vývojáře (v levém dolním rohu). Vyberte "Načíst nekomprimované" pro přidání nového rozšíření. Otevřete složku "dist" v zobrazeném dialogu a rozšíření bude načteno. Pro jeho použití budete potřebovat API klíč pro CO2 Signal API (můžete ho [získat zde e-mailem](https://www.co2signal.com/) - zadejte svůj e-mail do pole na této stránce) a [kód pro vaši oblast](http://api.electricitymap.org/v3/zones) odpovídající [elektrické mapě](https://www.electricitymap.org/map) (například v Bostonu "US-NEISO").

![instalace](../../../../../translated_images/install-on-edge.78634f02842c48283726c531998679a6f03a45556b2ee99d8ff231fe41446324.cs.png)

Jakmile zadáte API klíč a region do rozhraní rozšíření, barevný bod v liště rozšíření prohlížeče by se měl změnit tak, aby odrážel spotřebu energie ve vaší oblasti. Poskytne vám také návod, které aktivity s vysokou spotřebou energie by bylo vhodné provádět. Koncept tohoto systému "bodů" byl inspirován [rozšířením Energy Lollipop](https://energylollipop.com/) pro emise v Kalifornii.

---

**Prohlášení**:  
Tento dokument byl přeložen pomocí služby pro automatický překlad [Co-op Translator](https://github.com/Azure/co-op-translator). Přestože se snažíme o přesnost, mějte prosím na paměti, že automatické překlady mohou obsahovat chyby nebo nepřesnosti. Původní dokument v jeho původním jazyce by měl být považován za autoritativní zdroj. Pro důležité informace doporučujeme profesionální lidský překlad. Neodpovídáme za žádné nedorozumění nebo nesprávné interpretace vyplývající z použití tohoto překladu.