<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7965cd2bc5dc92ad888dc4c6ab2ab70a",
  "translation_date": "2025-08-25T21:04:49+00:00",
  "source_file": "3-terrarium/README.md",
  "language_code": "pa"
}
-->
# ਮੇਰਾ ਟੈਰੇਰੀਅਮ: HTML, CSS, ਅਤੇ DOM ਮੈਨਿਪੂਲੇਸ਼ਨ ਜਾਵਾਸਕ੍ਰਿਪਟ ਨਾਲ ਸਿੱਖਣ ਲਈ ਇੱਕ ਪ੍ਰੋਜੈਕਟ 🌵🌱

ਇੱਕ ਛੋਟਾ ਡ੍ਰੈਗ ਅਤੇ ਡ੍ਰੌਪ ਕੋਡ-ਧਿਆਨ। ਥੋੜ੍ਹੇ ਜਿਹੇ HTML, JS ਅਤੇ CSS ਦੀ ਮਦਦ ਨਾਲ, ਤੁਸੀਂ ਇੱਕ ਵੈੱਬ ਇੰਟਰਫੇਸ ਬਣਾਉਣ, ਇਸਨੂੰ ਸਜਾਉਣ ਅਤੇ ਆਪਣੇ ਚੋਣ ਦੇ ਕਈ ਇੰਟਰੈਕਸ਼ਨ ਸ਼ਾਮਲ ਕਰਨ ਦੇ ਯੋਗ ਹੋਵੋਗੇ।

![ਮੇਰਾ ਟੈਰੇਰੀਅਮ](../../../translated_images/screenshot_gray.0c796099a1f9f25e40aa55ead81f268434c00af30d7092490759945eda63067d.pa.png)

# ਪਾਠ

1. [HTML ਦਾ ਪਰਿਚਯ](./1-intro-to-html/README.md)
2. [CSS ਦਾ ਪਰਿਚਯ](./2-intro-to-css/README.md)
3. [DOM ਅਤੇ JS ਕਲੋਜ਼ਰਜ਼ ਦਾ ਪਰਿਚਯ](./3-intro-to-DOM-and-closures/README.md)

## ਸ਼੍ਰੇਯ

♥️ ਨਾਲ ਲਿਖਿਆ [Jen Looper](https://www.twitter.com/jenlooper) ਵੱਲੋਂ

CSS ਰਾਹੀਂ ਬਣਾਇਆ ਟੈਰੇਰੀਅਮ Jakub Mandra ਦੇ ਗਲਾਸ ਜਾਰ [codepen](https://codepen.io/Rotarepmi/pen/rjpNZY) ਤੋਂ ਪ੍ਰੇਰਿਤ ਹੈ।

ਕਲਾ ਦਾ ਕੰਮ [Jen Looper](http://jenlooper.com) ਵੱਲੋਂ Procreate ਦੀ ਮਦਦ ਨਾਲ ਹੱਥੋਂ ਖਿੱਚਿਆ ਗਿਆ ਹੈ।

## ਆਪਣਾ ਟੈਰੇਰੀਅਮ ਡਿਪਲੌਇ ਕਰੋ

ਤੁਸੀਂ ਆਪਣਾ ਟੈਰੇਰੀਅਮ ਵੈੱਬ 'ਤੇ Azure Static Web Apps ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਪ੍ਰਕਾਸ਼ਿਤ ਕਰ ਸਕਦੇ ਹੋ।

1. ਇਸ ਰਿਪੋਜ਼ਟਰੀ ਨੂੰ ਫੋਰਕ ਕਰੋ

2. ਇਹ ਬਟਨ ਦਬਾਓ

[![Azure 'ਤੇ ਡਿਪਲੌਇ ਕਰਨ ਲਈ ਬਟਨ](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/?feature.customportal=false&WT.mc_id=academic-77807-sagibbon#create/Microsoft.StaticApp)

3. ਆਪਣੀ ਐਪ ਬਣਾਉਣ ਲਈ ਵਿਜ਼ਾਰਡ ਦੀ ਪ੍ਰਕਿਰਿਆ ਪੂਰੀ ਕਰੋ। ਯਕੀਨੀ ਬਣਾਓ ਕਿ ਤੁਸੀਂ ਐਪ ਰੂਟ ਨੂੰ `/solution` ਜਾਂ ਆਪਣੇ ਕੋਡਬੇਸ ਦੇ ਰੂਟ 'ਤੇ ਸੈਟ ਕਰਦੇ ਹੋ। ਇਸ ਐਪ ਵਿੱਚ ਕੋਈ API ਨਹੀਂ ਹੈ, ਇਸ ਲਈ ਇਸ ਬਾਰੇ ਚਿੰਤਾ ਨਾ ਕਰੋ। ਤੁਹਾਡੇ ਫੋਰਕ ਕੀਤੇ ਰਿਪੋਜ਼ਟਰੀ ਵਿੱਚ ਇੱਕ GitHub ਫੋਲਡਰ ਬਣਾਇਆ ਜਾਵੇਗਾ ਜੋ Azure Static Web Apps ਦੀ ਬਿਲਡ ਸੇਵਾਵਾਂ ਨੂੰ ਤੁਹਾਡੀ ਐਪ ਨੂੰ ਨਵੀਂ URL 'ਤੇ ਬਣਾਉਣ ਅਤੇ ਪ੍ਰਕਾਸ਼ਿਤ ਕਰਨ ਵਿੱਚ ਮਦਦ ਕਰੇਗਾ।

**ਅਸਵੀਕਾਰਨਾ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀਤਾ ਲਈ ਯਤਨਸ਼ੀਲ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚੀਤਤਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼ ਨੂੰ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।