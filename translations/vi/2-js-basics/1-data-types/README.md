<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "b95fdd8310ef467305015ece1b0f9411",
  "translation_date": "2025-08-29T08:56:10+00:00",
  "source_file": "2-js-basics/1-data-types/README.md",
  "language_code": "vi"
}
-->
# JavaScript Cơ Bản: Kiểu Dữ Liệu

![JavaScript Basics - Data types](../../../../translated_images/webdev101-js-datatypes.4cc470179730702c756480d3ffa46507f746e5975ebf80f99fdaaf1cff09a7f4.vi.png)
> Sketchnote bởi [Tomomi Imura](https://twitter.com/girlie_mac)

## Câu Hỏi Trước Bài Giảng
[Câu hỏi trước bài giảng](https://ff-quizzes.netlify.app/web/)

Bài học này giới thiệu những kiến thức cơ bản về JavaScript, ngôn ngữ mang lại tính tương tác cho web.

> Bạn có thể học bài này trên [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-variables/?WT.mc_id=academic-77807-sagibbon)!

[![Variables](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Variables in JavaScript")

[![Data Types in JavaScript](https://img.youtube.com/vi/AWfA95eLdq8/0.jpg)](https://youtube.com/watch?v=AWfA95eLdq8 "Data Types in JavaScript")

> 🎥 Nhấn vào hình ảnh trên để xem video về biến và kiểu dữ liệu

Hãy bắt đầu với biến và các kiểu dữ liệu mà chúng chứa!

## Biến

Biến lưu trữ giá trị có thể được sử dụng và thay đổi trong suốt mã của bạn.

Việc tạo và **khai báo** một biến có cú pháp như sau **[keyword] [name]**. Nó bao gồm hai phần:

- **Từ khóa**. Từ khóa có thể là `let` hoặc `var`.  

✅ Từ khóa `let` được giới thiệu trong ES6 và mang lại cho biến một cái gọi là _phạm vi khối_. Nên sử dụng `let` thay vì `var`. Chúng ta sẽ tìm hiểu sâu hơn về phạm vi khối trong các phần sau.

- **Tên biến**, đây là tên bạn tự chọn.

### Bài Tập - Làm việc với biến

1. **Khai báo một biến**. Hãy khai báo một biến sử dụng từ khóa `let`:

    ```javascript
    let myVariable;
    ```

   `myVariable` đã được khai báo bằng từ khóa `let`. Hiện tại nó chưa có giá trị.

1. **Gán giá trị**. Lưu trữ một giá trị vào biến bằng toán tử `=` theo sau là giá trị mong muốn.

    ```javascript
    myVariable = 123;
    ```

   > Lưu ý: việc sử dụng `=` trong bài học này có nghĩa là chúng ta sử dụng "toán tử gán", dùng để đặt giá trị cho biến. Nó không biểu thị sự bằng nhau.

   `myVariable` đã được *khởi tạo* với giá trị 123.

1. **Tái cấu trúc**. Thay thế mã của bạn bằng câu lệnh sau.

    ```javascript
    let myVariable = 123;
    ```

    Câu lệnh trên được gọi là _khởi tạo rõ ràng_ khi một biến được khai báo và được gán giá trị cùng lúc.

1. **Thay đổi giá trị của biến**. Thay đổi giá trị của biến theo cách sau:

   ```javascript
   myVariable = 321;
   ```

   Sau khi một biến được khai báo, bạn có thể thay đổi giá trị của nó bất cứ lúc nào trong mã của bạn bằng toán tử `=` và giá trị mới.

   ✅ Thử ngay! Bạn có thể viết JavaScript trực tiếp trong trình duyệt của mình. Mở cửa sổ trình duyệt và điều hướng đến Công cụ dành cho nhà phát triển. Trong bảng điều khiển, bạn sẽ thấy một lời nhắc; nhập `let myVariable = 123`, nhấn Enter, sau đó nhập `myVariable`. Điều gì xảy ra? Lưu ý, bạn sẽ học thêm về các khái niệm này trong các bài học tiếp theo.

## Hằng Số

Việc khai báo và khởi tạo một hằng số tuân theo các nguyên tắc giống như biến, ngoại trừ từ khóa `const`. Hằng số thường được khai báo bằng chữ cái viết hoa.

```javascript
const MY_VARIABLE = 123;
```

Hằng số tương tự như biến, với hai ngoại lệ:

- **Phải có giá trị**. Hằng số phải được khởi tạo, nếu không sẽ xảy ra lỗi khi chạy mã.
- **Tham chiếu không thể thay đổi**. Tham chiếu của một hằng số không thể thay đổi sau khi khởi tạo, nếu không sẽ xảy ra lỗi khi chạy mã. Hãy xem hai ví dụ sau:
   - **Giá trị đơn giản**. Điều sau đây KHÔNG được phép:
   
      ```javascript
      const PI = 3;
      PI = 4; // not allowed
      ```
 
   - **Tham chiếu đối tượng được bảo vệ**. Điều sau đây KHÔNG được phép.
   
      ```javascript
      const obj = { a: 3 };
      obj = { b: 5 } // not allowed
      ```

    - **Giá trị đối tượng không được bảo vệ**. Điều sau đây ĐƯỢC phép:
    
      ```javascript
      const obj = { a: 3 };
      obj.a = 5;  // allowed
      ```

      Ở trên, bạn đang thay đổi giá trị của đối tượng nhưng không phải tham chiếu của nó, điều này được phép.

   > Lưu ý, một `const` có nghĩa là tham chiếu được bảo vệ khỏi việc gán lại. Tuy nhiên, giá trị không phải là _bất biến_ và có thể thay đổi, đặc biệt nếu nó là một cấu trúc phức tạp như một đối tượng.

## Kiểu Dữ Liệu

Biến có thể lưu trữ nhiều loại giá trị khác nhau, như số và văn bản. Những loại giá trị khác nhau này được gọi là **kiểu dữ liệu**. Kiểu dữ liệu là một phần quan trọng trong phát triển phần mềm vì nó giúp lập trình viên đưa ra quyết định về cách viết mã và cách phần mềm hoạt động. Hơn nữa, một số kiểu dữ liệu có các tính năng đặc biệt giúp chuyển đổi hoặc trích xuất thông tin bổ sung từ một giá trị.

✅ Kiểu dữ liệu cũng được gọi là các nguyên thủy dữ liệu của JavaScript, vì chúng là các kiểu dữ liệu cấp thấp nhất được cung cấp bởi ngôn ngữ. Có 7 kiểu dữ liệu nguyên thủy: string, number, bigint, boolean, undefined, null và symbol. Dành một chút thời gian để hình dung mỗi nguyên thủy này đại diện cho điều gì. `zebra` là gì? Còn `0` thì sao? `true`?

### Số

Trong phần trước, giá trị của `myVariable` là một kiểu dữ liệu số.

`let myVariable = 123;`

Biến có thể lưu trữ tất cả các loại số, bao gồm số thập phân hoặc số âm. Số cũng có thể được sử dụng với các toán tử số học, được đề cập trong [phần tiếp theo](../../../../2-js-basics/1-data-types).

### Toán Tử Số Học

Có một số loại toán tử để sử dụng khi thực hiện các chức năng số học, và một số được liệt kê dưới đây:

| Ký Hiệu | Mô Tả                                                                   | Ví Dụ                           |
| ------- | ----------------------------------------------------------------------- | -------------------------------- |
| `+`     | **Cộng**: Tính tổng của hai số                                          | `1 + 2 //kết quả mong đợi là 3`  |
| `-`     | **Trừ**: Tính hiệu của hai số                                          | `1 - 2 //kết quả mong đợi là -1` |
| `*`     | **Nhân**: Tính tích của hai số                                         | `1 * 2 //kết quả mong đợi là 2`  |
| `/`     | **Chia**: Tính thương của hai số                                       | `1 / 2 //kết quả mong đợi là 0.5`|
| `%`     | **Phần Dư**: Tính phần dư từ phép chia của hai số                      | `1 % 2 //kết quả mong đợi là 1`  |

✅ Thử ngay! Thử một phép toán số học trong bảng điều khiển của trình duyệt. Kết quả có làm bạn ngạc nhiên không?

### Chuỗi

Chuỗi là tập hợp các ký tự nằm giữa dấu nháy đơn hoặc nháy kép.

- `'Đây là một chuỗi'`
- `"Đây cũng là một chuỗi"`
- `let myString = 'Đây là giá trị chuỗi được lưu trong một biến';`

Hãy nhớ sử dụng dấu nháy khi viết chuỗi, nếu không JavaScript sẽ cho rằng đó là tên biến.

### Định Dạng Chuỗi

Chuỗi là dạng văn bản và sẽ cần định dạng theo thời gian.

Để **nối** hai hoặc nhiều chuỗi, hoặc ghép chúng lại với nhau, sử dụng toán tử `+`.

```javascript
let myString1 = "Hello";
let myString2 = "World";

myString1 + myString2 + "!"; //HelloWorld!
myString1 + " " + myString2 + "!"; //Hello World!
myString1 + ", " + myString2 + "!"; //Hello, World!

```

✅ Tại sao `1 + 1 = 2` trong JavaScript, nhưng `'1' + '1' = 11?` Hãy suy nghĩ về điều này. Còn `'1' + 1` thì sao?

**Template literals** là một cách khác để định dạng chuỗi, ngoại trừ việc sử dụng dấu backtick thay vì dấu nháy. Bất cứ điều gì không phải là văn bản thuần túy phải được đặt trong các placeholder `${ }`. Điều này bao gồm bất kỳ biến nào có thể là chuỗi.

```javascript
let myString1 = "Hello";
let myString2 = "World";

`${myString1} ${myString2}!` //Hello World!
`${myString1}, ${myString2}!` //Hello, World!
```

Bạn có thể đạt được mục tiêu định dạng của mình bằng cả hai phương pháp, nhưng template literals sẽ tôn trọng bất kỳ khoảng trắng và ngắt dòng nào.

✅ Khi nào bạn sẽ sử dụng template literal thay vì chuỗi thông thường?

### Booleans

Booleans chỉ có thể có hai giá trị: `true` hoặc `false`. Booleans có thể giúp đưa ra quyết định về dòng mã nào sẽ chạy khi các điều kiện nhất định được đáp ứng. Trong nhiều trường hợp, [toán tử](../../../../2-js-basics/1-data-types) hỗ trợ việc thiết lập giá trị của một Boolean và bạn sẽ thường thấy và viết các biến được khởi tạo hoặc giá trị của chúng được cập nhật bằng một toán tử.

- `let myTrueBool = true`
- `let myFalseBool = false`

✅ Một biến có thể được coi là 'truthy' nếu nó đánh giá là boolean `true`. Thú vị là, trong JavaScript, [tất cả các giá trị đều là truthy trừ khi được định nghĩa là falsy](https://developer.mozilla.org/docs/Glossary/Truthy).

---

## 🚀 Thử Thách

JavaScript nổi tiếng với những cách xử lý kiểu dữ liệu gây bất ngờ. Hãy nghiên cứu một chút về những 'điểm khó hiểu' này. Ví dụ: sự phân biệt chữ hoa chữ thường có thể gây rắc rối! Thử điều này trong bảng điều khiển của bạn: `let age = 1; let Age = 2; age == Age` (kết quả là `false` -- tại sao?). Bạn có thể tìm thấy những điểm khó hiểu nào khác?

## Câu Hỏi Sau Bài Giảng
[Câu hỏi sau bài giảng](https://ff-quizzes.netlify.app)

## Ôn Tập & Tự Học

Hãy xem [danh sách bài tập JavaScript này](https://css-tricks.com/snippets/javascript/) và thử làm một bài. Bạn học được gì?

## Bài Tập

[Thực hành Kiểu Dữ Liệu](assignment.md)

---

**Tuyên bố miễn trừ trách nhiệm**:  
Tài liệu này đã được dịch bằng dịch vụ dịch thuật AI [Co-op Translator](https://github.com/Azure/co-op-translator). Mặc dù chúng tôi cố gắng đảm bảo độ chính xác, xin lưu ý rằng các bản dịch tự động có thể chứa lỗi hoặc không chính xác. Tài liệu gốc bằng ngôn ngữ bản địa nên được coi là nguồn tham khảo chính thức. Đối với các thông tin quan trọng, chúng tôi khuyến nghị sử dụng dịch vụ dịch thuật chuyên nghiệp từ con người. Chúng tôi không chịu trách nhiệm cho bất kỳ sự hiểu lầm hoặc diễn giải sai nào phát sinh từ việc sử dụng bản dịch này.