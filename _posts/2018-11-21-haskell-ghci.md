---
title: "【Haskell】Tương tác với ghci"
tags: [programming, haskell]
categories: [programming, vietnamese]
share-img: /img/haskell.png
---

![](/img/haskell.png)

**GHC** là từ viết tắt cho **Glasgow Haskell Compiler**. Nghĩa là nó là một *compiler* cho Haskell. Có nhiều bộ combiler khác nhau nhưng GHC có vẻ hiện được dùng rộng rãi.

**GHCi** là *interactive interface* cho compiler *GHC*. Chúng ta có thể dùng *GHCi* để confirm một block code đơn giản có chạy đúng hay không.

Để bắt đầu dùng *ghci* gõ lệnh:

```bash
$ ghci
GHCi, version 8.4.3: http://www.haskell.org/ghc/  :? for help
Prelude>
```

`:q` để thoát khỏi giao diện interactive.

```bash
Prelude> :q
Leaving GHCi.
phuong.nguyen at P45547 in ~
```
Ví dụ đơn giản dùng `ghci`:

> Cộng 2 số:

```bash
Prelude> 1 + 2
3
Prelude>
```

> Gán biến:

```bash
Prelude> x = 1 + 2
Prelude> x
3
Prelude>
```

> Khai báo hàm:

```bash
Prelude> let f x = 2 * x + 1
Prelude> f 1
3
Prelude> f 2
5
Prelude>
```

**GHCi** có thể dùng để load một file vào. Có 2 cách làm việc này:

**Pass filename khi chạy `ghci`:**

```bash
$ ghci hello.hs
GHCi, version 8.4.3: http://www.haskell.org/ghc/  :? for help
[1 of 1] Compiling Main             ( hello.hs, interpreted )
Ok, one module loaded.
*Main> main
"Hello, world!"
*Main>
```

**Dùng trong interactive mode với `:l` (`:load`)**

```bash
$ ghci
GHCi, version 8.4.3: http://www.haskell.org/ghc/  :? for help
Prelude> :l hello.hs
[1 of 1] Compiling Main             ( hello.hs, interpreted )
Ok, one module loaded.
*Main> main
"Hello, world!"
*Main>
```

Danh sách bài viết về Haskell:

* [【Haskell】Hello world](/2018-11-16-haskell-hello-world/)

* [【Haskell】Tương tác với ghci](/2018-11-21-haskell-ghci/)