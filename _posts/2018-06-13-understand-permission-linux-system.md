---
title: "Understand Linux system file permission"
tags: [tech, english, linux]
share-img: /img/linux_file_permission.png
---

<table style="width: 100%">
<tr>
<td style="text-align:center">
<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//ws-na.amazon-adsystem.com/widgets/q?ServiceVersion=20070822&OneJS=1&Operation=GetAdHtml&MarketPlace=US&source=ac&ref=qf_sp_asin_til&ad_type=product_link&tracking_id=phuongnq-20&marketplace=amazon&region=US&placement=1788993195&asins=1788993195&linkId=01400fe06dd62553535dd378550fbcdf&show_border=false&link_opens_in_new_window=false&price_color=333333&title_color=0066C0&bg_color=FFFFFF">
</iframe>
</td>
<td style="text-align:center">
<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//ws-na.amazon-adsystem.com/widgets/q?ServiceVersion=20070822&OneJS=1&Operation=GetAdHtml&MarketPlace=US&source=ac&ref=qf_sp_asin_til&ad_type=product_link&tracking_id=phuongnq-20&marketplace=amazon&region=US&placement=1788990552&asins=1788990552&linkId=b5d83f88d6b1306fc872ee9ed51db52f&show_border=false&link_opens_in_new_window=false&price_color=333333&title_color=0066c0&bg_color=ffffff">
</iframe>
</td>
<td style="text-align:center">
<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//ws-na.amazon-adsystem.com/widgets/q?ServiceVersion=20070822&OneJS=1&Operation=GetAdHtml&MarketPlace=US&source=ac&ref=qf_sp_asin_til&ad_type=product_link&tracking_id=phuongnq-20&marketplace=amazon&region=US&placement=1784396877&asins=1784396877&linkId=77fcbb8b031914fc96edbb7187a0e501&show_border=false&link_opens_in_new_window=false&price_color=333333&title_color=0066c0&bg_color=ffffff">
</iframe>
</td>
</tr>
</table>

# Introduction

Files and directories are basic components for every Linux system. Wrongly assigning permisison to files or directories may lower security level of our system. This would cause our environment more vulnerable. For that reason, understand correctly how Linux files permission work is extremely important topic. We should only assign enough permission to certain files and only assign modification as well as excution permissions when neccessary. This manual will go through how permission works in Linux system.

# Manual

## Type of permissions

Basically, there are 3 types of permisison:

* **Read permission (r)**: User or group could read file content

* **Write permission (w)**: User or group could edit or modify file content

* **Execute permission (x)**: User or group could execute file

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

## Commands

To check a file permission we could use following command:

```
ls -la file_name
```

![](/img/linux_file_permission.png)

To change permission, use `chmod` command. `u` for **user**, `g` for **group**, `o` for **other**. We can all use `a` for **all**:

```
$ chmod ugo+rwx file_name
```

An other way is to use octal value:

```
$ chmod 777 file_name
```

`777` can understand as `111 111 111`, means permission is `rwxrwxrwx`.

We fill 0 if use does not have permission. For example `rwxr--r--` permission is `111 100 100` = `744`.

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

## Understand umask

`umask` is a Linux command to check default permission of newly created file or folder:

```
~ $ umask
0002
```

This mean:

* Any newly created folder with permission minus `777` - `002` = `775` or `rwxrwxr-x`.

* Any newly created file with permission: `777` - `002` - `111` = `664` or `rw-rw-r--`. This is because with newly created file, Linux system does not give `x` permission by default.

## Sticky bit

We can add sticky bit to a folder with following command:

```
$ chmod +t a_folder
```

With this, folder will have permisison with a `t` at the end:

```
drwxrwxrwt    2 PhuongNQ  staff       64 Jun 13 18:19 test
```

With sticky bit, all user can copy files to this folder but only owner can edit or delete files of that folder. (Even the permission here is 777).

<table style="width: 100%">
<tr>
<td style="text-align:center">
<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//ws-na.amazon-adsystem.com/widgets/q?ServiceVersion=20070822&OneJS=1&Operation=GetAdHtml&MarketPlace=US&source=ac&ref=qf_sp_asin_til&ad_type=product_link&tracking_id=phuongnq-20&marketplace=amazon&region=US&placement=1788993195&asins=1788993195&linkId=01400fe06dd62553535dd378550fbcdf&show_border=false&link_opens_in_new_window=false&price_color=333333&title_color=0066C0&bg_color=FFFFFF">
</iframe>
</td>
<td style="text-align:center">
<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//ws-na.amazon-adsystem.com/widgets/q?ServiceVersion=20070822&OneJS=1&Operation=GetAdHtml&MarketPlace=US&source=ac&ref=qf_sp_asin_til&ad_type=product_link&tracking_id=phuongnq-20&marketplace=amazon&region=US&placement=1788990552&asins=1788990552&linkId=b5d83f88d6b1306fc872ee9ed51db52f&show_border=false&link_opens_in_new_window=false&price_color=333333&title_color=0066c0&bg_color=ffffff">
</iframe>
</td>
<td style="text-align:center">
<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//ws-na.amazon-adsystem.com/widgets/q?ServiceVersion=20070822&OneJS=1&Operation=GetAdHtml&MarketPlace=US&source=ac&ref=qf_sp_asin_til&ad_type=product_link&tracking_id=phuongnq-20&marketplace=amazon&region=US&placement=1784396877&asins=1784396877&linkId=77fcbb8b031914fc96edbb7187a0e501&show_border=false&link_opens_in_new_window=false&price_color=333333&title_color=0066c0&bg_color=ffffff">
</iframe>
</td>
</tr>
</table>