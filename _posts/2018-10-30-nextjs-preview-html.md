---
title: "【NextJS】普通HTML表示ようのプレビュー機能"
tags: [programming, nodejs, javascript, nextjs]
categories: [programming, japanese]
share-img: /img/nodejs.jpeg
---

最近、ツールを開発するのに、よく[NextJS](https://nextjs.org/)というNodeJSフレームーワークを使っています。

フレームーワーク自体の構成は:

* クライアント側がReactJS

* サーバー側がExpressJS

通常、React Componentを使えば、問題なくページなど生成することができます。
しかし、要件によって、普通のHTMLファイル、しかも複雑JavaScriptコードもあるHTMLだと、React Componentに変換するのが難しいとことが多いです。(`<script>`タグが一つ、二つぐらいなら、React Componentに変換することができますが、複数あると、refactoringするのに、かなり時間かかると思います。)

そこで、今回実務で、ツールの要件で、複雑HTMLのプレビュー機能をNextJSで実装しなければなりませんでした。

やり方は下記のようにしました。

* プレビューボタンを押して

* サーバーのAPIにアクセスして、JSONデータが生成される

* 生成されたJSONデータを使って、`public/preview/html/${sessionID}.html`で保存しておく。`ExpressJS`ですと、`req.sessionID`というパラメーターがあって、そこでプレビューファイルが個別できる。

* 生成されたら、クライアントにファイルパスである`/preview/html/${sessionID}.html`をresponse

* クライアント側で、`<iframe>`タグを使って、htmlを表示する

Reactのスースコード:

```javascript
{showPreview && (
    <div>
        <iframe title="preview" style={ { width: '100%', height: '500px' } } src={previewPath} />
    </div>
)}
```

この方法で、どんな複雑htmlファイルもプレビューできるので、便利です。

NextJSは`<style dangerouslySetInnerHTML={ { __html: htmlContent } } />`のような使い道もあるようですが、`Server side rendering`の問題もあって、うまくいきませんでした。なので、色々試した結果、`<iframe>`を使うことにしました。

最後に、生成されたプレビュー用のhtmlファイルはあとで削除しないと、サーバーの容量が無くなりますので、batchで毎日削除します。NodeJSだと、`cron`モジュールなどを使えば、batch実装できます。

```bash
npm install --save cron
```

```javascript
const {CronJob} = require('cron');

new CronJob('* * * * * *', () => {
  console.log('do something here');
}, null, true);
```

ファイルを毎日削除コマンドは

```bash
find /public/preview/html/ -type f -mtime +7 -name '*.html' -print0 | xargs -r0 rm --
```

などが使えます。