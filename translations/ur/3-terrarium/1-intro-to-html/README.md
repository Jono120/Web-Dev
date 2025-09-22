<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "89f7f9f800ce7c9f149e98baaae8491a",
  "translation_date": "2025-08-28T15:28:10+00:00",
  "source_file": "3-terrarium/1-intro-to-html/README.md",
  "language_code": "ur"
}
-->
# ٹیرآریم پروجیکٹ حصہ 1: HTML کا تعارف

![HTML کا تعارف](../../../../translated_images/webdev101-html.4389c2067af68e98280c1bde52b6c6269f399eaae3659b7c846018d8a7b0bbd9.ur.png)
> اسکیچ نوٹ از [Tomomi Imura](https://twitter.com/girlie_mac)

## لیکچر سے پہلے کا کوئز

[لیکچر سے پہلے کا کوئز](https://ff-quizzes.netlify.app/web/quiz/15)

> ویڈیو دیکھیں

> 
> [![Git اور GitHub کی بنیادی ویڈیو](https://img.youtube.com/vi/1TvxJKBzhyQ/0.jpg)](https://www.youtube.com/watch?v=1TvxJKBzhyQ)

### تعارف

HTML، یا ہائپر ٹیکسٹ مارک اپ لینگویج، ویب کا 'ڈھانچہ' ہے۔ اگر CSS آپ کے HTML کو 'سجانے' کا کام کرتا ہے اور JavaScript اسے زندگی بخشتا ہے، تو HTML آپ کی ویب ایپلیکیشن کا جسم ہے۔ HTML کی ساخت بھی اس خیال کی عکاسی کرتی ہے، کیونکہ اس میں "head"، "body"، اور "footer" ٹیگز شامل ہیں۔

اس سبق میں، ہم HTML کا استعمال کرتے ہوئے اپنے ورچوئل ٹیرآریم کے انٹرفیس کا 'ڈھانچہ' بنائیں گے۔ اس میں ایک عنوان اور تین کالم ہوں گے: دائیں اور بائیں کالم جہاں ڈریگ ایبل پودے ہوں گے، اور درمیان کا علاقہ جو اصل میں شیشے جیسا ٹیرآریم ہوگا۔ اس سبق کے اختتام تک، آپ کالمز میں پودے دیکھ سکیں گے، لیکن انٹرفیس تھوڑا عجیب لگے گا؛ فکر نہ کریں، اگلے حصے میں آپ CSS اسٹائلز شامل کریں گے تاکہ انٹرفیس بہتر نظر آئے۔

### کام

اپنے کمپیوٹر پر ایک فولڈر بنائیں جس کا نام 'terrarium' ہو اور اس کے اندر ایک فائل بنائیں جس کا نام 'index.html' ہو۔ آپ یہ کام Visual Studio Code میں اپنے terrarium فولڈر کو کھول کر، ایک نیا VS Code ونڈو کھول کر، 'open folder' پر کلک کر کے اور اپنے نئے فولڈر کو منتخب کر کے کر سکتے ہیں۔ Explorer پین میں چھوٹے 'file' بٹن پر کلک کریں اور نئی فائل بنائیں:

![VS Code میں ایکسپلورر](../../../../translated_images/vs-code-index.e2986cf919471eb984a0afef231380c8b132b000635105f2397bd2754d1b689c.ur.png)

یا

اپنے git bash میں یہ کمانڈز استعمال کریں:
* `mkdir terrarium`
* `cd terrarium`
* `touch index.html`
* `code index.html` یا `nano index.html`

> index.html فائلز براؤزر کو یہ بتاتی ہیں کہ یہ فولڈر کی ڈیفالٹ فائل ہے؛ URLs جیسے `https://anysite.com/test` ممکنہ طور پر ایک فولڈر اسٹرکچر استعمال کر کے بنائے گئے ہیں جس میں `test` نامی فولڈر اور اس کے اندر `index.html` شامل ہو؛ `index.html` کو URL میں دکھانے کی ضرورت نہیں ہوتی۔

---

## DocType اور html ٹیگز

HTML فائل کی پہلی لائن اس کا DocType ہوتی ہے۔ یہ تھوڑا حیران کن ہو سکتا ہے کہ آپ کو یہ لائن فائل کے بالکل اوپر رکھنی ہوتی ہے، لیکن یہ پرانے براؤزرز کو بتاتی ہے کہ صفحہ کو موجودہ HTML اسپیسفکیشن کے مطابق اسٹینڈرڈ موڈ میں رینڈر کرنا ہے۔

> ٹپ: VS Code میں، آپ کسی ٹیگ پر ہوور کر کے MDN ریفرنس گائیڈز سے اس کے استعمال کے بارے میں معلومات حاصل کر سکتے ہیں۔

دوسری لائن `<html>` ٹیگ کا اوپننگ ٹیگ ہونا چاہیے، جس کے فوراً بعد اس کا کلوزنگ ٹیگ `</html>` ہو۔ یہ ٹیگز آپ کے انٹرفیس کے روٹ عناصر ہیں۔

### کام

اپنی `index.html` فائل کے اوپر یہ لائنز شامل کریں:

```HTML
<!DOCTYPE html>
<html></html>
```

✅ DocType کو ایک کوئری اسٹرنگ کے ساتھ سیٹ کر کے مختلف موڈز طے کیے جا سکتے ہیں: [Quirks Mode اور Standards Mode](https://developer.mozilla.org/docs/Web/HTML/Quirks_Mode_and_Standards_Mode)۔ یہ موڈز بہت پرانے براؤزرز (جیسے Netscape Navigator 4 اور Internet Explorer 5) کو سپورٹ کرنے کے لیے استعمال ہوتے تھے جو آج کل عام طور پر استعمال نہیں ہوتے۔ آپ اسٹینڈرڈ DocType ڈیکلریشن پر قائم رہ سکتے ہیں۔

---

## دستاویز کا 'head'

HTML دستاویز کے 'head' حصے میں آپ کے ویب صفحے کے بارے میں اہم معلومات شامل ہوتی ہیں، جنہیں [میٹا ڈیٹا](https://developer.mozilla.org/docs/Web/HTML/Element/meta) کہا جاتا ہے۔ ہمارے کیس میں، ہم ویب سرور کو یہ چار چیزیں بتاتے ہیں:

- صفحے کا عنوان
- صفحے کا میٹا ڈیٹا، جس میں شامل ہیں:
    - 'کریکٹر سیٹ'، جو بتاتا ہے کہ صفحے میں کون سا کریکٹر انکوڈنگ استعمال ہو رہا ہے
    - براؤزر کی معلومات، بشمول `x-ua-compatible` جو ظاہر کرتا ہے کہ IE=edge براؤزر سپورٹڈ ہے
    - معلومات کہ جب صفحہ لوڈ ہو تو ویوپورٹ کو کیسے برتاؤ کرنا چاہیے۔ ویوپورٹ کو ابتدائی اسکیل 1 پر سیٹ کرنا کنٹرول کرتا ہے کہ صفحہ پہلی بار لوڈ ہونے پر زوم لیول کیا ہوگا۔

### کام

اپنی دستاویز میں `<html>` ٹیگز کے درمیان ایک 'head' بلاک شامل کریں۔

```html
<head>
	<title>Welcome to my Virtual Terrarium</title>
	<meta charset="utf-8" />
	<meta http-equiv="X-UA-Compatible" content="IE=edge" />
	<meta name="viewport" content="width=device-width, initial-scale=1" />
</head>
```

✅ اگر آپ ویوپورٹ میٹا ٹیگ کو اس طرح سیٹ کریں: `<meta name="viewport" content="width=600">` تو کیا ہوگا؟ ویوپورٹ کے بارے میں مزید پڑھیں: [viewport](https://developer.mozilla.org/docs/Web/HTML/Viewport_meta_tag)۔

---

## دستاویز کا `body`

### HTML ٹیگز

HTML میں، آپ اپنی .html فائل میں ٹیگز شامل کرتے ہیں تاکہ ویب صفحے کے عناصر بن سکیں۔ ہر ٹیگ کے عام طور پر ایک اوپننگ اور کلوزنگ ٹیگ ہوتے ہیں، جیسے: `<p>hello</p>` جو ایک پیراگراف کو ظاہر کرتا ہے۔ اپنے انٹرفیس کا باڈی بنانے کے لیے `<body>` ٹیگز کا ایک سیٹ `<html>` ٹیگ کے جوڑے کے اندر شامل کریں؛ آپ کا مارک اپ اب اس طرح نظر آنا چاہیے:

### کام

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

اب، آپ اپنے صفحے کو بنانا شروع کر سکتے ہیں۔ عام طور پر، آپ صفحے میں الگ الگ عناصر بنانے کے لیے `<div>` ٹیگز استعمال کرتے ہیں۔ ہم ایک سیریز کے `<div>` عناصر بنائیں گے جو تصاویر پر مشتمل ہوں گے۔

### تصاویر

ایک HTML ٹیگ جو کلوزنگ ٹیگ کی ضرورت نہیں رکھتا وہ `<img>` ٹیگ ہے، کیونکہ اس میں ایک `src` عنصر ہوتا ہے جو صفحے کو آئٹم کو رینڈر کرنے کے لیے تمام معلومات فراہم کرتا ہے۔

اپنی ایپ میں ایک فولڈر بنائیں جس کا نام `images` ہو اور اس میں [source code folder](../../../../3-terrarium/solution/images) کی تمام تصاویر شامل کریں؛ (یہاں 14 پودوں کی تصاویر ہیں)۔

### کام

ان پودوں کی تصاویر کو `<body></body>` ٹیگز کے درمیان دو کالمز میں شامل کریں:

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

> نوٹ: اسپینز بمقابلہ ڈیو۔ ڈیو کو 'بلاک' عناصر سمجھا جاتا ہے، اور اسپینز کو 'ان لائن'۔ اگر آپ ان ڈیو کو اسپین میں تبدیل کریں تو کیا ہوگا؟

اس مارک اپ کے ساتھ، پودے اب اسکرین پر نظر آتے ہیں۔ یہ کافی برا لگتا ہے، کیونکہ ابھی تک انہیں CSS کے ذریعے اسٹائل نہیں کیا گیا، اور ہم یہ اگلے سبق میں کریں گے۔

ہر تصویر میں ایک alt ٹیکسٹ ہوتا ہے جو اس وقت ظاہر ہوگا جب آپ تصویر کو دیکھ یا رینڈر نہیں کر سکتے۔ یہ ایک اہم خصوصیت ہے جو رسائی کے لیے شامل کی جاتی ہے۔ رسائی کے بارے میں مزید جانیں مستقبل کے اسباق میں؛ فی الحال، یاد رکھیں کہ alt ایٹریبیوٹ تصویر کے لیے متبادل معلومات فراہم کرتا ہے اگر کسی وجہ سے صارف اسے دیکھ نہ سکے (مثلاً سست کنکشن، src ایٹریبیوٹ میں خرابی، یا اگر صارف اسکرین ریڈر استعمال کرتا ہو)۔

✅ کیا آپ نے نوٹ کیا کہ ہر تصویر کا alt ٹیگ ایک جیسا ہے؟ کیا یہ اچھی مشق ہے؟ کیوں یا کیوں نہیں؟ کیا آپ اس کوڈ کو بہتر بنا سکتے ہیں؟

---

## معنوی مارک اپ

عام طور پر، HTML لکھتے وقت 'معنوی' مارک اپ استعمال کرنا بہتر ہوتا ہے۔ اس کا کیا مطلب ہے؟ اس کا مطلب ہے کہ آپ HTML ٹیگز کو اس قسم کے ڈیٹا یا تعامل کی نمائندگی کے لیے استعمال کریں جس کے لیے وہ ڈیزائن کیے گئے ہیں۔ مثال کے طور پر، صفحے کے مرکزی عنوانی متن کو `<h1>` ٹیگ استعمال کرنا چاہیے۔

اپنے اوپننگ `<body>` ٹیگ کے فوراً نیچے یہ لائن شامل کریں:

```html
<h1>My Terrarium</h1>
```

معنوی مارک اپ کا استعمال، جیسے کہ ہیڈرز کو `<h1>` اور غیر ترتیب شدہ فہرستوں کو `<ul>` کے طور پر رینڈر کرنا، اسکرین ریڈرز کو صفحے پر نیویگیٹ کرنے میں مدد دیتا ہے۔ عام طور پر، بٹن کو `<button>` کے طور پر لکھا جانا چاہیے اور فہرستوں کو `<li>` کے طور پر۔ اگرچہ یہ _ممکن_ ہے کہ خاص طور پر اسٹائل کیے گئے `<span>` عناصر کو کلک ہینڈلرز کے ساتھ بٹن کی نقل کرنے کے لیے استعمال کیا جائے، لیکن معذور صارفین کے لیے یہ بہتر ہے کہ وہ ٹیکنالوجیز استعمال کریں تاکہ یہ معلوم کر سکیں کہ صفحے پر بٹن کہاں ہے، اور اس کے ساتھ تعامل کریں، اگر عنصر بٹن کے طور پر ظاہر ہو۔ اس وجہ سے، جتنا ممکن ہو معنوی مارک اپ استعمال کرنے کی کوشش کریں۔

✅ ایک اسکرین ریڈر دیکھیں اور [یہ کیسے ویب صفحے کے ساتھ تعامل کرتا ہے](https://www.youtube.com/watch?v=OUDV1gqs9GA)۔ کیا آپ دیکھ سکتے ہیں کہ غیر معنوی مارک اپ صارف کو کیوں مایوس کر سکتا ہے؟

## ٹیرآریم

اس انٹرفیس کا آخری حصہ ایسا مارک اپ بنانا شامل ہے جسے اسٹائل کیا جائے گا تاکہ ٹیرآریم بنایا جا سکے۔

### کام:

یہ مارک اپ آخری `</div>` ٹیگ کے اوپر شامل کریں:

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

✅ اگرچہ آپ نے یہ مارک اپ اسکرین پر شامل کیا، آپ کو بالکل کچھ بھی نظر نہیں آتا۔ کیوں؟

---

## 🚀چیلنج

HTML میں کچھ پرانے 'وائلڈ' ٹیگز ہیں جو اب بھی کھیلنے کے لیے مزے دار ہیں، حالانکہ آپ کو اپنے مارک اپ میں [یہ ٹیگز](https://developer.mozilla.org/docs/Web/HTML/Element#Obsolete_and_deprecated_elements) استعمال نہیں کرنے چاہئیں۔ پھر بھی، کیا آپ پرانے `<marquee>` ٹیگ کا استعمال کر کے h1 عنوان کو افقی طور پر اسکرول کر سکتے ہیں؟ (اگر آپ ایسا کریں، تو بعد میں اسے ہٹانا نہ بھولیں)

## لیکچر کے بعد کا کوئز

[لیکچر کے بعد کا کوئز](https://ff-quizzes.netlify.app/web/quiz/16)

## جائزہ اور خود مطالعہ

HTML وہ 'آزمودہ اور سچا' بلڈنگ بلاک سسٹم ہے جس نے ویب کو آج کے مقام تک پہنچانے میں مدد دی ہے۔ اس کی تاریخ کے بارے میں کچھ سیکھیں، پرانے اور نئے ٹیگز کا مطالعہ کریں۔ کیا آپ یہ معلوم کر سکتے ہیں کہ کچھ ٹیگز کو کیوں ختم کیا گیا اور کچھ شامل کیے گئے؟ مستقبل میں کون سے ٹیگز متعارف کرائے جا سکتے ہیں؟

ویب اور موبائل ڈیوائسز کے لیے سائٹس بنانے کے بارے میں مزید جانیں [Microsoft Learn](https://docs.microsoft.com/learn/modules/build-simple-website/?WT.mc_id=academic-77807-sagibbon) پر۔

## اسائنمنٹ

[اپنے HTML کی مشق کریں: ایک بلاگ ماک اپ بنائیں](assignment.md)

---

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے پوری کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا عدم درستگی ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے لیے ہم ذمہ دار نہیں ہیں۔