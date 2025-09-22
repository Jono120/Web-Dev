<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a7587943d38d095de8613e1b508609f5",
  "translation_date": "2025-08-28T17:01:03+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "pa"
}
-->
# ਬ੍ਰਾਊਜ਼ਰ ਐਕਸਟੈਂਸ਼ਨ ਪ੍ਰੋਜੈਕਟ ਭਾਗ 2: API ਨੂੰ ਕਾਲ ਕਰੋ, ਲੋਕਲ ਸਟੋਰੇਜ ਵਰਤੋ

## ਪੂਰਵ-ਵਿਚਾਰ ਕਵਿਜ਼

[ਪੂਰਵ-ਵਿਚਾਰ ਕਵਿਜ਼](https://ff-quizzes.netlify.app/web/quiz/25)

### ਪਰਿਚਯ

ਇਸ ਪਾਠ ਵਿੱਚ, ਤੁਸੀਂ ਆਪਣੇ ਬ੍ਰਾਊਜ਼ਰ ਐਕਸਟੈਂਸ਼ਨ ਦੇ ਫਾਰਮ ਨੂੰ ਸਬਮਿਟ ਕਰਕੇ API ਨੂੰ ਕਾਲ ਕਰੋਗੇ ਅਤੇ ਨਤੀਜੇ ਬ੍ਰਾਊਜ਼ਰ ਐਕਸਟੈਂਸ਼ਨ ਵਿੱਚ ਦਿਖਾਵੋਗੇ। ਇਸਦੇ ਨਾਲ, ਤੁਸੀਂ ਸਿੱਖੋਗੇ ਕਿ ਕਿਵੇਂ ਆਪਣੇ ਬ੍ਰਾਊਜ਼ਰ ਦੇ ਲੋਕਲ ਸਟੋਰੇਜ ਵਿੱਚ ਡਾਟਾ ਭਵਿੱਖ ਵਿੱਚ ਹਵਾਲੇ ਅਤੇ ਵਰਤੋਂ ਲਈ ਸਟੋਰ ਕੀਤਾ ਜਾ ਸਕਦਾ ਹੈ।

✅ ਸਹੀ ਫਾਈਲਾਂ ਵਿੱਚ ਗਿਣਤੀ ਵਾਲੇ ਸੈਗਮੈਂਟਾਂ ਦੀ ਪਾਲਣਾ ਕਰੋ ਤਾਂ ਜੋ ਤੁਹਾਨੂੰ ਪਤਾ ਲੱਗੇ ਕਿ ਕੋਡ ਕਿੱਥੇ ਰੱਖਣਾ ਹੈ।

### ਐਕਸਟੈਂਸ਼ਨ ਵਿੱਚ ਮੈਨਿਪੁਲੇਟ ਕਰਨ ਲਈ ਐਲਿਮੈਂਟ ਸੈਟ ਕਰੋ:

ਇਸ ਸਮੇਂ ਤੱਕ ਤੁਸੀਂ ਆਪਣੇ ਬ੍ਰਾਊਜ਼ਰ ਐਕਸਟੈਂਸ਼ਨ ਲਈ ਫਾਰਮ ਅਤੇ ਨਤੀਜਿਆਂ `<div>` ਲਈ HTML ਬਣਾਈ ਹੈ। ਹੁਣ ਤੋਂ, ਤੁਹਾਨੂੰ `/src/index.js` ਫਾਈਲ ਵਿੱਚ ਕੰਮ ਕਰਨ ਦੀ ਜ਼ਰੂਰਤ ਹੈ ਅਤੇ ਆਪਣੀ ਐਕਸਟੈਂਸ਼ਨ ਨੂੰ ਹੌਲੀ-ਹੌਲੀ ਬਣਾਉਣਾ ਹੈ। ਪ੍ਰੋਜੈਕਟ ਸੈਟਅਪ ਅਤੇ ਬਿਲਡ ਪ੍ਰੋਸੈਸ ਬਾਰੇ ਜਾਣਨ ਲਈ [ਪਿਛਲੇ ਪਾਠ](../1-about-browsers/README.md) ਨੂੰ ਵੇਖੋ।

ਆਪਣੀ `index.js` ਫਾਈਲ ਵਿੱਚ ਕੰਮ ਕਰਦੇ ਹੋਏ, ਕੁਝ `const` ਵੈਰੀਏਬਲ ਬਣਾਉਣ ਨਾਲ ਸ਼ੁਰੂ ਕਰੋ ਜੋ ਵੱਖ-ਵੱਖ ਫੀਲਡਾਂ ਨਾਲ ਸੰਬੰਧਿਤ ਮੁੱਲਾਂ ਨੂੰ ਰੱਖਦੇ ਹਨ:

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

ਇਹ ਸਾਰੇ ਫੀਲਡ CSS ਕਲਾਸ ਦੁਆਰਾ ਰਿਫਰੈਂਸ ਕੀਤੇ ਗਏ ਹਨ, ਜਿਵੇਂ ਤੁਸੀਂ ਪਿਛਲੇ ਪਾਠ ਵਿੱਚ HTML ਵਿੱਚ ਸੈਟ ਕੀਤਾ ਸੀ।

### ਲਿਸਨਰਜ਼ ਸ਼ਾਮਲ ਕਰੋ

ਅਗਲੇ ਕਦਮ ਵਿੱਚ, ਫਾਰਮ ਅਤੇ ਕਲੀਅਰ ਬਟਨ ਲਈ ਇਵੈਂਟ ਲਿਸਨਰਜ਼ ਸ਼ਾਮਲ ਕਰੋ ਜੋ ਫਾਰਮ ਰੀਸੈਟ ਕਰਦਾ ਹੈ, ਤਾਂ ਜੋ ਜੇਕਰ ਕੋਈ ਯੂਜ਼ਰ ਫਾਰਮ ਸਬਮਿਟ ਕਰਦਾ ਹੈ ਜਾਂ ਰੀਸੈਟ ਬਟਨ 'ਤੇ ਕਲਿਕ ਕਰਦਾ ਹੈ, ਕੁਝ ਹੋਵੇ। ਫਾਈਲ ਦੇ ਤਲ 'ਤੇ ਐਪ ਨੂੰ ਸ਼ੁਰੂ ਕਰਨ ਲਈ ਕਾਲ ਸ਼ਾਮਲ ਕਰੋ:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ ਧਿਆਨ ਦਿਓ ਕਿ ਸਬਮਿਟ ਜਾਂ ਕਲਿਕ ਇਵੈਂਟ ਸੁਣਨ ਲਈ ਵਰਤੀ ਗਈ ਸ਼ਾਰਟਹੈਂਡ ਅਤੇ ਇਹ ਕਿ ਇਵੈਂਟ ਨੂੰ ਕਿਵੇਂ `handleSubmit` ਜਾਂ `reset` ਫੰਕਸ਼ਨ ਨੂੰ ਪਾਸ ਕੀਤਾ ਜਾਂਦਾ ਹੈ। ਕੀ ਤੁਸੀਂ ਇਸ ਸ਼ਾਰਟਹੈਂਡ ਦਾ ਲੰਬੇ ਫਾਰਮੈਟ ਵਿੱਚ ਸਮਾਨ ਲਿਖ ਸਕਦੇ ਹੋ? ਤੁਹਾਨੂੰ ਕਿਹੜਾ ਪਸੰਦ ਹੈ?

### `init()` ਅਤੇ `reset()` ਫੰਕਸ਼ਨ ਬਣਾਓ:

ਹੁਣ ਤੁਸੀਂ ਐਕਸਟੈਂਸ਼ਨ ਨੂੰ ਸ਼ੁਰੂ ਕਰਨ ਵਾਲਾ ਫੰਕਸ਼ਨ ਬਣਾਉਣ ਜਾ ਰਹੇ ਹੋ, ਜਿਸਨੂੰ `init()` ਕਿਹਾ ਜਾਂਦਾ ਹੈ:

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

ਇਸ ਫੰਕਸ਼ਨ ਵਿੱਚ ਕੁਝ ਦਿਲਚਸਪ ਲਾਜਿਕ ਹੈ। ਇਸਨੂੰ ਪੜ੍ਹਦੇ ਹੋਏ, ਕੀ ਤੁਸੀਂ ਦੇਖ ਸਕਦੇ ਹੋ ਕਿ ਕੀ ਹੁੰਦਾ ਹੈ?

- ਦੋ `const` ਸੈਟ ਕੀਤੇ ਜਾਂਦੇ ਹਨ ਤਾਂ ਜੋ ਜਾਂਚਿਆ ਜਾ ਸਕੇ ਕਿ ਯੂਜ਼ਰ ਨੇ APIKey ਅਤੇ ਰੀਜਨ ਕੋਡ ਨੂੰ ਲੋਕਲ ਸਟੋਰੇਜ ਵਿੱਚ ਸਟੋਰ ਕੀਤਾ ਹੈ ਜਾਂ ਨਹੀਂ।
- ਜੇਕਰ ਇਹਨਾਂ ਵਿੱਚੋਂ ਕੋਈ ਵੀ `null` ਹੈ, ਫਾਰਮ ਨੂੰ 'block' ਵਜੋਂ ਡਿਸਪਲੇਅ ਕਰਨ ਲਈ ਇਸਦੀ ਸਟਾਈਲ ਨੂੰ ਬਦਲ ਕੇ ਦਿਖਾਓ।
- ਨਤੀਜੇ, ਲੋਡਿੰਗ, ਅਤੇ `clearBtn` ਨੂੰ ਛੁਪਾਓ ਅਤੇ ਕਿਸੇ ਵੀ ਐਰਰ ਟੈਕਸਟ ਨੂੰ ਖਾਲੀ ਸਟ੍ਰਿੰਗ ਵਿੱਚ ਸੈਟ ਕਰੋ।
- ਜੇਕਰ ਕੁੰਜੀ ਅਤੇ ਰੀਜਨ ਮੌਜੂਦ ਹਨ, ਇੱਕ ਰੂਟੀਨ ਸ਼ੁਰੂ ਕਰੋ:
  - API ਨੂੰ ਕਾਲ ਕਰੋ ਤਾਂ ਜੋ ਕਾਰਬਨ ਵਰਤੋਂ ਡਾਟਾ ਪ੍ਰਾਪਤ ਕੀਤਾ ਜਾ ਸਕੇ।
  - ਨਤੀਜਿਆਂ ਵਾਲੇ ਖੇਤਰ ਨੂੰ ਛੁਪਾਓ।
  - ਫਾਰਮ ਨੂੰ ਛੁਪਾਓ।
  - ਰੀਸੈਟ ਬਟਨ ਦਿਖਾਓ।

ਅੱਗੇ ਵਧਣ ਤੋਂ ਪਹਿਲਾਂ, ਬ੍ਰਾਊਜ਼ਰ ਵਿੱਚ ਉਪਲਬਧ ਇੱਕ ਬਹੁਤ ਮਹੱਤਵਪੂਰਨ ਧਾਰਨਾ ਬਾਰੇ ਸਿੱਖਣਾ ਲਾਭਦਾਇਕ ਹੈ: [LocalStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)। LocalStorage ਬ੍ਰਾਊਜ਼ਰ ਵਿੱਚ ਸਟ੍ਰਿੰਗਾਂ ਨੂੰ `key-value` ਜੋੜੇ ਵਜੋਂ ਸਟੋਰ ਕਰਨ ਦਾ ਇੱਕ ਲਾਭਦਾਇਕ ਤਰੀਕਾ ਹੈ। ਇਸ ਤਰ੍ਹਾਂ ਦੀ ਵੈੱਬ ਸਟੋਰੇਜ ਨੂੰ ਜਾਵਾਸਕ੍ਰਿਪਟ ਦੁਆਰਾ ਮੈਨੇਜ ਕੀਤਾ ਜਾ ਸਕਦਾ ਹੈ। LocalStorage ਦੀ ਮਿਆਦ ਨਹੀਂ ਖਤਮ ਹੁੰਦੀ, ਜਦਕਿ SessionStorage, ਵੈੱਬ ਸਟੋਰੇਜ ਦੀ ਇੱਕ ਹੋਰ ਕਿਸਮ, ਬ੍ਰਾਊਜ਼ਰ ਬੰਦ ਹੋਣ 'ਤੇ ਸਾਫ਼ ਹੋ ਜਾਂਦੀ ਹੈ। ਸਟੋਰੇਜ ਦੇ ਵੱਖ-ਵੱਖ ਕਿਸਮਾਂ ਦੇ ਉਪਯੋਗ ਦੇ ਫਾਇਦੇ ਅਤੇ ਨੁਕਸਾਨ ਹਨ।

> ਨੋਟ - ਤੁਹਾਡੇ ਬ੍ਰਾਊਜ਼ਰ ਐਕਸਟੈਂਸ਼ਨ ਦਾ ਆਪਣਾ ਲੋਕਲ ਸਟੋਰੇਜ ਹੈ; ਮੁੱਖ ਬ੍ਰਾਊਜ਼ਰ ਵਿੰਡੋ ਇੱਕ ਵੱਖਰਾ ਇੰਸਟੈਂਸ ਹੈ ਅਤੇ ਵੱਖਰੇ ਤਰੀਕੇ ਨਾਲ ਕੰਮ ਕਰਦਾ ਹੈ।

ਤੁਸੀਂ ਆਪਣੀ APIKey ਨੂੰ ਇੱਕ ਸਟ੍ਰਿੰਗ ਮੁੱਲ ਦੇਣ ਲਈ ਸੈਟ ਕਰਦੇ ਹੋ, ਉਦਾਹਰਨ ਵਜੋਂ, ਅਤੇ ਤੁਸੀਂ ਦੇਖ ਸਕਦੇ ਹੋ ਕਿ ਇਹ Edge 'ਤੇ "ਇੰਸਪੈਕਟ" ਕਰਕੇ ਸੈਟ ਕੀਤੀ ਗਈ ਹੈ (ਤੁਸੀਂ ਬ੍ਰਾਊਜ਼ਰ 'ਤੇ ਰਾਈਟ-ਕਲਿਕ ਕਰਕੇ ਇੰਸਪੈਕਟ ਕਰ ਸਕਦੇ ਹੋ) ਅਤੇ ਸਟੋਰੇਜ ਦੇਖਣ ਲਈ ਐਪਲੀਕੇਸ਼ਨ ਟੈਬ 'ਤੇ ਜਾ ਸਕਦੇ ਹੋ।

