<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "b95fdd8310ef467305015ece1b0f9411",
  "translation_date": "2025-08-29T01:00:22+00:00",
  "source_file": "2-js-basics/1-data-types/README.md",
  "language_code": "nl"
}
-->
# JavaScript Basis: Gegevenstypen

![JavaScript Basis - Gegevenstypen](../../../../translated_images/webdev101-js-datatypes.4cc470179730702c756480d3ffa46507f746e5975ebf80f99fdaaf1cff09a7f4.nl.png)
> Sketchnote door [Tomomi Imura](https://twitter.com/girlie_mac)

## Quiz voor de les
[Quiz voor de les](https://ff-quizzes.netlify.app/web/)

Deze les behandelt de basis van JavaScript, de taal die interactiviteit op het web mogelijk maakt.

> Je kunt deze les volgen op [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-variables/?WT.mc_id=academic-77807-sagibbon)!

[![Variabelen](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Variabelen in JavaScript")

[![Gegevenstypen in JavaScript](https://img.youtube.com/vi/AWfA95eLdq8/0.jpg)](https://youtube.com/watch?v=AWfA95eLdq8 "Gegevenstypen in JavaScript")

> 🎥 Klik op de afbeeldingen hierboven voor video's over variabelen en gegevenstypen

Laten we beginnen met variabelen en de gegevenstypen die ze bevatten!

## Variabelen

Variabelen slaan waarden op die je in je code kunt gebruiken en wijzigen.

Het maken en **declareren** van een variabele heeft de volgende syntax: **[trefwoord] [naam]**. Het bestaat uit twee delen:

- **Trefwoord**. Trefwoorden kunnen `let` of `var` zijn.  

✅ Het trefwoord `let` werd geïntroduceerd in ES6 en geeft je variabele een zogenaamde _block scope_. Het wordt aanbevolen om `let` te gebruiken in plaats van `var`. We zullen block scopes later uitgebreider behandelen.
- **De variabelenaam**, dit is een naam die je zelf kiest.

### Opdracht - werken met variabelen

1. **Declareer een variabele**. Laten we een variabele declareren met het trefwoord `let`:

    ```javascript
    let myVariable;
    ```

   `myVariable` is nu gedeclareerd met het trefwoord `let`. Het heeft momenteel nog geen waarde.

1. **Ken een waarde toe**. Sla een waarde op in een variabele met de `=` operator, gevolgd door de gewenste waarde.

    ```javascript
    myVariable = 123;
    ```

   > Opmerking: het gebruik van `=` in deze les betekent dat we gebruik maken van een "toewijzingsoperator", die wordt gebruikt om een waarde aan een variabele toe te wijzen. Het geeft geen gelijkheid aan.

   `myVariable` is nu *geïnitialiseerd* met de waarde 123.

1. **Refactor**. Vervang je code door de volgende instructie.

    ```javascript
    let myVariable = 123;
    ```

    Het bovenstaande wordt een _expliciete initialisatie_ genoemd, waarbij een variabele wordt gedeclareerd en tegelijkertijd een waarde krijgt toegewezen.

1. **Wijzig de variabelewaarde**. Wijzig de waarde van de variabele op de volgende manier:

   ```javascript
   myVariable = 321;
   ```

   Zodra een variabele is gedeclareerd, kun je de waarde op elk moment in je code wijzigen met de `=` operator en de nieuwe waarde.

   ✅ Probeer het! Je kunt JavaScript direct in je browser schrijven. Open een browservenster en ga naar de ontwikkelaarstools. In de console vind je een prompt; typ `let myVariable = 123`, druk op enter, en typ vervolgens `myVariable`. Wat gebeurt er? Let op, je leert meer over deze concepten in de volgende lessen.

## Constanten

Declaratie en initialisatie van een constante volgen dezelfde principes als een variabele, met uitzondering van het trefwoord `const`. Constanten worden meestal gedeclareerd met hoofdletters.

```javascript
const MY_VARIABLE = 123;
```

Constanten lijken op variabelen, met twee uitzonderingen:

- **Moet een waarde hebben**. Constanten moeten worden geïnitialiseerd, anders treedt er een fout op bij het uitvoeren van de code.
- **Referentie kan niet worden gewijzigd**. De referentie van een constante kan niet worden gewijzigd nadat deze is geïnitialiseerd, anders treedt er een fout op bij het uitvoeren van de code. Laten we twee voorbeelden bekijken:
   - **Eenvoudige waarde**. Het volgende is NIET toegestaan:
   
      ```javascript
      const PI = 3;
      PI = 4; // not allowed
      ```
 
   - **Objectreferentie is beschermd**. Het volgende is NIET toegestaan.
   
      ```javascript
      const obj = { a: 3 };
      obj = { b: 5 } // not allowed
      ```

    - **Objectwaarde is niet beschermd**. Het volgende IS toegestaan:
    
      ```javascript
      const obj = { a: 3 };
      obj.a = 5;  // allowed
      ```

      Hierboven verander je de waarde van het object, maar niet de referentie zelf, wat is toegestaan.

   > Opmerking: een `const` betekent dat de referentie beschermd is tegen heraanwijzing. De waarde is echter niet _onveranderlijk_ en kan veranderen, vooral als het een complex construct is zoals een object.

## Gegevenstypen

Variabelen kunnen verschillende soorten waarden opslaan, zoals getallen en tekst. Deze verschillende soorten waarden staan bekend als de **gegevenstype**. Gegevenstypen zijn een belangrijk onderdeel van softwareontwikkeling omdat ze ontwikkelaars helpen beslissingen te nemen over hoe de code moet worden geschreven en hoe de software moet werken. Bovendien hebben sommige gegevenstypen unieke eigenschappen die helpen om een waarde te transformeren of extra informatie eruit te halen.

✅ Gegevenstypen worden ook wel JavaScript data primitives genoemd, omdat het de laagste niveau gegevenstypen zijn die door de taal worden geleverd. Er zijn 7 primitieve gegevenstypen: string, number, bigint, boolean, undefined, null en symbol. Neem even de tijd om je voor te stellen wat elk van deze primitieve typen zou kunnen vertegenwoordigen. Wat is een `zebra`? Hoe zit het met `0`? `true`?

### Getallen

In de vorige sectie was de waarde van `myVariable` een gegevenstype getal.

`let myVariable = 123;`

Variabelen kunnen alle soorten getallen opslaan, inclusief decimalen of negatieve getallen. Getallen kunnen ook worden gebruikt met rekenkundige operators, behandeld in de [volgende sectie](../../../../2-js-basics/1-data-types).

### Rekenkundige Operators

Er zijn verschillende soorten operators om rekenkundige functies uit te voeren, en enkele worden hier vermeld:

| Symbool | Beschrijving                                                           | Voorbeeld                         |
| ------- | ---------------------------------------------------------------------- | --------------------------------- |
| `+`     | **Optelling**: Berekent de som van twee getallen                       | `1 + 2 //verwachte antwoord is 3` |
| `-`     | **Aftrekking**: Berekent het verschil tussen twee getallen             | `1 - 2 //verwachte antwoord is -1`|
| `*`     | **Vermenigvuldiging**: Berekent het product van twee getallen          | `1 * 2 //verwachte antwoord is 2` |
| `/`     | **Deling**: Berekent het quotiënt van twee getallen                    | `1 / 2 //verwachte antwoord is 0.5` |
| `%`     | **Rest**: Berekent de rest van de deling van twee getallen             | `1 % 2 //verwachte antwoord is 1` |

✅ Probeer het! Probeer een rekenkundige bewerking in de console van je browser. Verrassen de resultaten je?

### Strings

Strings zijn reeksen tekens die tussen enkele of dubbele aanhalingstekens staan.

- `'Dit is een string'`
- `"Dit is ook een string"`
- `let myString = 'Dit is een stringwaarde opgeslagen in een variabele';`

Vergeet niet aanhalingstekens te gebruiken bij het schrijven van een string, anders gaat JavaScript ervan uit dat het een variabelenaam is.

### Strings Formatteren

Strings zijn tekstueel en moeten van tijd tot tijd worden opgemaakt.

Om twee of meer strings te **concateneren**, of samen te voegen, gebruik je de `+` operator.

```javascript
let myString1 = "Hello";
let myString2 = "World";

myString1 + myString2 + "!"; //HelloWorld!
myString1 + " " + myString2 + "!"; //Hello World!
myString1 + ", " + myString2 + "!"; //Hello, World!

```

✅ Waarom is `1 + 1 = 2` in JavaScript, maar `'1' + '1' = 11?` Denk er eens over na. Wat gebeurt er met `'1' + 1`?

**Template literals** zijn een andere manier om strings op te maken, behalve dat in plaats van aanhalingstekens de backtick wordt gebruikt. Alles wat geen platte tekst is, moet in placeholders `${ }` worden geplaatst. Dit omvat alle variabelen die mogelijk strings zijn.

```javascript
let myString1 = "Hello";
let myString2 = "World";

`${myString1} ${myString2}!` //Hello World!
`${myString1}, ${myString2}!` //Hello, World!
```

Je kunt je opmaakdoelen bereiken met beide methoden, maar template literals respecteren eventuele spaties en regeleinden.

✅ Wanneer zou je een template literal gebruiken in plaats van een gewone string?

### Booleans

Booleans kunnen slechts twee waarden hebben: `true` of `false`. Booleans kunnen helpen beslissen welke regels code moeten worden uitgevoerd wanneer aan bepaalde voorwaarden wordt voldaan. In veel gevallen helpen [operators](../../../../2-js-basics/1-data-types) bij het instellen van de waarde van een Boolean en je zult vaak zien dat variabelen worden geïnitialiseerd of dat hun waarden worden bijgewerkt met een operator.

- `let myTrueBool = true`
- `let myFalseBool = false`

✅ Een variabele kan als 'truthy' worden beschouwd als deze evalueert naar een boolean `true`. Interessant is dat in JavaScript [alle waarden truthy zijn, tenzij ze als falsy zijn gedefinieerd](https://developer.mozilla.org/docs/Glossary/Truthy).

---

## 🚀 Uitdaging

JavaScript staat bekend om zijn verrassende manieren van omgaan met gegevenstypen. Doe wat onderzoek naar deze 'valkuilen'. Bijvoorbeeld: hoofdlettergevoeligheid kan je parten spelen! Probeer dit in je console: `let age = 1; let Age = 2; age == Age` (geeft `false` -- waarom?). Welke andere valkuilen kun je vinden?

## Quiz na de les
[Quiz na de les](https://ff-quizzes.netlify.app)

## Herhaling & Zelfstudie

Bekijk [deze lijst met JavaScript-oefeningen](https://css-tricks.com/snippets/javascript/) en probeer er een. Wat heb je geleerd?

## Opdracht

[Oefenen met Gegevenstypen](assignment.md)

---

**Disclaimer**:  
Dit document is vertaald met behulp van de AI-vertalingsservice [Co-op Translator](https://github.com/Azure/co-op-translator). Hoewel we streven naar nauwkeurigheid, dient u zich ervan bewust te zijn dat geautomatiseerde vertalingen fouten of onnauwkeurigheden kunnen bevatten. Het originele document in de oorspronkelijke taal moet worden beschouwd als de gezaghebbende bron. Voor kritieke informatie wordt professionele menselijke vertaling aanbevolen. Wij zijn niet aansprakelijk voor misverstanden of verkeerde interpretaties die voortvloeien uit het gebruik van deze vertaling.