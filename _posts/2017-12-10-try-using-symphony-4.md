---
title: Technical review - Try using Symfony 4
date: 2017-12-10 22:38:20
tags: [tech, english, programming, symfony, framework]
categories: [english, programming]
---
As we may have known, Symfony 4 was released on November 30th. We can check the release detail from [here](https://symfony.com/blog/hello-symfony-4). This post means to provide some summary for the new release as well as a memo for how to do some simple demos using *Symfony 4*. To whom who is not familiar with the framework, *Symfony* is a set of reusable PHP components, and a PHP framework for web projects. Refer to [Symfony homepage](https://symfony.com/) for more detail.
# New features & Improvement
* Introduction of **Symfony Flex**, to manage and install application instead of *Symfony Installer* in previous version. In my opinion, *Symfony Flex* is some kind of wrapper for *Composer*. And actually, *Symfony Flex* is a Composer plugin that modifies the behavior of the require, update, and remove commands. To know more detail, refer to this [link](https://symfony.com/doc/current/setup/flex.html)
* Auto-registered & autowired services to keep you coding, not configuring. So *Symfony* makes it easier for configuration, using *yaml* file to register and wire services. We can check in the default *config/services.yaml* file how the syntax would be. And refer to this [post](https://symfony.com/doc/current/service_container/3.3-di-changes.html) to learn more about this new feature.
* *Symfony 4* source code is 70% smaller compared to *Symfony 3*. They call this new version as micro-framework. I did't work with *Symfony 3* previously, but compare to complicated version *1* and *2*, this should be definitely good news that makes thing simpler.
* The last change is about *convention*. *Symfony 4*'s project has smaller directory structure and use more common code convention for PHP in overall.

![Directory structure for Symfony 4](https://images2.imgbox.com/6e/d2/GH4wxeAH_o.png)

# Begin setup & sample project

To use *Symfony 4*, we need to make sure current of PHP is *7.1* or higher. So check your PHP version with command
```
php --version
```

If the version is not PHP *7.1*, install the newest one. In Ubuntu, I installed with command
```
sudo apt install php7.1
```

Since *Symfony 4* uses *composer*, we need to install the tool as well. Refer to follow link for instruction: [Install Composer](https://getcomposer.org/download/).

After installed *PHP 7.1* and *Composer*, we can create a new project with:
```
composer create-project symfony/skeleton my-project
```
This will create a new folder `my-project` which contains source code for new project. While trying the command, I had an error saying `php-xml` is not installed.

![php-xml missing error](https://images2.imgbox.com/ed/e5/QoNbQqVk_o.png)

To solve this, install `php7-xml` with follow commands:
```
sudo add-apt-repository -y ppa:ondrej/php
sudo apt update
sudo apt install -y php7.0-mbstring php7.0-zip php7.0-xml
```
Then install dev server for the project
```
cd my-project
composer require server --dev
```
This command will install web server in source code of `my-project` as a *composer* package. Please note that this is for running the project in local environment. In actual project, we should use *Apache* or *Nginx*.

Finally, we can run the project with command:
```
 php bin/console server:run
```
If you can see the web runs in `http://localhost:8000` showing welcome message *Welcome to Symfony 4.0.1* (version may different), you have succeeded setup a new project with *Symfony 4*
![Welcome to Symfony 4](https://images2.imgbox.com/b2/79/zpuxSTa2_o.png)
# Try demo app

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

Next step, we will try an other demo which provided from *Symfony* community. This demo is a blog service with Admin functions as well. The application include features to: show blog posts, add comments, update/edit/delete posts. This is quite standard demo so that we can understand the basic of framework.

We can clone this demo source code from *Github*:
```
git clone https://github.com/symfony/demo
```

In addition to the requirement of *PHP 7.1*, this project requires *PDO-SQLite PHP extension enabled*. We could enable this in Ubuntu with follow command:
```
sudo apt-get install php7.1-sqlite3
```

After installed requirement and cloned *Github* project, install requirement with *Composer*:
```
cd demo
composer install
```
`composer install` command would take several minutes to complete downloading all needed packages. In the meantime, we can check those installing packages and searching the Internet what they are. This is a good practice to deeply understand a framework.

After everything is installed, run application with local server:
```
php bin/console server:run
```
The web application should be available again with URL `http://localhost:8000`. When accessing web page, we can check that there are two buttons: `Browse application` and `Browse backend`.
![Demo application](https://images2.imgbox.com/eb/e2/1TI0j87M_o.png)

Please try browsing the web application within that two buttons. *Symfony community* created quite a nice application with very good design. We can also check the source code of each part while browsing. For example, source code for `GET post`:
![GET post source code](https://images2.imgbox.com/eb/1c/ESJMekF7_o.png)

This feature is pretty cool and it is convenient to understand how the framework structure.

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

This post provided some overall information for newly released framework *Symfony 4*. I didn't touch too much to detailed source code. For more detail information how the source code structure as well as the fundemental of *Symfony 4*, we can check from homepage [document](https://symfony.com/doc/current/quick_tour/the_big_picture.html). They provide very good document for understanding everything. And actually, the most effective way to learn a new framework is to read the source code. So we can read above `demo` source code to understand more. Within each controller, they provide detailed comments about how router, security works. For example, `BlogController`:
![BlogController](https://images2.imgbox.com/d5/a1/1H4asv9C_o.png)
