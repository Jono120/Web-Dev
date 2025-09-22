<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "89f7f9f800ce7c9f149e98baaae8491a",
  "translation_date": "2025-08-28T15:06:17+00:00",
  "source_file": "3-terrarium/1-intro-to-html/README.md",
  "language_code": "ar"
}
-->
# مشروع التيراريوم الجزء الأول: مقدمة إلى HTML

![مقدمة إلى HTML](../../../../translated_images/webdev101-html.4389c2067af68e98280c1bde52b6c6269f399eaae3659b7c846018d8a7b0bbd9.ar.png)
> رسم توضيحي بواسطة [Tomomi Imura](https://twitter.com/girlie_mac)

## اختبار ما قبل المحاضرة

[اختبار ما قبل المحاضرة](https://ff-quizzes.netlify.app/web/quiz/15)

> شاهد الفيديو

> 
> [![فيديو أساسيات Git و GitHub](https://img.youtube.com/vi/1TvxJKBzhyQ/0.jpg)](https://www.youtube.com/watch?v=1TvxJKBzhyQ)

### المقدمة

HTML، أو لغة ترميز النص التشعبي، هي "الهيكل العظمي" للويب. إذا كانت CSS "تُزين" HTML و JavaScript تُضفي الحياة عليه، فإن HTML هو جسم تطبيق الويب الخاص بك. حتى أن صياغة HTML تعكس هذه الفكرة، حيث تتضمن علامات مثل "head"، "body"، و "footer".

في هذه الدرس، سنستخدم HTML لتصميم "الهيكل العظمي" لواجهة التيراريوم الافتراضي الخاص بنا. ستتضمن عنوانًا وثلاثة أعمدة: عمود على اليمين وآخر على اليسار حيث تعيش النباتات القابلة للسحب، ومنطقة مركزية ستكون التيراريوم الزجاجي. بحلول نهاية هذا الدرس، ستتمكن من رؤية النباتات في الأعمدة، لكن الواجهة ستبدو غريبة بعض الشيء؛ لا تقلق، في القسم التالي ستضيف أنماط CSS لتحسين مظهر الواجهة.

### المهمة

على جهاز الكمبيوتر الخاص بك، قم بإنشاء مجلد يسمى "terrarium" وداخله ملف يسمى "index.html". يمكنك القيام بذلك في Visual Studio Code بعد إنشاء مجلد التيراريوم الخاص بك عن طريق فتح نافذة جديدة في VS Code، والنقر على "فتح مجلد"، والانتقال إلى المجلد الجديد الخاص بك. انقر على زر "ملف" الصغير في لوحة المستكشف وقم بإنشاء الملف الجديد:

![المستكشف في VS Code](../../../../translated_images/vs-code-index.e2986cf919471eb984a0afef231380c8b132b000635105f2397bd2754d1b689c.ar.png)

أو

استخدم هذه الأوامر في git bash:
* `mkdir terrarium`
* `cd terrarium`
* `touch index.html`
* `code index.html` أو `nano index.html`

> ملفات index.html تشير إلى المتصفح بأنها الملف الافتراضي في المجلد؛ قد يتم بناء عناوين URL مثل `https://anysite.com/test` باستخدام هيكل مجلد يتضمن مجلدًا يسمى `test` مع ملف `index.html` بداخله؛ لا يجب أن يظهر `index.html` في عنوان URL.

---

## نوع المستند وعلامات html

السطر الأول في ملف HTML هو نوع المستند الخاص به. من المدهش قليلاً أنك بحاجة إلى وضع هذا السطر في أعلى الملف، لكنه يخبر المتصفحات القديمة بأن الصفحة يجب أن تُعرض في الوضع القياسي، وفقًا لمواصفات HTML الحالية.

> نصيحة: في VS Code، يمكنك تمرير المؤشر فوق علامة للحصول على معلومات حول استخدامها من أدلة مرجعية MDN.

السطر الثاني يجب أن يكون علامة الفتح `<html>`، متبوعة الآن بعلامة الإغلاق الخاصة بها `</html>`. هذه العلامات هي العناصر الجذرية لواجهتك.

### المهمة

أضف هذه الأسطر في أعلى ملف `index.html` الخاص بك:

```HTML
<!DOCTYPE html>
<html></html>
```

✅ هناك أوضاع مختلفة يمكن تحديدها عن طريق إعداد نوع المستند باستخدام سلسلة استعلام: [وضع Quirks ووضع Standards](https://developer.mozilla.org/docs/Web/HTML/Quirks_Mode_and_Standards_Mode). هذه الأوضاع كانت تدعم المتصفحات القديمة جدًا التي لا تُستخدم عادةً في الوقت الحاضر (مثل Netscape Navigator 4 و Internet Explorer 5). يمكنك الالتزام بإعلان نوع المستند القياسي.

---

## 'الرأس' في المستند

منطقة 'الرأس' في مستند HTML تتضمن معلومات أساسية عن صفحة الويب الخاصة بك، تُعرف أيضًا باسم [البيانات الوصفية](https://developer.mozilla.org/docs/Web/HTML/Element/meta). في حالتنا، نخبر خادم الويب الذي سيتم إرسال هذه الصفحة إليه ليتم عرضها، هذه الأشياء الأربعة:

-   عنوان الصفحة
-   البيانات الوصفية للصفحة بما في ذلك:
    -   'مجموعة الأحرف'، التي تخبر عن نوع ترميز الأحرف المستخدم في الصفحة
    -   معلومات المتصفح، بما في ذلك `x-ua-compatible` التي تشير إلى دعم متصفح IE=edge
    -   معلومات حول كيفية تصرف نافذة العرض عند تحميلها. إعداد نافذة العرض لتكون بمقياس أولي 1 يتحكم في مستوى التكبير عند تحميل الصفحة لأول مرة.

### المهمة

أضف كتلة 'الرأس' إلى مستندك بين علامات الفتح والإغلاق `<html>`.

```html
<head>
	<title>Welcome to my Virtual Terrarium</title>
	<meta charset="utf-8" />
	<meta http-equiv="X-UA-Compatible" content="IE=edge" />
	<meta name="viewport" content="width=device-width, initial-scale=1" />
</head>
```

✅ ماذا سيحدث إذا قمت بإعداد علامة البيانات الوصفية لنافذة العرض مثل هذا: `<meta name="viewport" content="width=600">`؟ اقرأ المزيد عن [نافذة العرض](https://developer.mozilla.org/docs/Web/HTML/Viewport_meta_tag).

---

## 'الجسم' في المستند

### علامات HTML

في HTML، تضيف علامات إلى ملف .html الخاص بك لإنشاء عناصر صفحة ويب. عادةً ما تحتوي كل علامة على علامة فتح وعلامة إغلاق، مثل هذا: `<p>hello</p>` للإشارة إلى فقرة. قم بإنشاء جسم واجهتك عن طريق إضافة مجموعة من علامات `<body>` داخل زوج علامات `<html>`؛ الآن يبدو الترميز الخاص بك كالتالي:

### المهمة

```html
<!DOCTYPE html>
<html>
	<head>
		<title>Welcome to my Virtual Terrarium</title>
		<meta charset="utf-8" />
		<meta http-equiv="X-UA-Compatible" content="IE=edge" />
		<meta name="viewport" content="width=device-width, initial-scale=1" />
	</head>
	<body></body>
</html>
```

الآن، يمكنك البدء في بناء صفحتك. عادةً، تستخدم علامات `<div>` لإنشاء العناصر المنفصلة في الصفحة. سنقوم بإنشاء سلسلة من عناصر `<div>` التي ستحتوي على صور.

### الصور

علامة HTML التي لا تحتاج إلى علامة إغلاق هي علامة `<img>`، لأنها تحتوي على عنصر `src` الذي يحتوي على جميع المعلومات التي تحتاجها الصفحة لعرض العنصر.

قم بإنشاء مجلد في تطبيقك يسمى `images` وأضف فيه جميع الصور الموجودة في [مجلد كود المصدر](../../../../3-terrarium/solution/images)؛ (هناك 14 صورة للنباتات).

### المهمة

أضف تلك الصور للنباتات إلى عمودين بين علامات `<body></body>`:

```html
<div id="page">
	<div id="left-container" class="container">
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant1" src="./images/plant1.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant2" src="./images/plant2.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant3" src="./images/plant3.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant4" src="./images/plant4.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant5" src="./images/plant5.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant6" src="./images/plant6.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant7" src="./images/plant7.png" />
		</div>
	</div>
	<div id="right-container" class="container">
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant8" src="./images/plant8.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant9" src="./images/plant9.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant10" src="./images/plant10.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant11" src="./images/plant11.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant12" src="./images/plant12.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant13" src="./images/plant13.png" />
		</div>
		<div class="plant-holder">
			<img class="plant" alt="plant" id="plant14" src="./images/plant14.png" />
		</div>
	</div>
</div>
```

> ملاحظة: الفرق بين Spans و Divs. تعتبر Divs عناصر 'كتلة'، بينما تعتبر Spans 'خطية'. ماذا سيحدث إذا قمت بتحويل هذه divs إلى spans؟

مع هذا الترميز، تظهر النباتات الآن على الشاشة. يبدو الأمر سيئًا، لأنهم لم يتم تنسيقهم بعد باستخدام CSS، وسنقوم بذلك في الدرس التالي.

كل صورة تحتوي على نص بديل يظهر حتى إذا لم تتمكن من رؤية الصورة أو عرضها. هذا عنصر مهم يجب تضمينه لتحسين الوصول. تعرف على المزيد حول الوصول في الدروس المستقبلية؛ في الوقت الحالي، تذكر أن خاصية alt توفر معلومات بديلة للصورة إذا لم يتمكن المستخدم لسبب ما من عرضها (بسبب اتصال بطيء، خطأ في خاصية src، أو إذا كان المستخدم يستخدم قارئ الشاشة).

✅ هل لاحظت أن كل صورة تحتوي على نفس النص البديل؟ هل هذا ممارسة جيدة؟ لماذا أو لماذا لا؟ هل يمكنك تحسين هذا الكود؟

---

## الترميز الدلالي

بشكل عام، من الأفضل استخدام 'الدلالات' ذات المعنى عند كتابة HTML. ماذا يعني ذلك؟ يعني أنك تستخدم علامات HTML لتمثيل نوع البيانات أو التفاعل الذي تم تصميمها من أجله. على سبيل المثال، النص الرئيسي في الصفحة يجب أن يستخدم علامة `<h1>`.

أضف السطر التالي مباشرةً أسفل علامة الفتح `<body>`:

```html
<h1>My Terrarium</h1>
```

استخدام الترميز الدلالي مثل وجود العناوين كـ `<h1>` والقوائم غير المرتبة كـ `<ul>` يساعد قارئات الشاشة على التنقل عبر الصفحة. بشكل عام، يجب كتابة الأزرار كـ `<button>` والقوائم كـ `<li>`. بينما من الممكن استخدام عناصر `<span>` ذات أنماط خاصة مع معالجات النقر لتقليد الأزرار، من الأفضل للمستخدمين ذوي الإعاقة استخدام تقنيات لتحديد مكان الزر في الصفحة والتفاعل معه، إذا ظهر العنصر كزر. لهذا السبب، حاول استخدام الترميز الدلالي قدر الإمكان.

✅ ألقِ نظرة على قارئ الشاشة وكيف يتفاعل مع صفحة ويب [هنا](https://www.youtube.com/watch?v=OUDV1gqs9GA). هل يمكنك رؤية لماذا قد يُحبط المستخدم بسبب الترميز غير الدلالي؟

## التيراريوم

الجزء الأخير من هذه الواجهة يتضمن إنشاء ترميز سيتم تنسيقه لإنشاء تيراريوم.

### المهمة:

أضف هذا الترميز فوق علامة `</div>` الأخيرة:

```html
<div id="terrarium">
	<div class="jar-top"></div>
	<div class="jar-walls">
		<div class="jar-glossy-long"></div>
		<div class="jar-glossy-short"></div>
	</div>
	<div class="dirt"></div>
	<div class="jar-bottom"></div>
</div>
```

✅ على الرغم من أنك أضفت هذا الترميز إلى الشاشة، إلا أنك لا ترى أي شيء يظهر. لماذا؟

---

## 🚀التحدي

هناك بعض العلامات 'القديمة' في HTML التي لا تزال ممتعة للتجربة، على الرغم من أنه لا يجب استخدام العلامات المهملة مثل [هذه العلامات](https://developer.mozilla.org/docs/Web/HTML/Element#Obsolete_and_deprecated_elements) في الترميز الخاص بك. مع ذلك، هل يمكنك استخدام العلامة القديمة `<marquee>` لجعل عنوان h1 يتحرك أفقيًا؟ (إذا فعلت ذلك، لا تنسَ إزالتها بعد ذلك).

## اختبار ما بعد المحاضرة

[اختبار ما بعد المحاضرة](https://ff-quizzes.netlify.app/web/quiz/16)

## المراجعة والدراسة الذاتية

HTML هو نظام بناء 'مجرب وصحيح' ساعد في بناء الويب ليصبح ما هو عليه اليوم. تعرف قليلاً على تاريخه من خلال دراسة بعض العلامات القديمة والجديدة. هل يمكنك معرفة لماذا تم إهمال بعض العلامات وإضافة أخرى؟ ما العلامات التي قد يتم تقديمها في المستقبل؟

تعرف على المزيد حول بناء المواقع للويب والأجهزة المحمولة في [Microsoft Learn](https://docs.microsoft.com/learn/modules/build-simple-website/?WT.mc_id=academic-77807-sagibbon).

## الواجب

[تمرن على HTML: قم ببناء نموذج مدونة](assignment.md)

---

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الموثوق. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.