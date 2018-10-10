---
title: "NodeJSでmysql2パッケージを使うメモ"
tags: [programming, nodejs, javascript]
categories: [programming, japanese]
share-img: /img/nodejs.jpeg
---

# 前書き

最近NodeJSでMySQLを使う機会が増えて、個人のために使い方をメモします。基本的にはNodeJSの`mysql2`というパッケージを使用し、クエリを書きます。
`mysql2`を使う理由は最新非同期の`await/async`が使える理由です。

# インストール

```bash
npm install --save mysql2
```

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

# Modelで呼び出す

ファイルパス：`src/model/testModel.js`

```javascript
const MySqlConn = require('../config/mysql');

const ModelTest = {
    async get(type) {
        const pool = MySqlConn.getPool();
        const [rows] = await pool.query(`SELECT * FROM test_tb1 WHERE type=?`, type);

        return Promise.all(rows.map(async (row) => {
            const [countRes] = await pool.query(`SELECT COUNT(*) as count FROM test_tb2 WHERE templateId=?`, row.id);
            return {
                name: row.name,
                count: countRes[0].count,
            };
        }));
    }
};

module.exports = ModelTest;
```

この`ModelTest`で二つのことをやりました

* `test_tb1`というテーブルからデータを集計する

* 上の結果を`Promise.all`で、別テーブルの`COUNT(*)`でデータのカウントを習得する

* クエリの中、`prepare`を使って、変数パラメーターをクエリ文字列の外に管理できる

`Promise.all`を使うことで、`for`ループ中の`await`使用問題を回避できます。また、同時にクエリするので、クエリスピードが上がります。

詳細の`mysql2`パッケージの使い方はGithubで参照する:　[https://github.com/sidorares/node-mysql2](https://github.com/sidorares/node-mysql2)
