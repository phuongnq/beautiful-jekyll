---
title: "JavaScript Tutorial: Khai báo trước khi dùng"
tags: [vietnamese, programming, javascript]
categories: [programming, javascript]
share-img: /img/javascript.jpg
---

Thoạt nhìn JavaScript có vẻ là một ngôn ngữ flexible, chúng ta có thể tự do code theo style của riêng mình. Tuy nhiên mọi việc có thể trở lên phức tạp nếu chúng ta không chú ý. Hãy cùng xem thử ví dụ sau đây:

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

```javascript
    // broken code
    const tmpFunc = function() {
        aVariable = 5;
        console.log(aVariable);
    }

    tmpFunc();
    console.log(aVariable);
```

Kết quả sau khi chạy:

```bash
    5
    5
```

Với đoạn code trên, chúng ta không khai báo biến dùng từ khoá `let`, `const` cho biến `aVariable`, vì vậy biến này được coi như **biến global**. Kết quả là dòng lệnh `console.log(aVariable)` bên ngoài hàm `tmpFunc` vẫn in ra kết quả `5`.

Hãy cùng sửa lại với việc khai báo biến với `let`:

```javascript
    // declared code
    const tmpFunc = function() {
        let aVariable = 5;
        console.log(aVariable);
    }

    tmpFunc();
    console.log(aVariable);
```

Khi chạy chúng ta sẽ gặp phải thông báo lỗi:

```bash
Uncaught ReferenceError: aVariable is not defined
```

Bằng việc khai báo biến, `aVariable` không còn là **biến global** nữa mà là **biến local** chỉ có tác dụng bên trong hàm `tmpFunc`.

Sai sót việc không khai báo biến có thể chỉ do typo, tuy nhiên nhiều khi hậu quả nó gây ra có thể rất lớn. Ví dụ như đoạn code:

```javascript
    // broken code
    const outer = function() {
        for (i = 1; i <= 3; i++) {
            inner();
        }
    };

    const inner = function() {
        for (i = 1; i <= 5; i++) {
            console.log(i);
        }
    };

    outer();
```

Đoạn code trên cho ra kết quả:

```bash
1
2
3
4
5
```

Chúng ta expect hàm `inner()` sẽ được gọi 3 lần do biến `i` chạy từ `1 -> 3`. Tuy nhiên do hàm `outer()` cũng dùng chung biến `i`, và chúng ta đã không khai báo `i` nên tình huống xảy ra như sau:

* Biến `i` là **biến global**

* Khi gọi `outer()` thì biến `i` được gán giá trị **1**

* `inner()` được gọi và biến `i` chạy từ `1 -> 5`. In ra kết quả từ **1...5**

* Sau khi chạy hết `inner()` một vòng, kiểm tra `i`:

    ```javascript
    for (i = 1; i <= 3; i++) {
        inner();
    }
    ```
Thì khi đó `i` đã có giá trị **5** nên vòng lặp kết thúc, không chạy `inner()` thêm lần nữa.

Để fix lỗi này, chúng ta cần khai báo biến `i` trong hai vòng loop:

```javascript
    const outer = function() {
        for (let i = 1; i <= 3; i++) {
            inner();
        }
    };

    const inner = function() {
        for (let i = 1; i <= 5; i++) {
            console.log(i);
        }
    };

    outer();
```

Khi chạy chúng ta sẽ thấy giá trị `1...5` sẽ được in ra 3 lần như kỳ vọng.

# Kết luận

* Luôn khai báo biến với từ khoá `let`, `const` trước khi dùng

* Dùng các công cụ kiểm tra **code convention** như [ESLint](https://eslint.org/) để sửa lỗi trong khi code

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

Danh sách tutorial JavaScript:

* [Cẩn thận với dấu ngắt dòng;](https://phuongnq.me/2018-07-27-javascript-tutorial-01/)

* [Dùng === thay cho ==](https://phuongnq.me/2018-07-29-javascript-tutorial-02/)

* [Khai báo trước khi dùng](https://phuongnq.me/2018-07-30-javascript-tutorial-03/)