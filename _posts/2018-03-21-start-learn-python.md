---
title: "Learn Python - Start introduction"
tags: [tech, english, python]
categories: [english]
share-img: /img/python-logo.png
---

![](/img/python-logo.png)

## Introduction

So I start learning **Python**. There are some reasons for my decision.
First of all, there are some languages that are easy to learn for beginner: **JavaScript** and **Python**. **JavaScript** is famous in Web application domain, expecially after the appearance of **NodeJS** which is used for server side. In the other hand, **Python** is more general purpose programming language, and also easy to learn. **Python** is famous in data, science domains. There is a Youtube channel [CS Dojo](https://www.youtube.com/channel/UCxX9wt5FWQUAAz4UrysqK9A) that mentions which languages we should learn first, check out the video here:
<iframe width="560" height="315" src="https://www.youtube.com/embed/poJfwre2PIs" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

I myself is a *JavaScript/NodeJS* web developer so quite familiar with *JavaScript* stack. And I want to learn **Python** as an other script language. These are some benefits or reasons that I could think of if learning *Python*:

* It is easy to learn as programming language or learn algorithm

* There are many samples of success stories which used *Python*. Check out [here](https://www.python.org/about/success/)

* Python is famous in data, science, AI domains. Actually, some of my friends are fan of AIs, they are using Python. I would like to know a little about the language to take conversation with them :).

* Python is used a lot in *Google*, include *Youtube*. As an Youtube engineer mentioned:

    > Python is fast enough for our site and allows us to produce maintainable features in record times, with a minimum of developers," said Cuong Do, Software Architect, YouTube.com.

    I myself is a fan of *Google* stack, so *Python* should be a good choice to learn.

* Python is incredible Growing. Checkout the artical from [StackOverflow](https://stackoverflow.blog/2017/09/06/incredible-growth-python/)
![](/img/growth_major_languages.png)

* It is **general purpose language**: you can do Web development,  Desktop GUI/CUI application development, Backend jobs, Scripting, Data Analysis, Machine Learning , Computer Vision, Game development, Web Scrapping, Browser Automation, etc with Python.

* Python has great community and documentation from official website is quite good. Check it out [here](https://www.python.org/doc/)

* There are ton more reasons, just searching `why learn Python` in **Quora** and check more answers [here](https://www.quora.com/search?q=why+learn+python)

## Python versions

There are two major versions of *Python* we should considerion: *Python 3* or *Python 2*? Not similar to other languages, in *Python*, while they released version 3, there are still a lot of source code written in version 2.x (especially 2.7). And actually, the community still support with updating version 2.

I also do a quick search on [Quora](https://www.quora.com/search?q=python+2+or+3) which version should I use: Python 2 or Python 3. So the conclusion is: Use Python 3 if you start learning or start new project. Please checkout *Quora* for the reason.

One more reason for myself is that I would like to learn *Django* - Python web framework and newest version comes with Python 3. Check the [FQA - What Python version can I use with Django?](https://docs.djangoproject.com/en/2.0/faq/install/#faq-python-version-support)

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

## Install Python 3 in Ubuntu

Make sure your system has Python 3 installed:

```
$ sudo apt-get update
$ sudo apt-get install python3.6
```

Start command `python3.6` to check it is installed:

```
$ python3.6
Python 3.6.3 (default, Oct  3 2017, 21:45:48) 
[GCC 7.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

Though, it is inconvenience to type `python3.6` so I made an *alias* to link `python3.6` to `python`:

```
$ vim ~/.bash_aliases
```

Add following line:

```
alias python=python3
```

Then check it was linked:

```
$ source ~/.bash_profile
$ python --version
Python 3.6.3
```

Finally make sure to install `pip` which is Python package management tool:

```
$ sudo apt-get install python3-pip
```

Check it is available with:

```
$ pip3 --version
pip 9.0.1 from /usr/lib/python3/dist-packages (python 3.6)
```

I also made an alias for `pip3` -> `pip`:

```
alias pip=pip3
```

## Editor to write Python code

My favorite text editor is **Visual Studio Code** so I would like to use it for writting Python source code. There is an official document for this [here - Python in Visual Studio Code](https://code.visualstudio.com/docs/languages/python)

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

## Test with `hello world`

* Create a new file `test.py`, add following line:

```
print("Hello, World!")
```

From command line tool:

```
$ python test.py 
Hello, World!
```

And that's it. We've succeeded running the very first Python hello world application. Please check for more articals about Python in my blog.

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
