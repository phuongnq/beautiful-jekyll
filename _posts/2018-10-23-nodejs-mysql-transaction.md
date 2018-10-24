---
title: "【Node.js】MySQLのトランザクション対応 "
tags: [programming, nodejs, javascript]
categories: [programming, japanese]
share-img: /img/nodejs.jpeg
---

`mysql2`という`npm`パッケージを使うと、簡単にトランザクションが実装できます。

まずはパッケージのインストール

```bash
npm install --save mysql2
```

`--save`パラメーターを使うことで、`package.json`に保存されます。Gitなどを使えば、他のメンバーは`npm install`だけで、`mysql2`が入れるようになります。

# Poolオブジェクト作成

ファイルパス：`src/config/mysql.js`

```javascript
const mysql = require('mysql2');

const MySQLConn = {
    getPool() {
        if (!this.pool) {
            this.pool = mysql.createPool({
                host: 'localhost',
                port: 3306,
                user: 'root',
                password: 'password123',
                database: 'test',
                waitForConnections: true,
                connectionLimit: 10,
                queueLimit: 0
            });
        }

        return this.pool.promise();
    },
};

module.exports = MySQLConn;
```

上記が宣言した`pool`オブジェクトを呼び出して、トランザクションを開始します。

ファイルパス：`src/model/testModel.js`

```javascript
const MySqlConn = require('../config/mysql');

const ModelTest = {
    async delete(id) {
        const pool = MySqlConn.getPool();
        const conn = await pool.getConnection();
        try {
            await conn.beginTransaction();

            await conn.query(`DELETE FROM table_1 WHERE contentId=1`, id);

            await conn.query(`DELETE FROM table_2 WHERE contentId=1`, id);

            await conn.query(`DELETE FROM table_3 WHERE contentId=1`, id);

            await conn.query(`INSERT INTO table_log (id, value) VALUES(?, ?)`, [id, value]);

            await conn.commit();
        } catch (ex) {
            await conn.rollback();
            return null;
        } finally {
            conn.release();
        }

        return id;
    }
};

module.exports = ModelTest;
```

トランザクションを使う場合は

`await conn.beginTransaction()`と`await conn.commit()`の中、自由にクエリ追加することができます。

注意しないといけないことは下記です。

* 最後にconnectionオブジェクトをリリースこと `conn.release()`。そうしないと、メモリリーク原因になります。

* `try/catch`で例外を処理します。その時は、トランザクションをロールバックしないといけません。`await conn.rollback()`で実行します。

* `await/async`を使うことで、簡潔かつコールバックなく、わかりやすいソースコードがかけます。

<table border="0" cellpadding="0" cellspacing="0"><tr><td><div style="border:1px solid #95a5a6;border-radius:.75rem;background-color:#FFFFFF;margin:0px;padding:5px 0;text-align:center;overflow:hidden;"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F12221765%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F16328264%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MCwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjF9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><img src="https://hbb.afl.rakuten.co.jp/hgb/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?me_id=1213310&item_id=16328264&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F6068%2F9784873116068.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F6068%2F9784873116068.jpg%3F_ex%3D400x400&s=400x400&t=picttext" border="0" style="margin:2px" alt="" title=""></a><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F12221765%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F16328264%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MCwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjF9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  >Nodeクックブック [ デビッド・マーク・クレメンツ ]</a></p><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F12221765%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F16328264%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MCwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjF9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><div style="margin:15px;"><img src="https://static.affiliate.rakuten.co.jp/makelink/rl.svg" style="float:left;max-height:27px;width:auto;margin-top:5px"><div style="float:right;width:50%;height:32px;background-color:#bf0000;color:#fff !important;font-size:14px;font-weight:500;line-height:32px;margin-left:1px;padding: 0 12px;border-radius:16px;cursor:pointer;text-align:center;">楽天で購入</div></div></a></div><br><p style="color:#000000;font-size:12px;line-height:1.4em;margin:5px;word-wrap:break-word"></p></td><td><div style="border:1px solid #95a5a6;border-radius:.75rem;background-color:#FFFFFF;margin:0px;padding:5px 0;text-align:center;overflow:hidden;"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15552726%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F19222623%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MCwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjF9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><img src="https://hbb.afl.rakuten.co.jp/hgb/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?me_id=1213310&item_id=19222623&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F5220%2F9784798055220.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F5220%2F9784798055220.jpg%3F_ex%3D400x400&s=400x400&t=picttext" border="0" style="margin:2px" alt="" title=""></a><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15552726%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F19222623%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MCwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjF9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  >Node.js 超入門 第2版 [ 掌田津耶乃 ]</a></p><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15552726%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F19222623%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MCwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjF9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><div style="margin:15px;"><img src="https://static.affiliate.rakuten.co.jp/makelink/rl.svg" style="float:left;max-height:27px;width:auto;margin-top:5px"><div style="float:right;width:50%;height:32px;background-color:#bf0000;color:#fff !important;font-size:14px;font-weight:500;line-height:32px;margin-left:1px;padding: 0 12px;border-radius:16px;cursor:pointer;text-align:center;">楽天で購入</div></div></a></div><br><p style="color:#000000;font-size:12px;line-height:1.4em;margin:5px;word-wrap:break-word"></p></td></tr></table>