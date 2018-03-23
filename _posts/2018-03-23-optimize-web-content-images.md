---
title: "What is optimize images for web and why we should care about it"
tags: [tech, english, web, optimize]
share-img: /img/web_optimize.jpg
---

![](/img/web_optimize.jpg)

# Why we should care about it

In general, website loading speed is a critical element that affect the success of a web service. If you think loading speed is important but not that critical, think about it again! Every second of delaying page load could result: much fewer page views, decrease in customer satisfition or conversion rate as well.

There are many studies proved that every second of latency would affect conversion, especially for e-commerce websites. Actually, according to research from *Amazon*:

> Every 100ms delay costs 1% of sales

In the SEO world, the story is similar. Website loading time influences your SEO ranking. The rule is simple: slow sites rank lower. According to [a post from Google](https://webmasters.googleblog.com/2010/04/using-site-speed-in-web-search-ranking.html):

> Speeding up websites is important — not just to site owners, but to all Internet users. 
Faster sites create happy users and we've seen in our internal studies that when a site responds slowly, visitors spend less time there. But faster sites don't just improve user experience; recent data shows that improving site speed also reduces operating costs. 
Like us, our users place a lot of value in speed — that's why we've decided to take site speed into account in our search rankings. We use a variety of sources to determine the speed of a site relative to other sites.

An other factor to consider is for mobiles. With PC, we normally use strong Wifi or cable internet connection. But for mobiles, we connect with 3G/4G connection. And if new customers connect to your website using a mobile device, there is a chance she would not comeback again if your website is too slow.

There are many factors we could consider while optimize website load speed, such as: improve caching, optimize JavaScript/CSS contents, etc. But the easies factor we could optimize is images. I supprise that there are many websites that use so big size image to just display a thumbnail!

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

# How to optimize images

Google has a very convenient tool to check your page speed, including how good your images are. Check [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/). Just input your website url and Google would analyze your score for mobile and PC, max is 100. Here I take sample of [wwww.rakuten.com](www.rakuten.com), an e-commerce website from **Rakuten Inc**.

![](/img/pagespeed_insight_sample.png)

The score is about average.

The nice thing about **PageSpeed Insight** is that they also provide strategy to optimize your content. Please check detail post for optimizing images [here](https://developers.google.com/speed/docs/insights/OptimizeImages).

For very quick summary, optimize images usually includes optimizing **JPEG**, **PNG** and **GIF** files. Each file type has difference attributes and need difference optimize algorithms. We can use tool like [ImageMagick](http://www.imagemagick.org/script/index.php) to optimize images:

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

## JPEG

**JPEG** is lossy format, we can optimize JPEG images by reducing quality. According to post from Google:

> Reduce quality to 85 if it was higher. With quality larger than 85, the image becomes larger quickly, while the visual improvement is little.

> Reduce Chroma sampling to 4:2:0, because human visual system is less sensitive to colors as compared to luminance.

> Use progressive format for images over 10k bytes. Progressive JPEG usually has higher compression ratio than baseline JPEG for large image, and has the benefits of progressively rendering.

> Use grayscale color space if the image is black and white.

Command with **ImageMagick**:

```
convert INPUT.jpg -sampling-factor 4:2:0 -strip [-resize WxH] [-quality N] [-interlace JPEG] [-colorspace Gray/sRGB] OUTPUT.jpg
```

## PNG and GIF

**PNG** and **GIF** are lossless format. The strategy according to Google:

> Always convert GIF to PNG unless the original is animated or tiny (less than a few hundred bytes).

> For both GIF and PNG, remove alpha channel if all of the pixels are opaque.

Commands with *ImageMagick*:

```
convert INPUT.gif_or_png -strip [-resize WxH] [-alpha Remove] OUTPUT.png
```

```
convert cuppa.png -strip cuppa_converted.png
```

Still, we can optimize PNG files to quality around 80%-85% to get smaller images. This would be case-by-case depends on actuall websites.

## Tools other than *ImageMagick*

Google use **ImageMagick** as a simulation how we could optimize images. But as from my experiment, there are some cases *ImageMagick* is not the best choice. Actually for **PNG**, there are cases that *ImageMagick* would make optimized file larger than original file. To get the best optimized images, consider to use other open source libraries. [This website](https://jamiemason.github.io/ImageOptim-CLI/) compares some open sources libraries about optimizing each type of images.

And again, each type of image (**JPEG**, **PNG**, **GIF**) has different attributes, so in order to get best optimized quality, we have to learn deeper about each type and decide best algorithm for them. If you don't have time to develop your own optimizer, there is a software for MacOS users, which I found to have very well implementation, much better than *ImageMagick*. Check it out [ImageOptim](https://imageoptim.com/mac).

An other choice for big web service is to use CDN, like [Akamai](https://www.akamai.com/). These CDN services also come with solution for optimizing images. But of course, we have to pay extra money for it.

If you need any consultant to develop your own optimize tool, please feel free to contact me: nquangphuong[at]gmail.com. I can create tool like internal application for optimizing your images.

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