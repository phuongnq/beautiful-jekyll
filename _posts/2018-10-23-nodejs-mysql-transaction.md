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