![Local storage pane](../../../../translated_images/localstorage.472f8147b6a3f8d141d9551c95a2da610ac9a3c6a73d4a1c224081c98bae09d9.pa.png)

✅ ਉਹ ਸਥਿਤੀਆਂ ਬਾਰੇ ਸੋਚੋ ਜਿੱਥੇ ਤੁਸੀਂ ਕੁਝ ਡਾਟਾ LocalStorage ਵਿੱਚ ਸਟੋਰ ਨਹੀਂ ਕਰਨਾ ਚਾਹੁੰਦੇ। ਆਮ ਤੌਰ 'ਤੇ, API Keys ਨੂੰ LocalStorage ਵਿੱਚ ਰੱਖਣਾ ਇੱਕ ਖਰਾਬ ਵਿਚਾਰ ਹੈ! ਕੀ ਤੁਸੀਂ ਦੇਖ ਸਕਦੇ ਹੋ ਕਿ ਕਿਉਂ? ਸਾਡੇ ਕੇਸ ਵਿੱਚ, ਕਿਉਂਕਿ ਸਾਡਾ ਐਪ ਸਿਰਫ ਸਿੱਖਣ ਲਈ ਹੈ ਅਤੇ ਐਪ ਸਟੋਰ ਵਿੱਚ ਤੈਨਾਤ ਨਹੀਂ ਕੀਤਾ ਜਾਵੇਗਾ, ਅਸੀਂ ਇਸ ਤਰੀਕੇ ਨੂੰ ਵਰਤਾਂਗੇ।

