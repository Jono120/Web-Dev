<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "8a07db14e75ac62f013b7de5df05981d",
  "translation_date": "2025-08-28T14:57:37+00:00",
  "source_file": "7-bank-project/1-template-route/README.md",
  "language_code": "ar"
}
-->
# بناء تطبيق مصرفي الجزء 1: قوالب HTML والمسارات في تطبيق ويب

## اختبار ما قبل المحاضرة

[اختبار ما قبل المحاضرة](https://ff-quizzes.netlify.app/web/quiz/41)

### المقدمة

منذ ظهور JavaScript في المتصفحات، أصبحت المواقع الإلكترونية أكثر تفاعلية وتعقيدًا من أي وقت مضى. تُستخدم تقنيات الويب الآن بشكل شائع لإنشاء تطبيقات كاملة الوظائف تعمل مباشرة في المتصفح، والتي نسميها [تطبيقات الويب](https://en.wikipedia.org/wiki/Web_application). وبما أن تطبيقات الويب تفاعلية للغاية، فإن المستخدمين لا يرغبون في انتظار إعادة تحميل الصفحة بالكامل في كل مرة يتم فيها تنفيذ إجراء. لهذا السبب يتم استخدام JavaScript لتحديث HTML مباشرة باستخدام DOM، لتوفير تجربة مستخدم أكثر سلاسة.

في هذه الدرس، سنضع الأساسيات لإنشاء تطبيق مصرفي على الويب، باستخدام قوالب HTML لإنشاء شاشات متعددة يمكن عرضها وتحديثها دون الحاجة إلى إعادة تحميل صفحة HTML بالكامل.

### المتطلبات الأساسية

تحتاج إلى خادم ويب محلي لاختبار تطبيق الويب الذي سنبنيه في هذا الدرس. إذا لم يكن لديك واحد، يمكنك تثبيت [Node.js](https://nodejs.org) واستخدام الأمر `npx lite-server` من مجلد المشروع الخاص بك. سيقوم ذلك بإنشاء خادم ويب محلي وفتح تطبيقك في المتصفح.

### التحضير

على جهاز الكمبيوتر الخاص بك، قم بإنشاء مجلد باسم `bank` يحتوي على ملف باسم `index.html` بداخله. سنبدأ من هذا [القالب الأساسي](https://en.wikipedia.org/wiki/Boilerplate_code) لـ HTML:

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

## قوالب HTML

إذا كنت ترغب في إنشاء شاشات متعددة لصفحة ويب، فإن أحد الحلول هو إنشاء ملف HTML لكل شاشة تريد عرضها. ومع ذلك، يأتي هذا الحل مع بعض العيوب:

- يجب إعادة تحميل HTML بالكامل عند التبديل بين الشاشات، مما قد يكون بطيئًا.
- من الصعب مشاركة البيانات بين الشاشات المختلفة.

نهج آخر هو استخدام ملف HTML واحد فقط، وتعريف عدة [قوالب HTML](https://developer.mozilla.org/docs/Web/HTML/Element/template) باستخدام عنصر `<template>`. القالب هو كتلة HTML قابلة لإعادة الاستخدام لا يتم عرضها بواسطة المتصفح، ويجب تفعيلها أثناء وقت التشغيل باستخدام JavaScript.

### المهمة

سنقوم بإنشاء تطبيق مصرفي يحتوي على شاشتين: صفحة تسجيل الدخول ولوحة التحكم. أولاً، دعنا نضيف في جسم HTML عنصرًا نائبًا سنستخدمه لتفعيل الشاشات المختلفة لتطبيقنا:

```html
<div id="app">Loading...</div>
```

قمنا بإعطائه `id` لتسهيل تحديد موقعه باستخدام JavaScript لاحقًا.

> نصيحة: بما أن محتوى هذا العنصر سيتم استبداله، يمكننا وضع رسالة تحميل أو مؤشر يتم عرضه أثناء تحميل التطبيق.

بعد ذلك، دعنا نضيف أسفل ذلك قالب HTML لصفحة تسجيل الدخول. في الوقت الحالي، سنضع فقط عنوانًا وقسمًا يحتوي على رابط سنستخدمه للتنقل.

```html
<template id="login">
  <h1>Bank App</h1>
  <section>
    <a href="/dashboard">Login</a>
  </section>
</template>
```

ثم سنضيف قالب HTML آخر لصفحة لوحة التحكم. ستحتوي هذه الصفحة على أقسام مختلفة:

- رأس يحتوي على عنوان ورابط لتسجيل الخروج.
- الرصيد الحالي لحساب البنك.
- قائمة بالمعاملات، معروضة في جدول.

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

> نصيحة: عند إنشاء قوالب HTML، إذا كنت تريد رؤية كيف ستبدو، يمكنك تعليق سطور `<template>` و `</template>` باستخدام `<!-- -->`.

✅ لماذا تعتقد أننا نستخدم سمات `id` على القوالب؟ هل يمكننا استخدام شيء آخر مثل الفئات؟

## عرض القوالب باستخدام JavaScript

إذا جربت ملف HTML الحالي في المتصفح، ستلاحظ أنه يبقى عالقًا في عرض "Loading...". هذا لأننا بحاجة إلى إضافة بعض أكواد JavaScript لتفعيل وعرض قوالب HTML.

عادةً ما يتم تفعيل القالب في 3 خطوات:

1. استرجاع عنصر القالب في DOM، على سبيل المثال باستخدام [`document.getElementById`](https://developer.mozilla.org/docs/Web/API/Document/getElementById).
2. نسخ عنصر القالب باستخدام [`cloneNode`](https://developer.mozilla.org/docs/Web/API/Node/cloneNode).
3. إرفاقه بـ DOM تحت عنصر مرئي، على سبيل المثال باستخدام [`appendChild`](https://developer.mozilla.org/docs/Web/API/Node/appendChild).

✅ لماذا نحتاج إلى نسخ القالب قبل إرفاقه بـ DOM؟ ماذا تعتقد سيحدث إذا تخطينا هذه الخطوة؟

### المهمة

قم بإنشاء ملف جديد باسم `app.js` في مجلد المشروع الخاص بك واستورد هذا الملف في قسم `<head>` من HTML:

```html
<script src="app.js" defer></script>
```

الآن في `app.js`، سننشئ دالة جديدة باسم `updateRoute`:

```js
function updateRoute(templateId) {
  const template = document.getElementById(templateId);
  const view = template.content.cloneNode(true);
  const app = document.getElementById('app');
  app.innerHTML = '';
  app.appendChild(view);
}
```

ما نقوم به هنا هو بالضبط الخطوات الثلاث الموضحة أعلاه. نقوم بتفعيل القالب باستخدام `id` الخاص به، ونضع محتواه المنسوخ داخل العنصر النائب لتطبيقنا. لاحظ أننا نحتاج إلى استخدام `cloneNode(true)` لنسخ الشجرة الكاملة للقالب.

الآن قم باستدعاء هذه الدالة مع أحد القوالب وشاهد النتيجة.

```js
updateRoute('login');
```

✅ ما الغرض من هذا الكود `app.innerHTML = '';`؟ ماذا يحدث بدونه؟

## إنشاء المسارات

عند الحديث عن تطبيق ويب، نشير إلى *التوجيه* كعملية ربط **عناوين URL** بشاشات محددة يجب عرضها. في موقع ويب يحتوي على ملفات HTML متعددة، يتم ذلك تلقائيًا حيث يتم عكس مسارات الملفات في عنوان URL. على سبيل المثال، مع هذه الملفات في مجلد المشروع الخاص بك:

```
mywebsite/index.html
mywebsite/login.html
mywebsite/admin/index.html
```

إذا قمت بإنشاء خادم ويب مع `mywebsite` كجذر، سيكون تعيين عنوان URL كالتالي:

```
https://site.com            --> mywebsite/index.html
https://site.com/login.html --> mywebsite/login.html
https://site.com/admin/     --> mywebsite/admin/index.html
```

ومع ذلك، بالنسبة لتطبيق الويب الخاص بنا، نحن نستخدم ملف HTML واحد يحتوي على جميع الشاشات، لذا لن يساعدنا هذا السلوك الافتراضي. علينا إنشاء هذا التعيين يدويًا وتحديث القالب المعروض باستخدام JavaScript.

### المهمة

سنستخدم كائنًا بسيطًا لتنفيذ [خريطة](https://en.wikipedia.org/wiki/Associative_array) بين مسارات URL وقوالبنا. أضف هذا الكائن في أعلى ملف `app.js` الخاص بك.

```js
const routes = {
  '/login': { templateId: 'login' },
  '/dashboard': { templateId: 'dashboard' },
};
```

الآن دعنا نعدل قليلاً دالة `updateRoute`. بدلاً من تمرير `templateId` مباشرة كمعامل، نريد استرجاعه أولاً من خلال النظر إلى عنوان URL الحالي، ثم استخدام خريطتنا للحصول على قيمة `templateId` المقابلة. يمكننا استخدام [`window.location.pathname`](https://developer.mozilla.org/docs/Web/API/Location/pathname) للحصول على قسم المسار فقط من عنوان URL.

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

هنا قمنا بربط المسارات التي أعلناها بالقالب المقابل. يمكنك تجربتها للتأكد من أنها تعمل بشكل صحيح عن طريق تغيير عنوان URL يدويًا في المتصفح.

✅ ماذا يحدث إذا أدخلت مسارًا غير معروف في عنوان URL؟ كيف يمكننا حل هذه المشكلة؟

## إضافة التنقل

الخطوة التالية لتطبيقنا هي إضافة إمكانية التنقل بين الصفحات دون الحاجة إلى تغيير عنوان URL يدويًا. يتضمن ذلك شيئين:

1. تحديث عنوان URL الحالي.
2. تحديث القالب المعروض بناءً على عنوان URL الجديد.

لقد قمنا بالفعل بمعالجة الجزء الثاني باستخدام دالة `updateRoute`، لذا علينا معرفة كيفية تحديث عنوان URL الحالي.

سنحتاج إلى استخدام JavaScript وبالتحديد [`history.pushState`](https://developer.mozilla.org/docs/Web/API/History/pushState) الذي يسمح بتحديث عنوان URL وإنشاء إدخال جديد في سجل التصفح، دون إعادة تحميل HTML.

> ملاحظة: بينما يمكن استخدام عنصر HTML الرابط [`<a href>`](https://developer.mozilla.org/docs/Web/HTML/Element/a) بمفرده لإنشاء روابط لعناوين URL مختلفة، فإنه سيجعل المتصفح يعيد تحميل HTML افتراضيًا. من الضروري منع هذا السلوك عند التعامل مع التوجيه باستخدام JavaScript مخصص، باستخدام دالة `preventDefault()` على حدث النقر.

### المهمة

دعنا ننشئ دالة جديدة يمكننا استخدامها للتنقل في تطبيقنا:

```js
function navigate(path) {
  window.history.pushState({}, path, path);
  updateRoute();
}
```

تقوم هذه الطريقة أولاً بتحديث عنوان URL الحالي بناءً على المسار المعطى، ثم تقوم بتحديث القالب. الخاصية `window.location.origin` تعيد جذر عنوان URL، مما يسمح لنا بإعادة بناء عنوان URL كامل من مسار معين.

الآن بعد أن لدينا هذه الدالة، يمكننا معالجة المشكلة التي لدينا إذا لم يتطابق مسار مع أي مسار معرف. سنقوم بتعديل دالة `updateRoute` بإضافة مسار افتراضي إلى أحد المسارات الموجودة إذا لم نتمكن من العثور على تطابق.

```js
function updateRoute() {
  const path = window.location.pathname;
  const route = routes[path];

  if (!route) {
    return navigate('/login');
  }

  ...
```

إذا لم يتم العثور على مسار، سنقوم الآن بإعادة التوجيه إلى صفحة `login`.

الآن دعنا ننشئ دالة للحصول على عنوان URL عند النقر على رابط، ولمنع السلوك الافتراضي للرابط في المتصفح:

```js
function onLinkClick(event) {
  event.preventDefault();
  navigate(event.target.href);
}
```

دعنا نكمل نظام التنقل بإضافة روابط *تسجيل الدخول* و *تسجيل الخروج* في HTML.

```html
<a href="/dashboard" onclick="onLinkClick(event)">Login</a>
...
<a href="/login" onclick="onLinkClick(event)">Logout</a>
```

الكائن `event` أعلاه يلتقط حدث `click` ويمرره إلى دالة `onLinkClick`.

باستخدام خاصية [`onclick`](https://developer.mozilla.org/docs/Web/API/GlobalEventHandlers/onclick) قم بربط حدث `click` بكود JavaScript، هنا استدعاء دالة `navigate()`.

جرب النقر على هذه الروابط، يجب أن تكون الآن قادرًا على التنقل بين الشاشات المختلفة لتطبيقك.

✅ دالة `history.pushState` هي جزء من معيار HTML5 ومطبقة في [جميع المتصفحات الحديثة](https://caniuse.com/?search=pushState). إذا كنت تقوم ببناء تطبيق ويب للمتصفحات القديمة، هناك حيلة يمكنك استخدامها بدلاً من هذا API: استخدام [الهاش (`#`)](https://en.wikipedia.org/wiki/URI_fragment) قبل المسار يمكنك تنفيذ التوجيه الذي يعمل مع التنقل العادي للروابط ولا يعيد تحميل الصفحة، حيث كان الغرض منه إنشاء روابط داخلية داخل الصفحة.

## التعامل مع أزرار الرجوع والتقدم في المتصفح

استخدام `history.pushState` ينشئ إدخالات جديدة في سجل التنقل في المتصفح. يمكنك التحقق من ذلك عن طريق الضغط مطولاً على *زر الرجوع* في المتصفح، يجب أن يعرض شيئًا مثل هذا:

![لقطة شاشة لسجل التنقل](../../../../translated_images/history.7fdabbafa521e06455b738d3dafa3ff41d3071deae60ead8c7e0844b9ed987d8.ar.png)

إذا حاولت النقر على زر الرجوع عدة مرات، ستلاحظ أن عنوان URL الحالي يتغير ويتم تحديث السجل، لكن نفس القالب يظل معروضًا.

هذا لأن التطبيق لا يعرف أننا بحاجة إلى استدعاء `updateRoute()` في كل مرة يتغير السجل. إذا نظرت إلى [توثيق `history.pushState`](https://developer.mozilla.org/docs/Web/API/History/pushState)، يمكنك أن ترى أنه إذا تغيرت الحالة - بمعنى أننا انتقلنا إلى عنوان URL مختلف - يتم تشغيل حدث [`popstate`](https://developer.mozilla.org/docs/Web/API/Window/popstate_event). سنستخدم ذلك لإصلاح هذه المشكلة.

### المهمة

لضمان تحديث القالب المعروض عند تغيير سجل المتصفح، سنرفق دالة جديدة تستدعي `updateRoute()`. سنقوم بذلك في أسفل ملف `app.js` الخاص بنا:

```js
window.onpopstate = () => updateRoute();
updateRoute();
```

> ملاحظة: استخدمنا [دالة سهمية](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Functions/Arrow_functions) هنا لتحديد معالج حدث `popstate` من أجل الاختصار، ولكن دالة عادية ستعمل بنفس الطريقة.

إليك فيديو تذكيري حول الدوال السهمية:

[![دوال سهمية](https://img.youtube.com/vi/OP6eEbOj2sc/0.jpg)](https://youtube.com/watch?v=OP6eEbOj2sc "دوال سهمية")

> 🎥 انقر على الصورة أعلاه لمشاهدة فيديو حول الدوال السهمية.

الآن جرب استخدام أزرار الرجوع والتقدم في المتصفح، وتأكد من أن المسار المعروض يتم تحديثه بشكل صحيح هذه المرة.

---

## 🚀 التحدي

أضف قالبًا جديدًا ومسارًا لصفحة ثالثة تعرض معلومات عن مطوري هذا التطبيق.

## اختبار ما بعد المحاضرة

[اختبار ما بعد المحاضرة](https://ff-quizzes.netlify.app/web/quiz/42)

## المراجعة والدراسة الذاتية

التوجيه هو أحد الأجزاء التي قد تكون معقدة بشكل مفاجئ في تطوير الويب، خاصة مع انتقال الويب من سلوكيات تحديث الصفحة إلى تحديثات صفحة تطبيق واحد. اقرأ قليلاً عن [كيفية تعامل خدمة Azure Static Web App](https://docs.microsoft.com/azure/static-web-apps/routes/?WT.mc_id=academic-77807-sagibbon) مع التوجيه. هل يمكنك شرح لماذا بعض القرارات الموضحة في هذا المستند ضرورية؟

## الواجب

[تحسين التوجيه](assignment.md)

---

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الرسمي. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.