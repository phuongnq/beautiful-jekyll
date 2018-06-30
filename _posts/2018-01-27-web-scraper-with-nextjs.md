---
title: "Create a website scraper with NextJS"
tags: [tech, english, nodejs, reactjs, nextjs]
categories: [english, programming]
---

# Introduction

> What is NextJS?

NextJS is a *NodeJS framework* that allows us to write *server-side rendering React* web application.

So there are two keywords here: **server-side rendering** and **React**.

* As we may have known, *React* is a JavaScript UI library that allows us to build user interface. *React* use virtual dom and build with *components* so that we can re-use them in multiple places. There are ton of articals or tutorials about *React*, here is it's official web site: https://reactjs.org/

* How about **server-side rendering**? Normally, React libarary uses *client-side rendering*, which means that when we access the web page, all required JavaScript would be downloaded to client then being rendered to DOM elements. This is absolutely best practice, especially for single page application, that we don't have to load the page again when navigating around. But there is a problem with *client-side rendering*. It is not very good for *SEO*. To solve this problem, one of solution is to use **server-side rendering**. That is, the *initial render* would be performed by server side, then sent to client. From that point, other rendering would be taken over by client side. By doing this, we can both decrease the first load size, and also increase *SEO* optimization and still using *React* library.

> Why use NextJS?

By using *NextJS*, we can use both *server-side rendering* technique and using *ReactJS* library. An other plus to count is that it works smoothly with *ExpressJS* which is best NodeJS web framework right now. Last but not least, when using *NextJS*, I can easily configure default routes by seperating files, something similar to PHP. For example, when access to `/sample_route`, it would, by default executes content in `sample_route.js` in server side. This is very convenient if we want to build a quick demo application. Of course, still we can modify this behavior to make routing more structural.

**NextJS** GitHub page: [https://github.com/zeit/next.js/](https://github.com/zeit/next.js/)

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

# Implementation

In this note, I would like to introduce how I used *NextJS* to build a sample web scraper. The original idea is to use `website-scraper` package from [npm](https://www.npmjs.com/package/website-scraper). They provides a [sample](https://github.com/website-scraper/demo) which uses *AngularJS*, so I want to create my own version using *React*.

Let's start the steps.

## Preparation

Make sure to latest version of NodeJS/NextJS. In my case:

* Node version: `v9.3.0`

* npm version: `5.6.0`

* I also use boilerplates, you can search for some of them in [this link](https://github.com/unicodeveloper/awesome-nextjs). I chosen to use [next-express-bootstrap-boilerplate](https://github.com/MustansirZia/next-express-bootstrap-boilerplate) which provide NextJS in ExpressJS framework with support of bootstrap and SCSS. You can use both `npm` or `yarn` with this boilerplate. Please follow their GitHub manual for installation instruction.

First, install *npm* package

```
sudo npm i -g next-express-bootstrap-boilerplate
```

Then `cd` to source code folder, run command:

```
next-boilerplate
```

After everything installed, run web application with command:

```
npm run dev
```

or

```
yarn dev
```

Here is how the default display look like:

![NextJS sample](/img/nextjs_sample_01.png)

You can check boilerplate [GitHub page](https://github.com/MustansirZia/next-express-bootstrap-boilerplate) to understand structure of source code. The basic idea is that when accessing `/` root route, it would execute file `/apps/page/index.js`, and for `/profile`, it would execute file `/apps/page/profile.js` to render UI. This is quite straightforward and easy to understand for beginner.

Since we don't need `/profile` route, I delete file `/apps/page/profile.js` and modify `/apps/page/index.js` to add UI for URL input, submit form. Here is how new UI look like:

![NextJS sample](/img/nextjs_sample_02.png)

The application structure is quite simple:

* An input form to input URL to scrape

* When submitting, it calls React component `Index` function `doSubmitUrl` to do `POST` call to `/scrape_url` using `fetch`. To understand `fetch`, refer to how to [Use Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch).

* In server side, `app.js`, add a function to handle `POST /scrape_url`:

```
    app.post('/scrape_url', (req, res) => {
        const scrapeUrl = req.body.url;
        if (!scrapeUrl) {
            return res.status(500).send('Please provide a valid URL');
        }
        const folderName = (new Date()).getTime();
        const options = {
            urls: [scrapeUrl],
            directory: `tmp/${folderName}`,
        }

        scrape(options).then((result) => {
            const zipFile = `./tmp/${folderName}.zip`;
            zipFolder(options.directory, zipFile, (err) => {
                if (err) {
                    console.log(err);
                    return res.status(500).send('zip file failed');
                } else {
                    return res.download(zipFile);
                }
            })
        }).catch((err) => {
            console.log(err);
            return res.status(500).send('zip file failed');
        });
    });
```

This responds a file to client and in client side, we render a link with `blob` response data, as a part of `doSubmitUrl` function:

```
    doSubmitUrl() {
        const data = { url: this.state.url }
        const url = '/scrape_url';
        fetch(url, {
            method: 'POST',
            body: JSON.stringify(data),
            headers: new Headers({
                'Content-Type': 'application/json'
            }),
        })
        .then((response) => response.blob())
        .then((blob) => {
            const link=document.createElement('a');
            link.href=window.URL.createObjectURL(blob);
            link.text=`${this.state.url}.zip`;
            const downloadLink = document.getElementById('downloadLink');
            downloadLink.appendChild(link);
        })
        .catch(error => console.error('Error:', error));
    }
```

Here is my whole project in GitHub: [website-scraper-demo-nextjs](https://github.com/phuongnq/website-scraper-demo-nextjs)

# Conclusion

In this post I introduced how to use NextJS to build a website scraper. NextJS, with a boilerplate helps us to create initial source code quickly so we can begin to code our real applications. I don't have a chance to try NextJS for larger project but for simple demos, this is effective way to make thing done. And with *ExpressJS* behide, there should be no problem to use NextJS in larger scale. There are some more websites built with NextJS listed here: [https://github.com/zeit/next.js/issues/1458](https://github.com/zeit/next.js/issues/1458)

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