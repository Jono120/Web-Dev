<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "89d0df9854ed020f155e94882ae88d4c",
  "translation_date": "2025-08-28T16:28:24+00:00",
  "source_file": "7-bank-project/3-data/README.md",
  "language_code": "ne"
}
-->
# बैंकिङ एप निर्माण भाग ३: डेटा प्राप्ति र प्रयोग गर्ने विधिहरू

## प्रि-लेक्चर क्विज

[प्रि-लेक्चर क्विज](https://ff-quizzes.netlify.app/web/quiz/45)

### परिचय

हरेक वेब एप्लिकेसनको केन्द्रमा *डेटा* हुन्छ। डेटा विभिन्न प्रकारका हुन सक्छ, तर यसको मुख्य उद्देश्य सधैं प्रयोगकर्तालाई जानकारी देखाउनु हो। वेब एपहरू बढ्दो अन्तरक्रियात्मक र जटिल हुँदै गइरहेका छन्, जसले गर्दा प्रयोगकर्ताले जानकारी कसरी पहुँच गर्छ र यससँग कसरी अन्तरक्रिया गर्छ भन्ने कुरा वेब विकासको महत्त्वपूर्ण भाग बनेको छ।

यस पाठमा, हामीले कसरी सर्भरबाट डेटा असिन्क्रोनस रूपमा प्राप्त गर्ने र यो डेटा प्रयोग गरेर HTML पुनःलोड नगरी वेब पृष्ठमा जानकारी देखाउने भन्ने कुरा सिक्नेछौं।

### पूर्वआवश्यकता

यस पाठका लागि तपाईंले [लगइन र दर्ता फारम](../2-forms/README.md) निर्माण गरिसक्नुपर्छ। साथै, तपाईंले [Node.js](https://nodejs.org) स्थापना गर्नुपर्छ र [सर्भर API](../api/README.md) स्थानीय रूपमा चलाउनुपर्छ ताकि तपाईंले खाता डेटा प्राप्त गर्न सक्नुहुन्छ।

सर्भर सही रूपमा चलिरहेको छ कि छैन भनेर जाँच गर्न, टर्मिनलमा यो कमाण्ड चलाउनुहोस्:

```sh
curl http://localhost:5000/api
# -> should return "Bank API v1.0.0" as a result
```

---

## AJAX र डेटा प्राप्ति

परम्परागत वेबसाइटहरूले प्रयोगकर्ताले कुनै लिङ्क चयन गर्दा वा फारममार्फत डेटा पठाउँदा HTML पृष्ठ पुनःलोड गरेर सामग्री अद्यावधिक गर्छन्। नयाँ डेटा लोड गर्न प्रत्येक पटक, वेब सर्भरले नयाँ HTML पृष्ठ फिर्ता पठाउँछ, जसलाई ब्राउजरले पुनःप्रक्रिया गर्नुपर्छ। यसले प्रयोगकर्ताको हालको कार्यलाई अवरोध पुर्‍याउँछ र पुनःलोडको क्रममा अन्तरक्रियालाई सीमित गर्छ। यस वर्कफ्लोलाई *मल्टि-पेज एप्लिकेसन* (MPA) भनिन्छ।

![मल्टि-पेज एप्लिकेसनमा अद्यावधिक वर्कफ्लो](../../../../translated_images/mpa.7f7375a1a2d4aa779d3f928a2aaaf9ad76bcdeb05cfce2dc27ab126024050f51.ne.png)

जब वेब एप्लिकेसनहरू थप जटिल र अन्तरक्रियात्मक हुन थाले, [AJAX (Asynchronous JavaScript and XML)](https://en.wikipedia.org/wiki/Ajax_(programming)) नामक नयाँ प्रविधि देखा पर्‍यो। यस प्रविधिले वेब एपहरूलाई HTML पृष्ठ पुनःलोड नगरी सर्भरबाट डेटा असिन्क्रोनस रूपमा पठाउन र प्राप्त गर्न अनुमति दिन्छ, जसले गर्दा छिटो अद्यावधिक र सहज प्रयोगकर्ता अन्तरक्रिया सम्भव हुन्छ। सर्भरबाट नयाँ डेटा प्राप्त भएपछि, [DOM](https://developer.mozilla.org/docs/Web/API/Document_Object_Model) API प्रयोग गरेर हालको HTML पृष्ठलाई पनि JavaScript मार्फत अद्यावधिक गर्न सकिन्छ। समयसँगै, यो दृष्टिकोण [*सिंगल-पेज एप्लिकेसन* (SPA)](https://en.wikipedia.org/wiki/Single-page_application) मा विकसित भएको छ।

![सिंगल-पेज एप्लिकेसनमा अद्यावधिक वर्कफ्लो](../../../../translated_images/spa.268ec73b41f992c2a21ef9294235c6ae597b3c37e2c03f0494c2d8857325cc57.ne.png)

AJAX पहिलो पटक परिचय गराउँदा, असिन्क्रोनस रूपमा डेटा प्राप्त गर्न [`XMLHttpRequest`](https://developer.mozilla.org/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest) मात्र उपलब्ध API थियो। तर आधुनिक ब्राउजरहरूले अब अझ सुविधाजनक र शक्तिशाली [`Fetch` API](https://developer.mozilla.org/docs/Web/API/Fetch_API) पनि कार्यान्वयन गरेका छन्, जसले प्रॉमिस प्रयोग गर्छ र JSON डेटा ह्यान्डल गर्न अझ उपयुक्त छ।

> सबै आधुनिक ब्राउजरहरूले `Fetch API` समर्थन गर्छन्, तर यदि तपाईंको वेब एप्लिकेसन पुराना ब्राउजरहरूमा पनि काम गर्नुपर्छ भने, [caniuse.com मा अनुकूलता तालिका](https://caniuse.com/fetch) जाँच गर्नु सधैं राम्रो हुन्छ।

### कार्य

[अघिल्लो पाठमा](../2-forms/README.md) हामीले खाता सिर्जना गर्न दर्ता फारम कार्यान्वयन गरेका थियौं। अब हामीले विद्यमान खाताको प्रयोग गरेर लगइन गर्ने र यसको डेटा प्राप्त गर्ने कोड थप्नेछौं। `app.js` फाइल खोल्नुहोस् र नयाँ `login` फङ्सन थप्नुहोस्:

```js
async function login() {
  const loginForm = document.getElementById('loginForm')
  const user = loginForm.user.value;
}
```

यहाँ हामीले `getElementById()` प्रयोग गरेर फारम तत्व प्राप्त गर्छौं, र त्यसपछि `loginForm.user.value` बाट इनपुटबाट प्रयोगकर्ताको नाम प्राप्त गर्छौं। प्रत्येक फारम कन्ट्रोललाई यसको नाम (HTML मा `name` एट्रिब्युट प्रयोग गरेर सेट गरिएको) को रूपमा फारमको प्रोपर्टीबाट पहुँच गर्न सकिन्छ।

दर्ताका लागि हामीले गरेको जस्तै, हामीले सर्भर अनुरोध गर्न अर्को फङ्सन सिर्जना गर्नेछौं, तर यस पटक खाता डेटा प्राप्त गर्न:

```js
async function getAccount(user) {
  try {
    const response = await fetch('//localhost:5000/api/accounts/' + encodeURIComponent(user));
    return await response.json();
  } catch (error) {
    return { error: error.message || 'Unknown error' };
  }
}
```

हामी `fetch` API प्रयोग गरेर सर्भरबाट डेटा असिन्क्रोनस रूपमा अनुरोध गर्छौं, तर यस पटक हामीलाई URL बाहेक अन्य कुनै अतिरिक्त प्यारामिटर आवश्यक पर्दैन, किनभने हामी केवल डेटा सोध्दैछौं। डिफल्ट रूपमा, `fetch` ले [`GET`](https://developer.mozilla.org/docs/Web/HTTP/Methods/GET) HTTP अनुरोध सिर्जना गर्छ, जुन हामीलाई यहाँ चाहिएको हो।

✅ `encodeURIComponent()` एउटा फङ्सन हो जसले URL का लागि विशेष क्यारेक्टरहरूलाई एस्केप गर्छ। यदि हामीले यो फङ्सनलाई कल नगरी `user` मानलाई सिधै URL मा प्रयोग गर्‍यौं भने के समस्या हुन सक्छ?

अब हामीले हाम्रो `login` फङ्सनलाई `getAccount` प्रयोग गर्न अद्यावधिक गरौं:

```js
async function login() {
  const loginForm = document.getElementById('loginForm')
  const user = loginForm.user.value;
  const data = await getAccount(user);

  if (data.error) {
    return console.log('loginError', data.error);
  }

  account = data;
  navigate('/dashboard');
}
```

पहिले, `getAccount` असिन्क्रोनस फङ्सन भएकाले हामीले यसलाई `await` कीवर्डसँग मिलाउनुपर्छ ताकि सर्भरको नतिजाको प्रतीक्षा गर्न सकियोस्। कुनै पनि सर्भर अनुरोधमा जस्तै, हामीले त्रुटि अवस्थाहरूको पनि सामना गर्नुपर्छ। अहिलेका लागि, हामी केवल त्रुटि देखाउनको लागि एउटा लग सन्देश थप्नेछौं, र पछि यसमा फर्कनेछौं।

त्यसपछि हामीले डेटा कतै भण्डारण गर्नुपर्छ ताकि पछि ड्यासबोर्ड जानकारी देखाउन प्रयोग गर्न सकियोस्। किनभने `account` भेरिएबल अझै अवस्थित छैन, हामीले यसलाई हाम्रो फाइलको शीर्षमा एउटा ग्लोबल भेरिएबलको रूपमा सिर्जना गर्नेछौं:

```js
let account = null;
```

प्रयोगकर्ताको डेटा भेरिएबलमा सुरक्षित भएपछि, हामीले `navigate()` फङ्सन प्रयोग गरेर *लगइन* पृष्ठबाट *ड्यासबोर्ड* मा जान सक्छौं।

अन्ततः, हामीले लगइन फारम सबमिट हुँदा हाम्रो `login` फङ्सनलाई कल गर्नुपर्छ, HTML परिमार्जन गरेर:

```html
<form id="loginForm" action="javascript:login()">
```

नयाँ खाता दर्ता गरेर र त्यही खाता प्रयोग गरेर लगइन प्रयास गरेर सबै कुरा सही रूपमा काम गरिरहेको छ कि छैन परीक्षण गर्नुहोस्।

अर्को भागमा अघि बढ्नु अघि, हामीले `register` फङ्सनलाई पनि यसलाई थपेर पूरा गर्न सक्छौं:

```js
account = result;
navigate('/dashboard');
```

✅ के तपाईंलाई थाहा छ कि डिफल्ट रूपमा, तपाईंले *त्यही डोमेन र पोर्ट* बाट मात्र सर्भर API कल गर्न सक्नुहुन्छ जुन तपाईंले हेर्दै हुनुहुन्छ? यो ब्राउजरहरूले लागू गरेको सुरक्षा संयन्त्र हो। तर, हाम्रो वेब एप `localhost:3000` मा चलिरहेको छ भने सर्भर API `localhost:5000` मा चलिरहेको छ, यो किन काम गर्छ? [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/docs/Web/HTTP/CORS) नामक प्रविधि प्रयोग गरेर, यदि सर्भरले प्रतिक्रिया मा विशेष हेडरहरू थप्छ भने, विशिष्ट डोमेनहरूको लागि अपवादहरू अनुमति दिँदै क्रस-ओरिजिन HTTP अनुरोधहरू सम्भव छ।

> API हरूको बारेमा थप जान्नको लागि यो [पाठ](https://docs.microsoft.com/learn/modules/use-apis-discover-museum-art/?WT.mc_id=academic-77807-sagibbon) लिनुहोस्।

## HTML अद्यावधिक गरेर डेटा देखाउनुहोस्

अब हामीसँग प्रयोगकर्ताको डेटा छ, हामीले यो देखाउनको लागि विद्यमान HTML अद्यावधिक गर्नुपर्छ। हामीले पहिले नै `document.getElementById()` जस्तै प्रयोग गरेर DOM बाट तत्व कसरी प्राप्त गर्ने भन्ने कुरा थाहा पाइसकेका छौं। आधारभूत तत्व प्राप्त गरेपछि, यसलाई परिमार्जन गर्न वा यसमा नयाँ चाइल्ड तत्वहरू थप्नका लागि यहाँ केही API हरू छन्:

- [`textContent`](https://developer.mozilla.org/docs/Web/API/Node/textContent) प्रोपर्टी प्रयोग गरेर तपाईंले तत्वको पाठ परिवर्तन गर्न सक्नुहुन्छ। ध्यान दिनुहोस् कि यो मान परिवर्तन गर्दा यसले सबै चाइल्ड तत्वहरू (यदि कुनै छ भने) हटाउँछ र यसलाई प्रदान गरिएको पाठले प्रतिस्थापन गर्छ। यसरी, यो कुनै पनि दिइएको तत्वका सबै चाइल्डहरू हटाउनको लागि खाली स्ट्रिङ `''` असाइन गरेर कुशल विधि पनि हो।

- [`document.createElement()`](https://developer.mozilla.org/docs/Web/API/Document/createElement) र [`append()`](https://developer.mozilla.org/docs/Web/API/ParentNode/append) विधि प्रयोग गरेर तपाईंले नयाँ चाइल्ड तत्वहरू सिर्जना र संलग्न गर्न सक्नुहुन्छ।

✅ [`innerHTML`](https://developer.mozilla.org/docs/Web/API/Element/innerHTML) प्रोपर्टी प्रयोग गरेर पनि तत्वको HTML सामग्री परिवर्तन गर्न सम्भव छ, तर यो [क्रस-साइट स्क्रिप्टिङ (XSS)](https://developer.mozilla.org/docs/Glossary/Cross-site_scripting) आक्रमणहरूको लागि संवेदनशील भएकाले यसलाई टाढा राख्नुपर्छ।

### कार्य

ड्यासबोर्ड स्क्रिनमा अघि बढ्नु अघि, *लगइन* पृष्ठमा एउटा कुरा गर्न बाँकी छ। हाल, यदि तपाईं अवैध प्रयोगकर्ता नामसँग लगइन प्रयास गर्नुहुन्छ भने, कन्सोलमा सन्देश देखिन्छ तर सामान्य प्रयोगकर्ताका लागि केही परिवर्तन हुँदैन र तपाईंलाई के भइरहेको छ थाहा हुँदैन।

हामीले लगइन `<button>` भन्दा ठीक अघि त्रुटि सन्देश देखाउनको लागि फारममा एउटा प्लेसहोल्डर तत्व थपौं:

```html
...
<div id="loginError"></div>
<button>Login</button>
...
```

यो `<div>` तत्व खाली छ, जसको अर्थ हामीले यसमा केही सामग्री थप्दासम्म स्क्रिनमा केही देखिने छैन। हामीले यसलाई `id` पनि दिएका छौं ताकि यसलाई सजिलैसँग JavaScript बाट प्राप्त गर्न सकियोस्।

`app.js` फाइलमा फर्केर नयाँ हेल्पर फङ्सन `updateElement` सिर्जना गर्नुहोस्:

```js
function updateElement(id, text) {
  const element = document.getElementById(id);
  element.textContent = text;
}
```

यो फङ्सन धेरै सरल छ: दिइएको तत्व *id* र *text* को आधारमा, यो मिल्दो `id` भएको DOM तत्वको पाठ सामग्री अद्यावधिक गर्छ। अब यो विधि `login` फङ्सनमा पहिलेको त्रुटि सन्देशको सट्टा प्रयोग गरौं:

```js
if (data.error) {
  return updateElement('loginError', data.error);
}
```

अब यदि तपाईं अवैध खातासँग लगइन प्रयास गर्नुहुन्छ भने, तपाईंले यस्तो देख्नुहुनेछ:

![लगइनको क्रममा देखाइएको त्रुटि सन्देशको स्क्रिनसट](../../../../translated_images/login-error.416fe019b36a63276764c2349df5d99e04ebda54fefe60c715ee87a28d5d4ad0.ne.png)

अब हामीसँग दृश्य रूपमा देखिने त्रुटि पाठ छ, तर यदि तपाईंले यसलाई स्क्रिन रिडरसँग प्रयास गर्नुभयो भने केही पनि घोषणा हुँदैन। पृष्ठमा गतिशील रूपमा थपिएको पाठ स्क्रिन रिडरहरूले घोषणा गर्नको लागि, यसले [लाइभ क्षेत्र](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/ARIA_Live_Regions) प्रयोग गर्न आवश्यक छ। यहाँ हामीले अलर्ट नामक लाइभ क्षेत्रको विशिष्ट प्रकार प्रयोग गर्नेछौं:

```html
<div id="loginError" role="alert"></div>
```

`register` फङ्सन त्रुटिहरूको लागि पनि उस्तै व्यवहार कार्यान्वयन गर्नुहोस् (HTML अद्यावधिक गर्न नबिर्सनुहोस्)।

## ड्यासबोर्डमा जानकारी देखाउनुहोस्

हामीले भर्खरै देखेका उस्तै प्रविधिहरू प्रयोग गरेर, हामीले ड्यासबोर्ड पृष्ठमा खाता जानकारी देखाउने काम पनि गर्नेछौं।

सर्भरबाट प्राप्त खाता वस्तु यस्तो देखिन्छ:

```json
{
  "user": "test",
  "currency": "$",
  "description": "Test account",
  "balance": 75,
  "transactions": [
    { "id": "1", "date": "2020-10-01", "object": "Pocket money", "amount": 50 },
    { "id": "2", "date": "2020-10-03", "object": "Book", "amount": -10 },
    { "id": "3", "date": "2020-10-04", "object": "Sandwich", "amount": -5 }
  ],
}
```

> नोट: तपाईंको जीवन सजिलो बनाउनको लागि, तपाईंले पहिले नै डेटा भरिएको `test` खाता प्रयोग गर्न सक्नुहुन्छ।

### कार्य

HTML मा "Balance" सेक्सनलाई प्लेसहोल्डर तत्वहरू थप्न प्रतिस्थापन गरौं:

```html
<section>
  Balance: <span id="balance"></span><span id="currency"></span>
</section>
```

त्यसपछि, खाता विवरण देखाउनको लागि नयाँ सेक्सन थपौं:

```html
<h2 id="description"></h2>
```

✅ खाता विवरण सामग्रीको शीर्षकको रूपमा कार्य गर्ने भएकाले, यसलाई शीर्षकको रूपमा अर्थपूर्ण रूपमा मार्कअप गरिएको छ। [शीर्षक संरचना](https://www.nomensa.com/blog/2017/how-structure-headings-web-accessibility) कसरी पहुँचयोग्यताका लागि महत्त्वपूर्ण छ भन्ने बारे थप जान्नुहोस्, र पृष्ठलाई आलोचनात्मक रूपमा हेरेर के अरू शीर्षक हुन सक्छ भनेर निर्धारण गर्नुहोस्।

अब, `app.js` मा नयाँ फङ्सन `updateDashboard` सिर्जना गरौं:

```js
function updateDashboard() {
  if (!account) {
    return navigate('/login');
  }

  updateElement('description', account.description);
  updateElement('balance', account.balance.toFixed(2));
  updateElement('currency', account.currency);
}
```

पहिले, हामीसँग आवश्यक खाता डेटा छ कि छैन भनेर जाँच गर्छौं। त्यसपछि हामीले पहिले सिर्जना गरेको `updateElement()` फङ्सन प्रयोग गरेर HTML अद्यावधिक गर्छौं।

> ब्यालेन्स प्रदर्शनलाई अझ राम्रो बनाउन, हामीले [`toFixed(2)`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed) विधि प्रयोग गरेर मानलाई दशमलव बिन्दु पछि २ अंक देखाउन बाध्य पार्छौं।

अब हरेक पटक ड्यासबोर्ड लोड हुँदा हाम्रो `updateDashboard()` फङ्सनलाई कल गर्न आवश्यक छ। यदि तपाईंले [पाठ १ को असाइनमेन्ट](../1-template-route/assignment.md) पहिले नै पूरा गर्नुभएको छ भने यो सरल हुनुपर्छ, अन्यथा तपाईंले निम्न कार्यान्वयन प्रयोग गर्न सक्नुहुन्छ।

`updateRoute()` फङ्सनको अन्त्यमा यो कोड थप्नुहोस्:

```js
if (typeof route.init === 'function') {
  route.init();
}
```

र रुट्स परिभाषालाई यससँग अद्यावधिक गर्नुहोस्:

```js
const routes = {
  '/login': { templateId: 'login' },
  '/dashboard': { templateId: 'dashboard', init: updateDashboard }
};
```

यस परिवर्तनसँगै, हरेक पटक ड्यासबोर्ड पृष्ठ देखाइन्छ, `updateDashboard()` फङ्सन कल हुन्छ। लगइन पछि, तपाईंले खाता ब्यालेन्स, मुद्रा र विवरण देख्न सक्नुहुनेछ।

## HTML टेम्प्लेटहरू प्रयोग गरेर तालिका पङ्क्तिहरू गतिशील रूपमा सिर्जना गर्नुहोस्

[पहिलो पाठमा](../1-template-route/README.md) हामीले HTML टेम्प्लेटहरू र [`appendChild()`](https://developer.mozilla.org/docs/Web/API/Node/appendChild) विधि प्रयोग गरेर हाम्रो एपमा नेभिगेसन कार्यान्वयन गरेका थियौं। टेम्प्लेटहरू साना पनि हुन सक्छन् र पृष्ठको पुनरावृत्त भागहरू गतिशील रूपमा जनसंख्या गर्न प्रयोग गर्न सकिन्छ।

हामीले HTML तालिकामा लेनदेनहरूको सूची देखाउन उस्तै दृष्टिकोण प्रयोग गर्नेछौं।

### कार्य

HTML `<body>` मा नयाँ टेम्प्लेट थप्नुहोस्:

```html
<template id="transaction">
  <tr>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</template>
```

यो टेम्प्लेटले एउटा मात्र तालिका पङ्क्ति प्रतिनिधित्व गर्छ, जसमा हामीले भर्न चाहेका ३ स्तम्भहरू छन्: लेनदेनको *मिति*, *वस्तु* र *रकम*।

त्यसपछि, ड्यासबोर्ड टेम्प्लेटभित्रको तालिकाको `<tbody>` तत्वमा यो `id` प्रोपर्टी थप्नुहोस् ताकि यसलाई JavaScript प्रयोग गरेर सजिलै फेला पार्न सकियोस्:

```html
<tbody id="transactions"></tbody>
```

हाम्रो HTML तयार छ, अब JavaScript कोडमा स्विच गरौं र नयाँ फङ्सन `createTransactionRow` सिर्जना गरौं:

```js
function createTransactionRow(transaction) {
  const template = document.getElementById('transaction');
  const transactionRow = template.content.cloneNode(true);
  const tr = transactionRow.querySelector('tr');
  tr.children[0].textContent = transaction.date;
  tr.children[1].textContent = transaction.object;
  tr.children[2].textContent = transaction.amount.toFixed(2);
  return transactionRow;
}
```

यस फङ्सनले यसको नामले भनेजस्तै गर्छ: हामीले पहिले सिर्जना गरेको टेम्प्लेट प्रयोग गरेर, यो नयाँ तालिका पङ्क्ति सिर्जना गर्छ र लेनदेन डेटा प्रयोग गरेर यसको सामग्री भर्छ। हामीले यो हाम्रो `updateDashboard()` फङ्सनमा तालिका जनसंख्या गर्न प्रयोग गर्नेछौं:

```js
const transactionsRows = document.createDocumentFragment();
for (const transaction of account.transactions) {
  const transactionRow = createTransactionRow(transaction);
  transactionsRows.appendChild(transactionRow);
}
updateElement('transactions', transactionsRows);
```

यहाँ हामीले [`document.createDocumentFragment()`](https://developer.mozilla.org/docs/Web/API/Document/createDocumentFragment) विधि प्रयोग गर्छौं, जसले नयाँ DOM फ्र्यागमेन्ट सिर्जना गर्छ, जसमा हामीले काम गर्न सक्छौं, र अन्ततः यसलाई हाम्रो HTML तालिकामा संलग्न गर्छौं।

यो कोड काम गर्न सक्ने बनाउन, हाम्रो `updateElement()` फङ्सन हाल पाठ सामग्री मात्र समर्थन गर्छ। यसको कोडलाई अलिकति परिवर्तन गरौं:

```js
function updateElement(id, textOrNode) {
  const element = document.getElementById(id);
  element.textContent = ''; // Removes all children
  element.append(textOrNode);
}
```

हामीले [`append()`](https://developer.mozilla.org/docs/Web/API/ParentNode/append) विधि प्रयोग गर्छौं, किनभने यसले पाठ वा [DOM Nodes](https://developer.mozilla.org/docs/Web/API/Node) दुबैलाई अभिभावक तत्वमा संलग्न गर्न अनुमति दिन्छ, जुन हाम्रा सबै प्रयोगका लागि उपयुक्त छ।
यदि तपाईंले `test` खाता प्रयोग गरेर लगइन गर्न प्रयास गर्नुभयो भने, अब तपाईंले ड्यासबोर्डमा लेनदेन सूची देख्न सक्नुहुन्छ 🎉।

---

## 🚀 चुनौती

ड्यासबोर्ड पृष्ठलाई वास्तविक बैंकिङ एपजस्तो देखिने बनाउनको लागि सँगै काम गर्नुहोस्। यदि तपाईंले पहिले नै आफ्नो एपलाई स्टाइल गर्नुभएको छ भने, [मिडिया क्वेरीहरू](https://developer.mozilla.org/docs/Web/CSS/Media_Queries) प्रयोग गरेर [उत्तरदायी डिजाइन](https://developer.mozilla.org/docs/Web/Progressive_web_apps/Responsive/responsive_design_building_blocks) बनाउने प्रयास गर्नुहोस्, जसले डेस्कटप र मोबाइल उपकरणहरूमा राम्रोसँग काम गर्छ।

यहाँ स्टाइल गरिएको ड्यासबोर्ड पृष्ठको उदाहरण छ:

![ड्यासबोर्डलाई स्टाइल गरेपछि प्राप्त हुने परिणामको उदाहरणको स्क्रिनसट](../../../../translated_images/screen2.123c82a831a1d14ab2061994be2fa5de9cec1ce651047217d326d4773a6348e4.ne.png)

## पोस्ट-व्याख्यान क्विज

[पोस्ट-व्याख्यान क्विज](https://ff-quizzes.netlify.app/web/quiz/46)

## असाइनमेन्ट

[तपाईंको कोडलाई पुनःसंरचना गर्नुहोस् र टिप्पणीहरू थप्नुहोस्](assignment.md)

---

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरेर अनुवाद गरिएको छ। हामी शुद्धताको लागि प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छ। यसको मूल भाषामा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीको लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।