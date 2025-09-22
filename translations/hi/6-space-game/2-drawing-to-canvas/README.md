<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "056641280211e52fd0adb81b6058ec55",
  "translation_date": "2025-08-29T15:56:14+00:00",
  "source_file": "6-space-game/2-drawing-to-canvas/README.md",
  "language_code": "hi"
}
-->
# स्पेस गेम बनाएं भाग 2: हीरो और मॉन्स्टर्स को कैनवास पर ड्रॉ करें

## प्री-लेक्चर क्विज़

[प्री-लेक्चर क्विज़](https://ff-quizzes.netlify.app/web/quiz/31)

## कैनवास

कैनवास एक HTML एलिमेंट है, जिसमें डिफ़ॉल्ट रूप से कोई सामग्री नहीं होती; यह एक खाली स्लेट की तरह होता है। आपको इस पर ड्रॉ करके इसे भरना होता है।

✅ [कैनवास API के बारे में अधिक पढ़ें](https://developer.mozilla.org/docs/Web/API/Canvas_API) MDN पर।

इसे आमतौर पर पेज के बॉडी का हिस्सा इस तरह घोषित किया जाता है:

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

ऊपर दिए गए कोड में हम `id`, `width` और `height` सेट कर रहे हैं।

- `id`: इसे सेट करें ताकि जब आपको इसके साथ इंटरैक्ट करना हो, तो इसका रेफरेंस प्राप्त कर सकें।
- `width`: यह एलिमेंट की चौड़ाई है।
- `height`: यह एलिमेंट की ऊंचाई है।

## सरल ज्यामिति ड्रॉ करना

कैनवास चीजों को ड्रॉ करने के लिए एक कार्टेशियन कोऑर्डिनेट सिस्टम का उपयोग करता है। इसलिए, यह x-अक्ष और y-अक्ष का उपयोग करता है यह बताने के लिए कि कुछ कहां स्थित है। स्थान `0,0` टॉप लेफ्ट पोजीशन है और बॉटम राइट वह है जिसे आपने कैनवास की चौड़ाई (WIDTH) और ऊंचाई (HEIGHT) के रूप में सेट किया है।

![कैनवास का ग्रिड](../../../../translated_images/canvas_grid.5f209da785ded492a01ece440e3032afe51efa500cc2308e5ea4252487ceaf0b.hi.png)
> छवि [MDN](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes) से

कैनवास एलिमेंट पर ड्रॉ करने के लिए आपको निम्नलिखित चरणों से गुजरना होगा:

1. **कैनवास एलिमेंट का रेफरेंस प्राप्त करें।**
2. **कैनवास एलिमेंट पर मौजूद कॉन्टेक्स्ट एलिमेंट का रेफरेंस प्राप्त करें।**
3. **कॉन्टेक्स्ट एलिमेंट का उपयोग करके ड्रॉ ऑपरेशन करें।**

ऊपर दिए गए चरणों के लिए कोड आमतौर पर इस प्रकार दिखता है:

```javascript
// draws a red rectangle
//1. get the canvas reference
canvas = document.getElementById("myCanvas");

//2. set the context to 2D to draw basic shapes
ctx = canvas.getContext("2d");

//3. fill it with the color red
ctx.fillStyle = 'red';

//4. and draw a rectangle with these parameters, setting location and size
ctx.fillRect(0,0, 200, 200) // x,y,width, height
```

✅ कैनवास API मुख्य रूप से 2D आकृतियों पर केंद्रित है, लेकिन आप वेब साइट पर 3D एलिमेंट भी ड्रॉ कर सकते हैं; इसके लिए आप [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API) का उपयोग कर सकते हैं।

आप कैनवास API के साथ कई प्रकार की चीजें ड्रॉ कर सकते हैं, जैसे:

- **ज्यामितीय आकृतियां**, हमने पहले ही दिखाया है कि एक आयत कैसे ड्रॉ करें, लेकिन आप और भी बहुत कुछ ड्रॉ कर सकते हैं।
- **पाठ (Text)**, आप किसी भी फॉन्ट और रंग के साथ टेक्स्ट ड्रॉ कर सकते हैं।
- **छवियां (Images)**, आप किसी छवि संपत्ति जैसे .jpg या .png के आधार पर छवि ड्रॉ कर सकते हैं।

✅ इसे आज़माएं! आप जानते हैं कि एक आयत कैसे ड्रॉ करें, क्या आप पेज पर एक सर्कल ड्रॉ कर सकते हैं? CodePen पर कुछ दिलचस्प कैनवास ड्रॉइंग्स देखें। यहां एक [विशेष रूप से प्रभावशाली उदाहरण](https://codepen.io/dissimulate/pen/KrAwx) है।

## एक छवि संपत्ति लोड करें और ड्रॉ करें

आप एक छवि संपत्ति को `Image` ऑब्जेक्ट बनाकर और उसकी `src` प्रॉपर्टी सेट करके लोड करते हैं। फिर आप `load` इवेंट को सुनते हैं ताकि यह जान सकें कि यह उपयोग के लिए तैयार है। कोड इस प्रकार दिखता है:

### संपत्ति लोड करें

```javascript
const img = new Image();
img.src = 'path/to/my/image.png';
img.onload = () => {
  // image loaded and ready to be used
}
```

### संपत्ति लोड करने का पैटर्न

ऊपर दिए गए कोड को इस तरह के निर्माण में लपेटने की सिफारिश की जाती है, ताकि इसे उपयोग करना आसान हो और आप इसे केवल तभी संशोधित करें जब यह पूरी तरह से लोड हो:

```javascript
function loadAsset(path) {
  return new Promise((resolve) => {
    const img = new Image();
    img.src = path;
    img.onload = () => {
      // image loaded and ready to be used
      resolve(img);
    }
  })
}

// use like so

async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')
}

```

गेम संपत्तियों को स्क्रीन पर ड्रॉ करने के लिए, आपका कोड इस प्रकार दिखेगा:

```javascript
async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')

  canvas = document.getElementById("myCanvas");
  ctx = canvas.getContext("2d");
  ctx.drawImage(heroImg, canvas.width/2,canvas.height/2);
  ctx.drawImage(monsterImg, 0,0);
}
```

## अब समय है अपना गेम बनाना शुरू करने का

### क्या बनाना है

आपको एक वेब पेज बनाना होगा जिसमें एक कैनवास एलिमेंट हो। इसे एक काले रंग की स्क्रीन `1024*768` पर रेंडर करना चाहिए। हमने आपको दो छवियां प्रदान की हैं:

- हीरो शिप

   ![हीरो शिप](../../../../translated_images/player.dd24c1afa8c71e9b82b2958946d4bad13308681392d4b5ddcc61a0e818ef8088.hi.png)

- 5*5 मॉन्स्टर

   ![मॉन्स्टर शिप](../../../../translated_images/enemyShip.5df2a822c16650c2fb3c06652e8ec8120cdb9122a6de46b9a1a56d54db22657f.hi.png)

### विकास शुरू करने के लिए अनुशंसित चरण

`your-work` सब फोल्डर में बनाए गए फाइल्स को ढूंढें। इसमें निम्नलिखित फाइल्स होनी चाहिए:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

Visual Studio Code में इस फोल्डर की एक कॉपी खोलें। आपके पास एक लोकल डेवलपमेंट एनवायरनमेंट सेटअप होना चाहिए, अधिमानतः Visual Studio Code के साथ, जिसमें NPM और Node इंस्टॉल हो। यदि आपके कंप्यूटर पर `npm` सेटअप नहीं है, तो [यहां देखें कि इसे कैसे सेट करें](https://www.npmjs.com/get-npm)।

अपने प्रोजेक्ट को `your_work` फोल्डर में नेविगेट करके शुरू करें:

```bash
cd your-work
npm start
```

ऊपर दिया गया कोड `http://localhost:5000` पते पर एक HTTP सर्वर शुरू करेगा। एक ब्राउज़र खोलें और उस पते को दर्ज करें। यह अभी एक खाली पेज है, लेकिन यह बदल जाएगा।

> नोट: स्क्रीन पर बदलाव देखने के लिए, अपने ब्राउज़र को रिफ्रेश करें।

### कोड जोड़ें

`your-work/app.js` में आवश्यक कोड जोड़ें ताकि नीचे दिए गए कार्यों को हल किया जा सके:

1. **कैनवास** को काले बैकग्राउंड के साथ ड्रॉ करें  
   > टिप: `/app.js` में उपयुक्त TODO के तहत दो लाइनें जोड़ें, `ctx` एलिमेंट को काला सेट करें और टॉप/लेफ्ट कोऑर्डिनेट्स को 0,0 पर और कैनवास की ऊंचाई और चौड़ाई के बराबर सेट करें।
2. **टेक्सचर लोड करें**  
   > टिप: `await loadTexture` का उपयोग करके प्लेयर और दुश्मन की छवियां जोड़ें और छवि पथ पास करें। आप उन्हें अभी स्क्रीन पर नहीं देख पाएंगे!
3. **हीरो** को स्क्रीन के केंद्र में नीचे के आधे हिस्से में ड्रॉ करें  
   > टिप: `drawImage` API का उपयोग करके heroImg को स्क्रीन पर ड्रॉ करें, `canvas.width / 2 - 45` और `canvas.height - canvas.height / 4)` सेट करें।
4. **5*5 मॉन्स्टर्स ड्रॉ करें**  
   > टिप: अब आप स्क्रीन पर दुश्मनों को ड्रॉ करने के लिए कोड को अनकमेंट कर सकते हैं। फिर, `createEnemies` फंक्शन पर जाएं और इसे बनाएं।

   पहले, कुछ कॉन्स्टेंट्स सेट करें:

    ```javascript
    const MONSTER_TOTAL = 5;
    const MONSTER_WIDTH = MONSTER_TOTAL * 98;
    const START_X = (canvas.width - MONSTER_WIDTH) / 2;
    const STOP_X = START_X + MONSTER_WIDTH;
    ```

    फिर, मॉन्स्टर्स की एक श्रृंखला को स्क्रीन पर ड्रॉ करने के लिए एक लूप बनाएं:

    ```javascript
    for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          ctx.drawImage(enemyImg, x, y);
        }
      }
    ```

## परिणाम

अंतिम परिणाम इस प्रकार दिखना चाहिए:

![काली स्क्रीन जिसमें एक हीरो और 5*5 मॉन्स्टर्स हैं](../../../../translated_images/partI-solution.36c53b48c9ffae2a5e15496b23b604ba5393433e4bf91608a7a0a020eb7a2691.hi.png)

## समाधान

कृपया पहले इसे स्वयं हल करने का प्रयास करें, लेकिन यदि आप अटक जाते हैं, तो [समाधान](../../../../6-space-game/2-drawing-to-canvas/solution/app.js) देखें।

---

## 🚀 चुनौती

आपने 2D-केंद्रित कैनवास API के साथ ड्रॉ करना सीखा है; [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API) पर एक नज़र डालें, और 3D ऑब्जेक्ट ड्रॉ करने का प्रयास करें।

## पोस्ट-लेक्चर क्विज़

[पोस्ट-लेक्चर क्विज़](https://ff-quizzes.netlify.app/web/quiz/32)

## समीक्षा और स्व-अध्ययन

कैनवास API के बारे में अधिक जानने के लिए [इसके बारे में पढ़ें](https://developer.mozilla.org/docs/Web/API/Canvas_API)।

## असाइनमेंट

[कैनवास API के साथ खेलें](assignment.md)

---

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता सुनिश्चित करने का प्रयास करते हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को प्रामाणिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम जिम्मेदार नहीं हैं।