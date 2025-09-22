<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a7587943d38d095de8613e1b508609f5",
  "translation_date": "2025-08-28T22:57:16+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "bn"
}
-->
# ব্রাউজার এক্সটেনশন প্রকল্প পার্ট ২: একটি API কল করা, লোকাল স্টোরেজ ব্যবহার করা

## প্রাক-লেকচার কুইজ

[প্রাক-লেকচার কুইজ](https://ff-quizzes.netlify.app/web/quiz/25)

### ভূমিকা

এই পাঠে, আপনি আপনার ব্রাউজার এক্সটেনশনের ফর্ম জমা দিয়ে একটি API কল করবেন এবং ফলাফল ব্রাউজার এক্সটেনশনে প্রদর্শন করবেন। এছাড়াও, আপনি শিখবেন কীভাবে আপনার ব্রাউজারের লোকাল স্টোরেজে ডেটা সংরক্ষণ করা যায় ভবিষ্যতে রেফারেন্স এবং ব্যবহারের জন্য।

✅ সঠিক ফাইলের নম্বরযুক্ত অংশগুলি অনুসরণ করুন যাতে আপনি কোড কোথায় স্থাপন করবেন তা জানতে পারেন।

### এক্সটেনশনে ম্যানিপুলেট করার উপাদানগুলি সেট আপ করুন:

এখন পর্যন্ত আপনি আপনার ব্রাউজার এক্সটেনশনের জন্য ফর্ম এবং ফলাফলের `<div>` এর HTML তৈরি করেছেন। এখন থেকে, আপনাকে `/src/index.js` ফাইলে কাজ করতে হবে এবং ধাপে ধাপে আপনার এক্সটেনশন তৈরি করতে হবে। আপনার প্রকল্প সেট আপ এবং বিল্ড প্রসেস সম্পর্কে জানার জন্য [পূর্ববর্তী পাঠ](../1-about-browsers/README.md) দেখুন।

`index.js` ফাইলে কাজ শুরু করে, বিভিন্ন ফিল্ডের সাথে সম্পর্কিত মানগুলি ধরে রাখার জন্য কিছু `const` ভেরিয়েবল তৈরি করুন:

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

এই সমস্ত ফিল্ডগুলি তাদের CSS ক্লাস দ্বারা রেফারেন্স করা হয়েছে, যা আপনি পূর্ববর্তী পাঠে HTML-এ সেট আপ করেছিলেন।

### লিসেনার যোগ করুন

এরপর, ফর্ম এবং ক্লিয়ার বোতামে ইভেন্ট লিসেনার যোগ করুন যা ফর্ম রিসেট করে, যাতে ব্যবহারকারী ফর্ম জমা দিলে বা রিসেট বোতামে ক্লিক করলে কিছু ঘটে। ফাইলের শেষে অ্যাপটি ইনিশিয়ালাইজ করার কল যোগ করুন:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ লক্ষ্য করুন সাবমিট বা ক্লিক ইভেন্ট শোনার জন্য ব্যবহৃত শর্টহ্যান্ড এবং কীভাবে ইভেন্টটি handleSubmit বা reset ফাংশনে পাস করা হয়। আপনি কি এই শর্টহ্যান্ডের সমতুল্য একটি দীর্ঘ ফর্ম্যাট লিখতে পারেন? কোনটি আপনার পছন্দ?

### init() ফাংশন এবং reset() ফাংশন তৈরি করুন:

এখন আপনি এক্সটেনশনটি ইনিশিয়ালাইজ করার ফাংশন তৈরি করবেন, যা init() নামে ডাকা হয়:

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

এই ফাংশনে কিছু আকর্ষণীয় লজিক রয়েছে। এটি পড়ে আপনি দেখতে পাচ্ছেন কী ঘটে?

- দুটি `const` সেট আপ করা হয়েছে চেক করতে যে ব্যবহারকারী লোকাল স্টোরেজে APIKey এবং region কোড সংরক্ষণ করেছেন কিনা।
- যদি এর যেকোনো একটি null হয়, ফর্মটি প্রদর্শন করুন এবং এর স্টাইল 'block' এ পরিবর্তন করুন।
- ফলাফল, লোডিং এবং clearBtn লুকান এবং যেকোনো ত্রুটির টেক্সট খালি স্ট্রিংয়ে সেট করুন।
- যদি একটি key এবং region থাকে, একটি রুটিন শুরু করুন:
  - API কল করে কার্বন ব্যবহারের ডেটা পান।
  - ফলাফল এলাকা লুকান।
  - ফর্ম লুকান।
  - রিসেট বোতাম দেখান।

পরবর্তী ধাপে যাওয়ার আগে, ব্রাউজারে উপলব্ধ একটি খুব গুরুত্বপূর্ণ ধারণা সম্পর্কে শেখা দরকার: [LocalStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)। LocalStorage একটি দরকারী উপায় ব্রাউজারে স্ট্রিং সংরক্ষণ করার জন্য একটি `key-value` জোড়া হিসাবে। এই ধরনের ওয়েব স্টোরেজ জাভাস্ক্রিপ্ট দ্বারা ম্যানিপুলেট করা যায় ব্রাউজারে ডেটা পরিচালনা করতে। LocalStorage মেয়াদোত্তীর্ণ হয় না, যেখানে SessionStorage, আরেক ধরনের ওয়েব স্টোরেজ, ব্রাউজার বন্ধ হলে সাফ হয়ে যায়। বিভিন্ন ধরনের স্টোরেজের ব্যবহারে সুবিধা এবং অসুবিধা রয়েছে।

> নোট - আপনার ব্রাউজার এক্সটেনশনের নিজস্ব লোকাল স্টোরেজ রয়েছে; প্রধান ব্রাউজার উইন্ডো একটি ভিন্ন ইনস্ট্যান্স এবং আলাদাভাবে আচরণ করে।

আপনার APIKey একটি স্ট্রিং মানে সেট করুন, উদাহরণস্বরূপ, এবং আপনি দেখতে পাবেন এটি Edge-এ সেট করা হয়েছে একটি ওয়েব পেজ "ইন্সপেক্ট" করে (আপনি ব্রাউজারে ডান ক্লিক করে ইন্সপেক্ট করতে পারেন) এবং অ্যাপ্লিকেশন ট্যাবে গিয়ে স্টোরেজ দেখতে পারেন।

![লোকাল স্টোরেজ প্যান](../../../../translated_images/localstorage.472f8147b6a3f8d141d9551c95a2da610ac9a3c6a73d4a1c224081c98bae09d9.bn.png)

✅ এমন পরিস্থিতি নিয়ে ভাবুন যেখানে আপনি কিছু ডেটা LocalStorage-এ সংরক্ষণ করতে চান না। সাধারণত, LocalStorage-এ API Keys রাখা একটি খারাপ ধারণা! কেন তা আপনি দেখতে পাচ্ছেন? আমাদের ক্ষেত্রে, যেহেতু আমাদের অ্যাপটি শুধুমাত্র শেখার জন্য এবং এটি অ্যাপ স্টোরে প্রকাশিত হবে না, আমরা এই পদ্ধতি ব্যবহার করব।

আপনি LocalStorage ম্যানিপুলেট করতে Web API ব্যবহার করেন, হয় `getItem()`, `setItem()`, বা `removeItem()` ব্যবহার করে। এটি ব্রাউজার জুড়ে ব্যাপকভাবে সমর্থিত।

`displayCarbonUsage()` ফাংশন তৈরি করার আগে যা `init()`-এ ডাকা হয়, আসুন প্রাথমিক ফর্ম জমা দেওয়ার কার্যকারিতা তৈরি করি।

### ফর্ম জমা দেওয়া পরিচালনা করুন

`handleSubmit` নামে একটি ফাংশন তৈরি করুন যা একটি ইভেন্ট আর্গুমেন্ট `(e)` গ্রহণ করে। ইভেন্টটি প্রচারিত হওয়া থেকে থামান (এই ক্ষেত্রে, আমরা ব্রাউজারকে রিফ্রেশ হওয়া থেকে থামাতে চাই) এবং একটি নতুন ফাংশন `setUpUser` কল করুন, আর্গুমেন্ট হিসাবে `apiKey.value` এবং `region.value` পাস করে। এইভাবে, আপনি প্রাথমিক ফর্মের মাধ্যমে আনা দুটি মান ব্যবহার করেন যখন প্রাসঙ্গিক ফিল্ডগুলি পূরণ করা হয়।

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ আপনার স্মৃতি সতেজ করুন - পূর্ববর্তী পাঠে আপনি যে HTML সেট আপ করেছিলেন তাতে দুটি ইনপুট ফিল্ড রয়েছে যার `values` আপনি ফাইলের শীর্ষে সেট করা `const` এর মাধ্যমে ক্যাপচার করেন, এবং সেগুলি উভয়ই `required` যাতে ব্রাউজার ব্যবহারকারীদের null মান ইনপুট করা থেকে থামায়।

### ব্যবহারকারী সেট আপ করুন

`setUpUser` ফাংশনে এগিয়ে যান, এখানে আপনি apiKey এবং regionName এর জন্য লোকাল স্টোরেজ মান সেট করেন। একটি নতুন ফাংশন যোগ করুন:

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

এই ফাংশনটি একটি লোডিং বার্তা দেখায় যখন API কল করা হয়। এই পর্যায়ে, আপনি এই ব্রাউজার এক্সটেনশনের সবচেয়ে গুরুত্বপূর্ণ ফাংশন তৈরি করতে পৌঁছেছেন!

### কার্বন ব্যবহারের প্রদর্শন

অবশেষে, API-তে প্রশ্ন করার সময় এসেছে!

আরও এগিয়ে যাওয়ার আগে, আমাদের API নিয়ে আলোচনা করা উচিত। API, বা [অ্যাপ্লিকেশন প্রোগ্রামিং ইন্টারফেস](https://www.webopedia.com/TERM/A/API.html), একটি ওয়েব ডেভেলপারের টুলবক্সের একটি গুরুত্বপূর্ণ উপাদান। এগুলি প্রোগ্রামগুলিকে একে অপরের সাথে ইন্টারঅ্যাক্ট এবং ইন্টারফেস করার জন্য মানক উপায় সরবরাহ করে। উদাহরণস্বরূপ, আপনি যদি এমন একটি ওয়েবসাইট তৈরি করেন যা একটি ডাটাবেসে প্রশ্ন করতে হবে, কেউ হয়তো আপনার জন্য একটি API তৈরি করেছে। অনেক ধরনের API থাকলেও, সবচেয়ে জনপ্রিয়গুলির মধ্যে একটি হল [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/)।

✅ 'REST' শব্দটি 'Representational State Transfer' এর জন্য দাঁড়ায় এবং ডেটা আনতে বিভিন্নভাবে কনফিগার করা URL ব্যবহার করার বৈশিষ্ট্য রয়েছে। ডেভেলপারদের জন্য উপলব্ধ বিভিন্ন ধরনের API সম্পর্কে একটু গবেষণা করুন। কোন ফরম্যাটটি আপনার কাছে আকর্ষণীয় মনে হয়?

এই ফাংশন সম্পর্কে গুরুত্বপূর্ণ বিষয়গুলি লক্ষ্য করুন। প্রথমত, [`async` কীওয়ার্ড](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) লক্ষ্য করুন। আপনার ফাংশনগুলি অ্যাসিঙ্ক্রোনাসভাবে চালানোর জন্য লেখা মানে এটি একটি অ্যাকশন, যেমন ডেটা ফেরত আসা, সম্পন্ন হওয়ার জন্য অপেক্ষা করে তারপর চালিয়ে যায়।

এখানে `async` সম্পর্কে একটি দ্রুত ভিডিও রয়েছে:

[![প্রমিজ ম্যানেজ করার জন্য Async এবং Await](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "প্রমিজ ম্যানেজ করার জন্য Async এবং Await")

> 🎥 উপরের ছবিতে ক্লিক করুন `async/await` সম্পর্কে একটি ভিডিওর জন্য।

C02Signal API-তে প্রশ্ন করার জন্য একটি নতুন ফাংশন তৈরি করুন:

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

এটি একটি বড় ফাংশন। এখানে কী ঘটছে?

- সেরা অনুশীলন অনুসরণ করে, আপনি এই ফাংশনটিকে অ্যাসিঙ্ক্রোনাস আচরণ করার জন্য একটি `async` কীওয়ার্ড ব্যবহার করেন। ফাংশনটিতে একটি `try/catch` ব্লক রয়েছে কারণ এটি একটি প্রমিজ ফেরত দেবে যখন API ডেটা ফেরত দেবে। যেহেতু আপনি API কত দ্রুত প্রতিক্রিয়া জানাবে তা নিয়ন্ত্রণ করতে পারবেন না (এটি প্রতিক্রিয়া জানাবে না!), আপনাকে এটি অ্যাসিঙ্ক্রোনাসভাবে কল করে এই অনিশ্চয়তা পরিচালনা করতে হবে।
- আপনি co2signal API-তে আপনার অঞ্চলের ডেটা পেতে প্রশ্ন করছেন, আপনার API Key ব্যবহার করে। সেই কী ব্যবহার করতে, আপনাকে আপনার হেডার প্যারামিটারে একটি প্রমাণীকরণের ধরন ব্যবহার করতে হবে।
- একবার API প্রতিক্রিয়া জানালে, আপনি এর প্রতিক্রিয়া ডেটার বিভিন্ন উপাদান আপনার স্ক্রিনের সেই অংশগুলিতে বরাদ্দ করেন যা আপনি এই ডেটা দেখানোর জন্য সেট আপ করেছেন।
- যদি কোনো ত্রুটি থাকে, বা কোনো ফলাফল না থাকে, আপনি একটি ত্রুটির বার্তা দেখান।

✅ অ্যাসিঙ্ক্রোনাস প্রোগ্রামিং প্যাটার্ন ব্যবহার করা আপনার টুলবক্সে আরেকটি খুব দরকারী টুল। [এই ধরনের কোড কনফিগার করার বিভিন্ন উপায়](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) সম্পর্কে পড়ুন।

অভিনন্দন! যদি আপনি আপনার এক্সটেনশন তৈরি করেন (`npm run build`) এবং এটি আপনার এক্সটেনশন প্যানেলে রিফ্রেশ করেন, তবে আপনার একটি কার্যকরী এক্সটেনশন রয়েছে! একমাত্র জিনিস যা কাজ করছে না তা হল আইকন, এবং আপনি এটি পরবর্তী পাঠে ঠিক করবেন।

---

## 🚀 চ্যালেঞ্জ

আমরা এই পাঠগুলিতে এখন পর্যন্ত বেশ কয়েকটি ধরনের API নিয়ে আলোচনা করেছি। একটি ওয়েব API বেছে নিন এবং এটি কী অফার করে তা গভীরভাবে গবেষণা করুন। উদাহরণস্বরূপ, ব্রাউজারে উপলব্ধ API যেমন [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API) দেখুন। আপনার মতে একটি দুর্দান্ত API কী তৈরি করে?

## পোস্ট-লেকচার কুইজ

[পোস্ট-লেকচার কুইজ](https://ff-quizzes.netlify.app/web/quiz/26)

## পর্যালোচনা এবং স্ব-অধ্যয়ন

এই পাঠে আপনি LocalStorage এবং API সম্পর্কে শিখেছেন, যা পেশাদার ওয়েব ডেভেলপারের জন্য খুবই দরকারী। আপনি কি ভাবতে পারেন কীভাবে এই দুটি জিনিস একসাথে কাজ করে? এমন একটি ওয়েবসাইট আর্কিটেক্ট করার কথা ভাবুন যা একটি API দ্বারা ব্যবহৃত আইটেমগুলি সংরক্ষণ করবে।

## অ্যাসাইনমেন্ট

[একটি API গ্রহণ করুন](assignment.md)

---

**অস্বীকৃতি**:  
এই নথিটি AI অনুবাদ পরিষেবা [Co-op Translator](https://github.com/Azure/co-op-translator) ব্যবহার করে অনুবাদ করা হয়েছে। আমরা যথাসম্ভব সঠিকতার জন্য চেষ্টা করি, তবে অনুগ্রহ করে মনে রাখুন যে স্বয়ংক্রিয় অনুবাদে ত্রুটি বা অসঙ্গতি থাকতে পারে। মূল ভাষায় থাকা নথিটিকে প্রামাণিক উৎস হিসেবে বিবেচনা করা উচিত। গুরুত্বপূর্ণ তথ্যের জন্য, পেশাদার মানব অনুবাদ সুপারিশ করা হয়। এই অনুবাদ ব্যবহারের ফলে কোনো ভুল বোঝাবুঝি বা ভুল ব্যাখ্যা হলে আমরা দায়বদ্ধ থাকব না।