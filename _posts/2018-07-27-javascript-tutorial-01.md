---
title: "JavaScript Tutorial: Cẩn thận với dấu ngắt dòng;"
tags: [vietnamese, programming, javascript]
categories: [programming, javascript]
share-img: /img/javascript.jpg
---

JavaScript là một trong những ngôn ngữ chứa nhiều điều đáng ngạc nhiên, và không phải tất cả mọi thứ đều dễ chịu. Nhiều khi cái chúng ta muốn làm lại không phải là cái ngôn ngữ sẽ xử lý. Trong những trường hợp như vậy, chúng ta là người thua cuộc và code viết ra sẽ có lỗi không như ý muốn khi chạy. Trong series này chúng ta sẽ nghiên cứu một số cú pháp của JavaScript mà dễ gây nhầm lẫn. Biết được những vùng grey này, chúng ta có thể dùng JavaScript mà không gặp phải những tai nạn đáng tiếc.

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-2750437710821247"
     data-ad-slot="8905029259"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>

# Cẩn thận khi bỏ qua dấu ngắt dòng;

Nhiều ngôn ngữ hiện đại không bắt buộc dùng dấu ngắt dòng (**semicolon** hay **;**). Tuy nhiên JavaScript không nằm trong số đó: dấu ngắt dòng thường là bắt buộc và nên có. Nếu chúng ta không thêm dấu ngắt dòng sau một dòng lệnh, JavaScript sẽ tự động thêm theo cơ chế gọi là **automatic semicolon insertion** (hay ASI).

> Tokens được parse từ trái sang phải. Khi gặp một token ở một dòng mới (new line) thì một dấu ngắt dòng (;) sẽ được thêm vào trước token đó.

Ví dụ:

> unexpected_semicolon.js

```javascript
    //BROKEN CODE​
    const​ unexpected = ​function​() {
        ​let​ first
        second = 1;

        console.log(first);
        console.log(second);
    }
​
    unexpected();

    console.log(second);
```

Cái gì không tốt trong ví dụ ở trên?

Đó là việc dùng biến `second` sau biến `first` mà không có dấu ngắt dòng. Với ASI, JavaScript sẽ tự động thêm vào trước `second` dấu ngắt dòng:

```javascript
    ​let​ first
    ​;second = 1;
```

Với đoạn code như trên, khi chạy thử trên browser/NodeJS thì sẽ cho ra kết quả:

```bash
    undefined
​    1
    1
```

Biến `first` có giá trị `undefined` thì chúng ta có thể dễ dàng hiểu được. Nhưng tại sao biến `second` ở bên ngoài hàm `unexpected` lại cho ra giá trị là `1`?

Lí do đơn giản là vì sau khi tự động thêm vào `;second = 1;` thì biến `second` đã trở thành biến global (Note: *Trong JavaScript, từ ES6 biến không được khai báo với từ khoá `const` hoặc `let` thì mặc định được coi là biến global*). Dẫn đến giá trị của nó tồn tại ngay cả bên ngoài hàm.

Hãy cùng xem xét một ví dụ khác nữa:

```javascript
    // broken code
    const execute = function (number) {
        if (number > 10) {
            return number
            +2;
        }

        if (number > 5) {
            return
            number * 2;
        }
    };

    console.log(execute(11));
    console.log(execute(6));
```

Đoạn code trên sau khi chạy sẽ cho ra kết quả:

```bash
    13
    undefined
```

Vì sao chúng ta có giá trị `undefined` cho `execute(6)`?

Chúng ta có thể dễ dàng nhận thấy 2 dấu ngắt dòng bị thiếu cho hai câu lệnh `return`.

**Câu lệnh thứ nhất:** Mặc dù không có dấu ngắt dòng, nhưng JavaScript hiểu được rằng cần có một con số sau toán tử `+` nên không có dấu ngắt dòng được thêm vào trước `+`.

**Câu lệnh thứ hai:** Sau `return` là một dòng mới bắt đầu bằng biến `number`. JavaScript sẽ hiểu đây là một câu lệnh mới do vậy tự động sửa thành `;number * 2;`. Kết quả là hàm `return` không có giá trị trả về. Và chúng ta thấy nó trả về `undefined` như trong ví dụ.

# Kết luận

* Nên dùng dấu ngắt dòng trong mọi trường hợp.

* Nếu dòng lệnh quá dài, chúng ta có thể ngắt thành nhiều dòng ngắn hơn. Nhưng chú ý cách ngắt sao cho JavaScript không tự động thêm dấu ngắt dòng không đúng, ảnh hưởng đến ý tưởng code ban đầu.

* Việc dùng các công cụ kiểm tra **code convention** như là [ESLint](https://eslint.org/) là rất quan trọng. Nó giúp chúng ta tránh được những lỗi cú pháp không cần thiết như việc tự động thêm dấu ngắt dòng.

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-2750437710821247"
     data-ad-slot="8905029259"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>
