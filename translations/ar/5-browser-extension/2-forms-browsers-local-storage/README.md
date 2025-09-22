<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a7587943d38d095de8613e1b508609f5",
  "translation_date": "2025-08-28T15:00:44+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "ar"
}
-->
# مشروع إضافة المتصفح الجزء الثاني: استدعاء API واستخدام التخزين المحلي

## اختبار ما قبل المحاضرة

[اختبار ما قبل المحاضرة](https://ff-quizzes.netlify.app/web/quiz/25)

### المقدمة

في هذا الدرس، ستقوم باستدعاء API من خلال إرسال نموذج إضافة المتصفح الخاص بك وعرض النتائج في الإضافة. بالإضافة إلى ذلك، ستتعلم كيفية تخزين البيانات في التخزين المحلي للمتصفح لاستخدامها لاحقًا.

✅ اتبع الأجزاء المرقمة في الملفات المناسبة لمعرفة أين تضع الكود الخاص بك.

### إعداد العناصر للتعامل معها في الإضافة:

بحلول هذه المرحلة، قمت ببناء ملف HTML للنموذج وعناصر النتائج `<div>` لإضافة المتصفح الخاصة بك. من الآن فصاعدًا، ستحتاج إلى العمل في ملف `/src/index.js` وبناء الإضافة خطوة بخطوة. ارجع إلى [الدرس السابق](../1-about-browsers/README.md) للحصول على إعداد المشروع وعملية البناء.

أثناء العمل في ملف `index.js`، ابدأ بإنشاء بعض المتغيرات `const` للاحتفاظ بالقيم المرتبطة بالحقول المختلفة:

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

جميع هذه الحقول يتم الإشارة إليها باستخدام css class، كما قمت بإعدادها في ملف HTML في الدرس السابق.

### إضافة المستمعات

بعد ذلك، أضف مستمعات الأحداث للنموذج وزر الإعادة الذي يعيد تعيين النموذج، بحيث إذا قام المستخدم بإرسال النموذج أو النقر على زر الإعادة، يحدث شيء ما. أضف أيضًا استدعاء لتهيئة التطبيق في نهاية الملف:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ لاحظ الاختصار المستخدم للاستماع إلى حدث الإرسال أو النقر، وكيف يتم تمرير الحدث إلى دوال `handleSubmit` أو `reset`. هل يمكنك كتابة المكافئ لهذا الاختصار بصيغة أطول؟ أيهما تفضل؟

### بناء دالتي `init()` و `reset()`:

الآن ستقوم ببناء الدالة التي تهيئ الإضافة، والتي تسمى `init()`:

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

في هذه الدالة، هناك منطق مثير للاهتمام. عند قراءته، هل يمكنك معرفة ما يحدث؟

- يتم إعداد متغيرين `const` للتحقق مما إذا كان المستخدم قد قام بتخزين APIKey ورمز المنطقة في التخزين المحلي.
- إذا كانت أي من هذه القيم تساوي null، يتم عرض النموذج عن طريق تغيير نمط العرض إلى 'block'.
- يتم إخفاء منطقة النتائج، والتحميل، وزر الإعادة، ويتم تعيين أي نص خطأ إلى سلسلة فارغة.
- إذا كان هناك مفتاح ورمز منطقة، يتم بدء روتين لـ:
  - استدعاء API للحصول على بيانات استخدام الكربون.
  - إخفاء منطقة النتائج.
  - إخفاء النموذج.
  - عرض زر الإعادة.

قبل المتابعة، من المفيد التعرف على مفهوم مهم جدًا متاح في المتصفحات: [التخزين المحلي](https://developer.mozilla.org/docs/Web/API/Window/localStorage). التخزين المحلي هو طريقة مفيدة لتخزين النصوص في المتصفح كزوج `key-value`. يمكن التلاعب بهذا النوع من التخزين باستخدام JavaScript لإدارة البيانات في المتصفح. التخزين المحلي لا ينتهي صلاحيته، بينما يتم مسح التخزين المؤقت (SessionStorage) عند إغلاق المتصفح. لكل نوع من التخزين مزايا وعيوب.

> ملاحظة - تحتوي إضافة المتصفح الخاصة بك على تخزين محلي خاص بها؛ نافذة المتصفح الرئيسية هي مثيل مختلف وتعمل بشكل منفصل.

يمكنك تعيين قيمة نصية لـ APIKey، على سبيل المثال، ويمكنك رؤية أنه تم تعيينها في Edge عن طريق "فحص" صفحة ويب (يمكنك النقر بزر الماوس الأيمن على المتصفح للفحص) والانتقال إلى علامة تبويب التطبيقات لرؤية التخزين.

![لوحة التخزين المحلي](../../../../translated_images/localstorage.472f8147b6a3f8d141d9551c95a2da610ac9a3c6a73d4a1c224081c98bae09d9.ar.png)

✅ فكر في المواقف التي لا ترغب فيها بتخزين بعض البيانات في التخزين المحلي. بشكل عام، وضع مفاتيح API في التخزين المحلي فكرة سيئة! هل يمكنك معرفة السبب؟ في حالتنا، نظرًا لأن تطبيقنا مخصص للتعلم فقط ولن يتم نشره في متجر التطبيقات، سنستخدم هذه الطريقة.

لاحظ أنك تستخدم Web API للتعامل مع التخزين المحلي، إما باستخدام `getItem()`، أو `setItem()`، أو `removeItem()`. يتم دعمها على نطاق واسع عبر المتصفحات.

قبل بناء دالة `displayCarbonUsage()` التي يتم استدعاؤها في `init()`، دعنا نبني الوظيفة التي تتعامل مع إرسال النموذج الأولي.

### التعامل مع إرسال النموذج

قم بإنشاء دالة تسمى `handleSubmit` تقبل وسيط حدث `(e)`. أوقف انتشار الحدث (في هذه الحالة، نريد إيقاف المتصفح من التحديث) واستدعِ دالة جديدة، `setUpUser`، مع تمرير الوسيطين `apiKey.value` و `region.value`. بهذه الطريقة، تستخدم القيمتين اللتين يتم إدخالهما عبر النموذج الأولي عند تعبئة الحقول المناسبة.

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ قم بتحديث ذاكرتك - ملف HTML الذي قمت بإعداده في الدرس السابق يحتوي على حقلين إدخال يتم التقاط قيمهما عبر `const` التي قمت بإعدادها في أعلى الملف، وكلاهما `required` لذا يمنع المتصفح المستخدمين من إدخال قيم فارغة.

### إعداد المستخدم

بالانتقال إلى دالة `setUpUser`، هنا يتم تعيين قيم التخزين المحلي لـ apiKey و regionName. أضف دالة جديدة:

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

تقوم هذه الدالة بعرض رسالة تحميل أثناء استدعاء API. في هذه المرحلة، وصلت إلى إنشاء أهم دالة في هذه الإضافة!

### عرض استخدام الكربون

أخيرًا، حان الوقت لاستدعاء API!

قبل المتابعة، يجب أن نناقش APIs. APIs، أو [واجهات برمجة التطبيقات](https://www.webopedia.com/TERM/A/API.html)، هي عنصر أساسي في أدوات مطوري الويب. توفر طرقًا قياسية لتفاعل البرامج مع بعضها البعض. على سبيل المثال، إذا كنت تبني موقع ويب يحتاج إلى استعلام قاعدة بيانات، قد يكون هناك API تم إنشاؤه لتستخدمه. بينما هناك أنواع عديدة من APIs، أحد الأنواع الأكثر شيوعًا هو [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/).

✅ يشير مصطلح 'REST' إلى 'نقل الحالة التمثيلية' ويتميز باستخدام عناوين URL مهيأة بطرق مختلفة لجلب البيانات. قم ببعض البحث حول الأنواع المختلفة من APIs المتاحة للمطورين. أي نوع يثير اهتمامك؟

هناك أشياء مهمة يجب ملاحظتها حول هذه الدالة. أولاً، لاحظ الكلمة المفتاحية [`async`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function). كتابة الدوال بحيث تعمل بشكل غير متزامن يعني أنها تنتظر إكمال إجراء معين، مثل استرجاع البيانات، قبل المتابعة.

إليك فيديو سريع حول `async`:

[![Async و Await لإدارة الوعود](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "Async و Await لإدارة الوعود")

> 🎥 انقر على الصورة أعلاه لمشاهدة فيديو حول async/await.

قم بإنشاء دالة جديدة لاستعلام API الخاص بـ C02Signal:

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

هذه دالة كبيرة. ما الذي يحدث هنا؟

- باتباع أفضل الممارسات، تستخدم الكلمة المفتاحية `async` لجعل هذه الدالة تعمل بشكل غير متزامن. تحتوي الدالة على كتلة `try/catch` لأنها ستعيد وعدًا عند استرجاع البيانات من API. نظرًا لأنك لا تتحكم في سرعة استجابة API (قد لا يستجيب على الإطلاق!)، تحتاج إلى التعامل مع هذا الأمر عن طريق استدعائه بشكل غير متزامن.
- تقوم باستعلام API الخاص بـ co2signal للحصول على بيانات منطقتك، باستخدام مفتاح API الخاص بك. لاستخدام هذا المفتاح، تحتاج إلى استخدام نوع من المصادقة في معلمات الرأس.
- بمجرد استجابة API، تقوم بتعيين عناصر مختلفة من بيانات الاستجابة إلى الأجزاء التي قمت بإعدادها لعرض هذه البيانات.
- إذا كان هناك خطأ، أو إذا لم تكن هناك نتيجة، تعرض رسالة خطأ.

✅ استخدام أنماط البرمجة غير المتزامنة هو أداة مفيدة أخرى في صندوق أدواتك. اقرأ [عن الطرق المختلفة](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) التي يمكنك من خلالها تكوين هذا النوع من الكود.

تهانينا! إذا قمت ببناء الإضافة الخاصة بك (`npm run build`) وقمت بتحديثها في لوحة الإضافات، لديك الآن إضافة تعمل! الشيء الوحيد الذي لا يعمل هو الأيقونة، وستقوم بإصلاح ذلك في الدرس التالي.

---

## 🚀 التحدي

لقد ناقشنا عدة أنواع من APIs حتى الآن في هذه الدروس. اختر API على الويب وابحث بعمق عما يقدمه. على سبيل المثال، ألقِ نظرة على APIs المتاحة داخل المتصفحات مثل [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API). ما الذي يجعل API رائعًا في رأيك؟

## اختبار ما بعد المحاضرة

[اختبار ما بعد المحاضرة](https://ff-quizzes.netlify.app/web/quiz/26)

## المراجعة والدراسة الذاتية

تعلمت عن التخزين المحلي وAPIs في هذا الدرس، وكلاهما مفيد جدًا لمطور الويب المحترف. هل يمكنك التفكير في كيفية عمل هذين الشيئين معًا؟ فكر في كيفية تصميم موقع ويب يقوم بتخزين العناصر لاستخدامها بواسطة API.

## الواجب

[تبنَّ API](assignment.md)

---

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الرسمي. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.