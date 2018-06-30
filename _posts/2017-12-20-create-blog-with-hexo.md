---
title: How to create technical blog with Hexo and deploy to EC2
date: 2017-12-20 22:22:46
tags: [tech, english, hexo, nodejs, ec2, manual]
categories: [english, programming]
---

Recently I was starting to write my technical, life hacking blog [www.phuongnq.me](http://www.phuongnq.me). As an engineer, I find writing blog is a great way to create output. And it also yields huge return in long term for the writing investment. Some benifits I could think of are:

* Being known as an expert for a specific field, for example: NodeJS, PHP, GoLang, server side architecture, front-end side frameworks, etc
* Expand your network by exchanging comments, openion with other people in same field
* Getting recruited
* Being better at writing, for me in English which is not my native language, etc
* To understand more about the subject: only when you can describe a matter to other people, then you actually understand what it is.

And for sure, by writing blog, we will get improve. Just small step everyday, we could accumulate extremly big improvment in the future!

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

I am a fan of NodeJS, and for that reason, I want to use some *NodeJS* based frameworks for [my blog](http://www.phuongnq.me). Many people may be familiar with [Wordpress](https://wordpress.com/), a free and open-source CMS (content management system) based on *PHP*. But compare to *NodeJS*, *PHP* has too many configurations, normally for *Apache*. That takes our time to do everything like install *Apache*, create *.htaccess*, etc. After some researches and recommendation from friend, I decidied to use **Hexo** for blogging. Here is it's [homepage](https://hexo.io/).

![Hexo blog framework](https://images2.imgbox.com/01/a8/EplZFzDw_o.png)

**Hexo** is a fast, simple & powerful blog framework. It was written in *NodeJS*, that means blazing fast and you can scale when there are more traffics! And **Hexo** has *Markdown* support, which is best markup language to writing document for engineers. An other great thing for **Hexo** is that deployment process is super easy with only 1 command. Last but not least, they provide many plugins, easy to modify themes, and the configuration is via *yml* file, which also makes engineers happy.

Here is how I use **Hexo**

* My local environment: **Ubuntu** *17.10*
* Server: *Amazon EC2* with **Ubuntu** instance

The processes are quite similar between *local* and *production* environment with an exception for deploying command. Here are the steps:

1. Make sure *node*, *npm* were installed. If you didn't, refer to official [document](https://docs.npmjs.com/getting-started/installing-node) for instruction.

2. Install `hexo-cli` globally with following command:

	```
	npm install hexo-cli -g
	```

	FYI, `cli` is abbreviation for **Command line interface**. So above command would install *Hexo command line interface* globally.

3. Setup your blog

	Please refer to steps [here](https://hexo.io/docs/setup.html). In my case for [wwww.phuongnq.me](http://www.phuongnq.me):

	```
	hexo init phuongnq.me
	cd phuongnq.me
	npm install
	```

	After above commands, directory created an in this screenshot:
	![blog page structure](https://images2.imgbox.com/22/dd/AlIEFINI_o.png)

	You can refer their document to check meaning of all directories. There are some note from me:

	**_config.yml**: put your configuration for your blog. For example: Blog name, description, URL, which theme to use, etc

        ```
        # Hexo Configuration
        ## Docs: https://hexo.io/docs/configuration.html
        ## Source: https://github.com/hexojs/hexo/

        # Site
        title: PhuongNQ Note
        subtitle:
        description:
        author: Nguyen Phuong (Phil)
        author_title: I'm full stack developer living in Japan. I want to learn something new everyday.
        avatar: https://scontent-nrt1-1.xx.fbcdn.net/v/t31.0-8/13975431_10207062330058043_5626558392744494659_o.jpg?oh=36384c2901c012c7c1bf6ebbd961dde6&oe=5AD13BB1
        language:
        timezone:

        # URL
        ## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
        url: http://www.phuongnq.me
        root: /
        permalink: :year/:month/:day/:title/
        permalink_defaults:

        # Directory
        source_dir: source
        public_dir: public
        tag_dir: tags
        archive_dir: archives
        category_dir: categories
        code_dir: downloads/code
        i18n_dir: :lang
        skip_render:

        # Writing
        new_post_name: :title.md # File name of new posts
        default_layout: post
        titlecase: false # Transform title into titlecase
        external_link: true # Open external links in new tab
        filename_case: 0
        render_drafts: false
        post_asset_folder: false
        relative_link: false
        future: true
        highlight:
        enable: true
        line_number: true
        auto_detect: false
        tab_replace:
        
        # Home page setting
        # path: Root path for your blogs index page. (default = '')
        # per_page: Posts displayed per page. (0 = disable pagination)
        # order_by: Posts order. (Order by date descending by default)
        index_generator:
        path: ''
        per_page: 10
        order_by: -date
        
        # Category & Tag
        default_category: uncategorized
        category_map:
        tag_map:

        # Date / Time format
        ## Hexo uses Moment.js to parse and display date
        ## You can customize the date format as defined in
        ## http://momentjs.com/docs/#/displaying/format/
        date_format: YYYY-MM-DD
        time_format: HH:mm:ss

        # Pagination
        ## Set per_page to 0 to disable pagination
        per_page: 10
        pagination_dir: page

        # Extensions
        ## Plugins: https://hexo.io/plugins/
        ## Themes: https://hexo.io/themes/
        theme: simple-japanese

        # Sidebar
        widgets:
        -  search
        -  profile
        -  recent_posts
        -  tagcloud
        -  archive

        # Contact
        contact:
        url: https://github.com/phuongnq
        icon: github # font-awesome icon. e.x) fa-github
        ```

    **themes** folder hold your theme, I'm using *simple-japanese* theme because I sometimes write in Japanese and I feel the theme is simple with clear view. You can check this theme source code and install steps in [Github](https://github.com/mitsuruog/hexo-theme-simple-japanese).

    **source/_posts**: all blog pages here. Files have extension *.md* which use Markdown language.

4. Create new post:

	```
 hexo new post create-blog-with-hexo
	```

	This command would output:

	```
	INFO  Created: ~/phuongnq.me/source/_posts/create-blog-with-hexo.md
	```

	This let you know the position of your blog content file, which name is `create-blog-with-hexo.md`.

5. To run locally:

	First install *server* *npm* module:

	```
npm install hexo-server --save
	```

	Then start server:

	```
hexo server
	```

	This command output:

	```
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
	```

	And you can check your website in *localhost* with port *4000*.

6. Finally, to deploy to *EC2* instance:

	The step would be similar from step 1 to 4. For step 5, we run in static mode, port 80:

	```
	sudo hexo server -s -p 80
	```

	In static mode, only files in the public folder will be served and file watching is disabled. So you need to run `generate` command after adding new blog post:

	```
	hexo generate
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

# Conclusion

In this post, I introduced a very breaf manual of using **Hexo** to create blog. There are other cool things we could do with **Hexo**. They provide customization for permalinks, themes, templates, variables, helpers, i18n or plugins as well. Please make sure to check their official document, and try something by yourselve.