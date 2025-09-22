<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a7587943d38d095de8613e1b508609f5",
  "translation_date": "2025-08-28T16:34:44+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "ne"
}
-->
# ब्राउजर एक्सटेन्सन प्रोजेक्ट भाग २: API कल गर्नुहोस्, लोकल स्टोरेज प्रयोग गर्नुहोस्

## प्रि-लेक्चर क्विज

[प्रि-लेक्चर क्विज](https://ff-quizzes.netlify.app/web/quiz/25)

### परिचय

यस पाठमा, तपाईं आफ्नो ब्राउजर एक्सटेन्सनको फारम सबमिट गरेर API कल गर्नुहुनेछ र परिणामहरू ब्राउजर एक्सटेन्सनमा देखाउनुहुनेछ। साथै, तपाईं आफ्नो ब्राउजरको लोकल स्टोरेजमा डाटा भविष्यको सन्दर्भ र प्रयोगका लागि कसरी भण्डारण गर्ने भन्ने कुरा सिक्नुहुनेछ।

✅ कोड कहाँ राख्ने भनेर जान्नका लागि सम्बन्धित फाइलहरूमा क्रमांकित खण्डहरू अनुसरण गर्नुहोस्।

### एक्सटेन्सनमा परिमार्जन गर्नका लागि तत्त्वहरू सेट गर्नुहोस्:

यस समयसम्म तपाईंले आफ्नो ब्राउजर एक्सटेन्सनको लागि फारम र परिणाम `<div>` को HTML बनाइसक्नुभएको छ। अबदेखि, तपाईंले `/src/index.js` फाइलमा काम गर्नुपर्नेछ र आफ्नो एक्सटेन्सनलाई क्रमशः निर्माण गर्नुपर्नेछ। आफ्नो प्रोजेक्ट सेटअप र बिल्ड प्रक्रियाबारे जान्न [अघिल्लो पाठ](../1-about-browsers/README.md) हेर्नुहोस्।

`index.js` फाइलमा काम गर्दै, विभिन्न फिल्डहरूसँग सम्बन्धित मानहरू राख्नका लागि केही `const` भेरिएबलहरू सिर्जना गरेर सुरु गर्नुहोस्:

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

यी सबै फिल्डहरू CSS क्लासद्वारा सन्दर्भित गरिएका छन्, जुन तपाईंले अघिल्लो पाठमा HTML मा सेट गर्नुभएको थियो।

### लिस्नरहरू थप्नुहोस्

अब, फारम र क्लियर बटनमा इभेन्ट लिस्नरहरू थप्नुहोस् जसले फारम सबमिट गर्दा वा क्लियर बटन क्लिक गर्दा केही कार्य गर्दछ, र फाइलको अन्त्यमा एप्लिकेसनलाई इनिसियलाइज गर्ने कल थप्नुहोस्:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ ध्यान दिनुहोस्, सबमिट वा क्लिक इभेन्ट सुन्नका लागि प्रयोग गरिएको छोटकरी तरिका, र कसरी इभेन्टलाई `handleSubmit` वा `reset` फंक्शनमा पास गरिएको छ। के तपाईं यो छोटकरी तरिकाको लामो संस्करण लेख्न सक्नुहुन्छ? कुन तरिका तपाईंलाई मन पर्छ?

### `init()` र `reset()` फंक्शन निर्माण गर्नुहोस्:

अब तपाईं एक्सटेन्सनलाई इनिसियलाइज गर्ने फंक्शन निर्माण गर्दै हुनुहुन्छ, जसलाई `init()` भनिन्छ:

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

यस फंक्शनमा केही रोचक तर्कहरू छन्। यसलाई पढ्दा, के हुन्छ भनेर बुझ्न सक्नुहुन्छ?

- दुई `const` सेटअप गरिन्छ, जसले जाँच गर्छ कि प्रयोगकर्ताले लोकल स्टोरेजमा APIKey र क्षेत्र कोड भण्डारण गरेका छन् कि छैनन्।
- यदि यीमध्ये कुनै पनि `null` छ भने, फारमलाई 'block' शैलीमा देखाउनुहोस्।
- परिणाम, लोडिङ, र `clearBtn` लुकाउनुहोस् र कुनै पनि त्रुटि पाठलाई खाली स्ट्रिङमा सेट गर्नुहोस्।
- यदि कुनै की र क्षेत्र छ भने, निम्न कार्य सुरु गर्नुहोस्:
  - API कल गरेर कार्बन प्रयोग डाटा प्राप्त गर्नुहोस्।
  - परिणाम क्षेत्र लुकाउनुहोस्।
  - फारम लुकाउनुहोस्।
  - रिसेट बटन देखाउनुहोस्।

अगाडि बढ्नु अघि, ब्राउजरमा उपलब्ध एक महत्त्वपूर्ण अवधारणाबारे जान्नु उपयोगी हुन्छ: [LocalStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)। LocalStorage ब्राउजरमा स्ट्रिङहरू `key-value` जोडीको रूपमा भण्डारण गर्न उपयोगी तरिका हो। यो प्रकारको वेब स्टोरेजलाई जाभास्क्रिप्टद्वारा हेरफेर गर्न सकिन्छ। LocalStorage समाप्त हुँदैन, जबकि SessionStorage, अर्को प्रकारको वेब स्टोरेज, ब्राउजर बन्द हुँदा खाली हुन्छ। विभिन्न प्रकारका स्टोरेजको प्रयोगका लागि फाइदा र बेफाइदा छन्।

> नोट - तपाईंको ब्राउजर एक्सटेन्सनको आफ्नै लोकल स्टोरेज छ; मुख्य ब्राउजर विन्डो फरक इन्स्ट्यान्स हो र छुट्टै व्यवहार गर्दछ।

तपाईंले आफ्नो APIKey लाई स्ट्रिङ मानमा सेट गर्न सक्नुहुन्छ, उदाहरणका लागि, र तपाईंले Edge मा यो सेट गरिएको देख्न सक्नुहुन्छ वेब पेजलाई "इन्स्पेक्ट" गरेर (तपाईं ब्राउजरमा दायाँ क्लिक गरेर इन्स्पेक्ट गर्न सक्नुहुन्छ) र एप्लिकेसन ट्याबमा गएर स्टोरेज हेर्न सक्नुहुन्छ।

![लोकल स्टोरेज प्यान](../../../../translated_images/localstorage.472f8147b6a3f8d141d9551c95a2da610ac9a3c6a73d4a1c224081c98bae09d9.ne.png)

✅ सोच्नुहोस्, कुन अवस्थामा तपाईं लोकल स्टोरेजमा केही डाटा भण्डारण गर्न चाहनुहुन्न। सामान्यतया, लोकल स्टोरेजमा API Keys राख्नु खराब विचार हो! तपाईंले किन देख्न सक्नुहुन्छ? हाम्रो अवस्थामा, किनभने हाम्रो एप शुद्ध रूपमा सिकाइका लागि हो र एप स्टोरमा तैनाथ गरिने छैन, हामी यो विधि प्रयोग गर्नेछौं।

तपाईंले लोकल स्टोरेजलाई हेरफेर गर्न वेब API प्रयोग गर्नुहुन्छ, `getItem()`, `setItem()`, वा `removeItem()` प्रयोग गरेर। यो ब्राउजरहरूमा व्यापक रूपमा समर्थित छ।

`displayCarbonUsage()` फंक्शन निर्माण गर्नुअघि, जुन `init()` मा कल गरिएको छ, सुरुमा फारम सबमिशन ह्यान्डल गर्ने कार्यक्षमता निर्माण गरौं।

### फारम सबमिशन ह्यान्डल गर्नुहोस्

`handleSubmit` नामक फंक्शन सिर्जना गर्नुहोस्, जसले `(e)` इभेन्ट आर्गुमेन्ट स्वीकार्छ। इभेन्टलाई फैलिनबाट रोक्नुहोस् (यस अवस्थामा, हामी ब्राउजरलाई रिफ्रेस हुनबाट रोक्न चाहन्छौं) र नयाँ फंक्शन `setUpUser` कल गर्नुहोस्, जसमा `apiKey.value` र `region.value` आर्गुमेन्ट पास गरिन्छ। यसरी, तपाईंले सुरुमा फारमबाट ल्याइएका दुई मानहरू प्रयोग गर्नुहुन्छ, जब सम्बन्धित फिल्डहरू भरिएका हुन्छन्।

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ आफ्नो स्मरण ताजा गर्नुहोस् - अघिल्लो पाठमा तपाईंले सेट गर्नुभएको HTML मा दुई इनपुट फिल्डहरू छन्, जसका `values` तपाईंले फाइलको शीर्षमा सेट गर्नुभएको `const` मार्फत क्याप्चर गरिन्छ, र ती दुवै `required` छन्, जसले ब्राउजरलाई प्रयोगकर्ताहरूलाई `null` मानहरू इनपुट गर्नबाट रोक्छ।

### प्रयोगकर्ता सेट गर्नुहोस्

`setUpUser` फंक्शनतर्फ अगाडि बढ्दै, यहाँ तपाईंले लोकल स्टोरेज मानहरू `apiKey` र `regionName` का लागि सेट गर्नुहुन्छ। नयाँ फंक्शन थप्नुहोस्:

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

यो फंक्शनले API कल हुँदा देखाउन लोडिङ सन्देश सेट गर्दछ। यस बिन्दुमा, तपाईं आफ्नो ब्राउजर एक्सटेन्सनको सबैभन्दा महत्त्वपूर्ण फंक्शन सिर्जना गर्न आइपुग्नुभएको छ!

### कार्बन प्रयोग देखाउनुहोस्

अन्ततः, API क्वेरी गर्ने समय आएको छ!

अगाडि बढ्नु अघि, हामीले API हरूबारे छलफल गर्नुपर्छ। API हरू, वा [Application Programming Interfaces](https://www.webopedia.com/TERM/A/API.html), वेब विकासकर्ताको उपकरणको महत्त्वपूर्ण तत्व हो। यीले प्रोग्रामहरूलाई एकअर्कासँग अन्तरक्रिया गर्न र इन्टरफेस गर्न मानक तरिकाहरू प्रदान गर्छन्। उदाहरणका लागि, यदि तपाईं डेटाबेस क्वेरी गर्न आवश्यक पर्ने वेबसाइट निर्माण गर्दै हुनुहुन्छ भने, कसैले तपाईंलाई प्रयोग गर्न API सिर्जना गरेको हुन सक्छ। API का धेरै प्रकारहरू छन्, तर सबैभन्दा लोकप्रियमध्ये एक हो [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/)।

✅ 'REST' शब्दले 'Representational State Transfer' लाई जनाउँछ र विभिन्न प्रकारका URL हरू प्रयोग गरेर डाटा फेच गर्ने सुविधा दिन्छ। विकासकर्ताहरूका लागि उपलब्ध विभिन्न प्रकारका API हरूबारे थोरै अनुसन्धान गर्नुहोस्। कुन ढाँचा तपाईंलाई मन पर्छ?

यस फंक्शनका महत्त्वपूर्ण पक्षहरू छन्। सुरुमा, [`async` कीवर्ड](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) लाई ध्यान दिनुहोस्। तपाईंको फंक्शनहरूलाई असिन्क्रोनस रूपमा लेख्दा, ती कुनै कार्य (जस्तै, डाटा फर्किने) पूरा नभएसम्म पर्खन्छन्।

`async` को बारेमा छोटो भिडियो यहाँ छ:

[![प्रमिसहरू व्यवस्थापन गर्न Async र Await](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "प्रमिसहरू व्यवस्थापन गर्न Async र Await")

> 🎥 माथिको छविमा क्लिक गरेर `async/await` को बारेमा भिडियो हेर्नुहोस्।

C02Signal API क्वेरी गर्न नयाँ फंक्शन सिर्जना गर्नुहोस्:

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

यो ठूलो फंक्शन हो। यहाँ के भइरहेको छ?

- राम्रो अभ्यासहरू अनुसरण गर्दै, तपाईंले `async` कीवर्ड प्रयोग गरेर यो फंक्शनलाई असिन्क्रोनस रूपमा व्यवहार गराउनुहुन्छ। फंक्शनले `try/catch` ब्लक समावेश गर्दछ, किनभने यो API बाट डाटा फर्किंदा प्रमिस फर्काउँछ। API कति छिटो प्रतिक्रिया दिन्छ भन्ने तपाईंको नियन्त्रणमा छैन (यो प्रतिक्रिया नदिन पनि सक्छ!), त्यसैले यो अनिश्चिततालाई असिन्क्रोनस रूपमा कल गरेर ह्यान्डल गर्न आवश्यक छ।
- तपाईं आफ्नो क्षेत्रको डाटा प्राप्त गर्न co2signal API क्वेरी गर्दै हुनुहुन्छ, आफ्नो API Key प्रयोग गरेर। त्यो की प्रयोग गर्न, तपाईंले आफ्नो हेडर प्यारामिटरहरूमा एक प्रकारको प्रमाणीकरण प्रयोग गर्नुपर्छ।
- API ले प्रतिक्रिया दिएपछि, यसको प्रतिक्रिया डाटाका विभिन्न तत्वहरूलाई तपाईंले सेट गर्नुभएको स्क्रिनका भागहरूमा असाइन गर्नुहुन्छ।
- यदि कुनै त्रुटि छ, वा कुनै परिणाम छैन भने, तपाईं त्रुटि सन्देश देखाउनुहुन्छ।

✅ असिन्क्रोनस प्रोग्रामिङ ढाँचाहरू तपाईंको उपकरणको अर्को धेरै उपयोगी उपकरण हो। [यस प्रकारको कोडलाई कन्फिगर गर्न सकिने विभिन्न तरिकाहरू](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) पढ्नुहोस्।

बधाई छ! यदि तपाईं आफ्नो एक्सटेन्सन निर्माण गर्नुहुन्छ (`npm run build`) र यसलाई आफ्नो एक्सटेन्सन प्यानमा रिफ्रेस गर्नुहुन्छ भने, तपाईंको एक्सटेन्सन काम गरिरहेको छ! केवल आइकन काम गरिरहेको छैन, र तपाईंले यो अर्को पाठमा समाधान गर्नुहुनेछ।

---

## 🚀 चुनौती

हामीले यी पाठहरूमा अहिलेसम्म विभिन्न प्रकारका API हरूबारे छलफल गरिसकेका छौं। कुनै वेब API छान्नुहोस् र यसले के प्रस्ताव गर्दछ भनेर गहिरो अनुसन्धान गर्नुहोस्। उदाहरणका लागि, ब्राउजरभित्र उपलब्ध API हरू जस्तै [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API) हेर्नुहोस्। तपाईंको विचारमा, केले राम्रो API बनाउँछ?

## पोस्ट-लेक्चर क्विज

[पोस्ट-लेक्चर क्विज](https://ff-quizzes.netlify.app/web/quiz/26)

## समीक्षा र आत्म अध्ययन

यस पाठमा तपाईंले लोकल स्टोरेज र API हरूबारे सिक्नुभयो, जुन व्यावसायिक वेब विकासकर्ताका लागि धेरै उपयोगी छन्। यी दुई चीजहरू कसरी सँगै काम गर्छन् भनेर सोच्न सक्नुहुन्छ? API द्वारा प्रयोग गरिने वस्तुहरू भण्डारण गर्ने वेबसाइट कसरी आर्किटेक्चर गर्ने भनेर सोच्नुहोस्।

## असाइनमेन्ट

[एडप्ट एन API](assignment.md)

---

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरी अनुवाद गरिएको हो। हामी यथासम्भव शुद्धताको प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादहरूमा त्रुटि वा अशुद्धता हुन सक्छ। यसको मूल भाषामा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्त्वपूर्ण जानकारीका लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याका लागि हामी जिम्मेवार हुने छैनौं।  