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

Promise được hỗ trợ khá sớm cho các bản NodeJS. Từ bản 0.12.18 đã bắt đầu hỗ trợ, và hoàn thiện các tính năng từ bản 6.15.1. Do vậy nếu dùng bản NodeJS khá mới thì chúng ta có thể tự tin đã hỗ trợ *Promise*.

## Quay lại await/async

Tóm tắt lại thì *await/async* đơn giản chỉ là cách viết *Promise* cho dễ hiểu và trực quan hơn.

* Khi định nghĩa hàm thì sẽ dùng từ khoá `async`, ngụ ý là `asynchronous function`

* Khi dùng hàm định nghĩa bởi `async` thì sẽ dùng từ khoá `await`. Ví dụ:

```javascript
const value = await fn();
...
```

Ngụ ý là *Chờ cho hàm fn() thực hiện xong*, lấy giá trị `resolve(value)` trả về cho biến `value` rồi thực hiện tiếp các lệnh sau đó.

### Định nghĩa hàm với async

Như tài liệu trên MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function

> The async function declaration defines an asynchronous function, which returns an AsyncFunction object. An asynchronous function is a function which operates asynchronously via the event loop, using an implicit Promise to return its result. But the syntax and structure of your code using async functions is much more like using standard synchronous functions.

Nghĩa là `async function` sẽ trả về một `AsyncFunction` Object. Object này hoạt động như *Promise*, tức chạy bất đồng bộ theo *event loop* của engine. Tuy nhiên về mặt syntax thì chúng ta có thể viết như là code đồng bộ, nghĩa là viết từ trên xuống dưới như bất kỳ cách viết nào trên ngôn ngữ C chẳng hạn.

Để hiểu rõ hàm `async`, chúng ta có thể chạy thử đoạn code sau (trên trình duyệt Chrome mới nhất hoặc bản NodeJS có hỗ trợ await/async):

```javascript
const fn = async () => {};
console.log(fn);
console.log(fn());
```

Kết quản nhận được khi chạy với NodeJS:

```bash
$ node
> const fn = async () => {}
undefined
>
> console.log(fn)
[AsyncFunction: fn]
undefined
> console.log(fn())
Promise {
  undefined,
  domain:
   Domain {
     domain: null,
     _events:
      [Object: null prototype] {
        removeListener: [Function: updateExceptionCapture],
        newListener: [Function: updateExceptionCapture],
        error: [Function: debugDomainError] },
     _eventsCount: 3,
     _maxListeners: undefined,
     members: [] } }
undefined
```

Như vậy chúng ta có thể thấy khi chạy hàm `fn()`, nó thực chất trả về một `Promise`. Còn bản thân `fn` là một Object `AsyncFunction`.

### Dùng hàm với `await`

Sau khi đã định nghĩa hàm với `async`, chúng ta dùng với từ khoá `await`. Ví dụ:

```javascript
const fn = async () => {
  return 'hello';
};

const main = async () => {
  const res = await fn();
  console.log(res);
};

main();
```

Như ở trên, hàm `fn` được định nghĩa là một hàm `async function`. Hàm `main` được định nghĩa là một hàm `async function` khác, mục đích để gọi `fn()`.

`fn` được gọi với từ khoá `await`:

```javascript
const res = await fn();
```

Sau đó `res` sẽ có giá trị trả về từ `fn`, kết quả in ra string *hello*.

Như vậy thay vì dùng *Promise* với chuỗi `.then()`, chúng ta dùng `await` để viết xử lý đợi Promise. Định nghĩa trên MDN cũng đề cập điều này:

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await

> The await operator is used to wait for a Promise. It can only be used inside an async function.

Ngoài ra, khi muốn bắt lỗi nếu xử lý Promise bị `reject`, chúng ta dùng `try/catch`. Ví dụ về hàm `loadImageAsync` có thể viết lại như sau:

```javascript
try {
  const image = await loadImageAsync('one.png');
  console.log('Image loaded', image);
  const size = { width: image.width, height: image.height };
  console.log('Image size:', size);
} catch (err) {
  console.error('Error in promise chain', err);
}
```

Chúng ta có thể thấy dùng `await` code nhìn trực quan và dễ hiểu hơn.

## Khoá học về NodeJS

<a href="https://click.linksynergy.com/link?id=Jg7nYe7Gmvg&offerid=507388.82778&type=2&murl=https%3A%2F%2Fwww.udemy.com%2Fall-about-nodejs%2F"><img border=0 src="https://udemy-images.udemy.com/course/480x270/82778_94fa_6.jpg" ></a><img border=0 width=1 height=1 src="https://ad.linksynergy.com/fs-bin/show?id=Jg7nYe7Gmvg&bids=507388.82778&type=2&subid=0" >

<a href="https://click.linksynergy.com/link?id=Jg7nYe7Gmvg&offerid=507388.1770580&type=2&murl=https%3A%2F%2Fwww.udemy.com%2Fnode-js-mongo-db-2018%2F"><IMG border=0 src="https://udemy-images.udemy.com/course/480x270/1770580_8a3a.jpg" ></a><IMG border=0 width=1 height=1 src="https://ad.linksynergy.com/fs-bin/show?id=Jg7nYe7Gmvg&bids=507388.1770580&type=2&subid=0" >

<a href="https://click.linksynergy.com/link?id=Jg7nYe7Gmvg&offerid=507388.1608308&type=2&murl=https%3A%2F%2Fwww.udemy.com%2Fbuild-a-chatapp-with-nodejssocketio-expressjs-mongodb%2F"><IMG border=0 src="https://udemy-images.udemy.com/course/480x270/1608308_826d_3.jpg" ></a><IMG border=0 width=1 height=1 src="https://ad.linksynergy.com/fs-bin/show?id=Jg7nYe7Gmvg&bids=507388.1608308&type=2&subid=0" >

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

Một số giải thích về await/async tham khảo trên: https://dev.to/jgs/javascript--asyncawait---2l41