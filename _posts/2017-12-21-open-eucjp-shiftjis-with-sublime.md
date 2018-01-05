---
title: How to open EUC-JP or SHIFT-JIS enconded Japanese files with Sublime Text 3
date: 2017-12-21 21:05:34
tags: [tech, manual, sublime3, english, encoding]
---

In Japanese, besides *UTF-8*, there are other encodings such as *EUC-JP* or *SHIFT-JIS*.

Normally we work with *UTF-8* encoded files. But if you are working for Japanese companies, especially old developed websites, there may be a chance you would have to work with other encoding methods. If we open a SHIFT-JIS or EUC-JP encoded files with **Sublime Text 3**, Japanese characters would be broken. And if you are careless, you may save the file in *UTF-8* after edited and the file could no longer be reverted to correct encoding. (Technically, we could always revert if the file is under *Github*, though).

<p stype="text-align: center">
	<img src="https://images2.imgbox.com/2e/82/Y2xAqKr8_o.png" />
</p>

There is an easy solution by using some **plugins**.

# Manual

1. [ConvertToUTF8](https://github.com/seanliang/ConvertToUTF8)

	Install this *package* from **Package Control**. Refer to manual at the end of this post how to do. This package convert opening file to *UTF-8* while editing, and convert back to original encoding when saving file.

2. [Codecs33](https://github.com/seanliang/Codecs33)
	Due to some issue of embedded Python with **Sublime Text 3**, plugin in *1* may not work properly. So we need to install **Codecs33** as well.

# How to install plugin with Sublime Text 3

1. `Ctrl + Shift + P` to open *Command Palette*, type **install**
2. Select **Package Control: Install Package**, Enter
3. Type package name to search
4. From search result, select right package