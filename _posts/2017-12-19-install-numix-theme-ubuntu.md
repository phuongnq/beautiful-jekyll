---
title: Install Numix theme and icon for Ubuntu 17.10
date: 2017-12-19 22:07:11
tags: [ubuntu, manual, english]
categories: [english, programming]
---

**Ubuntu** is my favorite OS of all time. It's newest [release](https://www.ubuntu.com/desktop/1710) is *17.10*. The Ubuntu Desktop now uses GNOME instead of Unity which is great news. An other thing I like about *Ubuntu* or *Linux* operating system in general is the posibility to customize GUI. If you want, you can make your Ubuntu destop similar to an MacOS!

In this post, I am going to introduce the steps to install **Numix GTK** theme and icons. I choose this theme because of it's simplicity and clear look. Take a minute to check their [Github page](https://github.com/numixproject/numix-gtk-theme). And here is how it looks like for my Desktop:

![Ubuntu with Numix theme](https://images2.imgbox.com/15/37/4LOhrn5n_o.png)

# Manual

First of all, make sure to install **Tweaks**. Tweaks is a tool that make it easier to configure Ubuntu desktop environment settings. We will use *Tweaks* to configure theme and icons later in this post.

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

```
sudo apt install gnome-tweak-tool

```

Please note that Ubuntu *17.10* use *Gnome* as default. If you are using older version of *Ubuntu* or using *Unity*, the command would be:

```
sudo apt-get install unity-tweak-tool
```

After that, run following commands to install *Numix* theme:

```
sudo add-apt-repository ppa:numix/ppa
sudo apt-get update
sudo apt-get install numix-gtk-theme
```

And to install *icons* package:

```
sudo apt-add-repository ppa:numix/ppa
sudo apt-get update
sudo apt-get install numix-icon-theme numix-folders
sudo apt-get install numix-icon-theme-circle
sudo apt-get install numix-icon-theme-square
```

You can also install some wallpapers as a plus:

```
sudo apt-get install numix-wallpaper-*

```

After everything install, open **Tweaks** and configure. (Click Windows key, type *tweaks* to select the application).
Here is my configuration:

![Tweaks configuration](https://images2.imgbox.com/5c/6a/WofcqXXS_o.png)

# Conclusion

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

In this post, I introduced how to install theme and icons for *Ubuntu*. There are hundreds of *themes* or *icon* sets available in the Internet. You can do a research and choose your preferer. There are many icon sets look more fancy with a lot of color. But for me, simplicity is the best so I chose a theme without too much flashy! For *Tweaks*, there are also more configuration so please feel free to do some modification.

Again, **Ubuntu** empower users to make the change to almost everything to our desktop. If you interested in, just Google how to do it!
