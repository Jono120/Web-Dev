<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "8a07db14e75ac62f013b7de5df05981d",
  "translation_date": "2025-08-28T15:40:23+00:00",
  "source_file": "7-bank-project/1-template-route/README.md",
  "language_code": "tl"
}
-->
# Gumawa ng Banking App Bahagi 1: HTML Templates at Routes sa isang Web App

## Pre-Lecture Quiz

[Pre-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/41)

### Panimula

Simula nang maimbento ang JavaScript sa mga browser, ang mga website ay naging mas interactive at mas komplikado kaysa dati. Ang mga web technology ay karaniwang ginagamit ngayon upang lumikha ng mga ganap na functional na application na tumatakbo direkta sa browser, na tinatawag nating [web applications](https://en.wikipedia.org/wiki/Web_application). Dahil ang mga web app ay lubos na interactive, ayaw ng mga user na maghintay ng buong page reload tuwing may gagawing aksyon. Kaya ginagamit ang JavaScript upang direktang i-update ang HTML gamit ang DOM, para sa mas maayos na karanasan ng user.

Sa araling ito, ilalatag natin ang pundasyon para gumawa ng web app ng bangko, gamit ang HTML templates upang lumikha ng maraming screen na maaaring ipakita at i-update nang hindi kailangang i-reload ang buong HTML page.

### Kinakailangan

Kailangan mo ng lokal na web server upang subukan ang web app na gagawin natin sa araling ito. Kung wala ka pa nito, maaari mong i-install ang [Node.js](https://nodejs.org) at gamitin ang command na `npx lite-server` mula sa iyong project folder. Magkakaroon ito ng lokal na web server at bubuksan ang iyong app sa browser.

### Paghahanda

Sa iyong computer, gumawa ng folder na pinangalanang `bank` na may file na `index.html` sa loob nito. Magsisimula tayo mula sa HTML [boilerplate](https://en.wikipedia.org/wiki/Boilerplate_code):

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

## HTML Templates

Kung nais mong lumikha ng maraming screen para sa isang web page, isang solusyon ay ang gumawa ng isang HTML file para sa bawat screen na nais mong ipakita. Gayunpaman, ang solusyong ito ay may ilang abala:

- Kailangan mong i-reload ang buong HTML kapag nagpapalit ng screen, na maaaring mabagal.
- Mahirap magbahagi ng data sa pagitan ng iba't ibang screen.

Isang alternatibo ay ang magkaroon lamang ng isang HTML file, at magtakda ng maraming [HTML templates](https://developer.mozilla.org/docs/Web/HTML/Element/template) gamit ang `<template>` na elemento. Ang template ay isang reusable na HTML block na hindi ipinapakita ng browser, at kailangang i-instantiate sa runtime gamit ang JavaScript.

### Gawain

Gagawa tayo ng banking app na may dalawang screen: ang login page at ang dashboard. Una, magdagdag tayo sa HTML body ng placeholder element na gagamitin natin upang i-instantiate ang iba't ibang screen ng ating app:

```html
<div id="app">Loading...</div>
```

Binigyan natin ito ng `id` upang mas madali itong mahanap gamit ang JavaScript mamaya.

> Tip: Dahil ang nilalaman ng elementong ito ay papalitan, maaari tayong maglagay ng loading message o indicator na ipapakita habang naglo-load ang app.

Susunod, magdagdag tayo sa ibaba ng HTML template para sa login page. Sa ngayon, maglalagay lamang tayo ng pamagat at isang seksyon na naglalaman ng link na gagamitin natin para sa navigation.

```html
<template id="login">
  <h1>Bank App</h1>
  <section>
    <a href="/dashboard">Login</a>
  </section>
</template>
```

Pagkatapos, magdagdag tayo ng isa pang HTML template para sa dashboard page. Ang page na ito ay maglalaman ng iba't ibang seksyon:

- Isang header na may pamagat at logout link
- Ang kasalukuyang balanse ng bank account
- Isang listahan ng mga transaksyon, na ipinapakita sa isang table

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

> Tip: Kapag gumagawa ng HTML templates, kung nais mong makita kung ano ang magiging hitsura nito, maaari mong i-comment out ang `<template>` at `</template>` na mga linya sa pamamagitan ng pag-enclose sa kanila gamit ang `<!-- -->`.

✅ Bakit sa tingin mo gumagamit tayo ng `id` attributes sa mga template? Maaari ba tayong gumamit ng iba tulad ng classes?

## Pagpapakita ng Templates gamit ang JavaScript

Kung susubukan mo ang kasalukuyang HTML file sa browser, makikita mong natigil ito sa pagpapakita ng `Loading...`. Ito ay dahil kailangan nating magdagdag ng JavaScript code upang i-instantiate at ipakita ang mga HTML templates.

Ang pag-instantiate ng template ay karaniwang ginagawa sa 3 hakbang:

1. Kunin ang template element sa DOM, halimbawa gamit ang [`document.getElementById`](https://developer.mozilla.org/docs/Web/API/Document/getElementById).
2. I-clone ang template element, gamit ang [`cloneNode`](https://developer.mozilla.org/docs/Web/API/Node/cloneNode).
3. I-attach ito sa DOM sa ilalim ng isang visible na elemento, halimbawa gamit ang [`appendChild`](https://developer.mozilla.org/docs/Web/API/Node/appendChild).

✅ Bakit kailangan nating i-clone ang template bago ito i-attach sa DOM? Ano sa tingin mo ang mangyayari kung laktawan natin ang hakbang na ito?

### Gawain

Gumawa ng bagong file na pinangalanang `app.js` sa iyong project folder at i-import ang file na iyon sa `<head>` na seksyon ng iyong HTML:

```html
<script src="app.js" defer></script>
```

Ngayon sa `app.js`, gagawa tayo ng bagong function na `updateRoute`:

```js
function updateRoute(templateId) {
  const template = document.getElementById(templateId);
  const view = template.content.cloneNode(true);
  const app = document.getElementById('app');
  app.innerHTML = '';
  app.appendChild(view);
}
```

Ang ginagawa natin dito ay eksaktong ang 3 hakbang na inilarawan sa itaas. Ini-instantiate natin ang template na may `id` na `templateId`, at inilalagay ang cloned content nito sa loob ng placeholder ng ating app. Tandaan na kailangan nating gumamit ng `cloneNode(true)` upang makopya ang buong subtree ng template.

Ngayon tawagin ang function na ito gamit ang isa sa mga template at tingnan ang resulta.

```js
updateRoute('login');
```

✅ Ano ang layunin ng code na ito `app.innerHTML = '';`? Ano ang mangyayari kung wala ito?

## Paglikha ng Routes

Kapag pinag-uusapan ang isang web app, tinatawag nating *Routing* ang layunin na i-map ang **URLs** sa mga partikular na screen na dapat ipakita. Sa isang website na may maraming HTML files, ito ay awtomatikong ginagawa dahil ang mga file path ay nakikita sa URL. Halimbawa, gamit ang mga file na ito sa iyong project folder:

```
mywebsite/index.html
mywebsite/login.html
mywebsite/admin/index.html
```

Kung gagawa ka ng web server na may `mywebsite` bilang root, ang URL mapping ay magiging:

```
https://site.com            --> mywebsite/index.html
https://site.com/login.html --> mywebsite/login.html
https://site.com/admin/     --> mywebsite/admin/index.html
```

Gayunpaman, para sa ating web app na gumagamit ng isang HTML file na naglalaman ng lahat ng screen, ang default na behavior na ito ay hindi makakatulong. Kailangan nating manu-manong gawin ang map na ito at i-update ang ipinapakitang template gamit ang JavaScript.

### Gawain

Gagamit tayo ng simpleng object upang mag-implement ng [map](https://en.wikipedia.org/wiki/Associative_array) sa pagitan ng URL paths at ng ating mga template. Idagdag ang object na ito sa itaas ng iyong `app.js` file.

```js
const routes = {
  '/login': { templateId: 'login' },
  '/dashboard': { templateId: 'dashboard' },
};
```

Ngayon, baguhin natin nang kaunti ang `updateRoute` function. Sa halip na direktang ipasa ang `templateId` bilang argumento, nais nating kunin ito sa pamamagitan ng pagtingin muna sa kasalukuyang URL, at pagkatapos ay gamitin ang ating map upang makuha ang kaukulang template ID value. Maaari nating gamitin ang [`window.location.pathname`](https://developer.mozilla.org/docs/Web/API/Location/pathname) upang makuha lamang ang path section mula sa URL.

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

Dito, in-map natin ang mga routes na idineklara natin sa kaukulang template. Maaari mong subukan kung gumagana ito nang tama sa pamamagitan ng manu-manong pagbabago ng URL sa iyong browser.

✅ Ano ang mangyayari kung maglagay ka ng unknown path sa URL? Paano natin ito masosolusyunan?

## Pagdaragdag ng Navigation

Ang susunod na hakbang para sa ating app ay ang magdagdag ng kakayahang mag-navigate sa pagitan ng mga page nang hindi kailangang manu-manong baguhin ang URL. Ito ay nangangahulugan ng dalawang bagay:

1. I-update ang kasalukuyang URL
2. I-update ang ipinapakitang template base sa bagong URL

Naasikaso na natin ang pangalawang bahagi gamit ang `updateRoute` function, kaya kailangan nating alamin kung paano i-update ang kasalukuyang URL.

Gagamit tayo ng JavaScript at partikular ang [`history.pushState`](https://developer.mozilla.org/docs/Web/API/History/pushState) na nagbibigay-daan upang i-update ang URL at lumikha ng bagong entry sa browsing history, nang hindi nire-reload ang HTML.

> Tandaan: Habang ang HTML anchor element [`<a href>`](https://developer.mozilla.org/docs/Web/HTML/Element/a) ay maaaring gamitin upang lumikha ng hyperlinks sa iba't ibang URL, ito ay magre-reload ng HTML bilang default. Kailangang pigilan ang behavior na ito kapag nagha-handle ng routing gamit ang custom na JavaScript, gamit ang `preventDefault()` function sa click event.

### Gawain

Gumawa tayo ng bagong function na magagamit upang mag-navigate sa ating app:

```js
function navigate(path) {
  window.history.pushState({}, path, path);
  updateRoute();
}
```

Ang method na ito ay unang ina-update ang kasalukuyang URL base sa ibinigay na path, pagkatapos ay ina-update ang template. Ang property na `window.location.origin` ay nagbabalik ng URL root, na nagbibigay-daan upang muling buuin ang isang kumpletong URL mula sa ibinigay na path.

Ngayon na mayroon na tayong function na ito, maaari nating asikasuhin ang problema kung ang isang path ay hindi tumutugma sa anumang naitalagang route. Babaguhin natin ang `updateRoute` function sa pamamagitan ng pagdaragdag ng fallback sa isa sa mga umiiral na route kung hindi tayo makahanap ng tugma.

```js
function updateRoute() {
  const path = window.location.pathname;
  const route = routes[path];

  if (!route) {
    return navigate('/login');
  }

  ...
```

Kung ang isang route ay hindi matagpuan, ire-redirect tayo ngayon sa `login` page.

Ngayon, gumawa tayo ng function upang makuha ang URL kapag na-click ang isang link, at upang pigilan ang default na behavior ng browser sa link:

```js
function onLinkClick(event) {
  event.preventDefault();
  navigate(event.target.href);
}
```

Kumpletuhin natin ang navigation system sa pamamagitan ng pagdaragdag ng bindings sa ating *Login* at *Logout* links sa HTML.

```html
<a href="/dashboard" onclick="onLinkClick(event)">Login</a>
...
<a href="/login" onclick="onLinkClick(event)">Logout</a>
```

Ang `event` object sa itaas ay kinukuha ang `click` event at ipinapasa ito sa ating `onLinkClick` function.

Gamit ang [`onclick`](https://developer.mozilla.org/docs/Web/API/GlobalEventHandlers/onclick) attribute, i-bind ang `click` event sa JavaScript code, dito ang tawag sa `navigate()` function.

Subukang i-click ang mga link na ito, dapat ay kaya mo nang mag-navigate sa pagitan ng iba't ibang screen ng iyong app.

✅ Ang `history.pushState` method ay bahagi ng HTML5 standard at na-implement sa [lahat ng modernong browser](https://caniuse.com/?search=pushState). Kung gumagawa ka ng web app para sa mas lumang browser, mayroong trick na maaari mong gamitin bilang kapalit ng API na ito: gamit ang [hash (`#`)](https://en.wikipedia.org/wiki/URI_fragment) bago ang path, maaari kang mag-implement ng routing na gumagana sa regular na anchor navigation at hindi nire-reload ang page, dahil ang layunin nito ay lumikha ng internal links sa loob ng isang page.

## Paghawak sa Back at Forward Buttons ng Browser

Ang paggamit ng `history.pushState` ay lumilikha ng mga bagong entry sa navigation history ng browser. Maaari mong tingnan ito sa pamamagitan ng pag-hold sa *back button* ng iyong browser, dapat itong magpakita ng ganito:

![Screenshot ng navigation history](../../../../translated_images/history.7fdabbafa521e06455b738d3dafa3ff41d3071deae60ead8c7e0844b9ed987d8.tl.png)

Kung susubukan mong i-click ang back button nang ilang beses, makikita mong nagbabago ang kasalukuyang URL at na-update ang history, ngunit ang parehong template ang nananatiling ipinapakita.

Ito ay dahil hindi alam ng application na kailangan nating tawagan ang `updateRoute()` tuwing nagbabago ang history. Kung titingnan mo ang [`history.pushState` documentation](https://developer.mozilla.org/docs/Web/API/History/pushState), makikita mo na kung nagbago ang state - ibig sabihin ay lumipat tayo sa ibang URL - ang [`popstate`](https://developer.mozilla.org/docs/Web/API/Window/popstate_event) event ay na-trigger. Gagamitin natin ito upang ayusin ang isyung iyon.

### Gawain

Upang matiyak na ang ipinapakitang template ay na-update kapag nagbago ang browser history, mag-a-attach tayo ng bagong function na tumatawag sa `updateRoute()`. Gagawin natin ito sa ibaba ng ating `app.js` file:

```js
window.onpopstate = () => updateRoute();
updateRoute();
```

> Tandaan: Gumamit tayo ng [arrow function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Functions/Arrow_functions) dito upang ideklara ang ating `popstate` event handler para sa pagiging maikli, ngunit ang regular na function ay gagana rin nang pareho.

Narito ang isang refresher video tungkol sa arrow functions:

[![Arrow Functions](https://img.youtube.com/vi/OP6eEbOj2sc/0.jpg)](https://youtube.com/watch?v=OP6eEbOj2sc "Arrow Functions")

> 🎥 I-click ang imahe sa itaas para sa isang video tungkol sa arrow functions.

Ngayon subukang gamitin ang back at forward buttons ng iyong browser, at tingnan kung ang ipinapakitang route ay na-update nang tama sa pagkakataong ito.

---

## 🚀 Hamon

Magdagdag ng bagong template at route para sa isang ikatlong page na nagpapakita ng credits para sa app na ito.

## Post-Lecture Quiz

[Post-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/42)

## Review at Self Study

Ang routing ay isa sa mga nakakagulat na mahirap na bahagi ng web development, lalo na habang ang web ay lumilipat mula sa page refresh behaviors patungo sa Single Page Application page refreshes. Magbasa nang kaunti tungkol sa [kung paano hinahawakan ng Azure Static Web App service](https://docs.microsoft.com/azure/static-web-apps/routes/?WT.mc_id=academic-77807-sagibbon) ang routing. Kaya mo bang ipaliwanag kung bakit ang ilan sa mga desisyong inilarawan sa dokumentong iyon ay kinakailangan?

## Takdang-Aralin

[Pagbutihin ang routing](assignment.md)

---

**Paunawa**:  
Ang dokumentong ito ay isinalin gamit ang AI translation service na [Co-op Translator](https://github.com/Azure/co-op-translator). Bagama't sinisikap naming maging tumpak, tandaan na ang mga awtomatikong pagsasalin ay maaaring maglaman ng mga pagkakamali o hindi pagkakatugma. Ang orihinal na dokumento sa kanyang katutubong wika ang dapat ituring na opisyal na sanggunian. Para sa mahalagang impormasyon, inirerekomenda ang propesyonal na pagsasalin ng tao. Hindi kami mananagot sa anumang hindi pagkakaunawaan o maling interpretasyon na dulot ng paggamit ng pagsasaling ito.