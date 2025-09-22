<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "8a07db14e75ac62f013b7de5df05981d",
  "translation_date": "2025-08-29T14:07:33+00:00",
  "source_file": "7-bank-project/1-template-route/README.md",
  "language_code": "de"
}
-->
# Erstellen einer Banking-App Teil 1: HTML-Vorlagen und Routen in einer Web-App

## Quiz vor der Vorlesung

[Quiz vor der Vorlesung](https://ff-quizzes.netlify.app/web/quiz/41)

### Einführung

Seit der Einführung von JavaScript in Browsern werden Websites interaktiver und komplexer als je zuvor. Webtechnologien werden mittlerweile häufig verwendet, um vollständig funktionale Anwendungen zu erstellen, die direkt im Browser laufen und die wir [Webanwendungen](https://de.wikipedia.org/wiki/Webanwendung) nennen. Da Web-Apps hochinteraktiv sind, möchten Benutzer nicht bei jeder Aktion auf ein vollständiges Neuladen der Seite warten. Aus diesem Grund wird JavaScript verwendet, um das HTML direkt über den DOM zu aktualisieren und so ein reibungsloseres Benutzererlebnis zu bieten.

In dieser Lektion legen wir die Grundlagen für die Erstellung einer Banking-Web-App, indem wir HTML-Vorlagen verwenden, um mehrere Bildschirme zu erstellen, die angezeigt und aktualisiert werden können, ohne die gesamte HTML-Seite neu laden zu müssen.

### Voraussetzungen

Du benötigst einen lokalen Webserver, um die Web-App zu testen, die wir in dieser Lektion erstellen. Falls du keinen hast, kannst du [Node.js](https://nodejs.org) installieren und den Befehl `npx lite-server` aus deinem Projektordner ausführen. Dadurch wird ein lokaler Webserver erstellt und deine App in einem Browser geöffnet.

### Vorbereitung

Erstelle auf deinem Computer einen Ordner namens `bank` mit einer Datei namens `index.html` darin. Wir beginnen mit diesem HTML-[Boilerplate](https://de.wikipedia.org/wiki/Boilerplate-Code):

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bank App</title>
  </head>
  <body>
    <!-- This is where you'll work -->
  </body>
</html>
```

---

## HTML-Vorlagen

Wenn du mehrere Bildschirme für eine Webseite erstellen möchtest, wäre eine Lösung, für jeden Bildschirm, den du anzeigen möchtest, eine separate HTML-Datei zu erstellen. Diese Lösung bringt jedoch einige Nachteile mit sich:

- Du musst das gesamte HTML neu laden, wenn du den Bildschirm wechselst, was langsam sein kann.
- Es ist schwierig, Daten zwischen den verschiedenen Bildschirmen zu teilen.

Eine andere Herangehensweise besteht darin, nur eine HTML-Datei zu haben und mehrere [HTML-Vorlagen](https://developer.mozilla.org/docs/Web/HTML/Element/template) mit dem `<template>`-Element zu definieren. Eine Vorlage ist ein wiederverwendbarer HTML-Block, der vom Browser nicht angezeigt wird und zur Laufzeit mithilfe von JavaScript instanziiert werden muss.

### Aufgabe

Wir erstellen eine Banking-App mit zwei Bildschirmen: der Login-Seite und dem Dashboard. Zunächst fügen wir im HTML-Body ein Platzhalter-Element hinzu, das wir verwenden, um die verschiedenen Bildschirme unserer App zu instanziieren:

```html
<div id="app">Loading...</div>
```

Wir geben ihm eine `id`, um es später mit JavaScript leichter zu finden.

> Tipp: Da der Inhalt dieses Elements ersetzt wird, können wir eine Ladeanzeige oder Nachricht einfügen, die angezeigt wird, während die App lädt.

Als Nächstes fügen wir unterhalb die HTML-Vorlage für die Login-Seite hinzu. Für den Moment fügen wir dort nur einen Titel und einen Abschnitt mit einem Link ein, den wir für die Navigation verwenden werden.

```html
<template id="login">
  <h1>Bank App</h1>
  <section>
    <a href="/dashboard">Login</a>
  </section>
</template>
```

Dann fügen wir eine weitere HTML-Vorlage für die Dashboard-Seite hinzu. Diese Seite wird verschiedene Abschnitte enthalten:

- Eine Kopfzeile mit einem Titel und einem Logout-Link
- Den aktuellen Kontostand
- Eine Liste von Transaktionen, die in einer Tabelle angezeigt werden

```html
<template id="dashboard">
  <header>
    <h1>Bank App</h1>
    <a href="/login">Logout</a>
  </header>
  <section>
    Balance: 100$
  </section>
  <section>
    <h2>Transactions</h2>
    <table>
      <thead>
        <tr>
          <th>Date</th>
          <th>Object</th>
          <th>Amount</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
  </section>
</template>
```

> Tipp: Wenn du HTML-Vorlagen erstellst und sehen möchtest, wie sie aussehen, kannst du die `<template>`- und `</template>`-Zeilen auskommentieren, indem du sie mit `<!-- -->` umschließt.

✅ Warum denkst du, verwenden wir `id`-Attribute für die Vorlagen? Könnten wir stattdessen etwas anderes wie Klassen verwenden?

## Vorlagen mit JavaScript anzeigen

Wenn du deine aktuelle HTML-Datei in einem Browser ausprobierst, wirst du sehen, dass sie bei `Loading...` hängen bleibt. Das liegt daran, dass wir etwas JavaScript-Code hinzufügen müssen, um die HTML-Vorlagen zu instanziieren und anzuzeigen.

Das Instanziieren einer Vorlage erfolgt normalerweise in drei Schritten:

1. Abrufen des Vorlagenelements im DOM, z. B. mit [`document.getElementById`](https://developer.mozilla.org/docs/Web/API/Document/getElementById).
2. Klonen des Vorlagenelements mit [`cloneNode`](https://developer.mozilla.org/docs/Web/API/Node/cloneNode).
3. Anhängen an das DOM unter einem sichtbaren Element, z. B. mit [`appendChild`](https://developer.mozilla.org/docs/Web/API/Node/appendChild).

✅ Warum müssen wir die Vorlage klonen, bevor wir sie an das DOM anhängen? Was denkst du, würde passieren, wenn wir diesen Schritt überspringen?

### Aufgabe

Erstelle eine neue Datei namens `app.js` in deinem Projektordner und importiere diese Datei im `<head>`-Abschnitt deines HTML:

```html
<script src="app.js" defer></script>
```

Nun erstellen wir in `app.js` eine neue Funktion `updateRoute`:

```js
function updateRoute(templateId) {
  const template = document.getElementById(templateId);
  const view = template.content.cloneNode(true);
  const app = document.getElementById('app');
  app.innerHTML = '';
  app.appendChild(view);
}
```

Was wir hier tun, sind genau die drei oben beschriebenen Schritte. Wir instanziieren die Vorlage mit der `id` `templateId` und platzieren deren geklonten Inhalt in unserem App-Platzhalter. Beachte, dass wir `cloneNode(true)` verwenden müssen, um den gesamten Unterbaum der Vorlage zu kopieren.

Rufe nun diese Funktion mit einer der Vorlagen auf und sieh dir das Ergebnis an.

```js
updateRoute('login');
```

✅ Was ist der Zweck dieses Codes `app.innerHTML = '';`? Was passiert ohne ihn?

## Routen erstellen

Wenn wir über eine Web-App sprechen, nennen wir *Routing* die Absicht, **URLs** bestimmten Bildschirmen zuzuordnen, die angezeigt werden sollen. Auf einer Website mit mehreren HTML-Dateien geschieht dies automatisch, da die Dateipfade in der URL reflektiert werden. Zum Beispiel mit diesen Dateien in deinem Projektordner:

```
mywebsite/index.html
mywebsite/login.html
mywebsite/admin/index.html
```

Wenn du einen Webserver mit `mywebsite` als Root erstellst, lautet die URL-Zuordnung:

```
https://site.com            --> mywebsite/index.html
https://site.com/login.html --> mywebsite/login.html
https://site.com/admin/     --> mywebsite/admin/index.html
```

Für unsere Web-App verwenden wir jedoch eine einzige HTML-Datei, die alle Bildschirme enthält, sodass dieses Standardverhalten uns nicht hilft. Wir müssen diese Zuordnung manuell erstellen und die angezeigte Vorlage mithilfe von JavaScript aktualisieren.

### Aufgabe

Wir verwenden ein einfaches Objekt, um eine [Map](https://de.wikipedia.org/wiki/Assoziatives_Array) zwischen URL-Pfaden und unseren Vorlagen zu implementieren. Füge dieses Objekt oben in deiner `app.js`-Datei hinzu.

```js
const routes = {
  '/login': { templateId: 'login' },
  '/dashboard': { templateId: 'dashboard' },
};
```

Nun ändern wir die Funktion `updateRoute` ein wenig. Anstatt direkt die `templateId` als Argument zu übergeben, möchten wir sie abrufen, indem wir zuerst die aktuelle URL betrachten und dann unsere Map verwenden, um den entsprechenden Wert der `templateId` zu erhalten. Wir können [`window.location.pathname`](https://developer.mozilla.org/docs/Web/API/Location/pathname) verwenden, um nur den Pfadabschnitt aus der URL zu erhalten.

```js
function updateRoute() {
  const path = window.location.pathname;
  const route = routes[path];

  const template = document.getElementById(route.templateId);
  const view = template.content.cloneNode(true);
  const app = document.getElementById('app');
  app.innerHTML = '';
  app.appendChild(view);
}
```

Hier haben wir die von uns deklarierten Routen den entsprechenden Vorlagen zugeordnet. Du kannst testen, ob es korrekt funktioniert, indem du die URL manuell in deinem Browser änderst.

✅ Was passiert, wenn du einen unbekannten Pfad in die URL eingibst? Wie könnten wir das lösen?

## Navigation hinzufügen

Der nächste Schritt für unsere App ist es, die Möglichkeit hinzuzufügen, zwischen Seiten zu navigieren, ohne die URL manuell ändern zu müssen. Das bedeutet zwei Dinge:

1. Aktualisierung der aktuellen URL
2. Aktualisierung der angezeigten Vorlage basierend auf der neuen URL

Den zweiten Teil haben wir bereits mit der Funktion `updateRoute` erledigt, daher müssen wir herausfinden, wie wir die aktuelle URL aktualisieren.

Wir müssen JavaScript verwenden, insbesondere [`history.pushState`](https://developer.mozilla.org/docs/Web/API/History/pushState), das es ermöglicht, die URL zu aktualisieren und einen neuen Eintrag in der Browser-Historie zu erstellen, ohne das HTML neu zu laden.

> Hinweis: Während das HTML-Ankerelement [`<a href>`](https://developer.mozilla.org/docs/Web/HTML/Element/a) allein verwendet werden kann, um Hyperlinks zu verschiedenen URLs zu erstellen, wird dadurch standardmäßig das HTML neu geladen. Es ist notwendig, dieses Verhalten zu verhindern, wenn Routing mit benutzerdefiniertem JavaScript behandelt wird, indem die Funktion `preventDefault()` für das Klickereignis verwendet wird.

### Aufgabe

Erstellen wir eine neue Funktion, die wir für die Navigation in unserer App verwenden können:

```js
function navigate(path) {
  window.history.pushState({}, path, path);
  updateRoute();
}
```

Diese Methode aktualisiert zuerst die aktuelle URL basierend auf dem angegebenen Pfad und dann die Vorlage. Die Eigenschaft `window.location.origin` gibt die URL-Root zurück, sodass wir eine vollständige URL aus einem gegebenen Pfad rekonstruieren können.

Da wir diese Funktion haben, können wir uns um das Problem kümmern, das wir haben, wenn ein Pfad keiner definierten Route entspricht. Wir ändern die Funktion `updateRoute`, indem wir eine Rückfalloption zu einer der bestehenden Routen hinzufügen, falls wir keine Übereinstimmung finden.

```js
function updateRoute() {
  const path = window.location.pathname;
  const route = routes[path];

  if (!route) {
    return navigate('/login');
  }

  ...
```

Wenn keine Route gefunden werden kann, leiten wir jetzt zur `login`-Seite weiter.

Erstellen wir nun eine Funktion, um die URL zu erhalten, wenn ein Link angeklickt wird, und um das Standardverhalten des Browsers für Links zu verhindern:

```js
function onLinkClick(event) {
  event.preventDefault();
  navigate(event.target.href);
}
```

Vervollständigen wir das Navigationssystem, indem wir Bindungen zu unseren *Login*- und *Logout*-Links im HTML hinzufügen.

```html
<a href="/dashboard" onclick="onLinkClick(event)">Login</a>
...
<a href="/login" onclick="onLinkClick(event)">Logout</a>
```

Das oben genannte `event`-Objekt erfasst das `click`-Ereignis und übergibt es an unsere Funktion `onLinkClick`.

Verwende das [`onclick`](https://developer.mozilla.org/docs/Web/API/GlobalEventHandlers/onclick)-Attribut, um das `click`-Ereignis an JavaScript-Code zu binden, hier den Aufruf der Funktion `navigate()`.

Probiere aus, auf diese Links zu klicken. Du solltest jetzt zwischen den verschiedenen Bildschirmen deiner App navigieren können.

✅ Die Methode `history.pushState` ist Teil des HTML5-Standards und wird in [allen modernen Browsern](https://caniuse.com/?search=pushState) implementiert. Wenn du eine Web-App für ältere Browser erstellst, gibt es einen Trick, den du anstelle dieser API verwenden kannst: Mit einem [Hash (`#`)](https://de.wikipedia.org/wiki/URI-Fragment) vor dem Pfad kannst du ein Routing implementieren, das mit regulärer Anker-Navigation funktioniert und die Seite nicht neu lädt, da es ursprünglich dazu gedacht war, interne Links innerhalb einer Seite zu erstellen.

## Umgang mit den Vor- und Zurück-Buttons des Browsers

Die Verwendung von `history.pushState` erstellt neue Einträge in der Navigationshistorie des Browsers. Du kannst das überprüfen, indem du den *Zurück-Button* deines Browsers gedrückt hältst. Es sollte etwas wie folgt angezeigt werden:

![Screenshot der Navigationshistorie](../../../../translated_images/history.7fdabbafa521e06455b738d3dafa3ff41d3071deae60ead8c7e0844b9ed987d8.de.png)

Wenn du ein paar Mal auf den Zurück-Button klickst, wirst du sehen, dass sich die aktuelle URL ändert und die Historie aktualisiert wird, aber dieselbe Vorlage weiterhin angezeigt wird.

Das liegt daran, dass die Anwendung nicht weiß, dass wir `updateRoute()` jedes Mal aufrufen müssen, wenn sich die Historie ändert. Wenn du dir die Dokumentation zu [`history.pushState`](https://developer.mozilla.org/docs/Web/API/History/pushState) ansiehst, kannst du sehen, dass, wenn sich der Zustand ändert - das bedeutet, dass wir zu einer anderen URL gewechselt sind - das [`popstate`](https://developer.mozilla.org/docs/Web/API/Window/popstate_event)-Ereignis ausgelöst wird. Wir werden das verwenden, um dieses Problem zu beheben.

### Aufgabe

Um sicherzustellen, dass die angezeigte Vorlage aktualisiert wird, wenn sich die Browser-Historie ändert, fügen wir eine neue Funktion hinzu, die `updateRoute()` aufruft. Wir tun dies am Ende unserer `app.js`-Datei:

```js
window.onpopstate = () => updateRoute();
updateRoute();
```

> Hinweis: Wir haben hier eine [Arrow-Funktion](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Functions/Arrow_functions) verwendet, um unseren `popstate`-Ereignis-Handler aus Gründen der Kürze zu deklarieren, aber eine reguläre Funktion würde genauso funktionieren.

Hier ist ein Auffrischungsvideo zu Arrow-Funktionen:

[![Arrow-Funktionen](https://img.youtube.com/vi/OP6eEbOj2sc/0.jpg)](https://youtube.com/watch?v=OP6eEbOj2sc "Arrow-Funktionen")

> 🎥 Klicke auf das Bild oben für ein Video über Arrow-Funktionen.

Probiere nun die Vor- und Zurück-Buttons deines Browsers aus und überprüfe, ob die angezeigte Route diesmal korrekt aktualisiert wird.

---

## 🚀 Herausforderung

Füge eine neue Vorlage und Route für eine dritte Seite hinzu, die die Credits für diese App anzeigt.

## Quiz nach der Vorlesung

[Quiz nach der Vorlesung](https://ff-quizzes.netlify.app/web/quiz/42)

## Überprüfung & Selbststudium

Routing ist einer der überraschend kniffligen Teile der Webentwicklung, insbesondere da sich das Web von Seitenaktualisierungsverhalten zu Single-Page-Application-Aktualisierungen bewegt. Lies ein wenig darüber, [wie der Azure Static Web App-Dienst](https://docs.microsoft.com/azure/static-web-apps/routes/?WT.mc_id=academic-77807-sagibbon) Routing behandelt. Kannst du erklären, warum einige der in diesem Dokument beschriebenen Entscheidungen notwendig sind?

## Aufgabe

[Verbessere das Routing](assignment.md)

---

**Haftungsausschluss**:  
Dieses Dokument wurde mit dem KI-Übersetzungsdienst [Co-op Translator](https://github.com/Azure/co-op-translator) übersetzt. Obwohl wir uns um Genauigkeit bemühen, weisen wir darauf hin, dass automatisierte Übersetzungen Fehler oder Ungenauigkeiten enthalten können. Das Originaldokument in seiner ursprünglichen Sprache sollte als maßgebliche Quelle betrachtet werden. Für kritische Informationen wird eine professionelle menschliche Übersetzung empfohlen. Wir übernehmen keine Haftung für Missverständnisse oder Fehlinterpretationen, die sich aus der Nutzung dieser Übersetzung ergeben.