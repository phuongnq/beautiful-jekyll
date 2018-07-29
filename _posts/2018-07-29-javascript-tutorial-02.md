---
title: "JavaScript Tutorial: Dùng === thay cho =="
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

# Hướng dẫn

Nhiều người lập trình với JavaScript thường hay dùng `==` khi so sánh bằng. Toán tử này mặc dù đúng là làm nhiệm vụ so sánh xem hai giá trị có bằng nhau hay không, tuy nhiên nó không kiểm tra **type** của **object** được đem ra so sánh. Điều này có thể dẫn đến những kết quả không mong muốn. Hãy cùng xem thử ví dụ sau đây:

```javascript
//Broken code

const a = '1';
const b = 1;
const c = '1.0';

console.log(a == b);
console.log(b == c);
console.log(a == c);
```

Theo như trên ví dụ chúng ta gán `a`, `b`, `c` lần lượt các giá trị `'1'`, `1` và `'1.0'`. `b` có kiểu `number` còn hai biến còn lại là kiểu `string`. Sau đó chúng ta so sánh lần lượt `a` với `b`, `b` với `c` và `c` với `a` dùng toán tử `==`. Nếu suy nghĩ theo toán học thì:

> Nếu a bằng b, b bằng c, suy ra c bằng a.

Tuy nhiên, khi chạy thử đoạn code ở trên ta sẽ được kết quả:

```bash
true
true
false
```

Tại sao lại như vậy?

Lý do là khi so sánh `a == b` hay `b == c`, hai toán hạng có kiểu `string` và `number` khác nhau. Vì vậy JavaScript sẽ đổi sang cùng kiểu trước khi đem chúng ra so sánh. Trong trường hợp này kiểu `string` sẽ được chuyển sang kiểu `number@`. Còn khi so sánh `c` với `a` do hai toán hạng cùng là `string`, sẽ không có sự chuyển đổi nào. Vì vậy hiển nhiên chúng ta có được string `'1'` thì khác với string `'1.0'`.

Hãy cùng xem lại ví dụ trên khi dùng toán tử `===`:

```javascript
const a = '1';
const b = 1;
const c = '1.0';

console.log(a === b);
console.log(b === c);
console.log(a === c);
```

```bash
false
false
false
```

Khi dùng `===`, chúng ta đã yêu cầu JavaScript thực hiện so sánh mà không đổi kiểu của toán hạng. Dẫn đến cả ba trường hợp đều cho ra `false`.

Trong tiếng Anh thì chúng ta gọi:

* `==` là **Abstract Equality Comparison** dùng khi muốn so sánh lỏng (Loose equality)

* `===` là **Strict Equality Comparison** dùng khi muốn so sánh hai object cùng kiểu (Strict equality)

Có thể tham khảo thêm document bằng tiếng Anh tại [đây](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)

# Kết luận

Khi code thực tế, hiếm khi chúng ta cần phải dùng `==`. Với mọi phép so sánh thì nên sử dụng `===`. Nếu trường hợp muốn so sánh giá trị của hai object không cùng kiểu, best practice là đổi chúng về cùng một kiểu trước khi so sánh với `===`.

Hiểu được **JavaScript** hoạt động như thế nào sẽ tránh được suy nghĩ đây là một ngôn ngữ kỳ quặc. Trên mạng có nhiều meme châm biếm phép so sánh `==` của JavaScript. Thực ra đó là do người viết chưa hiểu đúng ý nghĩa của nó.

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