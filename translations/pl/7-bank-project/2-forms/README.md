<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "8baca047d77a5f43fa4099c0578afa42",
  "translation_date": "2025-08-29T16:23:35+00:00",
  "source_file": "7-bank-project/2-forms/README.md",
  "language_code": "pl"
}
-->
# Budowa aplikacji bankowej, część 2: Tworzenie formularza logowania i rejestracji

## Quiz przed wykładem

[Quiz przed wykładem](https://ff-quizzes.netlify.app/web/quiz/43)

### Wprowadzenie

W niemal wszystkich nowoczesnych aplikacjach internetowych możesz założyć konto, aby mieć własną prywatną przestrzeń. Ponieważ wiele użytkowników może jednocześnie korzystać z aplikacji internetowej, potrzebny jest mechanizm do przechowywania danych osobowych każdego użytkownika oddzielnie i wybierania, które informacje mają być wyświetlane. Nie będziemy omawiać, jak [bezpiecznie zarządzać tożsamością użytkownika](https://en.wikipedia.org/wiki/Authentication), ponieważ jest to obszerny temat sam w sobie, ale zadbamy o to, aby każdy użytkownik mógł założyć jedno (lub więcej) konto bankowe w naszej aplikacji.

W tej części użyjemy formularzy HTML, aby dodać logowanie i rejestrację do naszej aplikacji internetowej. Zobaczymy, jak programowo przesyłać dane do API serwera, a ostatecznie jak zdefiniować podstawowe zasady walidacji danych wprowadzanych przez użytkownika.

### Wymagania wstępne

Musisz ukończyć [szablony HTML i routing](../1-template-route/README.md) aplikacji internetowej z poprzedniej lekcji. Musisz również zainstalować [Node.js](https://nodejs.org) i [uruchomić API serwera](../api/README.md) lokalnie, aby móc przesyłać dane do tworzenia kont.

**Zwróć uwagę**
Będziesz mieć dwa terminale uruchomione jednocześnie, jak wymieniono poniżej:
1. Dla głównej aplikacji bankowej, którą zbudowaliśmy w lekcji [szablony HTML i routing](../1-template-route/README.md)
2. Dla [API serwera aplikacji bankowej](../api/README.md), które właśnie skonfigurowaliśmy powyżej.

Musisz mieć oba serwery uruchomione, aby kontynuować resztę lekcji. Nasłuchują na różnych portach (port `3000` i port `5000`), więc wszystko powinno działać poprawnie.

Możesz sprawdzić, czy serwer działa poprawnie, wykonując to polecenie w terminalu:

```sh
curl http://localhost:5000/api
# -> should return "Bank API v1.0.0" as a result
```

---

## Formularz i kontrolki

Element `<form>` obejmuje sekcję dokumentu HTML, w której użytkownik może wprowadzać i przesyłać dane za pomocą interaktywnych kontrolek. Istnieje wiele różnych elementów interfejsu użytkownika (UI), które można używać w formularzu, najczęściej są to elementy `<input>` i `<button>`.

Istnieje wiele różnych [typów](https://developer.mozilla.org/docs/Web/HTML/Element/input) `<input>`, na przykład, aby utworzyć pole, w którym użytkownik może wprowadzić swoją nazwę użytkownika, możesz użyć:

```html
<input id="username" name="username" type="text">
```

Atrybut `name` będzie używany jako nazwa właściwości, gdy dane formularza zostaną przesłane. Atrybut `id` służy do powiązania `<label>` z kontrolką formularza.

> Zapoznaj się z pełną listą [typów `<input>`](https://developer.mozilla.org/docs/Web/HTML/Element/input) oraz [innych kontrolek formularza](https://developer.mozilla.org/docs/Learn/Forms/Other_form_controls), aby dowiedzieć się, jakie natywne elementy interfejsu użytkownika możesz wykorzystać podczas budowy swojego UI.

✅ Zauważ, że `<input>` jest [elementem pustym](https://developer.mozilla.org/docs/Glossary/Empty_element), do którego *nie* należy dodawać pasującego tagu zamykającego. Możesz jednak użyć notacji samodzielnie zamykającej `<input/>`, ale nie jest to wymagane.

Element `<button>` w formularzu jest trochę wyjątkowy. Jeśli nie określisz jego atrybutu `type`, automatycznie przesyła dane formularza do serwera po naciśnięciu. Oto możliwe wartości `type`:

- `submit`: Domyślnie w `<form>`, przycisk wywołuje akcję przesyłania formularza.
- `reset`: Przycisk resetuje wszystkie kontrolki formularza do ich początkowych wartości.
- `button`: Nie przypisuje domyślnego zachowania po naciśnięciu przycisku. Możesz wtedy przypisać niestandardowe akcje za pomocą JavaScript.

### Zadanie

Zacznijmy od dodania formularza do szablonu `login`. Będziemy potrzebować pola *username* oraz przycisku *Login*.

```html
<template id="login">
  <h1>Bank App</h1>
  <section>
    <h2>Login</h2>
    <form id="loginForm">
      <label for="username">Username</label>
      <input id="username" name="user" type="text">
      <button>Login</button>
    </form>
  </section>
</template>
```

Jeśli przyjrzysz się bliżej, zauważysz, że dodaliśmy tutaj również element `<label>`. Elementy `<label>` służą do dodawania nazwy do kontrolek UI, takich jak nasze pole nazwy użytkownika. Etykiety są ważne dla czytelności formularzy, ale mają również dodatkowe korzyści:

- Powiązanie etykiety z kontrolką formularza pomaga użytkownikom korzystającym z technologii wspomagających (np. czytników ekranu) zrozumieć, jakie dane mają podać.
- Możesz kliknąć etykietę, aby bezpośrednio skupić się na powiązanym polu, co ułatwia korzystanie na urządzeniach z ekranem dotykowym.

> [Dostępność](https://developer.mozilla.org/docs/Learn/Accessibility/What_is_accessibility) w sieci to bardzo ważny temat, który często jest pomijany. Dzięki [semantycznym elementom HTML](https://developer.mozilla.org/docs/Learn/Accessibility/HTML) nie jest trudno tworzyć dostępne treści, jeśli używasz ich poprawnie. Możesz [przeczytać więcej o dostępności](https://developer.mozilla.org/docs/Web/Accessibility), aby unikać typowych błędów i stać się odpowiedzialnym deweloperem.

Teraz dodamy drugi formularz do rejestracji, tuż poniżej poprzedniego:

```html
<hr/>
<h2>Register</h2>
<form id="registerForm">
  <label for="user">Username</label>
  <input id="user" name="user" type="text">
  <label for="currency">Currency</label>
  <input id="currency" name="currency" type="text" value="$">
  <label for="description">Description</label>
  <input id="description" name="description" type="text">
  <label for="balance">Current balance</label>
  <input id="balance" name="balance" type="number" value="0">
  <button>Register</button>
</form>
```

Za pomocą atrybutu `value` możemy zdefiniować domyślną wartość dla danego pola. Zauważ również, że pole `balance` ma typ `number`. Czy wygląda inaczej niż pozostałe pola? Spróbuj z nim interakcji.

✅ Czy możesz nawigować i korzystać z formularzy tylko za pomocą klawiatury? Jak byś to zrobił?

## Przesyłanie danych do serwera

Teraz, gdy mamy funkcjonalny interfejs użytkownika, kolejnym krokiem jest przesłanie danych do naszego serwera. Zróbmy szybki test za pomocą naszego obecnego kodu: co się dzieje, gdy klikniesz przycisk *Login* lub *Register*?

Czy zauważyłeś zmianę w sekcji URL przeglądarki?

![Zrzut ekranu pokazujący zmianę URL przeglądarki po kliknięciu przycisku Register](../../../../translated_images/click-register.e89a30bf0d4bc9ca867dc537c4cea679a7c26368bd790969082f524fed2355bc.pl.png)

Domyślna akcja dla `<form>` to przesłanie formularza do bieżącego URL serwera za pomocą [metody GET](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3), dołączając dane formularza bezpośrednio do URL. Ta metoda ma jednak pewne ograniczenia:

- Przesyłane dane są bardzo ograniczone pod względem rozmiaru (około 2000 znaków)
- Dane są bezpośrednio widoczne w URL (co nie jest idealne dla haseł)
- Nie działa z przesyłaniem plików

Dlatego możesz zmienić ją na użycie [metody POST](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.5), która przesyła dane formularza do serwera w treści żądania HTTP, bez żadnych wcześniejszych ograniczeń.

> Chociaż POST jest najczęściej używaną metodą do przesyłania danych, [w niektórych specyficznych scenariuszach](https://www.w3.org/2001/tag/doc/whenToUseGet.html) preferowane jest użycie metody GET, na przykład podczas implementacji pola wyszukiwania.

### Zadanie

Dodaj właściwości `action` i `method` do formularza rejestracji:

```html
<form id="registerForm" action="//localhost:5000/api/accounts" method="POST">
```

Teraz spróbuj zarejestrować nowe konto ze swoim imieniem. Po kliknięciu przycisku *Register* powinieneś zobaczyć coś takiego:

![Okno przeglądarki pod adresem localhost:5000/api/accounts, pokazujące ciąg JSON z danymi użytkownika](../../../../translated_images/form-post.61de4ca1b964d91a9e338416e19f218504dd0af5f762fbebabfe7ae80edf885f.pl.png)

Jeśli wszystko pójdzie dobrze, serwer powinien odpowiedzieć na Twoje żądanie odpowiedzią [JSON](https://www.json.org/json-en.html) zawierającą dane utworzonego konta.

✅ Spróbuj zarejestrować się ponownie z tym samym imieniem. Co się dzieje?

## Przesyłanie danych bez przeładowania strony

Jak zapewne zauważyłeś, istnieje pewien problem z podejściem, którego właśnie użyliśmy: podczas przesyłania formularza opuszczamy naszą aplikację, a przeglądarka przekierowuje na URL serwera. Staramy się unikać wszystkich przeładowań stron w naszej aplikacji internetowej, ponieważ tworzymy [aplikację jednostronicową (SPA)](https://en.wikipedia.org/wiki/Single-page_application).

Aby przesłać dane formularza do serwera bez wymuszania przeładowania strony, musimy użyć kodu JavaScript. Zamiast umieszczać URL w właściwości `action` elementu `<form>`, możesz użyć dowolnego kodu JavaScript poprzedzonego ciągiem `javascript:`, aby wykonać niestandardową akcję. Korzystanie z tego oznacza również, że będziesz musiał zaimplementować niektóre zadania, które wcześniej były automatycznie wykonywane przez przeglądarkę:

- Pobranie danych formularza
- Konwersja i kodowanie danych formularza do odpowiedniego formatu
- Utworzenie żądania HTTP i przesłanie go do serwera

### Zadanie

Zamień właściwość `action` formularza rejestracji na:

```html
<form id="registerForm" action="javascript:register()">
```

Otwórz `app.js` i dodaj nową funkcję o nazwie `register`:

```js
function register() {
  const registerForm = document.getElementById('registerForm');
  const formData = new FormData(registerForm);
  const data = Object.fromEntries(formData);
  const jsonData = JSON.stringify(data);
}
```

Tutaj pobieramy element formularza za pomocą `getElementById()` i używamy pomocnika [`FormData`](https://developer.mozilla.org/docs/Web/API/FormData), aby wyodrębnić wartości z kontrolek formularza jako zestaw par klucz/wartość. Następnie konwertujemy dane na zwykły obiekt za pomocą [`Object.fromEntries()`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries) i ostatecznie serializujemy dane do [JSON](https://www.json.org/json-en.html), formatu powszechnie używanego do wymiany danych w sieci.

Dane są teraz gotowe do przesłania do serwera. Utwórz nową funkcję o nazwie `createAccount`:

```js
async function createAccount(account) {
  try {
    const response = await fetch('//localhost:5000/api/accounts', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: account
    });
    return await response.json();
  } catch (error) {
    return { error: error.message || 'Unknown error' };
  }
}
```

Co robi ta funkcja? Po pierwsze, zauważ słowo kluczowe `async`. Oznacza to, że funkcja zawiera kod, który będzie wykonywany [**asynchronicznie**](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function). Gdy jest używane razem ze słowem kluczowym `await`, pozwala czekać na wykonanie kodu asynchronicznego - na przykład czekanie na odpowiedź serwera tutaj - zanim kontynuujemy.

Oto krótki film o użyciu `async/await`:

[![Async i Await do zarządzania obietnicami](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "Async i Await do zarządzania obietnicami")

> 🎥 Kliknij obrazek powyżej, aby obejrzeć film o async/await.

Używamy API `fetch()`, aby przesłać dane JSON do serwera. Ta metoda przyjmuje 2 parametry:

- URL serwera, więc tutaj ponownie umieszczamy `//localhost:5000/api/accounts`.
- Ustawienia żądania. To tutaj ustawiamy metodę na `POST` i dostarczamy `body` dla żądania. Ponieważ przesyłamy dane JSON do serwera, musimy również ustawić nagłówek `Content-Type` na `application/json`, aby serwer wiedział, jak interpretować zawartość.

Ponieważ serwer odpowie na żądanie JSON-em, możemy użyć `await response.json()`, aby przeanalizować zawartość JSON i zwrócić wynikowy obiekt. Zauważ, że ta metoda jest asynchroniczna, więc używamy tutaj słowa kluczowego `await`, aby upewnić się, że wszelkie błędy podczas analizy również zostaną wychwycone.

Teraz dodaj trochę kodu do funkcji `register`, aby wywołać `createAccount()`:

```js
const result = await createAccount(jsonData);
```

Ponieważ używamy tutaj słowa kluczowego `await`, musimy dodać słowo kluczowe `async` przed funkcją register:

```js
async function register() {
```

Na koniec dodajmy kilka logów, aby sprawdzić wynik. Ostateczna funkcja powinna wyglądać tak:

```js
async function register() {
  const registerForm = document.getElementById('registerForm');
  const formData = new FormData(registerForm);
  const jsonData = JSON.stringify(Object.fromEntries(formData));
  const result = await createAccount(jsonData);

  if (result.error) {
    return console.log('An error occurred:', result.error);
  }

  console.log('Account created!', result);
}
```

To było trochę długie, ale dotarliśmy do końca! Jeśli otworzysz [narzędzia deweloperskie przeglądarki](https://developer.mozilla.org/docs/Learn/Common_questions/What_are_browser_developer_tools) i spróbujesz zarejestrować nowe konto, nie powinieneś zauważyć żadnej zmiany na stronie internetowej, ale w konsoli pojawi się komunikat potwierdzający, że wszystko działa.

![Zrzut ekranu pokazujący komunikat logowania w konsoli przeglądarki](../../../../translated_images/browser-console.efaf0b51aaaf67782a29e1a0bb32cc063f189b18e894eb5926e02f1abe864ec2.pl.png)

✅ Czy uważasz, że dane są przesyłane do serwera w sposób bezpieczny? Co jeśli ktoś byłby w stanie przechwycić żądanie? Możesz przeczytać o [HTTPS](https://en.wikipedia.org/wiki/HTTPS), aby dowiedzieć się więcej o bezpiecznej komunikacji danych.

## Walidacja danych

Jeśli spróbujesz zarejestrować nowe konto bez ustawienia nazwy użytkownika, możesz zauważyć, że serwer zwraca błąd z kodem statusu [400 (Bad Request)](https://developer.mozilla.org/docs/Web/HTTP/Status/400#:~:text=The%20HyperText%20Transfer%20Protocol%20(HTTP,%2C%20or%20deceptive%20request%20routing).).

Przed przesłaniem danych do serwera dobrą praktyką jest [walidacja danych formularza](https://developer.mozilla.org/docs/Learn/Forms/Form_validation) z wyprzedzeniem, aby upewnić się, że wysyłasz poprawne żądanie. Kontrolki formularzy HTML5 oferują wbudowaną walidację za pomocą różnych atrybutów:

- `required`: pole musi być wypełnione, w przeciwnym razie formularz nie może zostać przesłany.
- `minlength` i `maxlength`: definiują minimalną i maksymalną liczbę znaków w polach tekstowych.
- `min` i `max`: definiują minimalną i maksymalną wartość pola numerycznego.
- `type`: definiuje rodzaj oczekiwanych danych, takich jak `number`, `email`, `file` lub [inne wbudowane typy](https://developer.mozilla.org/docs/Web/HTML/Element/input). Ten atrybut może również zmienić wizualne renderowanie kontrolki formularza.
- `pattern`: pozwala zdefiniować wzorzec [wyrażenia regularnego](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Regular_Expressions), aby sprawdzić, czy wprowadzone dane są poprawne.
Wskazówka: możesz dostosować wygląd swoich elementów formularza w zależności od tego, czy są poprawne, czy nie, używając pseudoklas CSS `:valid` i `:invalid`.
### Zadanie

Aby utworzyć poprawne nowe konto, wymagane są dwa pola: nazwa użytkownika i waluta, pozostałe pola są opcjonalne. Zaktualizuj HTML formularza, używając zarówno atrybutu `required`, jak i tekstu w etykiecie pola, aby to uwzględnić:

```html
<label for="user">Username (required)</label>
<input id="user" name="user" type="text" required>
...
<label for="currency">Currency (required)</label>
<input id="currency" name="currency" type="text" value="$" required>
```

Chociaż ta konkretna implementacja serwera nie narzuca ograniczeń dotyczących maksymalnej długości pól, zawsze warto ustalić rozsądne limity dla wprowadzanych przez użytkownika danych tekstowych.

Dodaj atrybut `maxlength` do pól tekstowych:

```html
<input id="user" name="user" type="text" maxlength="20" required>
...
<input id="currency" name="currency" type="text" value="$" maxlength="5" required>
...
<input id="description" name="description" type="text" maxlength="100">
```

Teraz, jeśli naciśniesz przycisk *Zarejestruj się* i któreś z pól nie spełnia zdefiniowanych zasad walidacji, powinieneś zobaczyć coś takiego:

![Zrzut ekranu pokazujący błąd walidacji podczas próby przesłania formularza](../../../../translated_images/validation-error.8bd23e98d416c22f80076d04829a4bb718e0e550fd622862ef59008ccf0d5dce.pl.png)

Walidacja taka, jak ta, wykonywana *przed* wysłaniem danych na serwer, nazywana jest walidacją **po stronie klienta**. Jednak należy pamiętać, że nie zawsze możliwe jest przeprowadzenie wszystkich sprawdzeń bez wysyłania danych. Na przykład, nie możemy tutaj sprawdzić, czy konto z tą samą nazwą użytkownika już istnieje, bez wysłania zapytania do serwera. Dodatkowa walidacja wykonywana na serwerze nazywana jest walidacją **po stronie serwera**.

Zazwyczaj obie metody muszą być zaimplementowane. Walidacja po stronie klienta poprawia doświadczenie użytkownika, zapewniając natychmiastową informację zwrotną, ale walidacja po stronie serwera jest kluczowa, aby upewnić się, że dane użytkownika, które przetwarzasz, są poprawne i bezpieczne.

---

## 🚀 Wyzwanie

Wyświetl komunikat o błędzie w HTML, jeśli użytkownik już istnieje.

Oto przykład, jak może wyglądać ostateczna strona logowania po dodaniu stylów:

![Zrzut ekranu strony logowania po dodaniu stylów CSS](../../../../translated_images/result.96ef01f607bf856aa9789078633e94a4f7664d912f235efce2657299becca483.pl.png)

## Quiz po wykładzie

[Quiz po wykładzie](https://ff-quizzes.netlify.app/web/quiz/44)

## Przegląd i samodzielna nauka

Programiści wykazali się dużą kreatywnością w tworzeniu formularzy, szczególnie w zakresie strategii walidacji. Dowiedz się więcej o różnych przepływach formularzy, przeglądając [CodePen](https://codepen.com); czy znajdziesz jakieś interesujące i inspirujące formularze?

## Zadanie

[Stwórz styl dla swojej aplikacji bankowej](assignment.md)

---

**Zastrzeżenie**:  
Ten dokument został przetłumaczony za pomocą usługi tłumaczenia AI [Co-op Translator](https://github.com/Azure/co-op-translator). Chociaż dokładamy wszelkich starań, aby zapewnić poprawność tłumaczenia, prosimy pamiętać, że automatyczne tłumaczenia mogą zawierać błędy lub nieścisłości. Oryginalny dokument w jego rodzimym języku powinien być uznawany za autorytatywne źródło. W przypadku informacji o kluczowym znaczeniu zaleca się skorzystanie z profesjonalnego tłumaczenia przez człowieka. Nie ponosimy odpowiedzialności za jakiekolwiek nieporozumienia lub błędne interpretacje wynikające z użycia tego tłumaczenia.