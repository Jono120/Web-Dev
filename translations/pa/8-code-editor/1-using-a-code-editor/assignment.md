<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "bd3aa6d2b879c30ea496c43aec1c49ed",
  "translation_date": "2025-08-28T17:12:35+00:00",
  "source_file": "8-code-editor/1-using-a-code-editor/assignment.md",
  "language_code": "pa"
}
-->
# vscode.dev ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਇੱਕ ਰਿਜ਼ਿਊਮ-ਵੈਬਸਾਈਟ ਬਣਾਓ

_ਕਿੰਨਾ ਵਧੀਆ ਹੋਵੇਗਾ ਜੇ ਕੋਈ ਰਿਕਰੂਟਰ ਤੁਹਾਡੇ ਰਿਜ਼ਿਊਮ ਦੀ ਮੰਗ ਕਰੇ ਅਤੇ ਤੁਸੀਂ ਉਨ੍ਹਾਂ ਨੂੰ ਇੱਕ URL ਭੇਜੋ?_ 😎

## ਉਦੇਸ਼

ਇਸ ਅਸਾਈਨਮੈਂਟ ਦੇ ਬਾਅਦ, ਤੁਸੀਂ ਸਿੱਖੋਗੇ ਕਿ:

- ਆਪਣਾ ਰਿਜ਼ਿਊਮ ਦਿਖਾਉਣ ਲਈ ਇੱਕ ਵੈਬਸਾਈਟ ਕਿਵੇਂ ਬਣਾਈ ਜਾਵੇ

### ਪੂਰਵ ਸ਼ਰਤਾਂ

