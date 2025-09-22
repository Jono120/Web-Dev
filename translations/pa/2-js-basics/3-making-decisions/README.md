<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f7009631b73556168ca435120a231c98",
  "translation_date": "2025-08-28T17:06:23+00:00",
  "source_file": "2-js-basics/3-making-decisions/README.md",
  "language_code": "pa"
}
-->
# ਜਾਵਾਸਕ੍ਰਿਪਟ ਬੁਨਿਆਦੀਆਂ: ਫੈਸਲੇ ਲੈਣਾ

![ਜਾਵਾਸਕ੍ਰਿਪਟ ਬੁਨਿਆਦੀਆਂ - ਫੈਸਲੇ ਲੈਣਾ](../../../../translated_images/webdev101-js-decisions.69e1b20f272dd1f0b1cb2f8adaff3ed2a77c4f91db96d8a0594132a353fa189a.pa.png)

> ਸਕੈਚਨੋਟ [Tomomi Imura](https://twitter.com/girlie_mac) ਵੱਲੋਂ

## ਲੈਕਚਰ ਤੋਂ ਪਹਿਲਾਂ ਕਵਿਜ਼

[ਲੈਕਚਰ ਤੋਂ ਪਹਿਲਾਂ ਕਵਿਜ਼](https://ff-quizzes.netlify.app/web/quiz/11)

ਫੈਸਲੇ ਲੈਣ ਅਤੇ ਆਪਣੇ ਕੋਡ ਦੇ ਚਲਣ ਦੇ ਕ੍ਰਮ ਨੂੰ ਨਿਯੰਤਰਿਤ ਕਰਨਾ ਤੁਹਾਡੇ ਕੋਡ ਨੂੰ ਦੁਬਾਰਾ ਵਰਤਣਯੋਗ ਅਤੇ ਮਜ਼ਬੂਤ ਬਣਾਉਂਦਾ ਹੈ। ਇਸ ਭਾਗ ਵਿੱਚ ਜਾਵਾਸਕ੍ਰਿਪਟ ਵਿੱਚ ਡਾਟਾ ਫਲੋ ਨੂੰ ਨਿਯੰਤਰਿਤ ਕਰਨ ਲਈ ਵਰਤੀ ਜਾਣ ਵਾਲੀ ਸਿੰਟੈਕਸ ਅਤੇ ਬੂਲੀਅਨ ਡਾਟਾ ਟਾਈਪਸ ਨਾਲ ਇਸਦੀ ਮਹੱਤਤਾ ਨੂੰ ਕਵਰ ਕੀਤਾ ਗਿਆ ਹੈ।

[![ਫੈਸਲੇ ਲੈਣਾ](https://img.youtube.com/vi/SxTp8j-fMMY/0.jpg)](https://youtube.com/watch?v=SxTp8j-fMMY "ਫੈਸਲੇ ਲੈਣਾ")

> 🎥 ਉਪਰ ਦਿੱਤੀ ਤਸਵੀਰ 'ਤੇ ਕਲਿਕ ਕਰੋ ਫੈਸਲੇ ਲੈਣ ਬਾਰੇ ਵੀਡੀਓ ਦੇਖਣ ਲਈ।

> ਤੁਸੀਂ ਇਹ ਪਾਠ [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-if-else/?WT.mc_id=academic-77807-sagibbon) 'ਤੇ ਲੈ ਸਕਦੇ ਹੋ!

## ਬੂਲੀਅਨਸ 'ਤੇ ਛੋਟਾ ਜਿਹਾ ਪੁਰਾਲੇਖ

ਬੂਲੀਅਨਸ ਸਿਰਫ ਦੋ ਮੁੱਲਾਂ ਹੋ ਸਕਦੇ ਹਨ: `true` ਜਾਂ `false`। ਬੂਲੀਅਨਸ ਇਹ ਫੈਸਲਾ ਕਰਨ ਵਿੱਚ ਮਦਦ ਕਰਦੇ ਹਨ ਕਿ ਜਦੋਂ ਕੁਝ ਸ਼ਰਤਾਂ ਪੂਰੀਆਂ ਹੁੰਦੀਆਂ ਹਨ ਤਾਂ ਕਿਹੜੀਆਂ ਲਾਈਨਾਂ ਚਲਣੀਆਂ ਚਾਹੀਦੀਆਂ ਹਨ।

ਆਪਣੇ ਬੂਲੀਅਨ ਨੂੰ ਇਸ ਤਰ੍ਹਾਂ true ਜਾਂ false ਸੈਟ ਕਰੋ:

`let myTrueBool = true`  
`let myFalseBool = false`

✅ ਬੂਲੀਅਨਸ ਦਾ ਨਾਮ ਅੰਗਰੇਜ਼ ਗਣਿਤਜ, ਦਰਸ਼ਨਸ਼ਾਸਤਰੀ ਅਤੇ ਤਰਕਸ਼ਾਸਤਰੀ George Boole (1815–1864) ਦੇ ਨਾਮ 'ਤੇ ਰੱਖਿਆ ਗਿਆ ਹੈ।

## ਤੁਲਨਾ ਆਪਰੇਟਰ ਅਤੇ ਬੂਲੀਅਨਸ

ਆਪਰੇਟਰ ਸ਼ਰਤਾਂ ਦਾ ਮੁਲਾਂਕਣ ਕਰਨ ਲਈ ਵਰਤੇ ਜਾਂਦੇ ਹਨ, ਜੋ ਤੁਲਨਾਵਾਂ ਕਰਕੇ ਬੂਲੀਅਨ ਮੁੱਲ ਬਣਾਉਂਦੇ ਹਨ। ਹੇਠਾਂ ਉਹ ਆਪਰੇਟਰ ਦਿੱਤੇ ਗਏ ਹਨ ਜੋ ਅਕਸਰ ਵਰਤੇ ਜਾਂਦੇ ਹਨ।

| ਚਿੰਨ੍ਹ | ਵੇਰਵਾ                                                                                                                                                   | ਉਦਾਹਰਨ            |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| `<`    | **ਘੱਟ**: ਦੋ ਮੁੱਲਾਂ ਦੀ ਤੁਲਨਾ ਕਰਦਾ ਹੈ ਅਤੇ `true` ਬੂਲੀਅਨ ਡਾਟਾ ਟਾਈਪ ਵਾਪਸ ਕਰਦਾ ਹੈ ਜੇ ਖੱਬੇ ਪਾਸੇ ਵਾਲਾ ਮੁੱਲ ਸੱਜੇ ਪਾਸੇ ਵਾਲੇ ਮੁੱਲ ਤੋਂ ਘੱਟ ਹੈ।                  | `5 < 6 // true`    |
| `<=`   | **ਘੱਟ ਜਾਂ ਬਰਾਬਰ**: ਦੋ ਮੁੱਲਾਂ ਦੀ ਤੁਲਨਾ ਕਰਦਾ ਹੈ ਅਤੇ `true` ਬੂਲੀਅਨ ਡਾਟਾ ਟਾਈਪ ਵਾਪਸ ਕਰਦਾ ਹੈ ਜੇ ਖੱਬੇ ਪਾਸੇ ਵਾਲਾ ਮੁੱਲ ਸੱਜੇ ਪਾਸੇ ਵਾਲੇ ਮੁੱਲ ਤੋਂ ਘੱਟ ਜਾਂ ਬਰਾਬਰ ਹੈ। | `5 <= 6 // true`   |
| `>`    | **ਵੱਧ**: ਦੋ ਮੁੱਲਾਂ ਦੀ ਤੁਲਨਾ ਕਰਦਾ ਹੈ ਅਤੇ `true` ਬੂਲੀਅਨ ਡਾਟਾ ਟਾਈਪ ਵਾਪਸ ਕਰਦਾ ਹੈ ਜੇ ਖੱਬੇ ਪਾਸੇ ਵਾਲਾ ਮੁੱਲ ਸੱਜੇ ਪਾਸੇ ਵਾਲੇ ਮੁੱਲ ਤੋਂ ਵੱਧ ਹੈ।                 | `5 > 6 // false`   |
| `>=`   | **ਵੱਧ ਜਾਂ ਬਰਾਬਰ**: ਦੋ ਮੁੱਲਾਂ ਦੀ ਤੁਲਨਾ ਕਰਦਾ ਹੈ ਅਤੇ `true` ਬੂਲੀਅਨ ਡਾਟਾ ਟਾਈਪ ਵਾਪਸ ਕਰਦਾ ਹੈ ਜੇ ਖੱਬੇ ਪਾਸੇ ਵਾਲਾ ਮੁੱਲ ਸੱਜੇ ਪਾਸੇ ਵਾਲੇ ਮੁੱਲ ਤੋਂ ਵੱਧ ਜਾਂ ਬਰਾਬਰ ਹੈ। | `5 >= 6 // false`  |
| `===`  | **ਸਖ਼ਤ ਸਮਾਨਤਾ**: ਦੋ ਮੁੱਲਾਂ ਦੀ ਤੁਲਨਾ ਕਰਦਾ ਹੈ ਅਤੇ `true` ਬੂਲੀਅਨ ਡਾਟਾ ਟਾਈਪ ਵਾਪਸ ਕਰਦਾ ਹੈ ਜੇ ਖੱਬੇ ਅਤੇ ਸੱਜੇ ਪਾਸੇ ਵਾਲੇ ਮੁੱਲ ਸਮਾਨ ਹਨ ਅਤੇ ਇੱਕੋ ਡਾਟਾ ਟਾਈਪ ਦੇ ਹਨ। | `5 === 6 // false` |
| `!==`  | **ਅਸਮਾਨਤਾ**: ਦੋ ਮੁੱਲਾਂ ਦੀ ਤੁਲਨਾ ਕਰਦਾ ਹੈ ਅਤੇ ਉਹ ਬੂਲੀਅਨ ਮੁੱਲ ਵਾਪਸ ਕਰਦਾ ਹੈ ਜੋ ਸਖ਼ਤ ਸਮਾਨਤਾ ਆਪਰੇਟਰ ਵਾਪਸ ਨਹੀਂ ਕਰਦਾ।                                      | `5 !== 6 // true`  |

✅ ਆਪਣੇ ਬ੍ਰਾਊਜ਼ਰ ਦੇ ਕਨਸੋਲ ਵਿੱਚ ਕੁਝ ਤੁਲਨਾਵਾਂ ਲਿਖ ਕੇ ਆਪਣਾ ਗਿਆਨ ਜਾਂਚੋ। ਕੀ ਕੋਈ ਵਾਪਸ ਆਇਆ ਡਾਟਾ ਤੁਹਾਨੂੰ ਹੈਰਾਨ ਕਰਦਾ ਹੈ?

## If ਸਟੇਟਮੈਂਟ

If ਸਟੇਟਮੈਂਟ ਆਪਣੇ ਬਲਾਕਾਂ ਵਿੱਚ ਕੋਡ ਚਲਾਏਗਾ ਜੇ ਸ਼ਰਤ true ਹੈ।

```javascript
if (condition) {
  //Condition is true. Code in this block will run.
}
```

ਲੌਜਿਕਲ ਆਪਰੇਟਰ ਅਕਸਰ ਸ਼ਰਤ ਬਣਾਉਣ ਲਈ ਵਰਤੇ ਜਾਂਦੇ ਹਨ।

```javascript
let currentMoney;
let laptopPrice;

if (currentMoney >= laptopPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
}
```

## If..Else ਸਟੇਟਮੈਂਟ

`else` ਸਟੇਟਮੈਂਟ ਆਪਣੇ ਬਲਾਕਾਂ ਵਿੱਚ ਕੋਡ ਚਲਾਏਗਾ ਜਦੋਂ ਸ਼ਰਤ false ਹੋਵੇ। ਇਹ `if` ਸਟੇਟਮੈਂਟ ਨਾਲ ਵਿਕਲਪਿਕ ਹੈ।

```javascript
let currentMoney;
let laptopPrice;

if (currentMoney >= laptopPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
} else {
  //Condition is false. Code in this block will run.
  console.log("Can't afford a new laptop, yet!");
}
```

✅ ਇਸ ਕੋਡ ਅਤੇ ਹੇਠਾਂ ਦਿੱਤੇ ਕੋਡ ਨੂੰ ਬ੍ਰਾਊਜ਼ਰ ਕਨਸੋਲ ਵਿੱਚ ਚਲਾ ਕੇ ਆਪਣੀ ਸਮਝ ਦੀ ਜਾਂਚ ਕਰੋ। `currentMoney` ਅਤੇ `laptopPrice` ਵੈਰੀਏਬਲ ਦੇ ਮੁੱਲਾਂ ਨੂੰ ਬਦਲੋ ਤਾਂ ਜੋ ਵਾਪਸ ਆਇਆ `console.log()` ਬਦਲ ਜਾਵੇ।

## Switch ਸਟੇਟਮੈਂਟ

`switch` ਸਟੇਟਮੈਂਟ ਵੱਖ-ਵੱਖ ਸ਼ਰਤਾਂ ਦੇ ਅਧਾਰ 'ਤੇ ਵੱਖ-ਵੱਖ ਕਾਰਵਾਈਆਂ ਕਰਨ ਲਈ ਵਰਤੀ ਜਾਂਦੀ ਹੈ। `switch` ਸਟੇਟਮੈਂਟ ਨੂੰ ਵਰਤ ਕੇ ਚਲਾਉਣ ਲਈ ਬਹੁਤ ਸਾਰੇ ਕੋਡ ਬਲਾਕਾਂ ਵਿੱਚੋਂ ਇੱਕ ਚੁਣੋ।

```javascript
switch (expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
  // code block
}
```

```javascript
// program using switch statement
let a = 2;

switch (a) {
  case 1:
    a = "one";
    break;
  case 2:
    a = "two";
    break;
  default:
    a = "not found";
    break;
}
console.log(`The value is ${a}`);
```

✅ ਇਸ ਕੋਡ ਅਤੇ ਹੇਠਾਂ ਦਿੱਤੇ ਕੋਡ ਨੂੰ ਬ੍ਰਾਊਜ਼ਰ ਕਨਸੋਲ ਵਿੱਚ ਚਲਾ ਕੇ ਆਪਣੀ ਸਮਝ ਦੀ ਜਾਂਚ ਕਰੋ। ਵੈਰੀਏਬਲ `a` ਦੇ ਮੁੱਲਾਂ ਨੂੰ ਬਦਲੋ ਤਾਂ ਜੋ ਵਾਪਸ ਆਇਆ `console.log()` ਬਦਲ ਜਾਵੇ।

## ਲੌਜਿਕਲ ਆਪਰੇਟਰ ਅਤੇ ਬੂਲੀਅਨਸ

ਫੈਸਲੇ ਲਈ ਕਈ ਵਾਰ ਇੱਕ ਤੋਂ ਵੱਧ ਤੁਲਨਾਵਾਂ ਦੀ ਲੋੜ ਹੋ ਸਕਦੀ ਹੈ, ਅਤੇ ਇਹਨਾਂ ਨੂੰ ਲੌਜਿਕਲ ਆਪਰੇਟਰਾਂ ਨਾਲ ਜੋੜ ਕੇ ਬੂਲੀਅਨ ਮੁੱਲ ਬਣਾਇਆ ਜਾ ਸਕਦਾ ਹੈ।

| ਚਿੰਨ੍ਹ | ਵੇਰਵਾ                                                                                     | ਉਦਾਹਰਨ                                                                 |
| ------ | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `&&`   | **ਲੌਜਿਕਲ AND**: ਦੋ ਬੂਲੀਅਨ ਅਭਿਵਿਆਦੀਆਂ ਦੀ ਤੁਲਨਾ ਕਰਦਾ ਹੈ। ਸਿਰਫ ਉਸੇ ਹਾਲਤ ਵਿੱਚ true ਵਾਪਸ ਕਰਦਾ ਹੈ ਜੇ ਦੋਵੇਂ ਪਾਸੇ true ਹਨ। | `(5 > 6) && (5 < 6 ) //ਇੱਕ ਪਾਸੇ false ਹੈ, ਦੂਜਾ true ਹੈ। false ਵਾਪਸ ਕਰਦਾ ਹੈ।` |
| `\|\|` | **ਲੌਜਿਕਲ OR**: ਦੋ ਬੂਲੀਅਨ ਅਭਿਵਿਆਦੀਆਂ ਦੀ ਤੁਲਨਾ ਕਰਦਾ ਹੈ। true ਵਾਪਸ ਕਰਦਾ ਹੈ ਜੇ ਘੱਟੋ-ਘੱਟ ਇੱਕ ਪਾਸੇ true ਹੈ।     | `(5 > 6) \|\| (5 < 6) //ਇੱਕ ਪਾਸੇ false ਹੈ, ਦੂਜਾ true ਹੈ। true ਵਾਪਸ ਕਰਦਾ ਹੈ।` |
| `!`    | **ਲੌਜਿਕਲ NOT**: ਬੂਲੀਅਨ ਅਭਿਵਿਆਦੀਆਂ ਦਾ ਉਲਟਾ ਮੁੱਲ ਵਾਪਸ ਕਰਦਾ ਹੈ।                             | `!(5 > 6) // 5 6 ਤੋਂ ਵੱਧ ਨਹੀਂ ਹੈ, ਪਰ "!" true ਵਾਪਸ ਕਰੇਗਾ।`         |

## ਲੌਜਿਕਲ ਆਪਰੇਟਰਾਂ ਨਾਲ ਸ਼ਰਤਾਂ ਅਤੇ ਫੈਸਲੇ

ਲੌਜਿਕਲ ਆਪਰੇਟਰਾਂ ਨੂੰ if..else ਸਟੇਟਮੈਂਟ ਵਿੱਚ ਸ਼ਰਤਾਂ ਬਣਾਉਣ ਲਈ ਵਰਤਿਆ ਜਾ ਸਕਦਾ ਹੈ।

```javascript
let currentMoney;
let laptopPrice;
let laptopDiscountPrice = laptopPrice - laptopPrice * 0.2; //Laptop price at 20 percent off

if (currentMoney >= laptopPrice || currentMoney >= laptopDiscountPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
} else {
  //Condition is true. Code in this block will run.
  console.log("Can't afford a new laptop, yet!");
}
```

### ਨੈਗੇਸ਼ਨ ਆਪਰੇਟਰ

ਤੁਸੀਂ ਹੁਣ ਤੱਕ ਦੇਖਿਆ ਹੈ ਕਿ ਤੁਸੀਂ `if...else` ਸਟੇਟਮੈਂਟ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਸ਼ਰਤਮੁਕਤ ਤਰਕਸ਼ੀਲਤਾ ਕਿਵੇਂ ਬਣਾਉਣੀ ਹੈ। ਜੋ ਕੁਝ ਵੀ `if` ਵਿੱਚ ਜਾਂਦਾ ਹੈ ਉਸਨੂੰ true/false ਵਿੱਚ ਮੁਲਾਂਕਣ ਕੀਤਾ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। `!` ਆਪਰੇਟਰ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਤੁਸੀਂ ਅਭਿਵਿਆਦਨਾ ਨੂੰ _ਨੈਗੇਟ_ ਕਰ ਸਕਦੇ ਹੋ। ਇਹ ਇਸ ਤਰ੍ਹਾਂ ਲੱਗੇਗਾ:

```javascript
if (!condition) {
  // runs if condition is false
} else {
  // runs if condition is true
}
```

### ਟਰਨਰੀ ਅਭਿਵਿਆਦਨਾਵਾਂ

`if...else` ਫੈਸਲੇ ਦੀ ਤਰਕਸ਼ੀਲਤਾ ਨੂੰ ਪ੍ਰਗਟ ਕਰਨ ਦਾ ਇੱਕੋ ਇਕ ਤਰੀਕਾ ਨਹੀਂ ਹੈ। ਤੁਸੀਂ ਕੁਝ ਐਸਾ ਵਰਤ ਸਕਦੇ ਹੋ ਜਿਸਨੂੰ ਟਰਨਰੀ ਆਪਰੇਟਰ ਕਿਹਾ ਜਾਂਦਾ ਹੈ। ਇਸਦਾ ਸਿੰਟੈਕਸ ਇਸ ਤਰ੍ਹਾਂ ਲੱਗਦਾ ਹੈ:

```javascript
let variable = condition ? <return this if true> : <return this if false>
```

ਹੇਠਾਂ ਇੱਕ ਹੋਰ ਵਾਸਤਵਿਕ ਉਦਾਹਰਨ ਦਿੱਤੀ ਗਈ ਹੈ:

```javascript
let firstNumber = 20;
let secondNumber = 10;
let biggestNumber = firstNumber > secondNumber ? firstNumber : secondNumber;
```

✅ ਇਸ ਕੋਡ ਨੂੰ ਕੁਝ ਵਾਰ ਪੜ੍ਹਨ ਲਈ ਇੱਕ ਮਿੰਟ ਲਓ। ਕੀ ਤੁਸੀਂ ਸਮਝਦੇ ਹੋ ਕਿ ਇਹ ਆਪਰੇਟਰ ਕਿਵੇਂ ਕੰਮ ਕਰ ਰਹੇ ਹਨ?

ਉਪਰ ਦਿੱਤਾ ਗਿਆ ਹੈ:

- ਜੇ `firstNumber` `secondNumber` ਤੋਂ ਵੱਡਾ ਹੈ
- ਤਾਂ `firstNumber` ਨੂੰ `biggestNumber` ਵਿੱਚ ਅਸਾਈਨ ਕਰੋ
- ਨਹੀਂ ਤਾਂ `secondNumber` ਨੂੰ ਅਸਾਈਨ ਕਰੋ।

ਟਰਨਰੀ ਅਭਿਵਿਆਦਨਾ ਹੇਠਾਂ ਦਿੱਤੇ ਕੋਡ ਨੂੰ ਲਿਖਣ ਦਾ ਸਿਰਫ ਇੱਕ ਸੰਕੁਚਿਤ ਤਰੀਕਾ ਹੈ:

```javascript
let biggestNumber;
if (firstNumber > secondNumber) {
  biggestNumber = firstNumber;
} else {
  biggestNumber = secondNumber;
}
```

---

## 🚀 ਚੁਣੌਤੀ

ਇੱਕ ਪ੍ਰੋਗਰਾਮ ਬਣਾਓ ਜੋ ਪਹਿਲਾਂ ਲੌਜਿਕਲ ਆਪਰੇਟਰਾਂ ਨਾਲ ਲਿਖਿਆ ਗਿਆ ਹੋਵੇ, ਅਤੇ ਫਿਰ ਇਸਨੂੰ ਟਰਨਰੀ ਅਭਿਵਿਆਦਨਾ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਦੁਬਾਰਾ ਲਿਖੋ। ਤੁਹਾਡਾ ਪਸੰਦੀਦਾ ਸਿੰਟੈਕਸ ਕਿਹੜਾ ਹੈ?

---

## ਲੈਕਚਰ ਤੋਂ ਬਾਅਦ ਕਵਿਜ਼

[ਲੈਕਚਰ ਤੋਂ ਬਾਅਦ ਕਵਿਜ਼](https://ff-quizzes.netlify.app/web/quiz/12)

## ਸਮੀਖਿਆ ਅਤੇ ਸਵੈ ਅਧਿਐਨ

ਉਪਲਬਧ ਬਹੁਤ ਸਾਰੇ ਆਪਰੇਟਰਾਂ ਬਾਰੇ ਹੋਰ ਪੜ੍ਹੋ [MDN 'ਤੇ](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators)।

Josh Comeau ਦਾ ਸ਼ਾਨਦਾਰ [operator lookup](https://joshwcomeau.com/operator-lookup/) ਦੇਖੋ!

## ਅਸਾਈਨਮੈਂਟ

[ਆਪਰੇਟਰ](assignment.md)

---

**ਅਸਵੀਕਰਤੀ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀ ਹੋਣ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰਦੇ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚੱਜੇਪਣ ਹੋ ਸਕਦੇ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼, ਜੋ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਹੈ, ਨੂੰ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।