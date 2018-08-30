---
title: "[Programming][NodeJS] - Starter Note"
tags: [programming, nodejs, javascript]
categories: [programming]
share-img: /img/nodejs.jpeg
---

This is a beginner level introduction about writing code with NodeJS.

![](/img/nodejs.jpeg)

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

# Code convention

## Motivation

Code convention is a set of rules or guid lines when writing code. The motivation is to make sure our source code is written with consistency among developers and could be shared or maintained by other developers without any issue. An other benefit is that by following rules, we reduce the number of mistakes may cause and also build a habit of writing best practice codes.

For languages such as JavaScript, developers too many freedom to write code as he/she wants. This may cause difficulty for other developers to understand or maintain.

For that reason, it is critical to follow code convention for JavaScript development.

## Tools

Follow code convention from [ESLint](https://eslint.org/)

There are other sources about JavaScript code convention that we can follow:

* Google: [https://google.github.io/styleguide/jsguide.html](https://google.github.io/styleguide/jsguide.html)
* Airbnb: [https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)
* Mozilla Code Style: [ttps://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Coding_Style](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Coding_Style)

# Editor

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

While coding JavaScript, we can use any Editor or IDE as long as it supports showing hidden space/tab and convenient for developers.

For NodeJS development, it is recommended to use editors which have ESLint plugins. Some of them are:

* VCCode: [https://code.visualstudio.com/](https://code.visualstudio.com/)

* Sublime Text: [https://www.sublimetext.com/](https://www.sublimetext.com/)

* Atom: [https://atom.io/](https://atom.io/)

IDE such as Eclipse could be used as well

## Below is a sample of how to use VCCode:

* Download and install from homepage: [https://code.visualstudio.com/](https://code.visualstudio.com/)

* Install packages:

```bash
code --install-extension christian-kohler.path-intellisense
code --install-extension DavidAnson.vscode-markdownlint
code --install-extension dbaeumer.vscode-eslint
code --install-extension donjayamanne.githistory
code --install-extension eamodio.gitlens
code --install-extension fabianlauer.vs-code-xml-format
code --install-extension ms-mssql.mssql
code --install-extension robertohuertasm.vscode-icons
```

* Sample of settings:

![](/img/vccode_user_setting.png)

```bash
{
    "gitlens.advanced.messages": {
        "suppressCommitHasNoPreviousCommitWarning": false,
        "suppressCommitNotFoundWarning": false,
        "suppressFileNotUnderSourceControlWarning": false,
        "suppressGitVersionWarning": false,
        "suppressLineUncommittedWarning": false,
        "suppressNoRepositoryWarning": false,
        "suppressResultsExplorerNotice": false,
        "suppressShowKeyBindingsNotice": true,
        "suppressUpdateNotice": false,
        "suppressWelcomeNotice": true
    },
    "files.autoGuessEncoding": true,
    "workbench.iconTheme": "vscode-icons",
    "editor.renderWhitespace": "all",
    "editor.fontSize": 13,
    "window.zoomLevel": 0,
    "editor.fontLigatures": true,
    "editor.renderLineHighlight": "all",
    "editor.renderIndentGuides": true,
    "editor.selectionHighlight": true,
    "explorer.autoReveal": true,
    "files.trimTrailingWhitespace": true,
    "workbench.colorCustomizations": {
        "statusBar.background" : "#007acc",
        "statusBar.noFolderBackground" : "#0A0A0D",
        "statusBar.debuggingBackground": "#cc6633"
    },
    "vsicons.projectDetection.autoReload": true,
    "workbench.startupEditor": "newUntitledFile",
    "vsicons.dontShowNewVersionMessage": true,
    "gitlens.keymap": "alternate",
    "workbench.colorTheme": "Monokai",
    "extensions.ignoreRecommendations": false,
    "gitlens.historyExplorer.enabled": true
}
```

* Other editors or IDEs have different setting but the main points are:

  * Show hidden characters such as space or tab so that we don't write extra characters

  * Add ESLint plugin so that editor/IDE would show errors and fixing suggestion. Sample of showing errors and fixing suggestion:

  ![](/img/eslint_sample.png)

# Note while writing code

## Use non-blocking code

NodeJS by natural uses an event loop to execute commands. It has only 1 thread to perform non-blocking I/O operations. For that reason, it is critical to writing non-blocking code to make sure NodeJS server does not block other requests.

Example: https://nodejs.org/en/docs/guides/blocking-vs-non-blocking/

> Blocking:

```javascript
const fs = require('fs');
const data = fs.readFileSync('/file.md'); // blocks here until file is read
```

> Non-blocking:

```javascript
const fs = require('fs');
fs.readFile('/file.md', (err, data) => {
  if (err) throw err;
});
```

## Use ES6 syntax/features when possible

Introduction of ES6 (ECMAScript 2015): [https://nodejs.org/en/docs/es6/](https://nodejs.org/en/docs/es6/)

List of ES6 syntax/features: [http://es6-features.org](http://es6-features.org)

To check if a version of NodeJS is compatible with ES6 or not: [https://node.green/](https://node.green/)

Especially, it is recommended to use await/async style to write asynchronous codes.

Documents:

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await)

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)

## References

List of some document & frameworks may be helpful for beginners:

* Official guides - include general document, NodeJS core concepts and some modules related guides: [https://nodejs.org/en/docs/guides/](https://nodejs.org/en/docs/guides/)

* ExpressJS framework: [https://expressjs.com/](https://expressjs.com/)

* Server Side Rendering with NextJS framework: [https://nextjs.org/](https://nextjs.org/)

* JavaScript tutorials in general: [https://github.com/getify/You-Dont-Know-JS](https://github.com/getify/You-Dont-Know-JS)

* NodeJS tutorial: [https://www.tutorialspoint.com/nodejs/](https://www.tutorialspoint.com/nodejs/)

* Use NPM packages when possible: [https://www.npmjs.com/](https://www.npmjs.com/)

  There are many libraries available which have been developed as open source. Consider using those libraries when develop new web application instead of doing every thing from scratch. Some helpful libraries:

  * Functions to process array, object, list: [https://lodash.com/](https://lodash.com/)

  * MySQL: [https://www.npmjs.com/package/mysql2](https://www.npmjs.com/package/mysql2)

  * Request HTTP: [https://www.npmjs.com/package/request](https://www.npmjs.com/package/request)

  * Request HTTP with promise: [https://www.npmjs.com/package/request-promise](https://www.npmjs.com/package/request-promise)

  * Logger with winston: [https://www.npmjs.com/package/winston](https://www.npmjs.com/package/winston)

There are many document and tutorials available in the Internet. It is always recommended to search Google for best practice before coding.

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

# Some books about NodeJS

<table border="0" cellpadding="0" cellspacing="0"><tr><td><div style="border:1px solid #000000;background-color:#FFFFFF;width:410px;margin:0px;padding-top:6px;text-align:center;overflow:auto;"><a href="https://hb.afl.rakuten.co.jp/hgc/16ebf0dd.31ab421d.16ebf0de.dec3052c/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Frakutenkobo-ebooks%2F549df5c453953cf2a029995105eca101%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Frakutenkobo-ebooks%2Fi%2F15083894%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><img src="https://hbb.afl.rakuten.co.jp/hgb/16ebf0dd.31ab421d.16ebf0de.dec3052c/?me_id=1278256&item_id=15083894&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Frakutenkobo-ebooks%2Fcabinet%2F0433%2F2000003790433.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Frakutenkobo-ebooks%2Fcabinet%2F0433%2F2000003790433.jpg%3F_ex%3D400x400&s=400x400&t=picttext" border="0" style="margin:2px" alt="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]" title="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]"></a><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16ebf0dd.31ab421d.16ebf0de.dec3052c/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Frakutenkobo-ebooks%2F549df5c453953cf2a029995105eca101%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Frakutenkobo-ebooks%2Fi%2F15083894%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  >Node.js Essentials【電子書籍】[ Fabian Cook ]</a><br><span >価格：2031円</span> <span style="color:#BBB">(2018/8/30時点)</span></p></div><br><p style="font-size:12px;line-height:1.4em;margin:5px;word-wrap:break-word"></p></td><td><div style="border:1px solid #000000;background-color:#FFFFFF;width:410px;margin:0px;padding-top:6px;text-align:center;overflow:auto;"><a href="https://hb.afl.rakuten.co.jp/hgc/16ebf0dd.31ab421d.16ebf0de.dec3052c/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Frakutenkobo-ebooks%2Fc0db7bf3510f33b2ae085766b7f5d401%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Frakutenkobo-ebooks%2Fi%2F15059223%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><img src="https://hbb.afl.rakuten.co.jp/hgb/16ebf0dd.31ab421d.16ebf0de.dec3052c/?me_id=1278256&item_id=15059223&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Frakutenkobo-ebooks%2Fcabinet%2F3873%2F2000003763873.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Frakutenkobo-ebooks%2Fcabinet%2F3873%2F2000003763873.jpg%3F_ex%3D400x400&s=400x400&t=picttext" border="0" style="margin:2px" alt="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]" title="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]"></a><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16ebf0dd.31ab421d.16ebf0de.dec3052c/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Frakutenkobo-ebooks%2Fc0db7bf3510f33b2ae085766b7f5d401%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Frakutenkobo-ebooks%2Fi%2F15059223%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  >Web Development with MongoDB and NodeJS - Second Edition【電子書籍】[ Mithun Satheesh ]</a><br><span >価格：3251円</span> <span style="color:#BBB">(2018/8/30時点)</span></p></div><br><p style="font-size:12px;line-height:1.4em;margin:5px;word-wrap:break-word"></p></td></tr><tr><td><div style="border:1px solid #000000;background-color:#FFFFFF;width:410px;margin:0px;padding-top:6px;text-align:center;overflow:auto;"><a href="https://hb.afl.rakuten.co.jp/hgc/16ebf0dd.31ab421d.16ebf0de.dec3052c/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Frakutenkobo-ebooks%2Ff3cf7d465fcf36138f22bb32f5ff097c%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Frakutenkobo-ebooks%2Fi%2F16089629%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><img src="https://hbb.afl.rakuten.co.jp/hgb/16ebf0dd.31ab421d.16ebf0de.dec3052c/?me_id=1278256&item_id=16089629&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Frakutenkobo-ebooks%2Fcabinet%2F6060%2F2000004866060.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Frakutenkobo-ebooks%2Fcabinet%2F6060%2F2000004866060.jpg%3F_ex%3D400x400&s=400x400&t=picttext" border="0" style="margin:2px" alt="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]" title="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]"></a><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16ebf0dd.31ab421d.16ebf0de.dec3052c/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Frakutenkobo-ebooks%2Ff3cf7d465fcf36138f22bb32f5ff097c%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Frakutenkobo-ebooks%2Fi%2F16089629%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  >Programming Web Applications with Node, Express and Pug【電子書籍】[ J?rg Krause ]</a><br><span >価格：2994円</span> <span style="color:#BBB">(2018/8/30時点)</span></p></div><br><p style="font-size:12px;line-height:1.4em;margin:5px;word-wrap:break-word"></p></td><td><div style="border:1px solid #000000;background-color:#FFFFFF;width:410px;margin:0px;padding-top:6px;text-align:center;overflow:auto;"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15166961%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F18816291%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><img src="https://hbb.afl.rakuten.co.jp/hgb/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?me_id=1213310&item_id=18816291&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F2576%2F9781617292576.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F2576%2F9781617292576.jpg%3F_ex%3D400x400&s=400x400&t=picttext" border="0" style="margin:2px" alt="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]" title="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]"></a><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15166961%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F18816291%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiI0MDB4NDAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  >Node.Js in Action NODEJS IN ACTION 2/E [ Alex R. Young ]</a><br><span >価格：12096円（税込、送料無料)</span> <span style="color:#BBB">(2018/8/30時点)</span></p></div><br><p style="font-size:12px;line-height:1.4em;margin:5px;word-wrap:break-word"></p></td></tr></table>