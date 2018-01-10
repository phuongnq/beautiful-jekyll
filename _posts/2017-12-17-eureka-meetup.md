---
title: Meetup note - Eureka meetup for front-end engineer
date: 2017-12-17 16:35:22
tags: [meetup, eureka, tech, english]
---

[Eureka](https://eure.jp/) inc is a venture company with around 130 employees. They provide services about dating in both web and native applications (iOS/Android). The major service is [Pairs](https://www.pairs.lv/) which is a matching service for people who is looking for relationship parter. **Pairs** has more than *6,000,000* users from Japan and Taiwan. They also have  plan to expand the business to Korea. I also have a chance to use this service and experience excellent UI/UX. The app for iOS works smoothly and I has an impression of in fashion which is absolutely neccessary for dating application.

**Eureka** seems to quite a techinical oriented company. They provide many meetups recently with contents expand from frontend to backend technology as well as specific subject like design, optimization, refactoring, etc.I took part in the meetup in *November 30, 2017* which was for front-end engineer. To know more about speaker of the meetup, refer to [connpass event page](https://eure.connpass.com/event/67457/) (Japanese). We can check [Eureka connpass home page](https://eure.connpass.com/) for more meetup in the future.

![Eureka office](https://images2.imgbox.com/f5/a7/Pupu9slm_o.jpg)

They also have very nice office with concentrate working space, coffee bar, and relaxing work space. The meetup also has free beers and pizza.

**Eureka** technical blog: https://developers.eure.jp/

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

# Agenda

## ClojureScript+re-frameで社内アプリケーションを開発した話
*Using clojureScript and re-frame to develop in office application*

Blog post: https://developers.eure.jp/tech/how-to-use-clojurescript-on-our-office-system/

* PPT document: https://www.slideshare.net/boxp/clojurescriptreframe
* Application: in office event management system (Slack login intergration, notification, Google calendar intergration).
* Server side: Golang
* Client side: ClojureScript
* According to [ClosureScript homepage](https://clojurescript.org/index)
> Clojure is a dynamic, general-purpose programming language supporting interactive development. Clojure is a functional programming language featuring a rich set of immutable, persistent data structures. As a dialect of Lisp, it has a code-as-data philosophy and a powerful macro system.
* With *REPL*, we could confirm if source code working while implementing so could speed up circle of writing code: https://www.youtube.com/watch?v=bLZsB_tZc14
* ClojureScript is a compiler for Clojure that targets JavaScript. To learn more: https://github.com/clojure/clojurescript
* Compare to *JavaScript*, *ClojureScript* also has similar technical stack:

Technical stack | JavaScript | ClojureScript
--------------- | -----------| -------------
UI | React, Vue, Polymer, etc | Om, [Reagent](https://github.com/reagent-project/reagent), Rum, etc
Manage state | Redux, Vuex, etc | [re-frame](https://github.com/Day8/re-frame), citrus, etc
Build tools | Webpack, Rollup, etc | [Leiningen](https://leiningen.org/), Boot, etc
Module | ES6, node, etc | [goog.module](https://github.com/google/closure-library/wiki/goog.module:-an-ES6-module-like-alternative-to-goog.provide)
asynchronous | Promise, RxJS, etc | core.async

* As in above stack, *ClojureScript* could work effectively with *ReactJS* using *re-frame* framework. There are articles of using *ClojureScript* with React, such as: https://qiita.com/lagenorhynque/items/7c049f3c3b967ee777ac (Japanese).

## A sustainable web-frontend

* The talk was about how *Pairs* front-end implemented. The service is using single page application (SPA) web app with AngularJS/TypeScript library. SPA is good for service oriented but not so good for SEO.
* The team had problem with AngualarJS so they created something similar to Flux architecture of *ReactJS*
* In the future, *Pairs* could be refactoring to *ReactJS* or *VueJS*, or other front-end libraries.


## うちのWebviewはこうなってるよ
*How webview is in Eureka*

* Introduction of [rio.js](http://riotjs.com/)
* There was no special reason to use RioJS, but while trying using the library, it worked! The library is quite small with around 10KB.
* Use *yarn* instead of *npm*: https://yarnpkg.com/en/
* Use *PostCSS*: http://postcss.org/

## 最近のWebパフォーマンスについて色々
*Recent web performance*

* W3C TPAC: https://www.w3.org/2016/09/TPAC/
* https://html5experts.jp/
* Introduction of *Long task API*

## Party & company tour