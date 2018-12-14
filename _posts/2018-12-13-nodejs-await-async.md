---
title: "【Node.js】Tìm hiểu về await/async"
tags: [programming, nodejs, javascript]
categories: [programming, japanese]
share-img: /img/nodejs.jpeg
---

`await/async` là một tính năng được hỗ trợ chính thức từ bản **NodeJS 7.6**. Cụ thể các bản hỗ trợ dùng có thể xem tham khảo trên link sau đây: [https://node.green/#ES2017-features-async-functions-await](https://node.green/#ES2017-features-async-functions-await)

Tác dụng chính của `await/async` đó là giúp chúng ta xử lý các operation *bất đồng bộ* (asynchronous), mà không bị vấn đề *callback hell* [1].

Muốn hiểu rõ về `await/async`, trước hết cần hiểu về `Promise`.

## Tìm hiểu về Promise

Theo như định nghĩa trên [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise):

> The Promise object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.

Từ định nghĩa này ta có thể biết được `Promise` đơn giản cũng là một `Object`, giống như các *Object* khác trong JavaScript.

Vì là *Object* nên có thể khởi tạo bằng việc dùng từ khoá `new`:

```javascript
new Promise( /* executor */ function(resolve, reject) { ... } );
```

**Tạo một Promise Object**

Như đề cập ở trên, để tạo ra một Promise Object, dùng với từ khoá `new`:

```javascript
const myFirstPromise = new Promise((resolve, reject) => {
  // do something asynchronous which eventually calls either:
  //
  //   resolve(someValue); // fulfilled
  // or
  //   reject("failure reason"); // rejected
});
```

Khi tạo ra một *Promise* mới thì sẽ truyền vào parameter là một hàm có 2 parameters: resolve & reject

* *resolve*: bản chất là một hàm được gọi khi code chạy thành công (fulfilled), giá trị muốn trả về truyền vào parameter của hàm `resolve`

* *reject*: bản chất là một hàm đowcj gọi khi code chạy không đúng, có lỗi hoặc là kết quả của *exception* (rejected). Giá trị muốn trả về (lý do lỗi, mã code lỗi, etc) tryền vào như parameter của hàm `reject`

Một ví dụ về tạo *Promise Object* khi thực hiện *HTTP Request*:

```javascript
function myAsyncFunction(url) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url);
    xhr.onload = () => resolve(xhr.responseText);
    xhr.onerror = () => reject(xhr.statusText);
    xhr.send();
  });
}
```

Như chúng ta có thể thấy trong hàm truyền vào *Promise Object*:

* Xử lý `GET` một *url* nào đó

* Nếu load thành công thì `resolve` với *response text*

* Nếu load thất bại thì `reject` với *status text*

**Dùng một Promise Object**

*Promise Object* được dùng đơn giản với cấu trúc

```javascript
aPromiseObject
    .then((someValue) => {
        // do something with someValue
    })
    .catch((ex) => {
        // do something with exception
    });
```

* someValue: là kết quả từ `resolve(someValue)` khi tạo Promise

* ex: là kết quả từ `reject("failure reason")`, trường hợp này `ex === 'failure reason'`

*Promise Object* có thể dùng theo kiểu *chain*, nghĩa là có nhiều *then* nếu trong mỗi `then` lại `return` giá trị nào đó. Ví dụ:

```javascript
loadImageAsync('one.png')
  .then(function(image) {
    console.log('Image loaded', image);
    return { width: image.width, height: image.height };
  })
  .then(function(size) {
    console.log('Image size:', size);
  })
  .catch(function(err) {
    console.error('Error in promise chain', err);
  });
```

**Lịch sử Promise**

Promise được hỗ trợ khá sớm cho các bản NodeJS. Từ bản 0.12.18 đã bắt đầu hỗ trợ, và hoàn thiện các tính năng từ bản 6.15.1.

## Quay lại await/async

## Chú thích:

(1): **callback hell** - Lập trình dùng *NodeJS* hay *JavaScript* nói chung sẽ hay gặp phải vấn đề *callback hell* do cấu trúc của ngôn ngữ là: đợi một *event* nào đó hoàn thiện, rồi gọi một đoạn code *callback* nào đó. Ví dụ về *callback hell*:

```javascript
fs.readdir(source, function (err, files) {
  if (err) {
    console.log('Error finding files: ' + err)
  } else {
    files.forEach(function (filename, fileIndex) {
      console.log(filename)
      gm(source + filename).size(function (err, values) {
        if (err) {
          console.log('Error identifying file size: ' + err)
        } else {
          console.log(filename + ' : ' + values)
          aspect = (values.width / values.height)
          widths.forEach(function (width, widthIndex) {
            height = Math.round(width / aspect)
            console.log('resizing ' + filename + 'to ' + height + 'x' + height)
            this.resize(width, height).write(dest + 'w' + width + '_' + filename, function(err) {
              if (err) console.log('Error writing file: ' + err)
            })
          }.bind(this))
        }
      })
    })
  }
});
```

**Tham khảo:**

Giới thiệu về await/async tham khảo: https://www.infoq.com/news/2017/02/node-76-async-await

Ví dụ về callback hell lấy trên trang: http://callbackhell.com/

Ví dụ về Promise lấy trên trang: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

Ví dụ về Promise chain lấy trên: https://github.com/mattdesl/promise-cookbook#promises