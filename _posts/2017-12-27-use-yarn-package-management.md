---
title: Dùng yarn thay thế cho npm
date: 2017-12-27 22:09:09
tags: [vietnamese, manual, npm, yarn, nodejs]
---

Nói đến package manager cho JavaScript thì mọi người thường nghĩ ngay đến `npm`. Tuy nhiên, ngoài `npm` ra thì có một thư viện khác dùng cũng khá hay, community đang ngày càng phát triển đó là **Yarn**. Trong bài viết này thì mình sẽ giới thiệu sơ qua về công cụ này, cách cài đặt và những câu lệnh sử dụng đơn giản.

<div style="text-align: center;">
	<img src="https://yarnpkg.com/assets/og_image.png" style="width: 100%;"/>
</div>

Như được giới thiệu trên [trang chủ](https://yarnpkg.com/en/):

> *Yarn* là một trình quản lý package cho source code. Nó cho phép bạn chia sẻ source code với những developer khác trên toàn thế giới. *Yarn* thực hiện việc này một cách nhanh chóng, bảo mật và đáng tin cậy.

> *Yarn* cho phép bạn dùng code của các developer khác để giải quyết vấn đề của mình, làm cho việc phát triển phần mềm dễ dàng hơn. Trong khi dùng các source code này nếu gặp vấn đề gì thì bạn có thể tạo issue hoặc gửi pull request lại để giúp cho cộng đồng *Yarn* được cập nhật mới nhất.

>  Code được chia sẻ thông qua **package**, hoặc cũng có lúc chúng ta gọi là **module**. Một *package* thì bao gồm tất cả source code được chia sẻ cùng với một file `package.json` chứa định nghĩa cho *package* đó.

# Hướng dẫn dùng

## Cài đặt

* Với Mac OS, chúng ta có thể cài đặt thông qua `brew`:

```
brew install yarn
```

Nếu chúng ta có dùng `nvm` để quản lý version cho **NodeJS** thì khi cài đặt *yarn*, hãy thêm option không cài *node*, để chúng ta dùng bản của *nvm*:

```
brew install yarn --without-node
```

Khi cần update *yarn*, chạy lệnh:

```
brew upgrade yarn
```

Để kiểm tra version đã cài đặt:

```
yarn --version
```

* Để cài đặt với *Ubuntu*:

Trước hết, chúng ta cần đăng ký thêm repository:

```
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```

Sau đó để cài đặt thì đơn giản là chạy lệnh:

```
sudo apt-get update && sudo apt-get install yarn
```

* Ngoài ra, cũng có một cách khác để cài đặt *yarn* thông qua *npm*:

```
npm install --global yarn
```

Chi tiết về tất cả cách cài đặt có thể tham khảo trên trang chủ: https://yarnpkg.com/en/docs/install

## Cách dùng

Về cách dùng nói chung cũng khá giống như khi chúng ta dùng `npm`:

Để tạo một dự án mới:

```
yarn init
```

Sau khi gõ lệnh thì *console* sẽ hiện ra một số câu hỏi, ví dụ:

```
yarn init v1.3.2
question name (test):
question version (1.0.0):
question description: test yarn
question entry point (index.js):
question repository url:
question author:
question license (MIT):
question private:
```

Nó bao gồm những thông tin cơ bản để tạo ra file `package.json`. Và sau khi trả lời hết các câu hỏi, file `package.json` sẽ được tạo ra với nội dung như chúng ta đã nhập.

Để thêm một package vào trong project:

```
yarn add [package]
yarn add [package]@[version]
yarn add [package]@[tag]
```

Ở đây chúng ta có 3 cách tạo: dùng chính tên package, dùng tên package với version hoặc dùng package với tag.
Ngoài ra, cũng có option ví dụ như để thêm vào `devDependencies`:

```
yarn add [package] --dev
```

Để upgrade package:

```
yarn upgrade [package]
yarn upgrade [package]@[version]
yarn upgrade [package]@[tag]
```

Để remove package:

```
yarn remove [package]
```

Ngoài ra chúng ta cũng có thể trực tiếp xoá định nghĩa package trong file `package.json` rồi gõ lệnh cài đặt dependency để cài/xoá package khỏi project:

```
yarn
```

Nếu quen dùng `npm`, chúng ta cũng có thể gõ

```
yarn install
```

Hai câu lệnh trên có tác dụng tương đương, đều dùng để cài đặt dependency.

Các package có thể search thông qua *Google* hoặc tìm trên trang chủ: https://yarnpkg.com/en/package.
Ví dụ mình thử tìm package về parse url, https://yarnpkg.com/en/package/url-parse. Thì để cài đặt gói này, chạy lệnh:

```
yarn add url-parse
```

Sau khi gõ lệnh và cài đặt thành công, chúng ta thấy được package đã được thêm vào trong file `package.json`,

```
"dependencies": {
    "url-parse": "^1.2.0"
}
```

Ngoài ra trong thư mục `node_modules` cũng đã xuất hiện thêm thư mục cho `url-parse`:

```
$ ls -ls node_modules/url-parse/
drwxr-xr-x  7 PhuongNQ  staff    224 Dec 27 17:58 .
drwxr-xr-x  6 PhuongNQ  staff    192 Dec 27 17:58 ..
-rw-r--r--  1 PhuongNQ  staff   1115 Feb 14  2015 LICENSE
-rw-r--r--  1 PhuongNQ  staff   6207 Nov  2 22:57 README.md
drwxr-xr-x  4 PhuongNQ  staff    128 Dec 27 17:58 dist
-rw-r--r--  1 PhuongNQ  staff  11517 Nov  2 22:57 index.js
-rw-r--r--  1 PhuongNQ  staff   1173 Nov  2 22:57 package.json
```