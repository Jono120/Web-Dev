<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a7587943d38d095de8613e1b508609f5",
  "translation_date": "2025-08-28T15:22:34+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "ur"
}
-->
# براؤزر ایکسٹینشن پروجیکٹ حصہ 2: API کال کریں، لوکل اسٹوریج استعمال کریں

## لیکچر سے پہلے کا کوئز

[لیکچر سے پہلے کا کوئز](https://ff-quizzes.netlify.app/web/quiz/25)

### تعارف

اس سبق میں، آپ اپنے براؤزر ایکسٹینشن کے فارم کو سبمٹ کرکے ایک API کال کریں گے اور نتائج کو اپنے براؤزر ایکسٹینشن میں دکھائیں گے۔ اس کے علاوہ، آپ یہ بھی سیکھیں گے کہ اپنے براؤزر کے لوکل اسٹوریج میں ڈیٹا کو مستقبل کے حوالے اور استعمال کے لیے کیسے محفوظ کیا جا سکتا ہے۔

✅ مناسب فائلوں میں نمبر شدہ حصوں کی پیروی کریں تاکہ آپ کو معلوم ہو کہ کوڈ کہاں رکھنا ہے۔

### ایکسٹینشن میں عناصر کو ترتیب دیں:

اس وقت تک آپ نے اپنے براؤزر ایکسٹینشن کے لیے فارم اور نتائج کے `<div>` کے لیے HTML بنا لیا ہوگا۔ اب سے، آپ کو `/src/index.js` فائل میں کام کرنا ہوگا اور اپنے ایکسٹینشن کو تھوڑا تھوڑا کرکے بنانا ہوگا۔ اپنے پروجیکٹ کو سیٹ اپ کرنے اور بلڈ پروسیس کے بارے میں جاننے کے لیے [پچھلے سبق](../1-about-browsers/README.md) کا حوالہ دیں۔

اپنی `index.js` فائل میں کام کرتے ہوئے، مختلف فیلڈز سے وابستہ ویلیوز کو رکھنے کے لیے کچھ `const` ویریبلز بنائیں:

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

یہ تمام فیلڈز ان کی CSS کلاس کے ذریعے حوالہ دی گئی ہیں، جیسا کہ آپ نے پچھلے سبق میں HTML میں سیٹ کیا تھا۔

### لسٹنرز شامل کریں

اگلا، فارم اور کلئیر بٹن پر ایونٹ لسٹنرز شامل کریں جو فارم کو ری سیٹ کرتا ہے، تاکہ اگر کوئی صارف فارم سبمٹ کرے یا ری سیٹ بٹن پر کلک کرے تو کچھ ہو۔ فائل کے آخر میں ایپ کو انیشیالائز کرنے کے لیے کال شامل کریں:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ نوٹ کریں کہ سبمٹ یا کلک ایونٹ سننے کے لیے استعمال ہونے والے شارٹ ہینڈ کو، اور یہ کہ ایونٹ کو کیسے `handleSubmit` یا `reset` فنکشنز میں پاس کیا جاتا ہے۔ کیا آپ اس شارٹ ہینڈ کا طویل فارمیٹ میں متبادل لکھ سکتے ہیں؟ آپ کو کون سا زیادہ پسند ہے؟

### `init()` اور `reset()` فنکشنز بنائیں:

اب آپ ایکسٹینشن کو انیشیالائز کرنے والے فنکشن کو بنائیں گے، جسے `init()` کہا جاتا ہے:

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

اس فنکشن میں کچھ دلچسپ لاجک ہے۔ اسے پڑھتے ہوئے، کیا آپ دیکھ سکتے ہیں کہ کیا ہو رہا ہے؟

- دو `const` سیٹ کیے گئے ہیں تاکہ چیک کیا جا سکے کہ آیا صارف نے لوکل اسٹوریج میں APIKey اور ریجن کوڈ محفوظ کیا ہے۔
- اگر ان میں سے کوئی بھی `null` ہو، تو فارم کو دکھائیں اور اس کا اسٹائل 'block' پر سیٹ کریں۔
- نتائج، لوڈنگ، اور `clearBtn` کو چھپائیں اور کسی بھی ایرر ٹیکسٹ کو خالی سٹرنگ پر سیٹ کریں۔
- اگر کوئی key اور region موجود ہو، تو ایک روٹین شروع کریں:
  - API کو کاربن یوزج ڈیٹا حاصل کرنے کے لیے کال کریں۔
  - نتائج کے علاقے کو چھپائیں۔
  - فارم کو چھپائیں۔
  - ری سیٹ بٹن کو دکھائیں۔

آگے بڑھنے سے پہلے، براؤزرز میں دستیاب ایک بہت اہم تصور کے بارے میں سیکھنا مفید ہے: [LocalStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)۔ لوکل اسٹوریج براؤزر میں `key-value` جوڑے کے طور پر سٹرنگز کو محفوظ کرنے کا ایک مفید طریقہ ہے۔ اس قسم کے ویب اسٹوریج کو جاوا اسکرپٹ کے ذریعے براؤزر میں ڈیٹا کو منظم کرنے کے لیے استعمال کیا جا سکتا ہے۔ لوکل اسٹوریج ختم نہیں ہوتی، جبکہ سیشن اسٹوریج، جو ایک اور قسم کا ویب اسٹوریج ہے، براؤزر بند ہونے پر صاف ہو جاتی ہے۔ مختلف قسم کے اسٹوریج کے استعمال کے اپنے فوائد اور نقصانات ہیں۔

> نوٹ - آپ کے براؤزر ایکسٹینشن کا اپنا لوکل اسٹوریج ہوتا ہے؛ مین براؤزر ونڈو ایک الگ انسٹینس ہے اور الگ سے کام کرتی ہے۔

آپ اپنے APIKey کو ایک سٹرنگ ویلیو کے طور پر سیٹ کرتے ہیں، مثال کے طور پر، اور آپ دیکھ سکتے ہیں کہ یہ ایج میں کیسے سیٹ کیا گیا ہے جب آپ کسی ویب پیج کو "انسپیکٹ" کرتے ہیں (آپ براؤزر پر رائٹ کلک کرکے انسپیکٹ کر سکتے ہیں) اور اسٹوریج کو دیکھنے کے لیے ایپلیکیشنز ٹیب پر جاتے ہیں۔

![لوکل اسٹوریج پین](../../../../translated_images/localstorage.472f8147b6a3f8d141d9551c95a2da610ac9a3c6a73d4a1c224081c98bae09d9.ur.png)

✅ ان حالات کے بارے میں سوچیں جہاں آپ کچھ ڈیٹا کو لوکل اسٹوریج میں محفوظ نہیں کرنا چاہیں گے۔ عام طور پر، API Keys کو لوکل اسٹوریج میں رکھنا ایک برا خیال ہے! کیا آپ دیکھ سکتے ہیں کیوں؟ ہمارے کیس میں، چونکہ ہماری ایپ صرف سیکھنے کے لیے ہے اور ایپ اسٹور پر ڈپلائی نہیں کی جائے گی، ہم اس طریقے کو استعمال کریں گے۔

نوٹ کریں کہ آپ لوکل اسٹوریج کو Web API کے ذریعے مینیپولیٹ کرتے ہیں، یا تو `getItem()`، `setItem()`، یا `removeItem()` کا استعمال کرتے ہوئے۔ یہ تمام براؤزرز میں وسیع پیمانے پر سپورٹڈ ہے۔

`displayCarbonUsage()` فنکشن بنانے سے پہلے جو `init()` میں کال کیا جاتا ہے، آئیے ابتدائی فارم سبمیشن کو ہینڈل کرنے کی فعالیت بناتے ہیں۔

### فارم سبمیشن کو ہینڈل کریں

ایک فنکشن بنائیں جسے `handleSubmit` کہا جاتا ہے جو ایک ایونٹ آرگیومنٹ `(e)` قبول کرتا ہے۔ ایونٹ کو پھیلنے سے روکیں (اس کیس میں، ہم براؤزر کو ریفریش ہونے سے روکنا چاہتے ہیں) اور ایک نیا فنکشن `setUpUser` کال کریں، جس میں `apiKey.value` اور `region.value` آرگیومنٹس پاس کریں۔ اس طرح، آپ ان دو ویلیوز کو استعمال کرتے ہیں جو ابتدائی فارم کے ذریعے لائی جاتی ہیں جب متعلقہ فیلڈز کو پاپولیٹ کیا جاتا ہے۔

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ اپنی یادداشت کو تازہ کریں - پچھلے سبق میں آپ نے جو HTML سیٹ کیا تھا اس میں دو ان پٹ فیلڈز ہیں جن کی `values` کو آپ نے فائل کے اوپر سیٹ کیے گئے `const` کے ذریعے کیپچر کیا ہے، اور وہ دونوں `required` ہیں تاکہ براؤزر صارفین کو null ویلیوز ان پٹ کرنے سے روکے۔

### صارف کو سیٹ اپ کریں

`setUpUser` فنکشن کی طرف بڑھتے ہوئے، یہاں آپ لوکل اسٹوریج ویلیوز کو `apiKey` اور `regionName` کے لیے سیٹ کرتے ہیں۔ ایک نیا فنکشن شامل کریں:

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

یہ فنکشن ایک لوڈنگ میسج کو دکھانے کے لیے سیٹ کرتا ہے جب تک کہ API کال نہ ہو۔ اس مقام پر، آپ اس براؤزر ایکسٹینشن کے سب سے اہم فنکشن کو بنانے تک پہنچ چکے ہیں!

### کاربن یوزج دکھائیں

آخر کار، API کو کوئری کرنے کا وقت آ گیا ہے!

آگے بڑھنے سے پہلے، ہمیں APIs پر بات کرنی چاہیے۔ APIs، یا [ایپلیکیشن پروگرامنگ انٹرفیسز](https://www.webopedia.com/TERM/A/API.html)، ایک ویب ڈویلپر کے ٹول باکس کا ایک اہم عنصر ہیں۔ یہ پروگرامز کو ایک دوسرے کے ساتھ انٹرفیس کرنے کے لیے معیاری طریقے فراہم کرتے ہیں۔ مثال کے طور پر، اگر آپ ایک ویب سائٹ بنا رہے ہیں جسے ڈیٹا بیس کو کوئری کرنے کی ضرورت ہے، تو کوئی آپ کے لیے ایک API بنا سکتا ہے۔ اگرچہ APIs کی کئی اقسام ہیں، ان میں سے ایک مقبول ترین [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/) ہے۔

✅ اصطلاح 'REST' کا مطلب 'Representational State Transfer' ہے اور اس میں مختلف طریقے سے کنفیگر کیے گئے URLs کا استعمال شامل ہے تاکہ ڈیٹا حاصل کیا جا سکے۔ ڈویلپرز کے لیے دستیاب مختلف قسم کے APIs پر تھوڑی تحقیق کریں۔ آپ کو کون سا فارمیٹ زیادہ پسند آیا؟

اس فنکشن کے بارے میں نوٹ کرنے کے لیے اہم چیزیں ہیں۔ سب سے پہلے، [`async` کی ورڈ](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) پر غور کریں۔ اپنے فنکشنز کو اس طرح لکھنا کہ وہ غیر متزامن طور پر چلیں، اس کا مطلب ہے کہ وہ کسی ایکشن، جیسے ڈیٹا کی واپسی، کے مکمل ہونے کا انتظار کرتے ہیں اس سے پہلے کہ وہ آگے بڑھیں۔

یہاں `async` کے بارے میں ایک مختصر ویڈیو ہے:

[![پرامسز کو مینیج کرنے کے لیے Async اور Await](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "پرامسز کو مینیج کرنے کے لیے Async اور Await")

> 🎥 اوپر دی گئی تصویر پر کلک کریں `async/await` کے بارے میں ویڈیو دیکھنے کے لیے۔

C02Signal API کو کوئری کرنے کے لیے ایک نیا فنکشن بنائیں:

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

یہ ایک بڑا فنکشن ہے۔ یہاں کیا ہو رہا ہے؟

- بہترین پریکٹسز کی پیروی کرتے ہوئے، آپ اس فنکشن کو غیر متزامن بنانے کے لیے `async` کی ورڈ استعمال کرتے ہیں۔ یہ فنکشن ایک `try/catch` بلاک پر مشتمل ہے کیونکہ یہ API سے ڈیٹا واپس آنے پر ایک پرامس واپس کرے گا۔ چونکہ آپ کے پاس اس رفتار پر کنٹرول نہیں ہے جس پر API جواب دے گا (یہ بالکل بھی جواب نہیں دے سکتا!)، آپ کو اس غیر یقینی صورتحال کو غیر متزامن طور پر کال کرکے ہینڈل کرنے کی ضرورت ہے۔
- آپ اپنے ریجن کا ڈیٹا حاصل کرنے کے لیے co2signal API کو کوئری کر رہے ہیں، اپنے API Key کا استعمال کرتے ہوئے۔ اس key کو استعمال کرنے کے لیے، آپ کو اپنے ہیڈر پیرامیٹرز میں ایک قسم کی تصدیق کا استعمال کرنا ہوگا۔
- ایک بار جب API جواب دیتا ہے، تو آپ اس کے رسپانس ڈیٹا کے مختلف عناصر کو اپنی اسکرین کے ان حصوں میں تفویض کرتے ہیں جو آپ نے اس ڈیٹا کو دکھانے کے لیے سیٹ کیے ہیں۔
- اگر کوئی ایرر ہو، یا کوئی نتیجہ نہ ہو، تو آپ ایک ایرر میسج دکھاتے ہیں۔

✅ غیر متزامن پروگرامنگ پیٹرنز کا استعمال آپ کے ٹول باکس میں ایک اور بہت مفید ٹول ہے۔ [مختلف طریقوں](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) کے بارے میں پڑھیں جن سے آپ اس قسم کے کوڈ کو کنفیگر کر سکتے ہیں۔

مبارک ہو! اگر آپ اپنے ایکسٹینشن کو بلڈ کرتے ہیں (`npm run build`) اور اسے اپنے ایکسٹینشن پین میں ریفریش کرتے ہیں، تو آپ کے پاس ایک کام کرنے والا ایکسٹینشن ہے! واحد چیز جو کام نہیں کر رہی وہ آئیکن ہے، اور آپ اسے اگلے سبق میں ٹھیک کریں گے۔

---

## 🚀 چیلنج

ہم نے ان اسباق میں اب تک کئی قسم کے APIs پر بات کی ہے۔ ایک ویب API کا انتخاب کریں اور گہرائی میں تحقیق کریں کہ یہ کیا پیش کرتا ہے۔ مثال کے طور پر، براؤزرز میں دستیاب APIs جیسے [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API) کو دیکھیں۔ آپ کی رائے میں ایک بہترین API کیا بناتا ہے؟

## لیکچر کے بعد کا کوئز

[لیکچر کے بعد کا کوئز](https://ff-quizzes.netlify.app/web/quiz/26)

## جائزہ اور خود مطالعہ

آپ نے اس سبق میں لوکل اسٹوریج اور APIs کے بارے میں سیکھا، جو پیشہ ور ویب ڈویلپر کے لیے دونوں بہت مفید ہیں۔ کیا آپ سوچ سکتے ہیں کہ یہ دونوں چیزیں ایک ساتھ کیسے کام کرتی ہیں؟ اس بارے میں سوچیں کہ آپ ایک ایسی ویب سائٹ کو کیسے آرکیٹیکٹ کریں گے جو ایک API کے ذریعے استعمال ہونے والی اشیاء کو محفوظ کرے۔

## اسائنمنٹ

[ایک API اپنائیں](assignment.md)

---

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا غیر درستیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