<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "89d0df9854ed020f155e94882ae88d4c",
  "translation_date": "2025-08-28T16:08:12+00:00",
  "source_file": "7-bank-project/3-data/README.md",
  "language_code": "mr"
}
-->
# बँकिंग अ‍ॅप तयार करा भाग ३: डेटा मिळवण्याचे आणि वापरण्याचे पद्धती

## प्री-लेक्चर क्विझ

[प्री-लेक्चर क्विझ](https://ff-quizzes.netlify.app/web/quiz/45)

### परिचय

प्रत्येक वेब अ‍ॅप्लिकेशनच्या केंद्रस्थानी *डेटा* असतो. डेटा विविध स्वरूपात असतो, परंतु त्याचा मुख्य उद्देश नेहमीच वापरकर्त्याला माहिती दाखवणे असतो. वेब अ‍ॅप्स अधिकाधिक परस्परसंवादी आणि जटिल होत असल्याने, वापरकर्ता माहिती कशी मिळवतो आणि तिचा कसा उपयोग करतो, हे वेब विकासाचा महत्त्वाचा भाग बनले आहे.

या धड्यात, आपण सर्व्हरवरून डेटा असिंक्रोनस पद्धतीने कसा मिळवायचा आणि HTML पुन्हा लोड न करता वेब पृष्ठावर माहिती कशी दाखवायची हे पाहू.

### पूर्वतयारी

या धड्यासाठी तुम्ही [लॉगिन आणि नोंदणी फॉर्म](../2-forms/README.md) तयार केलेला असणे आवश्यक आहे. तुम्हाला [Node.js](https://nodejs.org) स्थापित करणे आणि [सर्व्हर API चालवणे](../api/README.md) आवश्यक आहे जेणेकरून तुम्हाला खाते डेटा मिळेल.

सर्व्हर योग्यरित्या चालू आहे की नाही हे तपासण्यासाठी टर्मिनलमध्ये खालील कमांड चालवा:

```sh
curl http://localhost:5000/api
# -> should return "Bank API v1.0.0" as a result
```

---

## AJAX आणि डेटा मिळवणे

पारंपरिक वेब साइट्समध्ये, वापरकर्ता लिंक निवडतो किंवा फॉर्मद्वारे डेटा सबमिट करतो तेव्हा संपूर्ण HTML पृष्ठ पुन्हा लोड करून सामग्री अपडेट केली जाते. नवीन डेटा लोड करण्यासाठी प्रत्येक वेळी वेब सर्व्हर नवीन HTML पृष्ठ परत करतो, ज्यामुळे ब्राउझरला प्रक्रिया करावी लागते, सध्याची क्रिया थांबते आणि रीलोड दरम्यान परस्परसंवाद मर्यादित होतो. या कार्यप्रवाहाला *मल्टी-पेज अ‍ॅप्लिकेशन* किंवा *MPA* म्हणतात.

![मल्टी-पेज अ‍ॅप्लिकेशनमधील अपडेट कार्यप्रवाह](../../../../translated_images/mpa.7f7375a1a2d4aa779d3f928a2aaaf9ad76bcdeb05cfce2dc27ab126024050f51.mr.png)

वेब अ‍ॅप्लिकेशन्स अधिक जटिल आणि परस्परसंवादी होऊ लागल्यावर, [AJAX (Asynchronous JavaScript and XML)](https://en.wikipedia.org/wiki/Ajax_(programming)) नावाची नवीन तंत्रज्ञान विकसित झाली. या तंत्रज्ञानामुळे वेब अ‍ॅप्स JavaScript वापरून सर्व्हरकडून डेटा असिंक्रोनस पद्धतीने पाठवू आणि मिळवू शकतात, HTML पृष्ठ पुन्हा लोड करण्याची गरज नसते, परिणामी जलद अपडेट्स आणि गुळगुळीत परस्परसंवाद होतो. सर्व्हरकडून नवीन डेटा प्राप्त झाल्यावर, JavaScript वापरून [DOM](https://developer.mozilla.org/docs/Web/API/Document_Object_Model) API च्या मदतीने विद्यमान HTML पृष्ठ अपडेट करता येते. कालांतराने, ही पद्धत [*सिंगल-पेज अ‍ॅप्लिकेशन* किंवा *SPA*](https://en.wikipedia.org/wiki/Single-page_application) म्हणून विकसित झाली.

![सिंगल-पेज अ‍ॅप्लिकेशनमधील अपडेट कार्यप्रवाह](../../../../translated_images/spa.268ec73b41f992c2a21ef9294235c6ae597b3c37e2c03f0494c2d8857325cc57.mr.png)

AJAX प्रथम सादर झाल्यावर, असिंक्रोनस पद्धतीने डेटा मिळवण्यासाठी उपलब्ध असलेली एकमेव API [`XMLHttpRequest`](https://developer.mozilla.org/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest) होती. परंतु आधुनिक ब्राउझर आता अधिक सोयीस्कर आणि शक्तिशाली [`Fetch` API](https://developer.mozilla.org/docs/Web/API/Fetch_API) लागू करतात, जी प्रॉमिसेस वापरते आणि JSON डेटा हाताळण्यासाठी अधिक योग्य आहे.

> सर्व आधुनिक ब्राउझर `Fetch API` ला समर्थन देतात, परंतु तुमचे वेब अ‍ॅप्लिकेशन जुने ब्राउझरवर चालवायचे असल्यास, [caniuse.com वर सुसंगतता टेबल](https://caniuse.com/fetch) तपासणे नेहमीच चांगले असते.

### कार्य

[मागील धड्यात](../2-forms/README.md) आपण खाते तयार करण्यासाठी नोंदणी फॉर्म अंमलात आणला. आता आपण विद्यमान खात्याचा वापर करून लॉगिन करण्यासाठी कोड जोडू आणि त्याचा डेटा मिळवू. `app.js` फाइल उघडा आणि नवीन `login` फंक्शन जोडा:

```js
async function login() {
  const loginForm = document.getElementById('loginForm')
  const user = loginForm.user.value;
}
```

येथे आपण `getElementById()` वापरून फॉर्म एलिमेंट मिळवतो आणि नंतर `loginForm.user.value` वापरून इनपुटमधून वापरकर्त्याचे नाव मिळवतो. प्रत्येक फॉर्म कंट्रोलला त्याच्या नावाने (HTML मध्ये `name` अ‍ॅट्रिब्युट वापरून सेट केलेले) फॉर्मच्या प्रॉपर्टी म्हणून प्रवेश करता येतो.

नोंदणीसाठी आपण जे केले त्याचप्रमाणे, सर्व्हर विनंती करण्यासाठी आणखी एक फंक्शन तयार करू, परंतु यावेळी खाते डेटा मिळवण्यासाठी:

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

आम्ही `fetch` API वापरून सर्व्हरकडून डेटा असिंक्रोनस पद्धतीने मिळवतो, परंतु यावेळी आम्हाला URL व्यतिरिक्त कोणतेही अतिरिक्त पॅरामीटर्स आवश्यक नाहीत, कारण आम्ही फक्त डेटा क्वेरी करत आहोत. डीफॉल्टनुसार, `fetch` [`GET`](https://developer.mozilla.org/docs/Web/HTTP/Methods/GET) HTTP विनंती तयार करते, जी येथे आपल्याला हवी आहे.

✅ `encodeURIComponent()` ही एक फंक्शन आहे जी URL साठी विशेष वर्ण एस्केप करते. जर आपण ही फंक्शन कॉल केली नाही आणि थेट `user` मूल्य URL मध्ये वापरले तर कोणत्या समस्या उद्भवू शकतात?

आता आपण `login` फंक्शन अपडेट करून `getAccount` वापरणार आहोत:

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

प्रथम, `getAccount` हे असिंक्रोनस फंक्शन असल्याने आम्हाला सर्व्हरच्या निकालाची वाट पाहण्यासाठी `await` कीवर्ड वापरावा लागतो. कोणत्याही सर्व्हर विनंतीप्रमाणे, आपल्याला त्रुटींचा सामना करावा लागतो. सध्या आम्ही फक्त त्रुटी दाखवण्यासाठी लॉग संदेश जोडणार आहोत आणि नंतर त्याकडे परत येऊ.

यानंतर, आम्हाला डेटा कुठेतरी साठवावा लागतो जेणेकरून नंतर डॅशबोर्ड माहिती दाखवण्यासाठी त्याचा उपयोग करता येईल. कारण `account` व्हेरिएबल अद्याप अस्तित्वात नाही, आम्ही आमच्या फाइलच्या शीर्षस्थानी एक ग्लोबल व्हेरिएबल तयार करू:

```js
let account = null;
```

वापरकर्त्याचा डेटा व्हेरिएबलमध्ये सेव्ह झाल्यानंतर, आपण *लॉगिन* पृष्ठावरून *डॅशबोर्ड* वर `navigate()` फंक्शन वापरून जाऊ शकतो.

शेवटी, लॉगिन फॉर्म सबमिट केल्यावर आपले `login` फंक्शन कॉल करण्यासाठी HTML मध्ये बदल करणे आवश्यक आहे:

```html
<form id="loginForm" action="javascript:login()">
```

नवीन खाते नोंदणी करून आणि त्याच खात्याचा वापर करून लॉगिन करण्याचा प्रयत्न करून सर्व काही योग्यरित्या कार्य करत आहे का ते तपासा.

पुढील भागाकडे जाण्यापूर्वी, आपण `register` फंक्शन पूर्ण करू शकतो आणि फंक्शनच्या शेवटी हे जोडू शकतो:

```js
account = result;
navigate('/dashboard');
```

✅ तुम्हाला माहित आहे का की डीफॉल्टनुसार, तुम्ही ज्या वेब पृष्ठावर आहात त्या *समान डोमेन आणि पोर्ट* वरूनच सर्व्हर API कॉल करू शकता? हे ब्राउझरद्वारे लागू केलेले सुरक्षा यंत्रणा आहे. पण थांबा, आपले वेब अ‍ॅप `localhost:3000` वर चालत आहे तर सर्व्हर API `localhost:5000` वर चालत आहे, तरीही ते कसे कार्य करते? [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/docs/Web/HTTP/CORS) नावाच्या तंत्राचा वापर करून, सर्व्हर विशिष्ट डोमेनसाठी अपवाद परवानगी देणारे विशेष हेडर्स प्रतिसादात जोडतो, ज्यामुळे क्रॉस-ऑरिजिन HTTP विनंत्या करणे शक्य होते.

> API बद्दल अधिक जाणून घेण्यासाठी [हा धडा](https://docs.microsoft.com/learn/modules/use-apis-discover-museum-art/?WT.mc_id=academic-77807-sagibbon) घ्या.

## HTML अपडेट करून डेटा दाखवा

आता आपल्याकडे वापरकर्ता डेटा आहे, आपल्याला विद्यमान HTML अपडेट करून तो दाखवायचा आहे. DOM मधून एखादा एलिमेंट मिळवण्यासाठी `document.getElementById()` वापरण्याची पद्धत आपल्याला आधीच माहित आहे. बेस एलिमेंट मिळाल्यानंतर, त्यास बदलण्यासाठी किंवा त्यामध्ये चाइल्ड एलिमेंट्स जोडण्यासाठी खालील API वापरता येतात:

- [`textContent`](https://developer.mozilla.org/docs/Web/API/Node/textContent) प्रॉपर्टी वापरून तुम्ही एखाद्या एलिमेंटचा मजकूर बदलू शकता. लक्षात ठेवा की हे मूल्य बदलल्याने एलिमेंटचे सर्व चाइल्ड (जर काही असतील) काढून टाकले जातात आणि दिलेल्या मजकुराने बदलले जाते. त्यामुळे, एखाद्या एलिमेंटचे सर्व चाइल्ड काढून टाकण्यासाठी रिक्त स्ट्रिंग `''` असाइन करणे ही एक कार्यक्षम पद्धत आहे.

- [`document.createElement()`](https://developer.mozilla.org/docs/Web/API/Document/createElement) आणि [`append()`](https://developer.mozilla.org/docs/Web/API/ParentNode/append) पद्धतीसह तुम्ही नवीन चाइल्ड एलिमेंट्स तयार करून जोडू शकता.

✅ [`innerHTML`](https://developer.mozilla.org/docs/Web/API/Element/innerHTML) प्रॉपर्टी वापरून एखाद्या एलिमेंटची HTML सामग्री बदलणे शक्य आहे, परंतु हे टाळले पाहिजे कारण ते [क्रॉस-साइट स्क्रिप्टिंग (XSS)](https://developer.mozilla.org/docs/Glossary/Cross-site_scripting) हल्ल्यांसाठी असुरक्षित आहे.

### कार्य

डॅशबोर्ड स्क्रीनवर जाण्यापूर्वी, *लॉगिन* पृष्ठावर आणखी एक गोष्ट करणे आवश्यक आहे. सध्या, जर तुम्ही अस्तित्वात नसलेल्या वापरकर्त्याच्या नावाने लॉगिन करण्याचा प्रयत्न केला, तर कन्सोलमध्ये संदेश दाखवला जातो, परंतु सामान्य वापरकर्त्यासाठी काहीही बदलत नाही आणि काय चालले आहे हे समजत नाही.

चला लॉगिन `<button>` च्या अगोदर एक प्लेसहोल्डर एलिमेंट जोडू जिथे आवश्यक असल्यास त्रुटी संदेश दाखवता येईल:

```html
...
<div id="loginError"></div>
<button>Login</button>
...
```

हा `<div>` एलिमेंट रिक्त आहे, म्हणजे स्क्रीनवर काहीही दिसणार नाही जोपर्यंत आपण त्यामध्ये काही सामग्री जोडत नाही. आम्ही त्याला `id` देतो जेणेकरून JavaScript वापरून तो सहजपणे मिळवता येईल.

`app.js` फाइलमध्ये परत जा आणि नवीन हेल्पर फंक्शन `updateElement` तयार करा:

```js
function updateElement(id, text) {
  const element = document.getElementById(id);
  element.textContent = text;
}
```

हे फंक्शन अगदी सोपे आहे: दिलेल्या एलिमेंट *id* आणि *text* च्या आधारे, ते दिलेल्या `id` असलेल्या DOM एलिमेंटचा मजकूर अपडेट करते. चला हे फंक्शन `login` फंक्शनमधील पूर्वीच्या त्रुटी संदेशाच्या जागी वापरू:

```js
if (data.error) {
  return updateElement('loginError', data.error);
}
```

आता जर तुम्ही अवैध खात्याने लॉगिन करण्याचा प्रयत्न केला, तर तुम्हाला असे काहीतरी दिसेल:

![लॉगिन दरम्यान दाखवलेला त्रुटी संदेश](../../../../translated_images/login-error.416fe019b36a63276764c2349df5d99e04ebda54fefe60c715ee87a28d5d4ad0.mr.png)

आता आपल्याकडे व्हिज्युअली त्रुटी मजकूर आहे, परंतु जर तुम्ही स्क्रीन रीडर वापरून प्रयत्न केला तर तुम्हाला लक्षात येईल की काहीही घोषित केले जात नाही. पृष्ठावर डायनॅमिक पद्धतीने जोडलेला मजकूर स्क्रीन रीडरद्वारे घोषित होण्यासाठी, त्याला [Live Region](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/ARIA_Live_Regions) वापरणे आवश्यक आहे. येथे आपण अलर्ट नावाच्या लाइव्ह रिजनचा वापर करणार आहोत:

```html
<div id="loginError" role="alert"></div>
```

`register` फंक्शनच्या त्रुटींसाठीही समान वर्तन अंमलात आणा (HTML अपडेट करायला विसरू नका).

## डॅशबोर्डवर माहिती दाखवा

आत्ताच पाहिलेल्या तंत्रांचा वापर करून, आपण डॅशबोर्ड पृष्ठावर खाते माहिती दाखवण्याची जबाबदारी घेणार आहोत.

सर्व्हरकडून प्राप्त झालेले खाते ऑब्जेक्ट असे दिसते:

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

> टीप: तुमचे काम सोपे करण्यासाठी, तुम्ही आधीपासून डेटा भरलेले `test` खाते वापरू शकता.

### कार्य

चला HTML मधील "Balance" विभाग बदलून प्लेसहोल्डर एलिमेंट्स जोडू:

```html
<section>
  Balance: <span id="balance"></span><span id="currency"></span>
</section>
```

आम्ही खाते वर्णन दाखवण्यासाठी खाली नवीन विभाग जोडणार आहोत:

```html
<h2 id="description"></h2>
```

✅ कारण खाते वर्णन त्याखालील सामग्रीसाठी शीर्षक म्हणून कार्य करते, ते सेमॅंटिकली हेडिंग म्हणून चिन्हांकित केले आहे. [हेडिंग स्ट्रक्चर](https://www.nomensa.com/blog/2017/how-structure-headings-web-accessibility) कसे महत्त्वाचे आहे याबद्दल अधिक जाणून घ्या आणि पृष्ठावर इतर काय हेडिंग असू शकते याचा गंभीरपणे विचार करा.

पुढे, `app.js` मध्ये नवीन फंक्शन तयार करू जे प्लेसहोल्डर भरते:

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

प्रथम, आमच्याकडे आवश्यक खाते डेटा आहे याची खात्री करतो. त्यानंतर, आम्ही पूर्वी तयार केलेल्या `updateElement()` फंक्शनचा वापर करून HTML अपडेट करतो.

> बॅलन्स डिस्प्ले अधिक आकर्षक बनवण्यासाठी, आम्ही [`toFixed(2)`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed) पद्धतीचा वापर करतो जेणेकरून मूल्य दशांश बिंदूच्या नंतर २ अंकांसह दाखवले जाईल.

आता प्रत्येक वेळी डॅशबोर्ड लोड झाल्यावर आपले `updateDashboard()` फंक्शन कॉल करणे आवश्यक आहे. जर तुम्ही [धडा १ असाइनमेंट](../1-template-route/assignment.md) पूर्ण केली असेल तर हे सोपे असावे, अन्यथा तुम्ही खालील अंमलबजावणी वापरू शकता.

`updateRoute()` फंक्शनच्या शेवटी हा कोड जोडा:

```js
if (typeof route.init === 'function') {
  route.init();
}
```

आणि रूट्सची व्याख्या खालीलप्रमाणे अपडेट करा:

```js
const routes = {
  '/login': { templateId: 'login' },
  '/dashboard': { templateId: 'dashboard', init: updateDashboard }
};
```

या बदलासह, प्रत्येक वेळी डॅशबोर्ड पृष्ठ प्रदर्शित केले जाते, `updateDashboard()` फंक्शन कॉल केले जाते. लॉगिन केल्यानंतर, तुम्हाला खाते बॅलन्स, चलन आणि वर्णन दिसले पाहिजे.

## HTML टेम्पलेट्ससह टेबल रो डायनॅमिक पद्धतीने तयार करा

[पहिल्या धड्यात](../1-template-route/README.md) आपण HTML टेम्पलेट्स आणि [`appendChild()`](https://developer.mozilla.org/docs/Web/API/Node/appendChild) पद्धतीचा वापर करून अ‍ॅपमधील नेव्हिगेशन अंमलात आणले. टेम्पलेट्स लहान देखील असू शकतात आणि पृष्ठाच्या पुनरावृत्ती होणाऱ्या भागांना डायनॅमिक पद्धतीने भरण्यासाठी वापरले जाऊ शकतात.

आम्ही HTML टेबलमध्ये व्यवहारांची यादी दाखवण्यासाठी समान दृष्टिकोन वापरणार आहोत.

### कार्य

HTML `<body>` मध्ये नवीन टेम्पलेट जोडा:

```html
<template id="transaction">
  <tr>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</template>
```

हे टेम्पलेट एका टेबल रोचे प्रतिनिधित्व करते, ज्यामध्ये आम्हाला भरायच्या ३ कॉलम्स आहेत: व्यवहाराची *तारीख*, *वस्तू* आणि *रक्कम*.

यानंतर, टेबलमधील `<tbody>` एलिमेंटला `id` प्रॉपर्टी जोडा जेणेकरून JavaScript वापरून ते शोधणे सोपे होईल:

```html
<tbody id="transactions"></tbody>
```

आमचे HTML तयार आहे, आता JavaScript कोडकडे वळू आणि नवीन फंक्शन `createTransactionRow` तयार करू:

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

हे फंक्शन त्याच्या नावाप्रमाणेच कार्य करते: आम्ही तयार केलेल्या टेम्पलेटचा वापर करून, ते नवीन टेबल रो तयार करते आणि व्यवहार डेटा वापरून त्याची सामग्री भरते. आम्ही हे आमच्या `updateDashboard()` फंक्शनमध्ये टेबल भरण्यासाठी वापरणार आहोत:

```js
const transactionsRows = document.createDocumentFragment();
for (const transaction of account.transactions) {
  const transactionRow = createTransactionRow(transaction);
  transactionsRows.appendChild(transactionRow);
}
updateElement('transactions', transactionsRows);
```

येथे आम्ही [`document.createDocumentFragment()`](https://developer.mozilla.org/docs/Web/API/Document/createDocumentFragment) पद्धतीचा वापर करतो, जी नवीन DOM फ्रॅगमेंट तयार करते ज्यावर आपण काम करू शकतो, आणि शेवटी ते आमच्या HTML टेबलला जोडतो.

हे कोड कार्य करण्यासाठी अजून एक गोष्ट करणे आवश्यक आहे, कारण आमचे `updateElement()` फंक्शन सध्या फक्त मजकूर सामग्रीला समर्थन देते. त्याचा कोड थोडा बदलू:

```js
function updateElement(id, textOrNode) {
  const element = document.getElementById(id);
  element.textContent = ''; // Removes all children
  element.append(textOrNode);
}
```

आम्ही [`append()`](https://developer.mozilla.org/docs/Web/API/ParentNode/append) पद्धतीचा वापर
जर तुम्ही `test` खाते वापरून लॉगिन करण्याचा प्रयत्न केला, तर आता तुम्हाला डॅशबोर्डवर व्यवहारांची यादी दिसेल 🎉.

---

## 🚀 आव्हान

एकत्र काम करून डॅशबोर्ड पृष्ठ खऱ्या बँकिंग अ‍ॅपसारखे दिसेल असे बनवा. जर तुम्ही आधीच तुमचे अ‍ॅप स्टाइल केले असेल, तर [media queries](https://developer.mozilla.org/docs/Web/CSS/Media_Queries) वापरून [responsive design](https://developer.mozilla.org/docs/Web/Progressive_web_apps/Responsive/responsive_design_building_blocks) तयार करण्याचा प्रयत्न करा, जे डेस्कटॉप आणि मोबाइल डिव्हाइसवर चांगले कार्य करेल.

स्टाइल केलेल्या डॅशबोर्ड पृष्ठाचे उदाहरण येथे आहे:

![स्टाइल केलेल्या डॅशबोर्डचे उदाहरण परिणामाचा स्क्रीनशॉट](../../../../translated_images/screen2.123c82a831a1d14ab2061994be2fa5de9cec1ce651047217d326d4773a6348e4.mr.png)

## व्याख्यानानंतरचा क्विझ

[व्याख्यानानंतरचा क्विझ](https://ff-quizzes.netlify.app/web/quiz/46)

## असाइनमेंट

[तुमचा कोड पुनर्रचना करा आणि त्यावर टिप्पणी द्या](assignment.md)

---

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) चा वापर करून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी, कृपया लक्षात घ्या की स्वयंचलित भाषांतरांमध्ये त्रुटी किंवा अचूकतेचा अभाव असू शकतो. मूळ भाषेतील मूळ दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी, व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर केल्यामुळे उद्भवणाऱ्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.