ਧਿਆਨ ਦਿਓ ਕਿ ਤੁਸੀਂ LocalStorage ਨੂੰ ਮੈਨਿਪੁਲੇਟ ਕਰਨ ਲਈ Web API ਵਰਤਦੇ ਹੋ, ਜਾਂ `getItem()`, `setItem()`, ਜਾਂ `removeItem()` ਵਰਤ ਕੇ। ਇਹ ਬ੍ਰਾਊਜ਼ਰਾਂ ਵਿੱਚ ਵਿਆਪਕ ਤੌਰ 'ਤੇ ਸਹਾਇਕ ਹੈ।

`displayCarbonUsage()` ਫੰਕਸ਼ਨ ਬਣਾਉਣ ਤੋਂ ਪਹਿਲਾਂ ਜੋ `init()` ਵਿੱਚ ਕਾਲ ਕੀਤਾ ਜਾਂਦਾ ਹੈ, ਆਓ ਸ਼ੁਰੂਆਤੀ ਫਾਰਮ ਸਬਮਿਟ ਕਰਨ ਦੀ ਕਾਰਗੁਜ਼ਾਰੀ ਬਣਾਈਏ।

### ਫਾਰਮ ਸਬਮਿਟ ਕਰਨ ਨੂੰ ਸੰਭਾਲੋ

