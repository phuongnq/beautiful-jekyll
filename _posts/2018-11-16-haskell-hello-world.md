---
title: "【Haskell】Hello world"
tags: [programming, haskell]
categories: [programming, vietnamese]
share-img: /img/haskell.png
---

![](/img/haskell.png)

# Cài đặt:

Tải từ trang chủ về cài: [https://www.haskell.org/downloads](https://www.haskell.org/downloads). Có bản cài cho cả MacOS/Windows/Linux.

Nếu trước đó cài bản cũ thì sau khi cài gõ lệnh:

```bash
$ sudo activate-hs
Password:

Haskell now set to:
    GHC      8.4.3
    Arch.    x86_64
    Platform 8.4.3

View documentation with this command:
    open /Library/Haskell/doc/start.html
```

Sau khi cài đặt kiểm tra thư mục:

```bash
$ ls -la /Library/Haskell/
total 24
drwxr-xr-x   7 root  wheel   238 11 16 18:46 .
drwxr-xr-x+ 66 root  wheel  2244  4 10  2018 ..
lrwxr-xr-x   1 root  wheel    11 11 16 18:46 bin -> current/bin
lrwxr-xr-x   1 root  wheel    16 11 16 18:46 current -> ghc-8.4.3-x86_64
lrwxr-xr-x   1 root  wheel    11 11 16 18:46 doc -> current/doc
drwxr-xr-x   8 root  wheel   272 12 13  2017 ghc-8.2.2-x86_64
drwxr-xr-x   8 root  wheel   272  6 11 09:07 ghc-8.4.3-x86_64
```


* Editor dùng *vscode*

* Cài thêm gói syntax cho Haskell: https://marketplace.visualstudio.com/items?itemName=justusadam.language-haskell

## Hello world

Tạo file `hello.hs`. `hs` là extension cho file source code Haskell.

```hs
--hello.hs First Haskell file

main = do
    print "Hello, world!"
```

Compile:

```bash
$ ghc hello.hs
[1 of 1] Compiling Main             ( hello.hs, hello.o )
gcc-8: error: unrecognized command line option '-no-pie'
`gcc-8' failed in phase `Assembler'. (Exit code: 1)
```

Bị lỗi trên sửa file: `$ code /Library/Frameworks/GHC.framework/Versions/Current/usr/lib/ghc-8.4.3/settings`:

```text
[ ("GCC extra via C opts"," -fwrapv -fno-builtin")
, ("C compiler command","/usr/local/bin/gcc-8")
, ("C compiler flags"," -fno-stack-protector")
, ("C compiler link flags"," ")
, ("C compiler supports -no-pie","NO")
, ("Haskell CPP command","/usr/local/bin/gcc-8")
, ("Haskell CPP flags", "-E -undef -traditional -Wno-invalid-pp-token -Wno-unicode -Wno-trigraphs")
, ("ld command","ld")
, ("ld flags","")
, ("ld supports compact unwind","YES")
, ("ld supports build-id","NO")
, ("ld supports filelist","YES")
, ("ld is GNU ld","NO")
, ("ar command","ar")
, ("ar flags","qcls")
, ("ar supports at file","NO")
, ("ranlib command","")
, ("touch command","touch")
, ("dllwrap command","/bin/false")
, ("windres command","/bin/false")
, ("libtool command","libtool")
, ("perl command","/usr/bin/perl")
, ("cross compiling","NO")
, ("target os","OSDarwin")
, ("target arch","ArchX86_64")
, ("target word size","8")
, ("target has GNU nonexec stack","False")
, ("target has .ident directive","True")
, ("target has subsections via symbols","True")
, ("target has RTS linker","YES")
, ("Unregisterised","NO")
, ("LLVM llc command","llc")
, ("LLVM opt command","opt")
, ("LLVM clang command","clang")
]
```

Nội dung: sửa `gcc` -> `/usr/local/bin/gcc-8`, `("C compiler supports -no-pie","YES")` -> `, ("C compiler supports -no-pie","NO")`

Chạy lại:

```bash
$ ghc hello.hs
[1 of 1] Compiling Main             ( hello.hs, hello.o )
Linking hello ...
```

```bash
$ ./hello
"Hello, world!"
```