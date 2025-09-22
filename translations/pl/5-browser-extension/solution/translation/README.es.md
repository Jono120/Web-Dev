<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "cbaf73f94a9ab4c680a10ef871e92948",
  "translation_date": "2025-08-24T13:20:53+00:00",
  "source_file": "5-browser-extension/solution/translation/README.es.md",
  "language_code": "pl"
}
-->
# Rozszerzenie przeglądarki Carbon Trigger: Pełny kod

Korzystając z API sygnału CO2 od tmrow do śledzenia zużycia energii elektrycznej, stwórz rozszerzenie przeglądarki, które będzie przypominać Ci bezpośrednio w przeglądarce o zużyciu energii elektrycznej w Twoim regionie. Używanie tego rozszerzenia pomoże Ci podejmować decyzje dotyczące Twoich działań na podstawie tych informacji.

![zrzut ekranu rozszerzenia](../../../../../5-browser-extension/solution/start/extension-screenshot.png)

## Pierwsze kroki

Musisz mieć zainstalowany [npm](https://npmjs.com). Pobierz kopię tego kodu do folderu na swoim komputerze.

Zainstaluj wszystkie wymagane pakiety:

```
npm install
```

Zbuduj rozszerzenie za pomocą webpack:

```
npm run build
```

Aby zainstalować w Edge, użyj menu z 'trzema kropkami' w prawym górnym rogu przeglądarki, aby znaleźć panel Rozszerzenia. Stamtąd wybierz 'Załaduj rozpakowane', aby załadować nowe rozszerzenie. Otwórz folder 'dist', gdy zostaniesz o to poproszony, a rozszerzenie zostanie załadowane. Aby z niego korzystać, będziesz potrzebować klucza API do API CO2 Signal ([zdobądź go tutaj przez e-mail](https://www.co2signal.com/) - wpisz swój adres e-mail w polu na tej stronie) oraz [kodu dla swojego regionu](http://api.electricitymap.org/v3/zones) odpowiadającego [Mapie energii elektrycznej](https://www.electricitymap.org/map) (na przykład w Bostonie używam 'US-NEISO').

![instalacja](../../../../../5-browser-extension/solution/start/install-on-edge.png)

Po wprowadzeniu klucza API i regionu w interfejsie rozszerzenia, kolorowy punkt na pasku rozszerzeń przeglądarki powinien zmienić się, aby odzwierciedlić zużycie energii w Twoim regionie i dać Ci wskazówkę dotyczącą działań o wysokim zużyciu energii, które byłyby dla Ciebie odpowiednie. Koncepcja tego systemu "punktów" została zainspirowana przez [rozszerzenie Energy Lollipop](https://energylollipop.com/) dla emisji w Kalifornii.

**Zastrzeżenie**:  
Ten dokument został przetłumaczony za pomocą usługi tłumaczenia AI [Co-op Translator](https://github.com/Azure/co-op-translator). Chociaż staramy się zapewnić dokładność, prosimy mieć na uwadze, że automatyczne tłumaczenia mogą zawierać błędy lub nieścisłości. Oryginalny dokument w jego rodzimym języku powinien być uznawany za wiarygodne źródło. W przypadku informacji krytycznych zaleca się skorzystanie z profesjonalnego tłumaczenia wykonanego przez człowieka. Nie ponosimy odpowiedzialności za jakiekolwiek nieporozumienia lub błędne interpretacje wynikające z użycia tego tłumaczenia.