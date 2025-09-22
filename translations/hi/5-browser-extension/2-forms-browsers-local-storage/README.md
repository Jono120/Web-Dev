<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a7587943d38d095de8613e1b508609f5",
  "translation_date": "2025-08-29T15:54:14+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "hi"
}
-->
# ब्राउज़र एक्सटेंशन प्रोजेक्ट भाग 2: API कॉल करें, लोकल स्टोरेज का उपयोग करें

## प्री-लेक्चर क्विज़

[प्री-लेक्चर क्विज़](https://ff-quizzes.netlify.app/web/quiz/25)

### परिचय

इस पाठ में, आप अपने ब्राउज़र एक्सटेंशन के फॉर्म को सबमिट करके एक API कॉल करेंगे और परिणामों को ब्राउज़र एक्सटेंशन में प्रदर्शित करेंगे। इसके अलावा, आप सीखेंगे कि ब्राउज़र के लोकल स्टोरेज में डेटा को भविष्य के संदर्भ और उपयोग के लिए कैसे संग्रहीत किया जा सकता है।

✅ उचित फाइलों में क्रमांकित खंडों का पालन करें ताकि आप जान सकें कि कोड को कहां रखना है।

### एक्सटेंशन में उपयोग करने के लिए एलिमेंट्स सेट करें:

अब तक आपने अपने ब्राउज़र एक्सटेंशन के लिए फॉर्म और परिणाम `<div>` के लिए HTML बना लिया है। अब से, आपको `/src/index.js` फाइल में काम करना होगा और अपने एक्सटेंशन को धीरे-धीरे बनाना होगा। [पिछले पाठ](../1-about-browsers/README.md) को देखें ताकि आप अपने प्रोजेक्ट को सेटअप और बिल्ड प्रक्रिया के बारे में जान सकें।

`index.js` फाइल में काम करते हुए, शुरुआत में कुछ `const` वेरिएबल्स बनाएं जो विभिन्न फील्ड्स से जुड़े मानों को पकड़ें:

```JavaScript
// form fields
const form = document.querySelector('.form-data');
const region = document.querySelector('.region-name');
const apiKey = document.querySelector('.api-key');

// results
const errors = document.querySelector('.errors');
const loading = document.querySelector('.loading');
const results = document.querySelector('.result-container');
const usage = document.querySelector('.carbon-usage');
const fossilfuel = document.querySelector('.fossil-fuel');
const myregion = document.querySelector('.my-region');
const clearBtn = document.querySelector('.clear-btn');
```

इन सभी फील्ड्स को उनके CSS क्लास द्वारा संदर्भित किया गया है, जैसा कि आपने पिछले पाठ में HTML में सेट किया था।

### लिसनर्स जोड़ें

इसके बाद, फॉर्म और क्लियर बटन पर इवेंट लिसनर्स जोड़ें, ताकि जब कोई उपयोगकर्ता फॉर्म सबमिट करे या रीसेट बटन पर क्लिक करे, तो कुछ कार्रवाई हो। इसके अलावा, फाइल के नीचे ऐप को इनिशियलाइज़ करने के लिए कॉल जोड़ें:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ ध्यान दें कि सबमिट या क्लिक इवेंट को सुनने के लिए शॉर्टहैंड का उपयोग किया गया है, और कैसे इवेंट को `handleSubmit` या `reset` फंक्शन में पास किया गया है। क्या आप इस शॉर्टहैंड का लंबा संस्करण लिख सकते हैं? आपको कौन सा तरीका पसंद है?

### `init()` और `reset()` फंक्शन बनाएं:

अब आप उस फंक्शन को बनाएंगे जो एक्सटेंशन को इनिशियलाइज़ करता है, जिसे `init()` कहा जाता है:

```JavaScript
function init() {
	//if anything is in localStorage, pick it up
	const storedApiKey = localStorage.getItem('apiKey');
	const storedRegion = localStorage.getItem('regionName');

	//set icon to be generic green
	//todo

	if (storedApiKey === null || storedRegion === null) {
		//if we don't have the keys, show the form
		form.style.display = 'block';
		results.style.display = 'none';
		loading.style.display = 'none';
		clearBtn.style.display = 'none';
		errors.textContent = '';
	} else {
        //if we have saved keys/regions in localStorage, show results when they load
        displayCarbonUsage(storedApiKey, storedRegion);
		results.style.display = 'none';
		form.style.display = 'none';
		clearBtn.style.display = 'block';
	}
};

function reset(e) {
	e.preventDefault();
	//clear local storage for region only
	localStorage.removeItem('regionName');
	init();
}

```

इस फंक्शन में कुछ दिलचस्प लॉजिक है। इसे पढ़ते हुए, क्या आप देख सकते हैं कि क्या हो रहा है?

- दो `const` सेट किए गए हैं ताकि यह जांचा जा सके कि उपयोगकर्ता ने लोकल स्टोरेज में APIKey और क्षेत्र कोड संग्रहीत किया है या नहीं।
- यदि इनमें से कोई भी null है, तो फॉर्म को 'block' के रूप में प्रदर्शित करने के लिए इसकी स्टाइल बदलें।
- परिणाम, लोडिंग, और `clearBtn` को छिपाएं और किसी भी त्रुटि पाठ को खाली स्ट्रिंग पर सेट करें।
- यदि कोई key और region मौजूद है, तो एक रूटीन शुरू करें:
  - API को कॉल करें ताकि कार्बन उपयोग डेटा प्राप्त किया जा सके।
  - परिणाम क्षेत्र को छिपाएं।
  - फॉर्म को छिपाएं।
  - रीसेट बटन दिखाएं।

आगे बढ़ने से पहले, ब्राउज़रों में उपलब्ध एक बहुत ही महत्वपूर्ण अवधारणा के बारे में जानना उपयोगी है: [LocalStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)। LocalStorage ब्राउज़र में स्ट्रिंग्स को `key-value` जोड़ी के रूप में संग्रहीत करने का एक उपयोगी तरीका है। इस प्रकार के वेब स्टोरेज को ब्राउज़र में डेटा प्रबंधित करने के लिए जावास्क्रिप्ट द्वारा हेरफेर किया जा सकता है। LocalStorage समाप्त नहीं होता है, जबकि SessionStorage, वेब स्टोरेज का एक अन्य प्रकार, ब्राउज़र बंद होने पर साफ़ हो जाता है। विभिन्न प्रकार के स्टोरेज के उपयोग के अपने फायदे और नुकसान हैं।

> नोट - आपके ब्राउज़र एक्सटेंशन का अपना लोकल स्टोरेज है; मुख्य ब्राउज़र विंडो एक अलग इंस्टेंस है और अलग तरीके से व्यवहार करती है।

आप अपने APIKey को एक स्ट्रिंग मान के रूप में सेट करते हैं, उदाहरण के लिए, और आप देख सकते हैं कि इसे Edge पर कैसे सेट किया गया है, "वेब पेज का निरीक्षण" करके (आप ब्राउज़र पर राइट-क्लिक करके निरीक्षण कर सकते हैं) और स्टोरेज देखने के लिए एप्लिकेशन टैब पर जा सकते हैं।

![लोकल स्टोरेज पैन](../../../../translated_images/localstorage.472f8147b6a3f8d141d9551c95a2da610ac9a3c6a73d4a1c224081c98bae09d9.hi.png)

✅ उन स्थितियों के बारे में सोचें जहां आप लोकल स्टोरेज में कुछ डेटा संग्रहीत नहीं करना चाहेंगे। सामान्य तौर पर, लोकल स्टोरेज में API Keys रखना एक बुरा विचार है! क्या आप देख सकते हैं क्यों? हमारे मामले में, चूंकि हमारा ऐप केवल सीखने के लिए है और इसे ऐप स्टोर में तैनात नहीं किया जाएगा, हम इस विधि का उपयोग करेंगे।

ध्यान दें कि आप लोकल स्टोरेज को हेरफेर करने के लिए वेब API का उपयोग करते हैं, या तो `getItem()`, `setItem()`, या `removeItem()` का उपयोग करके। यह ब्राउज़रों में व्यापक रूप से समर्थित है।

`displayCarbonUsage()` फंक्शन बनाने से पहले, जो `init()` में कॉल किया गया है, आइए प्रारंभिक फॉर्म सबमिशन को संभालने की कार्यक्षमता बनाएं।

### फॉर्म सबमिशन को संभालें

एक फंक्शन बनाएं जिसे `handleSubmit` कहा जाता है, जो एक इवेंट तर्क `(e)` स्वीकार करता है। इवेंट को फैलने से रोकें (इस मामले में, हम ब्राउज़र को रिफ्रेश होने से रोकना चाहते हैं) और एक नए फंक्शन `setUpUser` को कॉल करें, जिसमें `apiKey.value` और `region.value` तर्क पास करें। इस तरह, आप प्रारंभिक फॉर्म के माध्यम से लाए गए दो मानों का उपयोग करते हैं जब उपयुक्त फील्ड्स भरे जाते हैं।

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ अपनी याददाश्त ताज़ा करें - पिछले पाठ में सेट किए गए HTML में दो इनपुट फील्ड्स हैं जिनके `values` को आपने फाइल के शीर्ष पर सेट किए गए `const` के माध्यम से कैप्चर किया है, और वे दोनों `required` हैं ताकि ब्राउज़र उपयोगकर्ताओं को null मान इनपुट करने से रोक सके।

### उपयोगकर्ता सेट करें

`setUpUser` फंक्शन पर आगे बढ़ते हुए, यहां आप लोकल स्टोरेज में apiKey और regionName के लिए मान सेट करते हैं। एक नया फंक्शन जोड़ें:

```JavaScript
function setUpUser(apiKey, regionName) {
	localStorage.setItem('apiKey', apiKey);
	localStorage.setItem('regionName', regionName);
	loading.style.display = 'block';
	errors.textContent = '';
	clearBtn.style.display = 'block';
	//make initial call
	displayCarbonUsage(apiKey, regionName);
}
```

यह फंक्शन API को कॉल करते समय एक लोडिंग संदेश दिखाने के लिए सेट करता है। इस बिंदु पर, आप इस ब्राउज़र एक्सटेंशन के सबसे महत्वपूर्ण फंक्शन को बनाने के लिए पहुंच गए हैं!

### कार्बन उपयोग प्रदर्शित करें

अंत में, API को क्वेरी करने का समय आ गया है!

आगे बढ़ने से पहले, हमें APIs पर चर्चा करनी चाहिए। APIs, या [एप्लिकेशन प्रोग्रामिंग इंटरफेस](https://www.webopedia.com/TERM/A/API.html), एक वेब डेवलपर के टूलबॉक्स का एक महत्वपूर्ण तत्व हैं। वे प्रोग्राम्स को एक-दूसरे के साथ इंटरफेस और इंटरैक्ट करने के लिए मानक तरीके प्रदान करते हैं। उदाहरण के लिए, यदि आप एक वेबसाइट बना रहे हैं जिसे डेटाबेस को क्वेरी करने की आवश्यकता है, तो किसी ने आपके उपयोग के लिए एक API बनाया हो सकता है। जबकि APIs के कई प्रकार हैं, उनमें से एक सबसे लोकप्रिय [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/) है।

✅ 'REST' का मतलब 'Representational State Transfer' है और इसमें डेटा प्राप्त करने के लिए विभिन्न प्रकार से कॉन्फ़िगर किए गए URLs का उपयोग किया जाता है। डेवलपर्स के लिए उपलब्ध विभिन्न प्रकार के APIs पर थोड़ा शोध करें। आपको कौन सा प्रारूप पसंद आता है?

इस फंक्शन के बारे में महत्वपूर्ण बातें नोट करें। सबसे पहले, [`async` कीवर्ड](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) पर ध्यान दें। अपने फंक्शन्स को इस तरह से लिखना कि वे असिंक्रोनस रूप से चलें, इसका मतलब है कि वे किसी क्रिया, जैसे डेटा लौटने, के पूरा होने की प्रतीक्षा करते हैं, फिर आगे बढ़ते हैं।

यहां `async` पर एक त्वरित वीडियो है:

[![Async और Await के साथ प्रॉमिसेस प्रबंधित करना](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "Async और Await के साथ प्रॉमिसेस प्रबंधित करना")

> 🎥 ऊपर दी गई छवि पर क्लिक करें `async/await` के बारे में वीडियो देखने के लिए।

C02Signal API को क्वेरी करने के लिए एक नया फंक्शन बनाएं:

```JavaScript
import axios from '../node_modules/axios';

async function displayCarbonUsage(apiKey, region) {
	try {
		await axios
			.get('https://api.co2signal.com/v1/latest', {
				params: {
					countryCode: region,
				},
				headers: {
					'auth-token': apiKey,
				},
			})
			.then((response) => {
				let CO2 = Math.floor(response.data.data.carbonIntensity);

				//calculateColor(CO2);

				loading.style.display = 'none';
				form.style.display = 'none';
				myregion.textContent = region;
				usage.textContent =
					Math.round(response.data.data.carbonIntensity) + ' grams (grams C02 emitted per kilowatt hour)';
				fossilfuel.textContent =
					response.data.data.fossilFuelPercentage.toFixed(2) +
					'% (percentage of fossil fuels used to generate electricity)';
				results.style.display = 'block';
			});
	} catch (error) {
		console.log(error);
		loading.style.display = 'none';
		results.style.display = 'none';
		errors.textContent = 'Sorry, we have no data for the region you have requested.';
	}
}
```

यह एक बड़ा फंक्शन है। यहां क्या हो रहा है?

- सर्वोत्तम प्रथाओं का पालन करते हुए, आप इस फंक्शन को असिंक्रोनस रूप से व्यवहार करने के लिए `async` कीवर्ड का उपयोग करते हैं। फंक्शन में एक `try/catch` ब्लॉक होता है क्योंकि यह API से डेटा लौटने पर एक प्रॉमिस लौटाएगा। चूंकि आपके पास API के प्रतिक्रिया देने की गति पर नियंत्रण नहीं है (यह प्रतिक्रिया नहीं भी दे सकता है!), आपको इस अनिश्चितता को असिंक्रोनस रूप से कॉल करके संभालना होगा।
- आप co2signal API को अपने क्षेत्र का डेटा प्राप्त करने के लिए क्वेरी कर रहे हैं, अपने API Key का उपयोग करके। उस key का उपयोग करने के लिए, आपको अपने हेडर पैरामीटर्स में एक प्रकार का ऑथेंटिकेशन उपयोग करना होगा।
- एक बार जब API प्रतिक्रिया देता है, तो आप इसकी प्रतिक्रिया डेटा के विभिन्न तत्वों को अपनी स्क्रीन के उन हिस्सों को असाइन करते हैं जिन्हें आपने यह डेटा दिखाने के लिए सेट किया है।
- यदि कोई त्रुटि है, या कोई परिणाम नहीं है, तो आप एक त्रुटि संदेश दिखाते हैं।

✅ असिंक्रोनस प्रोग्रामिंग पैटर्न का उपयोग करना आपके टूलबॉक्स में एक और बहुत उपयोगी उपकरण है। [विभिन्न तरीकों](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) के बारे में पढ़ें जिनसे आप इस प्रकार के कोड को कॉन्फ़िगर कर सकते हैं।

बधाई हो! यदि आप अपने एक्सटेंशन को बिल्ड करते हैं (`npm run build`) और इसे अपने एक्सटेंशन पैन में रिफ्रेश करते हैं, तो आपके पास एक कार्यशील एक्सटेंशन है! केवल एक चीज जो काम नहीं कर रही है वह है आइकन, और आप इसे अगले पाठ में ठीक करेंगे।

---

## 🚀 चुनौती

हमने इन पाठों में अब तक कई प्रकार के API पर चर्चा की है। एक वेब API चुनें और गहराई से शोध करें कि यह क्या प्रदान करता है। उदाहरण के लिए, ब्राउज़रों में उपलब्ध APIs जैसे [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API) को देखें। आपके विचार में एक अच्छा API क्या बनाता है?

## पोस्ट-लेक्चर क्विज़

[पोस्ट-लेक्चर क्विज़](https://ff-quizzes.netlify.app/web/quiz/26)

## समीक्षा और स्व-अध्ययन

आपने इस पाठ में LocalStorage और APIs के बारे में सीखा, जो पेशेवर वेब डेवलपर के लिए बहुत उपयोगी हैं। क्या आप सोच सकते हैं कि ये दोनों चीजें एक साथ कैसे काम करती हैं? सोचें कि आप एक वेबसाइट को कैसे डिज़ाइन करेंगे जो API द्वारा उपयोग किए जाने वाले आइटम्स को संग्रहीत करे।

## असाइनमेंट

[एक API अपनाएं](assignment.md)

---

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता सुनिश्चित करने का प्रयास करते हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को आधिकारिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम जिम्मेदार नहीं हैं।