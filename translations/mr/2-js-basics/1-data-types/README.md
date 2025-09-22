<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "b95fdd8310ef467305015ece1b0f9411",
  "translation_date": "2025-08-28T16:18:40+00:00",
  "source_file": "2-js-basics/1-data-types/README.md",
  "language_code": "mr"
}
-->
# JavaScript Basics: डेटा प्रकार

![JavaScript Basics - Data types](../../../../translated_images/webdev101-js-datatypes.4cc470179730702c756480d3ffa46507f746e5975ebf80f99fdaaf1cff09a7f4.mr.png)
> स्केच नोट [Tomomi Imura](https://twitter.com/girlie_mac) यांनी तयार केले आहे

## व्याख्यानपूर्व प्रश्नमंजुषा
[व्याख्यानपूर्व प्रश्नमंजुषा](https://ff-quizzes.netlify.app/web/)

या धड्यात JavaScript च्या मूलभूत गोष्टींचा समावेश आहे, ही भाषा वेबवर संवाद साधण्यासाठी वापरली जाते.

> तुम्ही हा धडा [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-variables/?WT.mc_id=academic-77807-sagibbon) वर घेऊ शकता!

[![Variables](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Variables in JavaScript")

[![Data Types in JavaScript](https://img.youtube.com/vi/AWfA95eLdq8/0.jpg)](https://youtube.com/watch?v=AWfA95eLdq8 "Data Types in JavaScript")

> 🎥 वरील प्रतिमांवर क्लिक करा आणि व्हिडिओ पहा, ज्यामध्ये variables आणि data types बद्दल माहिती दिली आहे.

चला variables आणि त्यामध्ये असलेल्या डेटा प्रकारांपासून सुरुवात करूया!

## Variables

Variables म्हणजे अशा मूल्यांचे संग्रह आहेत जे तुमच्या कोडमध्ये वापरले जाऊ शकतात आणि बदलले जाऊ शकतात.

**घोषणा** करून एक variable तयार करण्यासाठी खालील syntax वापरला जातो **[keyword] [name]**. यामध्ये दोन भाग असतात:

- **Keyword**. Keywords `let` किंवा `var` असू शकतात.  

✅ ES6 मध्ये `let` keyword सादर करण्यात आले आणि यामुळे तुमच्या variable ला _block scope_ मिळतो. `let` वापरण्याची शिफारस केली जाते. आम्ही पुढील भागांमध्ये block scopes सविस्तरपणे कव्हर करू.
- **Variable name**, हे नाव तुम्ही स्वतः निवडता.

### कार्य - variables सोबत काम करणे

1. **एक variable घोषित करा**. `let` keyword वापरून एक variable घोषित करूया:

    ```javascript
    let myVariable;
    ```

   `myVariable` आता `let` keyword वापरून घोषित केले गेले आहे. सध्या त्याला कोणतेही मूल्य नाही.

1. **मूल्य असाइन करा**. `=` ऑपरेटर वापरून आणि अपेक्षित मूल्य देऊन variable मध्ये मूल्य संग्रहित करा.

    ```javascript
    myVariable = 123;
    ```

   > टीप: या धड्यात `=` चा वापर "assignment operator" म्हणून केला जातो, जो variable ला मूल्य सेट करण्यासाठी वापरला जातो. याचा समानतेशी काहीही संबंध नाही.

   `myVariable` आता 123 मूल्याने *initialized* केले गेले आहे.

1. **Refactor करा**. तुमचा कोड खालील विधानाने बदला.

    ```javascript
    let myVariable = 123;
    ```

    वरील विधानाला _explicit initialization_ म्हणतात, जेव्हा एक variable घोषित केला जातो आणि त्याच वेळी त्याला मूल्य असाइन केले जाते.

1. **Variable चे मूल्य बदला**. खालील प्रकारे variable चे मूल्य बदला:

   ```javascript
   myVariable = 321;
   ```

   एकदा variable घोषित झाल्यावर, तुम्ही कोणत्याही वेळी `=` ऑपरेटर आणि नवीन मूल्य वापरून त्याचे मूल्य बदलू शकता.

   ✅ प्रयत्न करा! तुम्ही तुमच्या ब्राउझरमध्ये थेट JavaScript लिहू शकता. एक ब्राउझर विंडो उघडा आणि Developer Tools मध्ये जा. कन्सोलमध्ये तुम्हाला एक prompt दिसेल; `let myVariable = 123` टाइप करा, return दाबा, नंतर `myVariable` टाइप करा. काय होते? लक्षात ठेवा, तुम्ही पुढील धड्यांमध्ये या संकल्पनांबद्दल अधिक शिकाल.

## Constants

Constant ची घोषणा आणि initialization variable प्रमाणेच असते, फक्त `const` keyword चा अपवाद आहे. Constants सामान्यतः uppercase अक्षरांमध्ये घोषित केले जातात.

```javascript
const MY_VARIABLE = 123;
```

Constants variables सारखेच असतात, फक्त दोन अपवादांसह:

- **मूल्य असणे आवश्यक आहे**. Constants initialized केले गेले पाहिजे, अन्यथा कोड चालवताना त्रुटी येईल.
- **Reference बदलता येत नाही**. Constant initialized झाल्यानंतर त्याचा reference बदलता येत नाही, अन्यथा कोड चालवताना त्रुटी येईल. चला दोन उदाहरणे पाहूया:
   - **साधे मूल्य**. खालील गोष्ट परवानगी नाही:
   
      ```javascript
      const PI = 3;
      PI = 4; // not allowed
      ```
 
   - **Object reference संरक्षित आहे**. खालील गोष्ट परवानगी नाही:
   
      ```javascript
      const obj = { a: 3 };
      obj = { b: 5 } // not allowed
      ```

    - **Object value संरक्षित नाही**. खालील गोष्ट परवानगी आहे:
    
      ```javascript
      const obj = { a: 3 };
      obj.a = 5;  // allowed
      ```

      वरील उदाहरणात तुम्ही object चे मूल्य बदलत आहात, reference नाही, त्यामुळे ते परवानगी आहे.

   > टीप, `const` म्हणजे reference पुनः असाइन करण्यापासून संरक्षित आहे. परंतु मूल्य _immutable_ नाही आणि ते बदलू शकते, विशेषतः जर ते object सारखे complex construct असेल.

## डेटा प्रकार

Variables अनेक प्रकारचे मूल्य संग्रहित करू शकतात, जसे की संख्या आणि मजकूर. या विविध प्रकारच्या मूल्यांना **डेटा प्रकार** म्हणतात. डेटा प्रकार सॉफ्टवेअर विकासाचा महत्त्वाचा भाग आहे कारण यामुळे विकसकांना कोड कसा लिहायचा आणि सॉफ्टवेअर कसे चालवायचे याबद्दल निर्णय घेण्यास मदत होते. याशिवाय, काही डेटा प्रकारांमध्ये अद्वितीय वैशिष्ट्ये असतात जी मूल्यामध्ये अतिरिक्त माहिती रूपांतरित किंवा काढण्यासाठी मदत करतात.

✅ डेटा प्रकार JavaScript डेटा primitives म्हणून ओळखले जातात, कारण ते भाषेद्वारे प्रदान केलेले सर्वात कमी-स्तरीय डेटा प्रकार आहेत. 7 primitive डेटा प्रकार आहेत: string, number, bigint, boolean, undefined, null आणि symbol. प्रत्येक primitive काय दर्शवते याचा विचार करा. `zebra` म्हणजे काय? `0` कसे? `true` कसे?

### Numbers

मागील विभागात, `myVariable` चे मूल्य number डेटा प्रकार होते.

`let myVariable = 123;`

Variables सर्व प्रकारच्या संख्या संग्रहित करू शकतात, ज्यामध्ये दशांश किंवा नकारात्मक संख्या समाविष्ट आहेत. Numbers arithmetic operators सोबत वापरले जाऊ शकतात, जे [पुढील विभागात](../../../../2-js-basics/1-data-types) कव्हर केले आहे.

### Arithmetic Operators

Arithmetic functions करताना वापरण्यासाठी अनेक प्रकारचे operators आहेत, त्यापैकी काही येथे दिले आहेत:

| Symbol | वर्णन                                                                  | उदाहरण                          |
| ------ | ---------------------------------------------------------------------- | -------------------------------- |
| `+`    | **जोडणी**: दोन संख्यांचा एकत्रित परिणाम काढतो                          | `1 + 2 // अपेक्षित उत्तर 3`     |
| `-`    | **वजाबाकी**: दोन संख्यांचा फरक काढतो                                   | `1 - 2 // अपेक्षित उत्तर -1`    |
| `*`    | **गुणाकार**: दोन संख्यांचा गुणाकार काढतो                               | `1 * 2 // अपेक्षित उत्तर 2`     |
| `/`    | **भागाकार**: दोन संख्यांचा भागाकार काढतो                               | `1 / 2 // अपेक्षित उत्तर 0.5`   |
| `%`    | **शेष**: दोन संख्यांच्या भागाकारातून शेष काढतो                         | `1 % 2 // अपेक्षित उत्तर 1`     |

✅ प्रयत्न करा! तुमच्या ब्राउझरच्या कन्सोलमध्ये एक arithmetic operation करून पहा. तुम्हाला परिणाम आश्चर्यकारक वाटतो का?

### Strings

Strings म्हणजे अक्षरांचा संच जो single किंवा double quotes मध्ये असतो.

- `'This is a string'`
- `"This is also a string"`
- `let myString = 'This is a string value stored in a variable';`

Strings लिहिताना quotes वापरणे लक्षात ठेवा, अन्यथा JavaScript त्याला variable चे नाव समजेल.

### Strings चे स्वरूपन

Strings मजकूरात्मक असतात आणि वेळोवेळी स्वरूपन आवश्यक असते.

दोन किंवा अधिक strings **concatenate** करण्यासाठी, किंवा त्यांना एकत्र जोडण्यासाठी, `+` ऑपरेटर वापरा.

```javascript
let myString1 = "Hello";
let myString2 = "World";

myString1 + myString2 + "!"; //HelloWorld!
myString1 + " " + myString2 + "!"; //Hello World!
myString1 + ", " + myString2 + "!"; //Hello, World!

```

✅ का `1 + 1 = 2` JavaScript मध्ये, पण `'1' + '1' = 11?` याचा विचार करा. `'1' + 1` बद्दल काय?

**Template literals** हे strings स्वरूपित करण्याचा आणखी एक मार्ग आहे, फक्त quotes ऐवजी backtick वापरला जातो. जे काही plain text नाही ते `${ }` placeholders मध्ये ठेवले पाहिजे. यामध्ये strings असलेले variables समाविष्ट आहेत.

```javascript
let myString1 = "Hello";
let myString2 = "World";

`${myString1} ${myString2}!` //Hello World!
`${myString1}, ${myString2}!` //Hello, World!
```

तुम्ही तुमच्या स्वरूपनाच्या उद्दिष्टांसाठी कोणताही पद्धत वापरू शकता, परंतु template literals spaces आणि line breaks आदर करतील.

✅ तुम्ही template literal कधी वापराल आणि plain string कधी वापराल?

### Booleans

Booleans फक्त दोन मूल्ये असू शकतात: `true` किंवा `false`. Booleans विशिष्ट अटी पूर्ण झाल्यावर कोणते कोड चालवायचे यावर निर्णय घेण्यास मदत करतात. अनेक वेळा, [operators](../../../../2-js-basics/1-data-types) Boolean चे मूल्य सेट करण्यात मदत करतात आणि तुम्ही variables initialized करताना किंवा त्यांचे मूल्य अपडेट करताना operators वापरत असल्याचे पाहाल.

- `let myTrueBool = true`
- `let myFalseBool = false`

✅ एखादे variable 'truthy' मानले जाऊ शकते जर ते Boolean `true` म्हणून मूल्यांकन केले गेले. आश्चर्यकारकपणे, JavaScript मध्ये [सर्व मूल्ये truthy असतात जोपर्यंत त्यांना falsy म्हणून परिभाषित केले जात नाही](https://developer.mozilla.org/docs/Glossary/Truthy).

---

## 🚀 आव्हान

JavaScript कधीकधी डेटा प्रकार हाताळण्याच्या आश्चर्यकारक पद्धतींसाठी कुप्रसिद्ध आहे. या 'gotchas' बद्दल थोडे संशोधन करा. उदाहरणार्थ: case sensitivity त्रास देऊ शकते! कन्सोलमध्ये हे करून पहा: `let age = 1; let Age = 2; age == Age` (याचा निकाल `false` लागतो -- का?). तुम्हाला आणखी कोणते gotchas सापडतात?

## व्याख्यानानंतरची प्रश्नमंजुषा
[व्याख्यानानंतरची प्रश्नमंजुषा](https://ff-quizzes.netlify.app)

## पुनरावलोकन आणि स्व-अभ्यास

[JavaScript सरावासाठी या यादीकडे](https://css-tricks.com/snippets/javascript/) पहा आणि एक प्रयत्न करा. तुम्ही काय शिकलात?

## असाइनमेंट

[डेटा प्रकार सराव](assignment.md)

---

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी कृपया लक्षात ठेवा की स्वयंचलित भाषांतरांमध्ये त्रुटी किंवा अचूकतेचा अभाव असू शकतो. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून निर्माण होणाऱ्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.