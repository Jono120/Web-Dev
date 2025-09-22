<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "bd3aa6d2b879c30ea496c43aec1c49ed",
  "translation_date": "2025-08-28T23:05:26+00:00",
  "source_file": "8-code-editor/1-using-a-code-editor/assignment.md",
  "language_code": "bn"
}
-->
# vscode.dev ব্যবহার করে একটি রিজিউম-ওয়েবসাইট তৈরি করুন

_কতটা চমৎকার হবে যদি কোনো রিক্রুটার আপনার রিজিউম চায় এবং আপনি তাদের একটি URL পাঠান?_ 😎

## লক্ষ্যসমূহ

এই অ্যাসাইনমেন্টের পর, আপনি শিখবেন কীভাবে:

- আপনার রিজিউম প্রদর্শনের জন্য একটি ওয়েবসাইট তৈরি করবেন

### পূর্বশর্ত

1. একটি GitHub অ্যাকাউন্ট। [GitHub](https://github.com/) এ যান এবং যদি আপনার অ্যাকাউন্ট না থাকে তবে একটি অ্যাকাউন্ট তৈরি করুন।

## ধাপসমূহ

**ধাপ ১:** একটি নতুন GitHub রিপোজিটরি তৈরি করুন এবং এটিকে `my-resume` নাম দিন।

**ধাপ ২:** আপনার রিপোজিটরিতে একটি `index.html` ফাইল তৈরি করুন। আমরা github.com-এ অন্তত একটি ফাইল যোগ করব কারণ আপনি vscode.dev-এ একটি খালি রিপোজিটরি খুলতে পারবেন না।

`creating a new file` লিঙ্কে ক্লিক করুন, `index.html` নাম টাইপ করুন এবং `Commit new file` বোতামটি নির্বাচন করুন।

![github.com-এ নতুন ফাইল তৈরি করুন](../../../../translated_images/new-file-github.com.c886796d800e8056561829a181be1382c5303da9d902d8b2dd82b68a4806e21f.bn.png)

**ধাপ ৩:** [VSCode.dev](https://vscode.dev) খুলুন এবং `Open Remote Repository` বোতামটি নির্বাচন করুন।

আপনার রিজিউম সাইটের জন্য আপনি যে রিপোজিটরি তৈরি করেছেন তার URL কপি করুন এবং ইনপুট বক্সে পেস্ট করুন:

_`your-username` আপনার GitHub ব্যবহারকারীর নাম দিয়ে প্রতিস্থাপন করুন_

```
https://github.com/your-username/my-resume
```

✅ সফল হলে, আপনি আপনার প্রকল্প এবং `index.html` ফাইলটি ব্রাউজারের টেক্সট এডিটরে খুলতে দেখতে পাবেন।

![নতুন ফাইল তৈরি করুন](../../../../translated_images/project-on-vscode.dev.e79815a9a95ee7feac72ebe5c941c91279716be37c575dbdbf2f43bea2c7d8b6.bn.png)

**ধাপ ৪:** `index.html` ফাইলটি খুলুন, নিচের কোডটি আপনার কোড এলাকায় পেস্ট করুন এবং সংরক্ষণ করুন।

<details>
    <summary><b>আপনার রিজিউম ওয়েবসাইটের বিষয়বস্তুর জন্য HTML কোড।</b></summary>
    
        <html>

            <head>
                <link href="style.css" rel="stylesheet">
                <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
                <title>আপনার নাম এখানে লিখুন!</title>
            </head>
            <body>
                <header id="header">
                    <!-- রিজিউম হেডার আপনার নাম এবং টাইটেল সহ -->
                    <h1>আপনার নাম এখানে লিখুন!</h1>
                    <hr>
                    আপনার ভূমিকা!
                    <hr>
                </header>
                <main>
                    <article id="mainLeft">
                        <section>
                            <h2>যোগাযোগ</h2>
                            <!-- যোগাযোগের তথ্য, সোশ্যাল মিডিয়া সহ -->
                            <p>
                                <i class="fa fa-envelope" aria-hidden="true"></i>
                                <a href="mailto:username@domain.top-level domain">আপনার ইমেইল এখানে লিখুন</a>
                            </p>
                            <p>
                                <i class="fab fa-github" aria-hidden="true"></i>
                                <a href="github.com/yourGitHubUsername">আপনার ব্যবহারকারীর নাম এখানে লিখুন!</a>
                            </p>
                            <p>
                                <i class="fab fa-linkedin" aria-hidden="true"></i>
                                <a href="linkedin.com/yourLinkedInUsername">আপনার ব্যবহারকারীর নাম এখানে লিখুন!</a>
                            </p>
                        </section>
                        <section>
                            <h2>দক্ষতা</h2>
                            <!-- আপনার দক্ষতা -->
                            <ul>
                                <li>দক্ষতা ১!</li>
                                <li>দক্ষতা ২!</li>
                                <li>দক্ষতা ৩!</li>
                                <li>দক্ষতা ৪!</li>
                            </ul>
                        </section>
                        <section>
                            <h2>শিক্ষা</h2>
                            <!-- আপনার শিক্ষা -->
                            <h3>আপনার কোর্স এখানে লিখুন!</h3>
                            <p>
                                আপনার প্রতিষ্ঠান এখানে লিখুন!
                            </p>
                            <p>
                                শুরুর তারিখ - শেষ তারিখ
                            </p>
                        </section>            
                    </article>
                    <article id="mainRight">
                        <section>
                            <h2>সম্পর্কে</h2>
                            <!-- আপনার সম্পর্কে -->
                            <p>আপনার সম্পর্কে একটি সংক্ষিপ্ত বিবরণ লিখুন!</p>
                        </section>
                        <section>
                            <h2>কর্ম অভিজ্ঞতা</h2>
                            <!-- আপনার কর্ম অভিজ্ঞতা -->
                            <h3>পদবী</h3>
                            <p>
                                প্রতিষ্ঠান নাম এখানে লিখুন | শুরুর মাস – শেষ মাস
                            </p>
                            <ul>
                                    <li>কাজ ১ - আপনি কী করেছেন তা লিখুন!</li>
                                    <li>কাজ ২ - আপনি কী করেছেন তা লিখুন!</li>
                                    <li>আপনার অবদানের ফলাফল/প্রভাব লিখুন</li>
                                    
                            </ul>
                            <h3>পদবী ২</h3>
                            <p>
                                প্রতিষ্ঠান নাম এখানে লিখুন | শুরুর মাস – শেষ মাস
                            </p>
                            <ul>
                                    <li>কাজ ১ - আপনি কী করেছেন তা লিখুন!</li>
                                    <li>কাজ ২ - আপনি কী করেছেন তা লিখুন!</li>
                                    <li>আপনার অবদানের ফলাফল/প্রভাব লিখুন</li>
                                    
                            </ul>
                        </section>
                    </article>
                </main>
            </body>
        </html>
</details>

HTML কোডে _প্লেসহোল্ডার টেক্সট_ পরিবর্তন করে আপনার রিজিউমের তথ্য যোগ করুন।

**ধাপ ৫:** My-Resume ফোল্ডারের উপর মাউস রাখুন, `New File ...` আইকনে ক্লিক করুন এবং আপনার প্রকল্পে দুটি নতুন ফাইল তৈরি করুন: `style.css` এবং `codeswing.json`।

**ধাপ ৬:** `style.css` ফাইলটি খুলুন, নিচের কোডটি পেস্ট করুন এবং সংরক্ষণ করুন।

<details>
        <summary><b>সাইটের লেআউট ফরম্যাট করার জন্য CSS কোড।</b></summary>
            
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

**ধাপ ৬:** `codeswing.json` ফাইলটি খুলুন, নিচের কোডটি পেস্ট করুন এবং সংরক্ষণ করুন।

    {
    "scripts": [],
    "styles": []
    }

**ধাপ ৭:** `Codeswing extension` ইনস্টল করুন যাতে কোড এলাকায় রিজিউম ওয়েবসাইটটি দেখতে পারেন।

Activity bar-এ _`Extensions`_ আইকনে ক্লিক করুন এবং Codeswing টাইপ করুন। Expanded activity bar-এ _নীল ইনস্টল বোতাম_ বা কোড এলাকায় প্রদর্শিত ইনস্টল বোতাম ব্যবহার করে এক্সটেনশনটি ইনস্টল করুন। এক্সটেনশন ইনস্টল করার পরপরই আপনার প্রকল্পে পরিবর্তনগুলি লক্ষ্য করুন 😃

![এক্সটেনশন ইনস্টল করুন](../../../../8-code-editor/images/install-extension.gif)

এক্সটেনশন ইনস্টল করার পর আপনার স্ক্রিনে এটি দেখতে পাবেন।

![Codeswing extension কার্যক্রমে](../../../../translated_images/after-codeswing-extension-pb.0ebddddcf73b550994947a9084e35e2836c713ae13839d49628e3c764c1cfe83.bn.png)

যদি আপনি আপনার পরিবর্তনে সন্তুষ্ট হন, `Changes` ফোল্ডারের উপর মাউস রাখুন এবং পরিবর্তনগুলি স্টেজ করতে `+` বোতামে ক্লিক করুন।

একটি কমিট বার্তা টাইপ করুন _(আপনার প্রকল্পে করা পরিবর্তনের বিবরণ)_ এবং `check` ক্লিক করে আপনার পরিবর্তনগুলি কমিট করুন। আপনার প্রকল্পে কাজ শেষ হলে, উপরের বাম দিকে থাকা হ্যামবার্গার মেনু আইকন নির্বাচন করে GitHub-এ রিপোজিটরিতে ফিরে যান।

অভিনন্দন 🎉 আপনি কয়েকটি ধাপে vscode.dev ব্যবহার করে আপনার রিজিউম ওয়েবসাইট তৈরি করেছেন।

## 🚀 চ্যালেঞ্জ

আপনার অনুমতি থাকা একটি রিমোট রিপোজিটরি খুলুন এবং কিছু ফাইল আপডেট করুন। এরপর, আপনার পরিবর্তনগুলির জন্য একটি নতুন ব্রাঞ্চ তৈরি করুন এবং একটি Pull Request করুন।

## পর্যালোচনা ও স্ব-অধ্যয়ন

[VSCode.dev](https://code.visualstudio.com/docs/editor/vscode-web?WT.mc_id=academic-0000-alfredodeza) এবং এর অন্যান্য বৈশিষ্ট্য সম্পর্কে আরও পড়ুন।

---

**অস্বীকৃতি**:  
এই নথিটি AI অনুবাদ পরিষেবা [Co-op Translator](https://github.com/Azure/co-op-translator) ব্যবহার করে অনুবাদ করা হয়েছে। আমরা যথাসম্ভব সঠিকতার জন্য চেষ্টা করি, তবে অনুগ্রহ করে মনে রাখবেন যে স্বয়ংক্রিয় অনুবাদে ত্রুটি বা অসঙ্গতি থাকতে পারে। মূল ভাষায় থাকা নথিটিকে প্রামাণিক উৎস হিসেবে বিবেচনা করা উচিত। গুরুত্বপূর্ণ তথ্যের জন্য, পেশাদার মানব অনুবাদ সুপারিশ করা হয়। এই অনুবাদ ব্যবহারের ফলে কোনো ভুল বোঝাবুঝি বা ভুল ব্যাখ্যা হলে আমরা দায়বদ্ধ থাকব না।