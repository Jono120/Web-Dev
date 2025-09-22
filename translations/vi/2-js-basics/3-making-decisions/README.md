<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f7009631b73556168ca435120a231c98",
  "translation_date": "2025-08-29T08:55:05+00:00",
  "source_file": "2-js-basics/3-making-decisions/README.md",
  "language_code": "vi"
}
-->
# Cơ bản về JavaScript: Ra quyết định

![Cơ bản về JavaScript - Ra quyết định](../../../../translated_images/webdev101-js-decisions.69e1b20f272dd1f0b1cb2f8adaff3ed2a77c4f91db96d8a0594132a353fa189a.vi.png)

> Sketchnote bởi [Tomomi Imura](https://twitter.com/girlie_mac)

## Câu hỏi trước bài giảng

[Câu hỏi trước bài giảng](https://ff-quizzes.netlify.app/web/quiz/11)

Việc ra quyết định và kiểm soát thứ tự chạy của mã giúp mã của bạn có thể tái sử dụng và mạnh mẽ hơn. Phần này sẽ đề cập đến cú pháp để kiểm soát luồng dữ liệu trong JavaScript và tầm quan trọng của nó khi sử dụng với kiểu dữ liệu Boolean.

[![Ra quyết định](https://img.youtube.com/vi/SxTp8j-fMMY/0.jpg)](https://youtube.com/watch?v=SxTp8j-fMMY "Ra quyết định")

> 🎥 Nhấp vào hình ảnh trên để xem video về việc ra quyết định.

> Bạn có thể học bài này trên [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-if-else/?WT.mc_id=academic-77807-sagibbon)!

## Tóm tắt ngắn gọn về Booleans

Booleans chỉ có thể có hai giá trị: `true` hoặc `false`. Booleans giúp đưa ra quyết định về dòng mã nào sẽ chạy khi các điều kiện nhất định được đáp ứng.

Đặt giá trị boolean của bạn là true hoặc false như sau:

`let myTrueBool = true`  
`let myFalseBool = false`

✅ Booleans được đặt tên theo nhà toán học, triết gia và nhà logic học người Anh George Boole (1815–1864).

## Toán tử so sánh và Booleans

Toán tử được sử dụng để đánh giá các điều kiện bằng cách so sánh, từ đó tạo ra giá trị Boolean. Dưới đây là danh sách các toán tử thường được sử dụng.

| Ký hiệu | Mô tả                                                                                                                                                   | Ví dụ               |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- |
| `<`     | **Nhỏ hơn**: So sánh hai giá trị và trả về kiểu dữ liệu Boolean `true` nếu giá trị bên trái nhỏ hơn giá trị bên phải                                     | `5 < 6 // true`     |
| `<=`    | **Nhỏ hơn hoặc bằng**: So sánh hai giá trị và trả về kiểu dữ liệu Boolean `true` nếu giá trị bên trái nhỏ hơn hoặc bằng giá trị bên phải                 | `5 <= 6 // true`    |
| `>`     | **Lớn hơn**: So sánh hai giá trị và trả về kiểu dữ liệu Boolean `true` nếu giá trị bên trái lớn hơn giá trị bên phải                                     | `5 > 6 // false`    |
| `>=`    | **Lớn hơn hoặc bằng**: So sánh hai giá trị và trả về kiểu dữ liệu Boolean `true` nếu giá trị bên trái lớn hơn hoặc bằng giá trị bên phải                 | `5 >= 6 // false`   |
| `===`   | **Bằng nghiêm ngặt**: So sánh hai giá trị và trả về kiểu dữ liệu Boolean `true` nếu giá trị bên trái và bên phải bằng nhau VÀ cùng kiểu dữ liệu          | `5 === 6 // false`  |
| `!==`   | **Không bằng**: So sánh hai giá trị và trả về giá trị Boolean ngược lại với kết quả của toán tử bằng nghiêm ngặt                                         | `5 !== 6 // true`   |

✅ Kiểm tra kiến thức của bạn bằng cách viết một số phép so sánh trong bảng điều khiển của trình duyệt. Có kết quả nào khiến bạn ngạc nhiên không?

## Câu lệnh If

Câu lệnh if sẽ chạy đoạn mã nằm giữa các khối của nó nếu điều kiện là true.

```javascript
if (condition) {
  //Condition is true. Code in this block will run.
}
```

Các toán tử logic thường được sử dụng để tạo điều kiện.

```javascript
let currentMoney;
let laptopPrice;

if (currentMoney >= laptopPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
}
```

## Câu lệnh If..Else

Câu lệnh `else` sẽ chạy đoạn mã nằm giữa các khối của nó khi điều kiện là false. Nó là tùy chọn khi sử dụng với câu lệnh `if`.

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

✅ Kiểm tra sự hiểu biết của bạn về đoạn mã này và đoạn mã sau bằng cách chạy nó trong bảng điều khiển trình duyệt. Thay đổi giá trị của các biến `currentMoney` và `laptopPrice` để thay đổi kết quả của `console.log()`.

## Câu lệnh Switch

Câu lệnh `switch` được sử dụng để thực hiện các hành động khác nhau dựa trên các điều kiện khác nhau. Sử dụng câu lệnh `switch` để chọn một trong nhiều khối mã cần thực thi.

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

✅ Kiểm tra sự hiểu biết của bạn về đoạn mã này và đoạn mã sau bằng cách chạy nó trong bảng điều khiển trình duyệt. Thay đổi giá trị của biến `a` để thay đổi kết quả của `console.log()`.

## Toán tử logic và Booleans

Các quyết định có thể yêu cầu nhiều hơn một phép so sánh và có thể được kết hợp với các toán tử logic để tạo ra giá trị Boolean.

| Ký hiệu | Mô tả                                                                                     | Ví dụ                                                                  |
| ------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `&&`    | **Logic AND**: So sánh hai biểu thức Boolean. Trả về true **chỉ khi** cả hai bên đều true | `(5 > 6) && (5 < 6 ) // Một bên false, bên kia true. Trả về false`     |
| `\|\|`  | **Logic OR**: So sánh hai biểu thức Boolean. Trả về true nếu ít nhất một bên là true      | `(5 > 6) \|\| (5 < 6) // Một bên false, bên kia true. Trả về true`     |
| `!`     | **Logic NOT**: Trả về giá trị ngược lại của một biểu thức Boolean                         | `!(5 > 6) // 5 không lớn hơn 6, nhưng "!" sẽ trả về true`              |

## Điều kiện và quyết định với toán tử logic

Toán tử logic có thể được sử dụng để tạo điều kiện trong các câu lệnh if..else.

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

### Toán tử phủ định

Bạn đã thấy cách sử dụng câu lệnh `if...else` để tạo logic điều kiện. Bất kỳ điều gì trong `if` cần được đánh giá là true/false. Bằng cách sử dụng toán tử `!`, bạn có thể _phủ định_ biểu thức. Nó sẽ trông như sau:

```javascript
if (!condition) {
  // runs if condition is false
} else {
  // runs if condition is true
}
```

### Biểu thức ba ngôi

`if...else` không phải là cách duy nhất để biểu diễn logic quyết định. Bạn cũng có thể sử dụng một thứ gọi là toán tử ba ngôi. Cú pháp của nó như sau:

```javascript
let variable = condition ? <return this if true> : <return this if false>
```

Dưới đây là một ví dụ cụ thể hơn:

```javascript
let firstNumber = 20;
let secondNumber = 10;
let biggestNumber = firstNumber > secondNumber ? firstNumber : secondNumber;
```

✅ Dành một phút để đọc đoạn mã này vài lần. Bạn có hiểu cách các toán tử này hoạt động không?

Đoạn mã trên nói rằng:

- nếu `firstNumber` lớn hơn `secondNumber`
- thì gán `firstNumber` cho `biggestNumber`
- ngược lại gán `secondNumber`.

Biểu thức ba ngôi chỉ là một cách viết gọn của đoạn mã dưới đây:

```javascript
let biggestNumber;
if (firstNumber > secondNumber) {
  biggestNumber = firstNumber;
} else {
  biggestNumber = secondNumber;
}
```

---

## 🚀 Thử thách

Tạo một chương trình được viết trước tiên với các toán tử logic, sau đó viết lại nó bằng biểu thức ba ngôi. Bạn thích cú pháp nào hơn?

---

## Câu hỏi sau bài giảng

[Câu hỏi sau bài giảng](https://ff-quizzes.netlify.app/web/quiz/12)

## Ôn tập & Tự học

Đọc thêm về nhiều toán tử có sẵn cho người dùng [trên MDN](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators).

Xem qua công cụ tra cứu toán tử tuyệt vời của Josh Comeau [operator lookup](https://joshwcomeau.com/operator-lookup/)!

## Bài tập

[Toán tử](assignment.md)

---

**Tuyên bố miễn trừ trách nhiệm**:  
Tài liệu này đã được dịch bằng dịch vụ dịch thuật AI [Co-op Translator](https://github.com/Azure/co-op-translator). Mặc dù chúng tôi cố gắng đảm bảo độ chính xác, xin lưu ý rằng các bản dịch tự động có thể chứa lỗi hoặc không chính xác. Tài liệu gốc bằng ngôn ngữ bản địa nên được coi là nguồn tham khảo chính thức. Đối với các thông tin quan trọng, nên sử dụng dịch vụ dịch thuật chuyên nghiệp từ con người. Chúng tôi không chịu trách nhiệm cho bất kỳ sự hiểu lầm hoặc diễn giải sai nào phát sinh từ việc sử dụng bản dịch này.