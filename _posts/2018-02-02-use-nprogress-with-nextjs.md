---
title: "Use Nprogress module with NextJS"
tags: [tech, english, nodejs, reactjs, nextjs]
---

# Introduction

In [previous post](https://phuongnq.me/2018-01-27-web-scraper-with-nextjs/), I have introduced about **NextJS** and how to implement a web scraper with **NextJS**. In this post, I would like to introduce how to integrate NProgress library to *NextJS* application.

You may have known, **NProgress** is a slim progress bar for web applications. It is inspired by similar bars of Google, YouTube, and Medium. Check out *NProgress* [homepage](http://ricostacruz.com/nprogress/) to see how it works. And there are [npm page](https://www.npmjs.com/package/react-nprogress) and [GitHub page](https://github.com/rstacruz/nprogress) as well. 

Here is the manual to include **NProgress** bar to a *nextjs web application*.

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

# Manual

Create a new folder for our application. In my case, I created `demo-nextjs-nprogress` directory. `cd` to that newly created directory and run `next-boilerplate` to create a new *expressjs boilerplate nextjs application*. If you didn't install **next-boilerplate**, refer to [Create a website scraper with NextJS](https://phuongnq.me/2018-01-27-web-scraper-with-nextjs/) for the manual.

```
$ cd demo-nextjs-nprogress
$ next-boilerplate
```

After everything installed (could take 1-2 minutes), check the application by running:

```
$ npm run dev

> next-express-bootstrap-boilerplate@0.0.5 dev /home/phuongnq/github/demo-nextjs-nprogress
> nodemon --ignore app/ app.js

[nodemon] 1.14.12
[nodemon] to restart at any time, enter `rs`
[nodemon] watching: *.*
[nodemon] starting `node app.js`
> Using external babel configuration
> Location: "/home/phuongnq/github/demo-nextjs-nprogress/app/.babelrc"
> Using "webpack" config function defined in next.config.js.
```

The application now should be available in address `localhost:9001`.

Now `Ctl+C` to exit the application and install `nprogress` library:

```
$ npm install --save nprogress
```

`--save` option is used to add `nprogress` to our `package.json`. After installed, we can check that there is folder `node_modules/nprogress`.

Copy `node_modules/nprogress/nprogress.css` to `app/styles/vendor/`:

```
$ cp node_modules/nprogress/nprogress.css app/styles/vendor
```

Now include this `css` in our load template: Update `app/components/Theme.js`:

```
import PropTypes from 'prop-types';
import BootstrapStyle from '../styles/vendor/bootstrap.min.css';
import NProgress from '../styles/vendor/nprogress.css';

const Theme = ({ children }) => (
    <div>
        <style dangerouslySetInnerHTML={ { __html: BootstrapStyle } } />
        <style dangerouslySetInnerHTML={ { __html: NProgress } } />
        {children}
    </div>
);

Theme.propTypes = {
    children: PropTypes.oneOfType([
        PropTypes.arrayOf(PropTypes.element),
        PropTypes.element
    ]).isRequired,
};

export default Theme;
```

Here we added two line:

```
import NProgress from '../styles/vendor/nprogress.css';
```

and

```
<style dangerouslySetInnerHTML={ { __html: NProgress } } />
```

And finally, edit `app/pages/index.js` to add events when changing routes:

```
import Link from 'next/link';
import { Component } from 'react';
import { Button } from 'react-bootstrap';
import Theme from '../components/Theme';
import Router from 'next/router';
import Nprogress from 'nprogress';

// Straight away require/import scss/css just like in react.
import indexStyle from '../styles/index.scss';

class Index extends Component {
    constructor(props) {
        super(props);

        Router.onRouteChangeStart = () => Nprogress.start();
        Router.onRouteChangeComplete = () => Nprogress.stop();
        Router.onRouteChangeError = () => Nprogress.stop();
    }
    render() {
        return (
            // Wrap your page inside <Theme> HOC to get bootstrap styling.
            // Theme can also be omitted if react-bootstrap components are not used.
            <Theme>
                {
                    /*
                    Set indexStyling via dangerouslySetInnerHTML.
                    This step will make the below classes to work.
                    */
                }
                <style dangerouslySetInnerHTML={ { __html: indexStyle } } />

                <span className="heading">React.js | Next.js | Express.js | Bootstrap - SCSS</span>
                <span className="text">with SSR.</span>

                {/* Acquire static assets from express static directly. */}
                <div className="img-container">
                    <img alt="" src="/icons/github.png" />
                </div>

                <span className="text">
                    <a href="https://github.com/MustansirZia/next-express-bootstrap-boilerplate">
                    Github
                    </a>
                </span>
                <br />
                <div className="btn">
                    <Link href="/profile">
                        <Button bsStyle="primary">Click Me</Button>
                    </Link>
                </div>

                {/* Styling using styled-jsx. */}
                <style jsx>{`
                    .btn {
                        display: flex;
                        justify-content: center;
                    }`
                }
                </style>
            </Theme>
        );
    }
}

export default Index;

```

In here, the important is to add events in `constructor`:

```
Router.onRouteChangeStart = () => Nprogress.start();
Router.onRouteChangeComplete = () => Nprogress.stop();
Router.onRouteChangeError = () => Nprogress.stop();
```

Those events are triggered when we navigating among routes. To understand more about routing with *nextjs*, check official document here: [Routing](https://github.com/zeit/next.js/#routing)

You can also check the whole source code in Github: [demo-nextjs-nprogress](https://github.com/phuongnq/demo-nextjs-nprogress).

Finally, run application again and confirm `nprogress` is working as expected:

```
$ npm install
$ npm run dev
```

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