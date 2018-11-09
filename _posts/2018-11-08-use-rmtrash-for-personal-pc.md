---
title: "【Unix/Linux】Dùng gói rmtrash thay cho rm command"
tags: [unix, linux]
categories: [programming, vietnamese]
share-img: /img/rm_rf_cmd.cmd
---

Với người dùng Unix/Linux thì lệnh `rm` là một trong những lệnh nguy hiểm nhất, nó xoá vĩnh viễn file, một đi không trở lại.

Cách đơn giản nhất để làm hỏng hệ điều hành là gõ lệnh với quyền `sudo`:

```bash
sudo rm - rf /
```

(Đừng thử) Lệnh này sẽ xoá toàn bộ thư mục gốc, không thể lấy lại được.

Với máy cá nhân, để tránh trường hợp này thì khuyến khích dùng gói `rmtrash`.

## rmtrash là gì

Gói này thực thi xoá file cho vào thùng rác (Trash), thay vì xoá hoàn toàn file khỏi ổ cứng.

Dưới đây là cài đặt cho MacOS.

### Cài đặt với homebrew

```bash
brew install rmtrash
```

### Thiết lập alias

Sau khi cài đặt thì thiết lập alias để thay thế lệnh `rm`:

```bash
$ vim ~/.bashrc
```

Thêm dòng:

```text
alias rm='rmtrash'
```

Load lại:

```bash
$ source ~/.bashrc
```

Kiểm tra đã thành công:

```bash
$ ls
sample.txt
$ rm sample.txt
```

![](/img/rmtrash_output.png)

Xoá thư mục:

```bash
$ ls rmtrash_test
test.txt
$ rm rmtrash_test
```

![](/img/rmtrash_folder.png)

Bài viết tham khảo: https://qiita.com/nakamurau1@github/items/7fd6ee87787d0687c2e2

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