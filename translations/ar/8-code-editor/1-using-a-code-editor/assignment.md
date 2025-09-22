<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "bd3aa6d2b879c30ea496c43aec1c49ed",
  "translation_date": "2025-08-28T15:08:18+00:00",
  "source_file": "8-code-editor/1-using-a-code-editor/assignment.md",
  "language_code": "ar"
}
-->
# إنشاء موقع سيرة ذاتية باستخدام vscode.dev

_ما مدى روعة أن يطلب منك مسؤول التوظيف سيرتك الذاتية فتقوم بإرسال رابط له؟_ 😎

## الأهداف

بعد هذا التمرين، ستتعلم كيفية:

- إنشاء موقع إلكتروني لعرض سيرتك الذاتية.

### المتطلبات الأساسية

1. حساب على GitHub. قم بزيارة [GitHub](https://github.com/) وأنشئ حسابًا إذا لم يكن لديك واحد بالفعل.

## الخطوات

**الخطوة 1:** أنشئ مستودعًا جديدًا على GitHub وأعطه اسم `my-resume`.

**الخطوة 2:** أنشئ ملفًا باسم `index.html` في المستودع الخاص بك. سنضيف ملفًا واحدًا على الأقل أثناء وجودنا على github.com لأنك لا تستطيع فتح مستودع فارغ على vscode.dev.

انقر على رابط `creating a new file`، اكتب الاسم `index.html`، ثم اختر زر `Commit new file`.

![إنشاء ملف جديد على github.com](../../../../translated_images/new-file-github.com.c886796d800e8056561829a181be1382c5303da9d902d8b2dd82b68a4806e21f.ar.png)

**الخطوة 3:** افتح [VSCode.dev](https://vscode.dev) واختر زر `Open Remote Repository`.

انسخ رابط المستودع الذي أنشأته للتو لموقع سيرتك الذاتية والصقه في مربع الإدخال:

_استبدل `your-username` باسم المستخدم الخاص بك على GitHub._

```
https://github.com/your-username/my-resume
```

✅ إذا نجحت العملية، ستظهر لك مشروعك وملف `index.html` مفتوحًا في محرر النصوص على المتصفح.

![إنشاء ملف جديد](../../../../translated_images/project-on-vscode.dev.e79815a9a95ee7feac72ebe5c941c91279716be37c575dbdbf2f43bea2c7d8b6.ar.png)

**الخطوة 4:** افتح ملف `index.html`، الصق الكود أدناه في منطقة الكود واحفظه.

<details>
    <summary><b>كود HTML المسؤول عن محتوى موقع سيرتك الذاتية.</b></summary>
    
        <html>

            <head>
                <link href="style.css" rel="stylesheet">
                <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
                <title>ضع اسمك هنا!</title>
            </head>
            <body>
                <header id="header">
                    <!-- رأس السيرة الذاتية مع اسمك ومهنتك -->
                    <h1>ضع اسمك هنا!</h1>
                    <hr>
                    دورك الوظيفي!
                    <hr>
                </header>
                <main>
                    <article id="mainLeft">
                        <section>
                            <h2>التواصل</h2>
                            <!-- معلومات التواصل بما في ذلك وسائل التواصل الاجتماعي -->
                            <p>
                                <i class="fa fa-envelope" aria-hidden="true"></i>
                                <a href="mailto:username@domain.top-level domain">اكتب بريدك الإلكتروني هنا</a>
                            </p>
                            <p>
                                <i class="fab fa-github" aria-hidden="true"></i>
                                <a href="github.com/yourGitHubUsername">اكتب اسم المستخدم الخاص بك هنا!</a>
                            </p>
                            <p>
                                <i class="fab fa-linkedin" aria-hidden="true"></i>
                                <a href="linkedin.com/yourLinkedInUsername">اكتب اسم المستخدم الخاص بك هنا!</a>
                            </p>
                        </section>
                        <section>
                            <h2>المهارات</h2>
                            <!-- مهاراتك -->
                            <ul>
                                <li>المهارة 1!</li>
                                <li>المهارة 2!</li>
                                <li>المهارة 3!</li>
                                <li>المهارة 4!</li>
                            </ul>
                        </section>
                        <section>
                            <h2>التعليم</h2>
                            <!-- تعليمك -->
                            <h3>اكتب تخصصك هنا!</h3>
                            <p>
                                اكتب اسم المؤسسة التعليمية هنا!
                            </p>
                            <p>
                                تاريخ البداية - تاريخ النهاية
                            </p>
                        </section>            
                    </article>
                    <article id="mainRight">
                        <section>
                            <h2>نبذة عني</h2>
                            <!-- نبذة عنك -->
                            <p>اكتب نبذة قصيرة عن نفسك!</p>
                        </section>
                        <section>
                            <h2>الخبرة العملية</h2>
                            <!-- خبرتك العملية -->
                            <h3>المسمى الوظيفي</h3>
                            <p>
                                اسم المؤسسة هنا | شهر البداية – شهر النهاية
                            </p>
                            <ul>
                                    <li>المهمة 1 - اكتب ما قمت به!</li>
                                    <li>المهمة 2 - اكتب ما قمت به!</li>
                                    <li>اكتب النتائج/الأثر الذي حققته</li>
                                    
                            </ul>
                            <h3>المسمى الوظيفي 2</h3>
                            <p>
                                اسم المؤسسة هنا | شهر البداية – شهر النهاية
                            </p>
                            <ul>
                                    <li>المهمة 1 - اكتب ما قمت به!</li>
                                    <li>المهمة 2 - اكتب ما قمت به!</li>
                                    <li>اكتب النتائج/الأثر الذي حققته</li>
                                    
                            </ul>
                        </section>
                    </article>
                </main>
            </body>
        </html>
</details>

قم بإضافة تفاصيل سيرتك الذاتية لاستبدال النصوص المؤقتة في كود HTML.

**الخطوة 5:** مرر فوق مجلد My-Resume، انقر على أيقونة `New File ...` وأنشئ ملفين جديدين في مشروعك: `style.css` و `codeswing.json`.

**الخطوة 6:** افتح ملف `style.css`، الصق الكود أدناه واحفظه.

<details>
        <summary><b>كود CSS لتنسيق تخطيط الموقع.</b></summary>
            
            body {
                font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
                font-size: 16px;
                max-width: 960px;
                margin: auto;
            }
            h1 {
                font-size: 3em;
                letter-spacing: .6em;
                padding-top: 1em;
                padding-bottom: 1em;
            }

            h2 {
                font-size: 1.5em;
                padding-bottom: 1em;
            }

            h3 {
                font-size: 1em;
                padding-bottom: 1em;
            }
            main { 
                display: grid;
                grid-template-columns: 40% 60%;
                margin-top: 3em;
            }
            header {
                text-align: center;
                margin: auto 2em;
            }

            section {
                margin: auto 1em 4em 2em;
            }

            i {
                margin-right: .5em;
            }

            p {
                margin: .2em auto
            }

            hr {
                border: none;
                background-color: lightgray;
                height: 1px;
            }

            h1, h2, h3 {
                font-weight: 100;
                margin-bottom: 0;
            }
            #mainLeft {
                border-right: 1px solid lightgray;
            }
            
</details>

**الخطوة 6:** افتح ملف `codeswing.json`، الصق الكود أدناه واحفظه.

    {
    "scripts": [],
    "styles": []
    }

**الخطوة 7:** قم بتثبيت إضافة `Codeswing` لمعاينة موقع السيرة الذاتية في منطقة الكود.

انقر على أيقونة _`Extensions`_ في شريط النشاط واكتب Codeswing. انقر على زر _التثبيت الأزرق_ في شريط النشاط الموسع لتثبيت الإضافة أو استخدم زر التثبيت الذي يظهر في منطقة الكود بمجرد تحديد الإضافة لتحميل معلومات إضافية. بعد تثبيت الإضافة مباشرة، لاحظ التغييرات التي طرأت على مشروعك 😃.

![تثبيت الإضافات](../../../../8-code-editor/images/install-extension.gif)

هذا ما ستراه على شاشتك بعد تثبيت الإضافة.

![إضافة Codeswing قيد العمل](../../../../translated_images/after-codeswing-extension-pb.0ebddddcf73b550994947a9084e35e2836c713ae13839d49628e3c764c1cfe83.ar.png)

إذا كنت راضيًا عن التغييرات التي أجريتها، مرر فوق مجلد `Changes` وانقر على زر `+` لتسجيل التغييرات.

اكتب رسالة الالتزام _(وصف للتغيير الذي أجريته على المشروع)_ وقم بتأكيد التغييرات بالنقر على علامة `check`. بمجرد الانتهاء من العمل على مشروعك، اختر أيقونة القائمة في الزاوية العلوية اليسرى للعودة إلى المستودع على GitHub.

تهانينا 🎉 لقد أنشأت للتو موقع سيرتك الذاتية باستخدام vscode.dev في خطوات قليلة.

## 🚀 التحدي

افتح مستودعًا بعيدًا لديك أذونات لإجراء تغييرات عليه وقم بتحديث بعض الملفات. بعد ذلك، حاول إنشاء فرع جديد مع تغييراتك وقم بإنشاء طلب سحب.

## المراجعة والدراسة الذاتية

اقرأ المزيد عن [VSCode.dev](https://code.visualstudio.com/docs/editor/vscode-web?WT.mc_id=academic-0000-alfredodeza) وبعض ميزاته الأخرى.

---

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الرسمي. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.