<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "bd3aa6d2b879c30ea496c43aec1c49ed",
  "translation_date": "2025-08-28T16:43:27+00:00",
  "source_file": "8-code-editor/1-using-a-code-editor/assignment.md",
  "language_code": "ne"
}
-->
# vscode.dev प्रयोग गरेर रिजुमे-वेबसाइट बनाउनुहोस्

_कति राम्रो होला जब कुनै भर्तीकर्ताले तपाईंको रिजुमे माग्छन् र तपाईं उनलाई एउटा URL पठाउनुहुन्छ?_ 😎

## उद्देश्यहरू

यस असाइनमेन्ट पछि, तपाईंले सिक्नुहुनेछ:

- आफ्नो रिजुमे प्रदर्शन गर्न वेबसाइट बनाउने

### पूर्व-आवश्यकताहरू

1. GitHub खाता। [GitHub](https://github.com/) मा जानुहोस् र यदि तपाईंले पहिले नै खाता बनाउनु भएको छैन भने खाता बनाउनुहोस्।

## चरणहरू

**चरण १:** नयाँ GitHub Repository बनाउनुहोस् र यसलाई `my-resume` नाम दिनुहोस्।

**चरण २:** आफ्नो रिपोजिटरीमा `index.html` फाइल बनाउनुहोस्। हामी github.com मा कम्तिमा एउटा फाइल थप्नेछौं किनभने तपाईं vscode.dev मा खाली रिपोजिटरी खोल्न सक्नुहुन्न।

`creating a new file` लिंकमा क्लिक गर्नुहोस्, `index.html` नाम टाइप गर्नुहोस् र `Commit new file` बटन चयन गर्नुहोस्।

![github.com मा नयाँ फाइल बनाउनुहोस्](../../../../translated_images/new-file-github.com.c886796d800e8056561829a181be1382c5303da9d902d8b2dd82b68a4806e21f.ne.png)

**चरण ३:** [VSCode.dev](https://vscode.dev) खोल्नुहोस् र `Open Remote Repository` बटन चयन गर्नुहोस्।

तपाईंले आफ्नो रिजुमे साइटको लागि सिर्जना गरेको रिपोजिटरीको URL कपी गर्नुहोस् र इनपुट बक्समा पेस्ट गर्नुहोस्:

_`your-username` लाई आफ्नो GitHub प्रयोगकर्ता नामले प्रतिस्थापन गर्नुहोस्।_

```
https://github.com/your-username/my-resume
```

✅ सफल भएमा, तपाईं आफ्नो प्रोजेक्ट र `index.html` फाइल ब्राउजरको टेक्स्ट एडिटरमा खुला देख्नुहुनेछ।

![नयाँ फाइल बनाउनुहोस्](../../../../translated_images/project-on-vscode.dev.e79815a9a95ee7feac72ebe5c941c91279716be37c575dbdbf2f43bea2c7d8b6.ne.png)

**चरण ४:** `index.html` फाइल खोल्नुहोस्, तलको कोड आफ्नो कोड क्षेत्रमा पेस्ट गर्नुहोस् र सुरक्षित गर्नुहोस्।

<details>
    <summary><b>रिजुमे वेबसाइटको सामग्रीको लागि HTML कोड।</b></summary>
    
        <html>

            <head>
                <link href="style.css" rel="stylesheet">
                <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
                <title>यहाँ आफ्नो नाम लेख्नुहोस्!</title>
            </head>
            <body>
                <header id="header">
                    <!-- रिजुमे हेडर तपाईंको नाम र शीर्षक सहित -->
                    <h1>यहाँ आफ्नो नाम लेख्नुहोस्!</h1>
                    <hr>
                    तपाईंको भूमिका!
                    <hr>
                </header>
                <main>
                    <article id="mainLeft">
                        <section>
                            <h2>सम्पर्क</h2>
                            <!-- सम्पर्क जानकारी सामाजिक सञ्जाल सहित -->
                            <p>
                                <i class="fa fa-envelope" aria-hidden="true"></i>
                                <a href="mailto:username@domain.top-level domain">यहाँ आफ्नो इमेल लेख्नुहोस्</a>
                            </p>
                            <p>
                                <i class="fab fa-github" aria-hidden="true"></i>
                                <a href="github.com/yourGitHubUsername">यहाँ आफ्नो प्रयोगकर्ता नाम लेख्नुहोस्!</a>
                            </p>
                            <p>
                                <i class="fab fa-linkedin" aria-hidden="true"></i>
                                <a href="linkedin.com/yourLinkedInUsername">यहाँ आफ्नो प्रयोगकर्ता नाम लेख्नुहोस्!</a>
                            </p>
                        </section>
                        <section>
                            <h2>सीपहरू</h2>
                            <!-- तपाईंका सीपहरू -->
                            <ul>
                                <li>सीप १!</li>
                                <li>सीप २!</li>
                                <li>सीप ३!</li>
                                <li>सीप ४!</li>
                            </ul>
                        </section>
                        <section>
                            <h2>शिक्षा</h2>
                            <!-- तपाईंको शिक्षा -->
                            <h3>यहाँ आफ्नो कोर्स लेख्नुहोस्!</h3>
                            <p>
                                यहाँ आफ्नो संस्था लेख्नुहोस्!
                            </p>
                            <p>
                                सुरु - अन्त्य मिति
                            </p>
                        </section>            
                    </article>
                    <article id="mainRight">
                        <section>
                            <h2>बारेमा</h2>
                            <!-- तपाईंको बारेमा -->
                            <p>आफ्नो बारेमा केही लेख्नुहोस्!</p>
                        </section>
                        <section>
                            <h2>कामको अनुभव</h2>
                            <!-- तपाईंको कामको अनुभव -->
                            <h3>कामको शीर्षक</h3>
                            <p>
                                यहाँ संस्थाको नाम लेख्नुहोस् | सुरु महिना – अन्त्य महिना
                            </p>
                            <ul>
                                    <li>कार्य १ - तपाईंले के गर्नुभयो लेख्नुहोस्!</li>
                                    <li>कार्य २ - तपाईंले के गर्नुभयो लेख्नुहोस्!</li>
                                    <li>तपाईंको योगदानको परिणाम/प्रभाव लेख्नुहोस्</li>
                                    
                            </ul>
                            <h3>कामको शीर्षक २</h3>
                            <p>
                                यहाँ संस्थाको नाम लेख्नुहोस् | सुरु महिना – अन्त्य महिना
                            </p>
                            <ul>
                                    <li>कार्य १ - तपाईंले के गर्नुभयो लेख्नुहोस्!</li>
                                    <li>कार्य २ - तपाईंले के गर्नुभयो लेख्नुहोस्!</li>
                                    <li>तपाईंको योगदानको परिणाम/प्रभाव लेख्नुहोस्</li>
                                    
                            </ul>
                        </section>
                    </article>
                </main>
            </body>
        </html>
</details>

HTML कोडमा _placeholder text_ लाई आफ्नो रिजुमे विवरणले प्रतिस्थापन गर्नुहोस्।

**चरण ५:** My-Resume फोल्डरमा होभर गर्नुहोस्, `New File ...` आइकनमा क्लिक गर्नुहोस् र आफ्नो प्रोजेक्टमा २ नयाँ फाइलहरू बनाउनुहोस्: `style.css` र `codeswing.json` फाइलहरू।

**चरण ६:** `style.css` फाइल खोल्नुहोस्, तलको कोड पेस्ट गर्नुहोस् र सुरक्षित गर्नुहोस्।

<details>
        <summary><b>साइटको लेआउटलाई फर्म्याट गर्न CSS कोड।</b></summary>
            
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

**चरण ६:** `codeswing.json` फाइल खोल्नुहोस्, तलको कोड पेस्ट गर्नुहोस् र सुरक्षित गर्नुहोस्।

    {
    "scripts": [],
    "styles": []
    }

**चरण ७:** `Codeswing extension` स्थापना गर्नुहोस् ताकि रिजुमे वेबसाइटलाई कोड क्षेत्रमा देख्न सकियोस्।

_`Extensions`_ आइकनमा क्लिक गर्नुहोस् र Codeswing टाइप गर्नुहोस्। विस्तारलाई चयन गरेपछि थप जानकारी लोड गर्न _ब्लू इन्स्टल बटन_ मा क्लिक गर्नुहोस् वा कोड क्षेत्रमा देखिने इन्स्टल बटन प्रयोग गर्नुहोस्। विस्तार स्थापना गरेपछि, आफ्नो प्रोजेक्टमा परिवर्तनहरू देख्न सक्नुहुन्छ 😃।

![Extensions स्थापना गर्नुहोस्](../../../../8-code-editor/images/install-extension.gif)

तपाईंले विस्तार स्थापना गरेपछि आफ्नो स्क्रिनमा यो देख्नुहुनेछ।

![Codeswing विस्तारको प्रभाव](../../../../translated_images/after-codeswing-extension-pb.0ebddddcf73b550994947a9084e35e2836c713ae13839d49628e3c764c1cfe83.ne.png)

यदि तपाईंले गरेका परिवर्तनहरूमा सन्तुष्ट हुनुहुन्छ भने, `Changes` फोल्डरमा होभर गर्नुहोस् र `+` बटनमा क्लिक गरेर परिवर्तनहरू स्टेज गर्नुहोस्।

कमिट सन्देश टाइप गर्नुहोस् _(प्रोजेक्टमा तपाईंले गरेको परिवर्तनको विवरण)_ र `check` क्लिक गरेर परिवर्तनहरू कमिट गर्नुहोस्। प्रोजेक्टमा काम सकिएपछि, GitHub मा रिपोजिटरीमा फर्कनको लागि माथि बायाँ रहेको ह्याम्बर्गर मेनु आइकन चयन गर्नुहोस्।

बधाई छ 🎉 तपाईंले केही चरणहरूमा vscode.dev प्रयोग गरेर आफ्नो रिजुमे वेबसाइट सिर्जना गर्नुभयो।

## 🚀 चुनौती

तपाईंले परिवर्तन गर्न अनुमति पाएको रिमोट रिपोजिटरी खोल्नुहोस् र केही फाइलहरू अपडेट गर्नुहोस्। त्यसपछि, आफ्नो परिवर्तनहरू सहित नयाँ ब्रान्च बनाउने प्रयास गर्नुहोस् र Pull Request गर्नुहोस्।

## समीक्षा र आत्म-अध्ययन

[VSCode.dev](https://code.visualstudio.com/docs/editor/vscode-web?WT.mc_id=academic-0000-alfredodeza) र यसको अन्य सुविधाहरूको बारेमा थप पढ्नुहोस्।

---

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरेर अनुवाद गरिएको हो। हामी शुद्धताको लागि प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छ। यसको मूल भाषा मा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीको लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।