ਇੱਕ ਫੰਕਸ਼ਨ ਬਣਾਓ ਜਿਸਨੂੰ `handleSubmit` ਕਿਹਾ ਜਾਂਦਾ ਹੈ ਜੋ ਇੱਕ ਇਵੈਂਟ ਆਰਗੂਮੈਂਟ `(e)` ਨੂੰ ਸਵੀਕਾਰ ਕਰਦਾ ਹੈ। ਇਵੈਂਟ ਨੂੰ ਪ੍ਰਸਾਰਿਤ ਕਰਨ ਤੋਂ ਰੋਕੋ (ਇਸ ਕੇਸ ਵਿੱਚ, ਅਸੀਂ ਬ੍ਰਾਊਜ਼ਰ ਨੂੰ ਰੀਫ੍ਰੈਸ਼ ਕਰਨ ਤੋਂ ਰੋਕਣਾ ਚਾਹੁੰਦੇ ਹਾਂ) ਅਤੇ ਇੱਕ ਨਵੇਂ ਫੰਕਸ਼ਨ `setUpUser` ਨੂੰ ਕਾਲ ਕਰੋ, `apiKey.value` ਅਤੇ `region.value` ਆਰਗੂਮੈਂਟ ਪਾਸ ਕਰਦੇ ਹੋਏ। ਇਸ ਤਰੀਕੇ ਨਾਲ, ਤੁਸੀਂ ਦੋ ਮੁੱਲਾਂ ਦੀ ਵਰਤੋਂ ਕਰਦੇ ਹੋ ਜੋ ਸ਼ੁਰੂਆਤੀ ਫਾਰਮ ਦੁਆਰਾ ਲਿਆਂਦੇ ਜਾਂਦੇ ਹਨ ਜਦੋਂ ਸਬੰਧਿਤ ਫੀਲਡਾਂ ਨੂੰ ਪੂਰਾ ਕੀਤਾ ਜਾਂਦਾ ਹੈ।

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ ਆਪਣੀ ਯਾਦ ਤਾਜ਼ਾ ਕਰੋ - ਪਿਛਲੇ ਪਾਠ ਵਿੱਚ ਤੁਸੀਂ ਸੈਟ ਕੀਤਾ HTML ਵਿੱਚ ਦੋ ਇਨਪੁਟ ਫੀਲਡ ਹਨ ਜਿਨ੍ਹਾਂ ਦੇ `values` ਨੂੰ ਤੁਸੀਂ ਫਾਈਲ ਦੇ ਸਿਖਰ 'ਤੇ ਸੈਟ ਕੀਤੇ `const` ਦੁਆਰਾ ਕੈਪਚਰ ਕਰਦੇ ਹੋ, ਅਤੇ ਇਹ ਦੋਵੇਂ `required` ਹਨ ਤਾਂ ਜੋ ਬ੍ਰਾਊਜ਼ਰ ਯੂਜ਼ਰ ਨੂੰ null ਮੁੱਲਾਂ ਦਾਖਲ ਕਰਨ ਤੋਂ ਰੋਕੇ।

