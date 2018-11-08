---
title: "【NodeJS】Tạo static server với NodeJS"
tags: [programming, nodejs, javascript]
categories: [programming, vietnamese]
share-img: /img/nodejs.jpg
---

Nhiều khi chúng ta có nhu cầu tạo ra một server đơn giản để serve files html/json phục vụ cho việc test. Một ví dụ đơn giản như là tạo ra server để test file HTML được encoding dưới dạng EUC-JP - một chuẩn encoding cũ của Nhật Bản. Trong khi file JSON (JavaScript Opbject Notation - https://www.json.org/) lại dưới dạng UTF-8.

Server như vậy có thể tạo ra rất đơn giản với *NodeJS*, dùng 2 gói *npm package* là `connect` và `serve-static`.

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

* **Gói package connect**:

    * Link GitHub: [https://github.com/senchalabs/connect](https://github.com/senchalabs/connect)

    * Đây là gói extend cho `http`, có thêm một số middleware, phục vụ cho việc gửi/nhận HTTP request

* **Gói package serve-static**:

   * Link GitHub: [https://github.com/expressjs/serve-static](https://github.com/expressjs/serve-static)

   * Đây là gói middle hỗ trợ việc response với file trong một thư mục nào đó (html, json, etc)

## Cài đặt

Tạo ra một thư mục mới rồi cài đặt 2 gói trên:

```bash
mkdir test_static_server && cd test_static_server
npm install connect
npm install serve-static
```

Tạo ra file `server.js` với nội dung:

```javascript
const connect = require('connect');
const serveStatic = require('serve-static');
connect().use(serveStatic(__dirname, {
    setHeaders: function(res, path, stat) {
        if (serveStatic.mime.lookup(path) === 'application/json') {
        res.setHeader('Content-Type', 'application/json');
    } else {
        res.setHeader('Content-Type', 'text/html; charset=EUC-JP');
    }
 }
})).listen(8080, function() {
    console.log('Server running on 8080...');
});
```

Chạy với lệnh:

```bash
 node server.js
```

Nếu không có lỗi thì server của chúng ta có thể nhận request qua cổng `8080`. Như trong đoạn code, chúng ta đã:

* Tạo một HTTP server để GET static files

* Files GET được là bất kỳ file nào trong thư mục gốc cùng với file `server.js` (Do config dùng biến `__dirname`)

* Thiết lập header riêng cho từng loại file:

    * Nếu là file JSON: chỉ đặt header `Content-Type` là `application/json`.

    * Nếu là file khác (text, html), thêm encoding `EUC-JP`.

* Ví dụ đặt file test.html vào thư mục gốc -> có thể hiển thị file này thông qua URL: *http://localhost:8080/test.html*

* Ví dụ đặt file test.json vào thư mục gốc -> có thể hiển thị file này thông qua URL: *http://localhost:8080/test.json*

Có một số config nữa cho static-server này, chúng ta có thể tham khảo thêm trên trang chủ [GitHub](https://github.com/expressjs/serve-static).

NodeJS đặc biệt thú vị vì chúng ta có thể tạo ra một con server chỉ với vài dòng code như trên.

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

<table border="0" cellpadding="0" cellspacing="0"><tr><td><div style="border:1px solid #95a5a6;border-radius:.75rem;background-color:#FFFFFF;margin:0px;padding:5px 0;text-align:center;overflow:hidden;"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F12221765%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F16328264%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MCwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjF9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><img src="https://hbb.afl.rakuten.co.jp/hgb/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?me_id=1213310&item_id=16328264&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F6068%2F9784873116068.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F6068%2F9784873116068.jpg%3F_ex%3D400x400&s=400x400&t=picttext" border="0" style="margin:2px" alt="" title=""></a><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F12221765%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F16328264%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MCwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjF9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  >Nodeクックブック [ デビッド・マーク・クレメンツ ]</a></p><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F12221765%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F16328264%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MCwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjF9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><div style="margin:15px;"><img src="https://static.affiliate.rakuten.co.jp/makelink/rl.svg" style="float:left;max-height:27px;width:auto;margin-top:5px"><div style="float:right;width:50%;height:32px;background-color:#bf0000;color:#fff !important;font-size:14px;font-weight:500;line-height:32px;margin-left:1px;padding: 0 12px;border-radius:16px;cursor:pointer;text-align:center;">楽天で購入</div></div></a></div><br><p style="color:#000000;font-size:12px;line-height:1.4em;margin:5px;word-wrap:break-word"></p></td><td><div style="border:1px solid #95a5a6;border-radius:.75rem;background-color:#FFFFFF;margin:0px;padding:5px 0;text-align:center;overflow:hidden;"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15552726%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F19222623%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MCwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjF9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><img src="https://hbb.afl.rakuten.co.jp/hgb/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?me_id=1213310&item_id=19222623&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F5220%2F9784798055220.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F5220%2F9784798055220.jpg%3F_ex%3D400x400&s=400x400&t=picttext" border="0" style="margin:2px" alt="" title=""></a><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15552726%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F19222623%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MCwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjF9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  >Node.js 超入門 第2版 [ 掌田津耶乃 ]</a></p><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15552726%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F19222623%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MCwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjF9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><div style="margin:15px;"><img src="https://static.affiliate.rakuten.co.jp/makelink/rl.svg" style="float:left;max-height:27px;width:auto;margin-top:5px"><div style="float:right;width:50%;height:32px;background-color:#bf0000;color:#fff !important;font-size:14px;font-weight:500;line-height:32px;margin-left:1px;padding: 0 12px;border-radius:16px;cursor:pointer;text-align:center;">楽天で購入</div></div></a></div><br><p style="color:#000000;font-size:12px;line-height:1.4em;margin:5px;word-wrap:break-word"></p></td></tr></table>