1. ਇੱਕ GitHub ਖਾਤਾ। [GitHub](https://github.com/) 'ਤੇ ਜਾਓ ਅਤੇ ਜੇਕਰ ਤੁਹਾਡੇ ਕੋਲ ਪਹਿਲਾਂ ਤੋਂ ਖਾਤਾ ਨਹੀਂ ਹੈ ਤਾਂ ਇੱਕ ਖਾਤਾ ਬਣਾਓ।

## ਕਦਮ

**ਕਦਮ 1:** ਇੱਕ ਨਵਾਂ GitHub Repository ਬਣਾਓ ਅਤੇ ਇਸਨੂੰ `my-resume` ਨਾਮ ਦਿਓ।

**ਕਦਮ 2:** ਆਪਣੇ Repository ਵਿੱਚ ਇੱਕ `index.html` ਫਾਈਲ ਬਣਾਓ। ਅਸੀਂ github.com 'ਤੇ ਘੱਟੋ-ਘੱਟ ਇੱਕ ਫਾਈਲ ਸ਼ਾਮਲ ਕਰਾਂਗੇ ਕਿਉਂਕਿ ਤੁਸੀਂ vscode.dev 'ਤੇ ਖਾਲੀ Repository ਨਹੀਂ ਖੋਲ੍ਹ ਸਕਦੇ।

`creating a new file` ਲਿੰਕ 'ਤੇ ਕਲਿਕ ਕਰੋ, `index.html` ਨਾਮ ਟਾਈਪ ਕਰੋ ਅਤੇ `Commit new file` ਬਟਨ ਚੁਣੋ।

![github.com 'ਤੇ ਨਵੀਂ ਫਾਈਲ ਬਣਾਓ](../../../../translated_images/new-file-github.com.c886796d800e8056561829a181be1382c5303da9d902d8b2dd82b68a4806e21f.pa.png)

**ਕਦਮ 3:** [VSCode.dev](https://vscode.dev) ਖੋਲ੍ਹੋ ਅਤੇ `Open Remote Repository` ਬਟਨ ਚੁਣੋ।

ਤੁਹਾਡੇ ਰਿਜ਼ਿਊਮ ਸਾਈਟ ਲਈ ਹੁਣੇ ਬਣਾਏ Repository ਦਾ URL ਕਾਪੀ ਕਰੋ ਅਤੇ ਇਸਨੂੰ ਇਨਪੁਟ ਬਾਕਸ ਵਿੱਚ ਪੇਸਟ ਕਰੋ:

_`your-username` ਨੂੰ ਆਪਣੇ GitHub ਯੂਜ਼ਰਨੇਮ ਨਾਲ ਬਦਲੋ_

```
https://github.com/your-username/my-resume
```

✅ ਜੇ ਸਫਲ ਹੋਵੇ, ਤਾਂ ਤੁਸੀਂ ਆਪਣਾ ਪ੍ਰੋਜੈਕਟ ਅਤੇ index.html ਫਾਈਲ ਬ੍ਰਾਊਜ਼ਰ ਵਿੱਚ ਟੈਕਸਟ ਐਡੀਟਰ 'ਤੇ ਖੁੱਲ੍ਹੇ ਹੋਏ ਦੇਖੋਗੇ।

![ਨਵੀਂ ਫਾਈਲ ਬਣਾਓ](../../../../translated_images/project-on-vscode.dev.e79815a9a95ee7feac72ebe5c941c91279716be37c575dbdbf2f43bea2c7d8b6.pa.png)

**ਕਦਮ 4:** `index.html` ਫਾਈਲ ਖੋਲ੍ਹੋ, ਹੇਠਾਂ ਦਿੱਤਾ ਕੋਡ ਆਪਣੇ ਕੋਡ ਖੇਤਰ ਵਿੱਚ ਪੇਸਟ ਕਰੋ ਅਤੇ ਸੇਵ ਕਰੋ।

<details>
    <summary><b>ਤੁਹਾਡੇ ਰਿਜ਼ਿਊਮ ਵੈਬਸਾਈਟ ਦੇ ਸਮੱਗਰੀ ਲਈ HTML ਕੋਡ।</b></summary>
    
        <html>

            <head>
                <link href="style.css" rel="stylesheet">
                <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
                <title>ਤੁਹਾਡਾ ਨਾਮ ਇੱਥੇ ਲਿਖੋ!</title>
            </head>
            <body>
                <header id="header">
                    <!-- ਰਿਜ਼ਿਊਮ ਹੈਡਰ ਤੁਹਾਡੇ ਨਾਮ ਅਤੇ ਟਾਈਟਲ ਨਾਲ -->
                    <h1>ਤੁਹਾਡਾ ਨਾਮ ਇੱਥੇ ਲਿਖੋ!</h1>
                    <hr>
                    ਤੁਹਾਡਾ ਰੋਲ!
                    <hr>
                </header>
                <main>
                    <article id="mainLeft">
                        <section>
                            <h2>ਸੰਪਰਕ</h2>
                            <!-- ਸੰਪਰਕ ਜਾਣਕਾਰੀ ਸਮੇਤ ਸੋਸ਼ਲ ਮੀਡੀਆ -->
                            <p>
                                <i class="fa fa-envelope" aria-hidden="true"></i>
                                <a href="mailto:username@domain.top-level domain">ਇੱਥੇ ਆਪਣਾ ਈਮੇਲ ਲਿਖੋ</a>
                            </p>
                            <p>
                                <i class="fab fa-github" aria-hidden="true"></i>
                                <a href="github.com/yourGitHubUsername">ਇੱਥੇ ਆਪਣਾ ਯੂਜ਼ਰਨੇਮ ਲਿਖੋ!</a>
                            </p>
                            <p>
                                <i class="fab fa-linkedin" aria-hidden="true"></i>
                                <a href="linkedin.com/yourLinkedInUsername">ਇੱਥੇ ਆਪਣਾ ਯੂਜ਼ਰਨੇਮ ਲਿਖੋ!</a>
                            </p>
                        </section>
                        <section>
                            <h2>ਹੁਨਰ</h2>
                            <!-- ਤੁਹਾਡੇ ਹੁਨਰ -->
                            <ul>
                                <li>ਹੁਨਰ 1!</li>
                                <li>ਹੁਨਰ 2!</li>
                                <li>ਹੁਨਰ 3!</li>
                                <li>ਹੁਨਰ 4!</li>
                            </ul>
                        </section>
                        <section>
                            <h2>ਸ਼ਿਕਸ਼ਾ</h2>
                            <!-- ਤੁਹਾਡੀ ਸ਼ਿਕਸ਼ਾ -->
                            <h3>ਇੱਥੇ ਆਪਣਾ ਕੋਰਸ ਲਿਖੋ!</h3>
                            <p>
                                ਇੱਥੇ ਆਪਣਾ ਸੰਸਥਾਨ ਲਿਖੋ!
                            </p>
                            <p>
                                ਸ਼ੁਰੂ - ਖਤਮ ਮਿਤੀ
                            </p>
                        </section>            
                    </article>
                    <article id="mainRight">
                        <section>
                            <h2>ਬਾਰੇ</h2>
                            <!-- ਤੁਹਾਡੇ ਬਾਰੇ -->
                            <p>ਆਪਣੇ ਬਾਰੇ ਕੁਝ ਲਿਖੋ!</p>
                        </section>
                        <section>
                            <h2>ਕੰਮ ਦਾ ਅਨੁਭਵ</h2>
                            <!-- ਤੁਹਾਡਾ ਕੰਮ ਦਾ ਅਨੁਭਵ -->
                            <h3>ਨੌਕਰੀ ਦਾ ਟਾਈਟਲ</h3>
                            <p>
                                ਇੱਥੇ ਸੰਸਥਾ ਦਾ ਨਾਮ ਲਿਖੋ | ਸ਼ੁਰੂ ਮਹੀਨਾ – ਖਤਮ ਮਹੀਨਾ
                            </p>
                            <ul>
                                    <li>ਟਾਸਕ 1 - ਤੁਸੀਂ ਕੀ ਕੀਤਾ!</li>
                                    <li>ਟਾਸਕ 2 - ਤੁਸੀਂ ਕੀ ਕੀਤਾ!</li>
                                    <li>ਤੁਹਾਡੇ ਯੋਗਦਾਨ ਦੇ ਨਤੀਜੇ/ਅਸਰ ਲਿਖੋ</li>
                                    
                            </ul>
                            <h3>ਨੌਕਰੀ ਦਾ ਟਾਈਟਲ 2</h3>
                            <p>
                                ਇੱਥੇ ਸੰਸਥਾ ਦਾ ਨਾਮ ਲਿਖੋ | ਸ਼ੁਰੂ ਮਹੀਨਾ – ਖਤਮ ਮਹੀਨਾ
                            </p>
                            <ul>
                                    <li>ਟਾਸਕ 1 - ਤੁਸੀਂ ਕੀ ਕੀਤਾ!</li>
                                    <li>ਟਾਸਕ 2 - ਤੁਸੀਂ ਕੀ ਕੀਤਾ!</li>
                                    <li>ਤੁਹਾਡੇ ਯੋਗਦਾਨ ਦੇ ਨਤੀਜੇ/ਅਸਰ ਲਿਖੋ</li>
                                    
                            </ul>
                        </section>
                    </article>
                </main>
            </body>
        </html>
</details>

HTML ਕੋਡ ਵਿੱਚ _placeholder text_ ਨੂੰ ਬਦਲ ਕੇ ਆਪਣੇ ਰਿਜ਼ਿਊਮ ਦੀ ਜਾਣਕਾਰੀ ਸ਼ਾਮਲ ਕਰੋ।

**ਕਦਮ 5:** My-Resume ਫੋਲਡਰ 'ਤੇ ਹਵਰ ਕਰੋ, `New File ...` ਆਈਕਨ 'ਤੇ ਕਲਿਕ ਕਰੋ ਅਤੇ ਆਪਣੇ ਪ੍ਰੋਜੈਕਟ ਵਿੱਚ 2 ਨਵੀਆਂ ਫਾਈਲਾਂ ਬਣਾਓ: `style.css` ਅਤੇ `codeswing.json` ਫਾਈਲਾਂ।

**ਕਦਮ 6:** `style.css` ਫਾਈਲ ਖੋਲ੍ਹੋ, ਹੇਠਾਂ ਦਿੱਤਾ ਕੋਡ ਪੇਸਟ ਕਰੋ ਅਤੇ ਸੇਵ ਕਰੋ।

<details>
        <summary><b>ਸਾਈਟ ਦੇ ਲੇਆਉਟ ਨੂੰ ਫਾਰਮੈਟ ਕਰਨ ਲਈ CSS ਕੋਡ।</b></summary>
            
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

**ਕਦਮ 6:** `codeswing.json` ਫਾਈਲ ਖੋਲ੍ਹੋ, ਹੇਠਾਂ ਦਿੱਤਾ ਕੋਡ ਪੇਸਟ ਕਰੋ ਅਤੇ ਸੇਵ ਕਰੋ।

    {
    "scripts": [],
    "styles": []
    }

**ਕਦਮ 7:** `Codeswing extension` ਇੰਸਟਾਲ ਕਰੋ ਤਾਂ ਜੋ ਰਿਜ਼ਿਊਮ ਵੈਬਸਾਈਟ ਨੂੰ ਕੋਡ ਖੇਤਰ ਵਿੱਚ ਵੇਖਿਆ ਜਾ ਸਕੇ।

_`Extensions`_ ਆਈਕਨ 'ਤੇ ਕਲਿਕ ਕਰੋ ਅਤੇ Codeswing ਟਾਈਪ ਕਰੋ। ਜਾਂ ਤਾਂ ਵਧੇਰੇ ਜਾਣਕਾਰੀ ਲੋਡ ਕਰਨ ਲਈ ਐਕਟਿਵਿਟੀ ਬਾਰ 'ਤੇ ਨੀਲਾ ਇੰਸਟਾਲ ਬਟਨ ਚੁਣੋ ਜਾਂ ਕੋਡ ਖੇਤਰ 'ਤੇ ਆਉਣ ਵਾਲੇ ਇੰਸਟਾਲ ਬਟਨ ਦੀ ਵਰਤੋਂ ਕਰੋ। ਐਕਸਟੈਂਸ਼ਨ ਇੰਸਟਾਲ ਕਰਨ ਤੋਂ ਬਾਅਦ, ਆਪਣੇ ਪ੍ਰੋਜੈਕਟ ਵਿੱਚ ਹੋਏ ਬਦਲਾਅ ਨੂੰ ਵੇਖੋ 😃

![ਐਕਸਟੈਂਸ਼ਨ ਇੰਸਟਾਲ ਕਰੋ](../../../../8-code-editor/images/install-extension.gif)

ਇਹ ਤੁਹਾਡੇ ਸਕ੍ਰੀਨ 'ਤੇ ਦਿਖਾਈ ਦੇਵੇਗਾ ਜਦੋਂ ਤੁਸੀਂ ਐਕਸਟੈਂਸ਼ਨ ਇੰਸਟਾਲ ਕਰਦੇ ਹੋ।

![Codeswing ਐਕਸਟੈਂਸ਼ਨ](../../../../translated_images/after-codeswing-extension-pb.0ebddddcf73b550994947a9084e35e2836c713ae13839d49628e3c764c1cfe83.pa.png)

ਜੇ ਤੁਸੀਂ ਕੀਤੇ ਬਦਲਾਅ ਤੋਂ ਸੰਤੁਸ਼ਟ ਹੋ, ਤਾਂ `Changes` ਫੋਲਡਰ 'ਤੇ ਹਵਰ ਕਰੋ ਅਤੇ ਬਦਲਾਅ ਨੂੰ ਸਟੇਜ ਕਰਨ ਲਈ `+` ਬਟਨ 'ਤੇ ਕਲਿਕ ਕਰੋ।

ਕਮਿਟ ਮੈਸੇਜ ਟਾਈਪ ਕਰੋ _(ਤੁਹਾਡੇ ਪ੍ਰੋਜੈਕਟ ਵਿੱਚ ਕੀਤੇ ਬਦਲਾਅ ਦਾ ਵੇਰਵਾ)_ ਅਤੇ `check` 'ਤੇ ਕਲਿਕ ਕਰਕੇ ਆਪਣੇ ਬਦਲਾਅ ਨੂੰ ਕਮਿਟ ਕਰੋ। ਜਦੋਂ ਤੁਸੀਂ ਆਪਣੇ ਪ੍ਰੋਜੈਕਟ 'ਤੇ ਕੰਮ ਕਰਨਾ ਖਤਮ ਕਰ ਲੈਂਦੇ ਹੋ, ਤਾਂ GitHub 'ਤੇ Repository 'ਤੇ ਵਾਪਸ ਜਾਣ ਲਈ ਉੱਪਰ ਖੱਬੇ ਹੰਬਰਗਰ ਮੀਨੂ ਆਈਕਨ ਨੂੰ ਚੁਣੋ।

ਵਧਾਈਆਂ 🎉 ਤੁਸੀਂ ਕੁਝ ਕਦਮਾਂ ਵਿੱਚ vscode.dev ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਆਪਣੀ ਰਿਜ਼ਿਊਮ ਵੈਬਸਾਈਟ ਬਣਾਈ ਹੈ।

## 🚀 ਚੁਣੌਤੀ

ਕੋਈ ਰਿਮੋਟ Repository ਖੋਲ੍ਹੋ ਜਿਸ 'ਤੇ ਤੁਹਾਨੂੰ ਬਦਲਾਅ ਕਰਨ ਦੀ ਇਜਾਜ਼ਤ ਹੈ ਅਤੇ ਕੁਝ ਫਾਈਲਾਂ ਅਪਡੇਟ ਕਰੋ। ਅਗਲੇ ਕਦਮ ਵਿੱਚ, ਆਪਣੇ ਬਦਲਾਅ ਨਾਲ ਇੱਕ ਨਵੀਂ ਸ਼ਾਖਾ ਬਣਾਉਣ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰੋ ਅਤੇ ਇੱਕ Pull Request ਬਣਾਓ।

## ਸਮੀਖਿਆ ਅਤੇ ਸਵੈ-ਅਧਿਐਨ

[VSCode.dev](https://code.visualstudio.com/docs/editor/vscode-web?WT.mc_id=academic-0000-alfredodeza) ਅਤੇ ਇਸਦੇ ਹੋਰ ਫੀਚਰਾਂ ਬਾਰੇ ਹੋਰ ਪੜ੍ਹੋ।

---

**ਅਸਵੀਕਰਤੀ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀ ਹੋਣ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰਦੇ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚੱਜੇਪਣ ਹੋ ਸਕਦੇ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼, ਜੋ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਹੈ, ਨੂੰ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।