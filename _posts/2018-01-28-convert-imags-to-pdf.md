---
title: "Convert Image files to PDF in Ubuntu"
tags: [tech, english, ubuntu, imagemagick, convert]
---

# Introduction

In Windows OS or MacOS, there are many ways to convert multiple image files (.png, .jpg) to a single .pdf file. How can we do the similar thing using *Ubuntu*? The answer is to use **ImageMagick** command tools `convert`.

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

If you don't have **ImageMagick** installed, refer to official [document]() for the manual how to install in Ubuntu.

We can install from source code for newest version or using `apt-get` for a deliverred version:

```
$ sudo apt-get install imagemagick
```

Check installed **ImageMagick** with command:

```
$ convert --version
Version: ImageMagick 6.9.7-4 Q16 x86_64 20170114 http://www.imagemagick.org
Copyright: © 1999-2017 ImageMagick Studio LLC
License: http://www.imagemagick.org/script/license.php
Features: Cipher DPC Modules OpenMP 
Delegates (built-in): bzlib djvu fftw fontconfig freetype jbig jng jpeg lcms lqr ltdl lzma openexr pangocairo png tiff wmf x xml zlib
```

After make sure **ImageMagick** installed, we can easily convert .png, .jpg file to .pdf with follow command:

```
convert "*.jpg" -quality 100 output.pdf
```

This command would take all .jpg files in current folder and convert to output.pdf with image quality 100%. We can do a combination of *.jpg* and *.png* such as:

```
convert "*.{png,jpeg}" -quality 100 outfile.pdf
```

To know other options, commands with `convert`, try using `help`:

```
convert help
```

**ImageMagick** is a convenient tool to process images files. They can do many other things. Please check their [homepage](http://www.imagemagick.org) for more detail or pick a book about **ImageMagick** if you are interested in the tool.

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
