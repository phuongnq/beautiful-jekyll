---
title: "【Node.js】Upgrade npm package up-to-date"
tags: [programming, nodejs, javascript]
categories: [programming, english]
share-img: /img/nodejs.jpeg
---

# Situation

Start a new project from some boilerplates. You need to upgrade all npm packages to *up-to-date* state.

# Manual

Check current outdated packages with `npm outdated` command:

```bash
$ npm outdated
Package                    Current  Wanted  Latest  Location
autoprefixer                 9.1.5   9.1.5   9.4.4   a-tool-name
eslint                       5.6.1  5.12.0  5.12.0  a-tool-name
eslint-plugin-jsx-a11y       6.1.1   6.1.2   6.1.2  a-tool-name
eslint-plugin-react         7.11.1  7.12.3  7.12.3  a-tool-name
express                     4.16.3  4.16.4  4.16.4  a-tool-name
next                         7.0.1   7.0.2   7.0.2  a-tool-name
node-sass                    4.9.3  4.11.0  4.11.0  a-tool-name
nodemon                     1.18.4  1.18.9  1.18.9  a-tool-name
normalize.css                8.0.0   8.0.1   8.0.1  a-tool-name
pm2                          3.2.2   3.2.7   3.2.7  a-tool-name
raw-loader                   0.5.1   0.5.1   1.0.0  a-tool-name
react                       16.5.2  16.7.0  16.7.0  a-tool-name
react-dom                   16.5.2  16.7.0  16.7.0  a-tool-name
react-icons                  3.1.0   3.3.0   3.3.0  a-tool-name
sweetalert2                 7.28.4  7.33.1  7.33.1  a-tool-name
winston-daily-rotate-file    3.3.3   3.5.2   3.5.2  a-tool-name
```

Try updating everything with `npm update`:

```bash
$ npm update

> node-sass@4.11.0 install /opt/some-dummy-directory/src/node_modules/node-sass
> node scripts/install.js

Downloading binary from https://github.com/sass/node-sass/releases/download/v4.11.0/darwin-x64-67_binding.node
Download complete  ⸩ ⠋ :
Binary saved to /opt/some-dummy-directory/src/node_modules/node-sass/vendor/darwin-x64-67/binding.node
Caching binary to /home/dummy-user/.npm/node-sass/4.11.0/darwin-x64-67_binding.node

> node-sass@4.11.0 postinstall /opt/some-dummy-directory/src/node_modules/node-sass
> node scripts/build.js

Binary found at /opt/some-dummy-directory/src/node_modules/node-sass/vendor/darwin-x64-67/binding.node
Testing binary
Binary is fine

> nodemon@1.18.9 postinstall /opt/some-dummy-directory/src/node_modules/nodemon
> node bin/postinstall || exit 0

npm WARN ajv-keywords@3.2.0 requires a peer of ajv@^6.0.0 but none is installed. You must install peer dependencies yourself.
npm WARN tool-persona@1.0.0 license should be a valid SPDX license expression

+ normalize.css@8.0.1
+ eslint-plugin-react@7.12.3
+ eslint-plugin-jsx-a11y@6.1.2
+ node-sass@4.11.0
+ react@16.7.0
+ nodemon@1.18.9
+ react-icons@3.3.0
+ react-dom@16.7.0
+ winston-daily-rotate-file@3.5.2
+ express@4.16.4
+ pm2@3.2.7
+ eslint@5.12.0
+ sweetalert2@7.33.1
+ next@7.0.2
added 23 packages from 91 contributors, removed 62 packages, updated 131 packages, moved 15 packages and audited 14739 packages in 36.453s
```

Double check with `npm outdated`:

```bash
$ npm outdated
Package       Current  Wanted  Latest  Location
autoprefixer    9.1.5   9.1.5   9.4.4  a-tool-name
raw-loader      0.5.1   0.5.1   1.0.0  a-tool-name
```

Upgrade remaining packages manually:

```bash
$ npm install --save autoprefixer@9.4.4
$ npm install --save raw-loader@1.0.0
```

Check again outdated package:

```bash
$ npm outdated
```

At this point, nothing should be output. Your `package.json` should be *up-to-date*

# References

https://docs.npmjs.com/cli/outdated.html

https://docs.npmjs.com/updating-packages-downloaded-from-the-registry