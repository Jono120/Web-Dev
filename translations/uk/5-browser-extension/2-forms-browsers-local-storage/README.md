<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a7587943d38d095de8613e1b508609f5",
  "translation_date": "2025-08-28T18:12:39+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "uk"
}
-->
# Проєкт розширення для браузера, частина 2: Виклик API, використання локального сховища

## Тест перед лекцією

[Тест перед лекцією](https://ff-quizzes.netlify.app/web/quiz/25)

### Вступ

У цьому уроці ви навчитеся викликати API, надсилаючи форму вашого розширення для браузера, і відображати результати у розширенні. Крім того, ви дізнаєтеся, як зберігати дані у локальному сховищі браузера для подальшого використання.

✅ Дотримуйтесь нумерованих сегментів у відповідних файлах, щоб знати, куди вставляти ваш код.

### Налаштування елементів для маніпуляцій у розширенні:

На цьому етапі ви вже створили HTML для форми та `<div>` для результатів вашого розширення. Тепер вам потрібно працювати у файлі `/src/index.js` і поступово будувати ваше розширення. Зверніться до [попереднього уроку](../1-about-browsers/README.md), щоб налаштувати ваш проєкт і ознайомитися з процесом збірки.

Працюючи у файлі `index.js`, почніть із створення кількох змінних `const`, щоб зберігати значення, пов'язані з різними полями:

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

Усі ці поля посилаються на їхні CSS-класи, які ви налаштували у HTML на попередньому уроці.

### Додайте слухачі подій

Далі додайте слухачі подій для форми та кнопки очищення, яка скидає форму. Таким чином, якщо користувач надсилає форму або натискає кнопку скидання, щось відбуватиметься. Також додайте виклик для ініціалізації програми в кінці файлу:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ Зверніть увагу на скорочений синтаксис для прослуховування подій submit або click і те, як подія передається у функції handleSubmit або reset. Чи можете ви написати еквівалент цього скорочення у більш розгорнутому форматі? Який підхід вам більше подобається?

### Створіть функції init() та reset():

Тепер вам потрібно створити функцію, яка ініціалізує розширення, і називається вона init():

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

У цій функції є цікава логіка. Прочитайте її уважно, чи можете ви зрозуміти, що відбувається?

- Створюються дві змінні `const`, щоб перевірити, чи зберіг користувач APIKey і код регіону у локальному сховищі.
- Якщо будь-яке з цих значень дорівнює null, форма відображається, змінюючи її стиль на 'block'.
- Ховаються результати, завантаження та кнопка очищення, а текст помилки встановлюється як порожній рядок.
- Якщо ключ і регіон існують, запускається процедура:
  - виклик API для отримання даних про вуглецевий слід,
  - приховування області результатів,
  - приховування форми,
  - відображення кнопки скидання.

Перед тим як рухатися далі, корисно дізнатися про дуже важливу концепцію, доступну у браузерах: [LocalStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage). LocalStorage — це зручний спосіб зберігати рядки у браузері у вигляді пар `ключ-значення`. Цей тип веб-сховища можна маніпулювати за допомогою JavaScript для управління даними у браузері. LocalStorage не має терміну дії, тоді як SessionStorage, інший тип веб-сховища, очищується при закритті браузера. Різні типи сховищ мають свої переваги та недоліки.

> Зверніть увагу: ваше розширення для браузера має власне локальне сховище; головне вікно браузера — це окремий екземпляр і працює незалежно.

Ви можете встановити значення для вашого APIKey, наприклад, і побачити його у Edge, "інспектуючи" веб-сторінку (ви можете клацнути правою кнопкою миші у браузері, щоб інспектувати) і перейти на вкладку Applications, щоб побачити сховище.

![Панель локального сховища](../../../../translated_images/localstorage.472f8147b6a3f8d141d9551c95a2da610ac9a3c6a73d4a1c224081c98bae09d9.uk.png)

✅ Подумайте про ситуації, коли ви НЕ хотіли б зберігати певні дані у LocalStorage. Загалом, зберігати API Keys у LocalStorage — погана ідея! Чи розумієте ви чому? У нашому випадку, оскільки наш додаток створений лише для навчання і не буде розміщений у магазині додатків, ми використовуємо цей метод.

Зверніть увагу, що ви використовуєте Web API для маніпуляцій із LocalStorage, використовуючи `getItem()`, `setItem()` або `removeItem()`. Це широко підтримується у браузерах.

Перед тим як створювати функцію `displayCarbonUsage()`, яка викликається у `init()`, давайте створимо функціонал для обробки початкового надсилання форми.

### Обробка надсилання форми

Створіть функцію `handleSubmit`, яка приймає аргумент події `(e)`. Зупиніть поширення події (у цьому випадку ми хочемо зупинити оновлення браузера) і викличте нову функцію `setUpUser`, передаючи аргументи `apiKey.value` і `region.value`. Таким чином, ви використовуєте два значення, які вводяться через початкову форму, коли відповідні поля заповнені.

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ Освіжіть пам'ять — HTML, який ви створили на попередньому уроці, має два поля введення, значення яких захоплюються через `const`, які ви створили на початку файлу, і вони обидва є `required`, тому браузер не дозволяє користувачам вводити порожні значення.

### Налаштування користувача

Переходячи до функції `setUpUser`, тут ви встановлюєте значення локального сховища для apiKey і regionName. Додайте нову функцію:

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

Ця функція встановлює повідомлення про завантаження, яке відображається під час виклику API. На цьому етапі ви підійшли до створення найважливішої функції цього розширення для браузера!

### Відображення вуглецевого сліду

Нарешті, настав час зробити запит до API!

Перед тим як рухатися далі, варто обговорити API. API, або [Інтерфейси програмування додатків](https://www.webopedia.com/TERM/A/API.html), є критичним елементом інструментарію веб-розробника. Вони забезпечують стандартні способи взаємодії програм між собою. Наприклад, якщо ви створюєте веб-сайт, який потребує доступу до бази даних, хтось міг створити API для використання. Хоча існує багато типів API, одним із найпопулярніших є [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/).

✅ Термін 'REST' означає 'Representational State Transfer' і передбачає використання різноманітно налаштованих URL для отримання даних. Проведіть невелике дослідження про різні типи API, доступні розробникам. Який формат вам подобається найбільше?

Є кілька важливих моментів у цій функції. По-перше, зверніть увагу на ключове слово [`async`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function). Написання функцій, які працюють асинхронно, означає, що вони чекають завершення певної дії, наприклад, повернення даних, перед тим як продовжити.

Ось коротке відео про `async`:

[![Async і Await для управління обіцянками](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "Async і Await для управління обіцянками")

> 🎥 Натисніть на зображення вище, щоб переглянути відео про async/await.

Створіть нову функцію для запиту до API C02Signal:

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

Це велика функція. Що тут відбувається?

- Дотримуючись найкращих практик, ви використовуєте ключове слово `async`, щоб зробити цю функцію асинхронною. Функція містить блок `try/catch`, оскільки вона повертає обіцянку, коли API повертає дані. Оскільки ви не контролюєте швидкість відповіді API (він може взагалі не відповісти!), вам потрібно обробляти цю невизначеність, викликаючи його асинхронно.
- Ви робите запит до API co2signal, щоб отримати дані вашого регіону, використовуючи ваш API Key. Для використання цього ключа потрібно використовувати тип автентифікації у параметрах заголовка.
- Коли API відповідає, ви призначаєте різні елементи його даних відповідним частинам вашого екрану, які ви налаштували для відображення цих даних.
- Якщо виникає помилка або немає результату, ви відображаєте повідомлення про помилку.

✅ Використання асинхронних шаблонів програмування — це ще один дуже корисний інструмент у вашому арсеналі. Прочитайте [про різні способи](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) налаштування такого коду.

Вітаємо! Якщо ви зберете ваше розширення (`npm run build`) і оновите його у панелі розширень, у вас буде працююче розширення! Єдине, що поки не працює, — це іконка, і ви виправите це у наступному уроці.

---

## 🚀 Виклик

Ми обговорили кілька типів API у цих уроках. Оберіть веб-API і дослідіть детально, що воно пропонує. Наприклад, ознайомтеся з API, доступними у браузерах, такими як [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API). Що, на вашу думку, робить API чудовим?

## Тест після лекції

[Тест після лекції](https://ff-quizzes.netlify.app/web/quiz/26)

## Огляд і самостійне навчання

У цьому уроці ви дізналися про LocalStorage і API, обидва дуже корисні для професійного веб-розробника. Чи можете ви подумати, як ці дві речі працюють разом? Подумайте, як би ви спроєктували веб-сайт, який зберігає елементи для використання API.

## Завдання

[Освойте API](assignment.md)

---

**Відмова від відповідальності**:  
Цей документ був перекладений за допомогою сервісу автоматичного перекладу [Co-op Translator](https://github.com/Azure/co-op-translator). Хоча ми прагнемо до точності, будь ласка, майте на увазі, що автоматичні переклади можуть містити помилки або неточності. Оригінальний документ на його рідній мові слід вважати авторитетним джерелом. Для критичної інформації рекомендується професійний людський переклад. Ми не несемо відповідальності за будь-які непорозуміння або неправильні тлумачення, що виникають внаслідок використання цього перекладу.