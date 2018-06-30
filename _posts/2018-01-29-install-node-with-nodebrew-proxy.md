---
title: "How to use node with nodebrew under proxy"
tags: [tech, english, node, nodebrew, proxy]
categories: [english, programming]
---

Normally we can use just install and use `node`, `npm` packages directly from the Internet. But under some special circumstances, we may need to install via proxy or use different node version. We can do that with `nodebrew` and here is the manual.

Nodebrew GitHub page: [https://github.com/hokaccha/nodebrew](https://github.com/hokaccha/nodebrew)


## Install node under proxy

To install with proxy, first export `http_proxy` and `https_proxy`:

```
$ export http_proxy="http://<proxy_host>:<proxy_port>"
$ export https_proxy="https://<proxy_host>:<proxy_port>"
```

> Above commands are for `bash`, if you use other `shell` application, make sure to use correct commands.

Install with `curl`:

```
$ curl -L git.io/nodebrew | perl - setup
```

Make sure to add `nodebrew` directory to `$PATH`. In `bash` we can modify to add to `~/.bash_profile`:

```
export PATH=$HOME/.nodebrew/current/bin:$PATH
```

Reload:

```
$ source ~/.bash_profile
```

Confirm `nodebrew` installed with:

```
$ nodebrew help
```

To install `node`:

```
$ nodebrew ls-remote

...
v8.9.0    v8.9.1    v8.9.2    v8.9.3    v8.9.4

v9.0.0

v9.1.0

v9.2.0    v9.2.1

v9.3.0

v9.4.0
...
```

To install a version:

```
$ nodebrew install-binary v9.4.0
```

Confirm installed versions:

```
$ nodebrew ls

v0.12.4
v4.1.1
v5.7.0
v6.5.0
v9.4.0

current: v6.5.0
```

To use a version:

```
$ nodebrew use v9.4.0
```

Check `node` with command:

```
$ node --version

v9.3.0
```

## Install npm package under proxy

After installed `node`, check `npm` was installed:

```
$ npm --version

5.5.1
```

To configure proxy:

```
$ npm config set proxy http://<host>:<port>
$ npm config set https-proxy https://<host>:<port>
```

After that we can type `npm install` inside a node project as normal.

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