### ਯੂਜ਼ਰ ਸੈਟ ਕਰੋ

`setUpUser` ਫੰਕਸ਼ਨ ਵੱਲ ਵਧਦੇ ਹੋਏ, ਇੱਥੇ ਤੁਸੀਂ apiKey ਅਤੇ regionName ਲਈ ਲੋਕਲ ਸਟੋਰੇਜ ਮੁੱਲਾਂ ਸੈਟ ਕਰਦੇ ਹੋ। ਇੱਕ ਨਵਾਂ ਫੰਕਸ਼ਨ ਸ਼ਾਮਲ ਕਰੋ:

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

ਇਹ ਫੰਕਸ਼ਨ API ਨੂੰ ਕਾਲ ਕਰਨ ਦੌਰਾਨ ਦਿਖਾਉਣ ਲਈ ਇੱਕ ਲੋਡਿੰਗ ਸੁਨੇਹਾ ਸੈਟ ਕਰਦਾ ਹੈ। ਇਸ ਪੜਾਅ 'ਤੇ, ਤੁਸੀਂ ਇਸ ਬ੍ਰਾਊਜ਼ਰ ਐਕਸਟੈਂਸ਼ਨ ਦੇ ਸਭ ਤੋਂ ਮਹੱਤਵਪੂਰਨ ਫੰਕਸ਼ਨ ਨੂੰ ਬਣਾਉਣ 'ਤੇ ਪਹੁੰਚ ਗਏ ਹੋ!

### ਕਾਰਬਨ ਵਰਤੋਂ ਦਿਖਾਓ

ਅੰਤ ਵਿੱਚ, API ਨੂੰ ਕਵੈਰੀ ਕਰਨ ਦਾ ਸਮਾਂ ਹੈ!

ਅੱਗੇ ਵਧਣ ਤੋਂ ਪਹਿਲਾਂ, ਅਸੀਂ API ਬਾਰੇ ਚਰਚਾ ਕਰਨੀ ਚਾਹੀਦੀ ਹੈ। API, ਜਾਂ [Application Programming Interfaces](https://www.webopedia.com/TERM/A/API.html), ਵੈੱਬ ਡਿਵੈਲਪਰ ਦੇ ਟੂਲਬਾਕਸ ਦਾ ਇੱਕ ਮਹੱਤਵਪੂਰਨ ਤੱਤ ਹੈ। ਇਹ ਪ੍ਰੋਗਰਾਮਾਂ ਨੂੰ ਇੱਕ-ਦੂਜੇ ਨਾਲ ਇੰਟਰਫੇਸ ਕਰਨ ਲਈ ਮਿਆਰੀ ਤਰੀਕੇ ਪ੍ਰਦਾਨ ਕਰਦੇ ਹਨ। ਉਦਾਹਰਨ ਵਜੋਂ, ਜੇਕਰ ਤੁਸੀਂ ਇੱਕ ਵੈੱਬਸਾਈਟ ਬਣਾਉਣ ਜਾ ਰਹੇ ਹੋ ਜਿਸਨੂੰ ਡਾਟਾਬੇਸ ਨੂੰ ਕਵੈਰੀ ਕਰਨ ਦੀ ਜ਼ਰੂਰਤ ਹੈ, ਤਾਂ ਕੋਈ ਤੁਹਾਡੇ ਲਈ ਵਰਤਣ ਲਈ API ਬਣਾਇਆ ਹੋ ਸਕਦਾ ਹੈ। ਜਦਕਿ API ਦੀਆਂ ਕਈ ਕਿਸਮਾਂ ਹਨ, ਸਭ ਤੋਂ ਪ੍ਰਸਿੱਧ ਵਿੱਚੋਂ ਇੱਕ ਹੈ [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/)।

✅ 'REST' ਦਾ ਅਰਥ 'Representational State Transfer' ਹੈ ਅਤੇ ਇਹ ਵੱਖ-ਵੱਖ ਤਰੀਕੇ ਨਾਲ ਕਨਫਿਗਰ ਕੀਤੇ URLs ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਡਾਟਾ ਪ੍ਰਾਪਤ ਕਰਨ ਦੀ ਵਿਸ਼ੇਸ਼ਤਾ ਹੈ। ਡਿਵੈਲਪਰਾਂ ਲਈ ਉਪਲਬਧ ਵੱਖ-ਵੱਖ ਕਿਸਮਾਂ ਦੇ API ਬਾਰੇ ਕੁਝ ਖੋਜ ਕਰੋ। ਤੁਹਾਨੂੰ ਕਿਹੜਾ ਫਾਰਮੈਟ ਪਸੰਦ ਹੈ?

ਇਸ ਫੰਕਸ਼ਨ ਬਾਰੇ ਕੁਝ ਮਹੱਤਵਪੂਰਨ ਗੱਲਾਂ ਹਨ। ਪਹਿਲਾਂ, [`async` ਕੀਵਰਡ](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) 'ਤੇ ਧਿਆਨ ਦਿਓ। ਆਪਣੇ ਫੰਕਸ਼ਨ ਨੂੰ ਇਸ ਤਰੀਕੇ ਨਾਲ ਲਿਖਣਾ ਕਿ ਇਹ ਅਸਿੰਕ੍ਰੋਨਸ ਤਰੀਕੇ ਨਾਲ ਚਲਦੇ ਹਨ, ਇਸਦਾ ਮਤਲਬ ਹੈ ਕਿ ਇਹ ਕਿਸੇ ਕਾਰਵਾਈ, ਜਿਵੇਂ ਕਿ ਡਾਟਾ ਵਾਪਸ ਆਉਣਾ, ਪੂਰਾ ਹੋਣ ਦੀ ਉਡੀਕ ਕਰਦੇ ਹਨ।

ਇੱਥੇ `async` ਬਾਰੇ ਇੱਕ ਛੋਟੀ ਵੀਡੀਓ ਹੈ:

[![Async and Await for managing promises](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "Async and Await for managing promises")

> 🎥 ਉੱਪਰ ਦਿੱਤੀ ਤਸਵੀਰ 'ਤੇ ਕਲਿਕ ਕਰੋ `async/await` ਬਾਰੇ ਵੀਡੀਓ ਦੇਖਣ ਲਈ।

C02Signal API ਨੂੰ ਕਵੈਰੀ ਕਰਨ ਲਈ ਇੱਕ ਨਵਾਂ ਫੰਕਸ਼ਨ ਬਣਾਓ:

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

ਇਹ ਇੱਕ ਵੱਡਾ ਫੰਕਸ਼ਨ ਹੈ। ਇੱਥੇ ਕੀ ਹੋ ਰਿਹਾ ਹੈ?

- ਸ੍ਰੇਸ਼ਠ ਤਰੀਕਿਆਂ ਦੀ ਪਾਲਣਾ ਕਰਦੇ ਹੋਏ, ਤੁਸੀਂ ਇਸ ਫੰਕਸ਼ਨ ਨੂੰ ਅਸਿੰਕ੍ਰੋਨਸ ਬਣਾਉਣ ਲਈ `async` ਕੀਵਰਡ ਦੀ ਵਰਤੋਂ ਕਰਦੇ ਹੋ। ਫੰਕਸ਼ਨ ਵਿੱਚ ਇੱਕ `try/catch` ਬਲਾਕ ਹੈ ਕਿਉਂਕਿ ਇਹ API ਤੋਂ ਡਾਟਾ ਵਾਪਸ ਆਉਣ 'ਤੇ ਇੱਕ ਪ੍ਰੋਮਿਸ ਵਾਪਸ ਕਰੇਗਾ। ਕਿਉਂਕਿ ਤੁਹਾਡੇ ਕੋਲ API ਦੇ ਜਵਾਬ ਦੇਣ ਦੀ ਗਤੀ 'ਤੇ ਕੰਟਰੋਲ ਨਹੀਂ ਹੈ (ਇਹ ਜਵਾਬ ਨਹੀਂ ਦੇ ਸਕਦਾ!), ਤੁਸੀਂ ਇਸ ਅਨਿਸ਼ਚਿਤਤਾ ਨੂੰ ਅਸਿੰਕ੍ਰੋਨਸ ਤਰੀਕੇ ਨਾਲ ਕਾਲ ਕਰਕੇ ਸੰਭਾਲਣ ਦੀ ਜ਼ਰੂਰਤ ਹੈ।
- ਤੁਸੀਂ co2signal API ਨੂੰ ਆਪਣੇ ਰੀਜਨ ਦਾ ਡਾਟਾ ਪ੍ਰਾਪਤ ਕਰਨ ਲਈ ਕਵੈਰੀ ਕਰ ਰਹੇ ਹੋ, ਆਪਣੀ API Key ਦੀ ਵਰਤੋਂ ਕਰਦੇ ਹੋ। ਉਸ ਕੁੰਜੀ ਨੂੰ ਵਰਤਣ ਲਈ, ਤੁਹਾਨੂੰ ਆਪਣੇ ਹੈਡਰ ਪੈਰਾਮੀਟਰਾਂ ਵਿੱਚ ਇੱਕ ਕਿਸਮ ਦੀ ਪ੍ਰਮਾਣਿਕਤਾ ਦੀ ਲੋੜ ਹੈ।
- ਜਦੋਂ API ਜਵਾਬ ਦਿੰਦਾ ਹੈ, ਤੁਸੀਂ ਇਸਦੇ ਜਵਾਬ ਡਾਟਾ ਦੇ ਵੱਖ-ਵੱਖ ਤੱਤਾਂ ਨੂੰ ਆਪਣੇ ਸਕ੍ਰੀਨ ਦੇ ਹਿੱਸਿਆਂ ਵਿੱਚ ਅਸਾਈਨ ਕਰਦੇ ਹੋ ਜੋ ਤੁਸੀਂ ਇਹ ਡਾਟਾ ਦਿਖਾਉਣ ਲਈ ਸੈਟ ਕੀਤਾ ਹੈ।
- ਜੇਕਰ ਕੋਈ ਗਲਤੀ ਹੈ, ਜਾਂ ਕੋਈ ਨਤੀਜਾ ਨਹੀਂ ਹੈ, ਤਾਂ ਤੁਸੀਂ ਇੱਕ ਗਲਤੀ ਸੁਨੇਹਾ ਦਿਖਾਉਂਦੇ ਹੋ।

✅ ਅਸਿੰਕ੍ਰੋਨਸ ਪ੍ਰੋਗਰਾਮਿੰਗ ਪੈਟਰਨ ਦੀ ਵਰਤੋਂ ਕਰਨਾ ਤੁਹਾਡੇ ਟੂਲਬਾਕਸ ਵਿੱਚ ਇੱਕ ਹੋਰ ਬਹੁਤ ਹੀ ਲਾਭਦਾਇਕ ਟੂਲ ਹੈ। [ਵੱਖ-ਵੱਖ ਤਰੀਕਿਆਂ](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) ਬਾਰੇ ਪੜ੍ਹੋ ਜਿਨ੍ਹਾਂ ਨਾਲ ਤੁਸੀਂ ਇਸ ਕਿਸਮ ਦੇ ਕੋਡ ਨੂੰ ਕਨਫਿਗਰ ਕਰ ਸਕਦੇ ਹੋ।

ਮੁਬਾਰਕਾਂ! ਜੇਕਰ ਤੁਸੀਂ ਆਪਣੀ ਐਕਸਟੈਂਸ਼ਨ ਨੂੰ ਬਣਾਉਂਦੇ ਹੋ (`npm run build`) ਅਤੇ ਇਸਨੂੰ ਆਪਣੇ ਐਕਸਟੈਂਸ਼ਨ ਪੈਨ ਵਿੱਚ ਰੀਫ੍ਰੈਸ਼ ਕਰਦੇ ਹੋ, ਤਾਂ ਤੁਹਾਡੇ ਕੋਲ ਇੱਕ ਕੰਮ ਕਰਨ ਵਾਲੀ ਐਕਸਟੈਂਸ਼ਨ ਹੈ! ਸਿਰਫ ਇੱਕ ਚੀਜ਼ ਜੋ ਕੰਮ ਨਹੀਂ ਕਰ ਰਹੀ ਹੈ ਉਹ ਹੈ ਆਈਕਨ, ਅਤੇ ਤੁਸੀਂ ਇਸਨੂੰ ਅਗਲੇ ਪਾਠ ਵਿੱਚ ਠੀਕ ਕਰੋਗੇ।

---

## 🚀 ਚੁਣੌਤੀ

ਅਸੀਂ ਹੁਣ ਤੱਕ ਪਾਠਾਂ ਵਿੱਚ ਕਈ ਕਿਸਮਾਂ ਦੇ API ਬਾਰੇ ਚਰਚਾ ਕੀਤੀ ਹੈ। ਇੱਕ ਵੈੱਬ API ਚੁਣੋ ਅਤੇ ਇਸਦੇ ਦੌਰਾਨ ਕੀ ਪੇਸ਼ਕਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ ਇਸ ਬਾਰੇ ਗਹਿਰਾਈ ਵਿੱਚ ਖੋਜ ਕਰੋ। ਉਦਾਹਰਨ ਵਜੋਂ, ਬ੍ਰਾਊਜ਼ਰਾਂ ਵਿੱਚ ਉਪਲਬਧ API ਨੂੰ ਵੇਖੋ ਜਿਵੇਂ ਕਿ [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API)। ਤੁਹਾਡੇ ਵਿਚਾਰ ਵਿੱਚ ਇੱਕ ਵਧੀਆ API ਕਿਹੜਾ ਬਣਾਉਂਦਾ ਹੈ?

## ਪਾਠ-ਪ੍ਰਸਚਾਤ ਕਵਿਜ਼

[ਪਾਠ-ਪ੍ਰਸਚਾਤ ਕਵਿਜ਼](https://ff-quizzes.netlify.app/web/quiz/26)

## ਸਮੀਖਿਆ ਅਤੇ ਸਵੈ-ਅਧਿਐਨ

ਤੁਸੀਂ ਇਸ ਪਾਠ ਵਿੱਚ LocalStorage ਅਤੇ API ਬਾਰੇ ਸਿੱਖਿਆ, ਜੋ ਕਿ ਪੇਸ਼ੇਵਰ ਵੈੱਬ ਡਿਵੈਲਪਰ ਲਈ ਬਹੁਤ ਹੀ ਲਾਭਦਾਇਕ ਹਨ। ਕੀ ਤੁਸੀਂ ਸੋਚ ਸਕਦੇ ਹੋ ਕਿ ਇਹ ਦੋ ਚੀਜ਼ਾਂ ਇਕੱਠੇ ਕਿਵੇਂ ਕੰਮ ਕਰਦੀਆਂ ਹਨ? ਸੋਚੋ ਕਿ ਤੁਸੀਂ ਇੱਕ ਵੈੱਬਸਾਈਟ ਨੂੰ ਕਿਵੇਂ ਆਰਕੀਟੈਕਟ ਕਰਦੇ ਹੋ ਜੋ API ਦੁਆਰਾ ਵਰਤਣ ਲਈ ਆਈਟਮ ਸਟੋਰ ਕਰੇਗੀ।

## ਅਸਾਈਨਮੈਂਟ

[Adopt an API](assignment.md)

---

**ਅਸਵੀਕਰਤੀ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀ ਹੋਣ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰਦੇ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚਤਤਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼ ਨੂੰ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।