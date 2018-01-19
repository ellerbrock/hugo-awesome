![hugo-awesome](https://github.frapsoft.com/top/open-source-v1.png)

# hugo-awesome

[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.svg)](https://github.com/ellerbrock/open-source-badges/) [![Gitter Chat](https://badges.gitter.im/frapsoft/frapsoft.svg)](https://gitter.im/frapsoft/frapsoft/) [![MIT Licence](https://badges.frapsoft.com/os/mit/mit.svg?v=103)](https://opensource.org/licenses/mit-license.php)

## Introduction

Tempalte for [Hugo](https://gohugo.io), a static page generator.  
Layout with the [Bulma](https://bulma.io/) CSS Framework based on Flexbox.

## Cloud Ready

Build to run after initial setup in every environment without further configuration,  
but flexible enought to execute hugo, compile [SASS](http://sass-lang.com/install) to CSS with the help of a [Gulp](https://gulpjs.com/) Build automatically.  


## Screenshots

![home](https://github.frapsoft.com/top/hugo-awesome-home.jpg)

<br><br><br><br>

![go](https://github.frapsoft.com/top/hugo-awesome-go.jpg)


## How to use

- `hugo new site yoursite`
- `cd yoursite/themes`
- `git clone https://github.com/ellerbrock/hugo-awesome`
- `mv .env docker-compose.yml ..`
- `cd ..`


## Hugo Configuration

Example `config.toml`:

```
baseURL = "https://ellerbrock.github.io"
title = "💫 Awesome Hugo 🦄"
theme = "hugo-awesome"
disableHugoGeneratorInject = true
publishDir = "docs"
ignoreFiles = [ "\\.dev$", "\\.backup$", "\\.old$"  ]
pluralizeListTitles = true

[author]
  name = "Maik Ellerbrock"
  homepage = "https://frapsoft.com"
  github = "https://github.com/ellerbrock"
  twitter = "https://twitter.com/frapsoft"
  facebook = "https://www.facebook.com/frapsoft"
  googleplus = "https://plus.google.com/116540931335841862774"
```

## Docker Build Configuration

[Gulp](https://gulpjs.com/) Build Pipeline with SASS Compiler ready to run out of the box.

`.env`

```
PORT_HUGO=127.0.0.1:1313

DIR_HUGO_DEV=./
DIR_HUGO_PROD=./export

DIR_SASS=./themes/hugo-awesome/static/sass
DIR_CSS=./themes/hugo-awesome/static/css

FILES_SASS=*.+(sass|scss)
GULP_DEBUG=true
```

`docker-compose.yml`

```
version: '3'

services:

  hugo:
    image: ellerbrock/hugo:latest
    working_dir: /site
    command: server --bind 0.0.0.0 -w
    volumes:
      - ${DIR_HUGO_DEV}:/site
    ports:
      - ${PORT_HUGO}:1313
    networks:
      - webdev

  gulp:
    image: ellerbrock/alpine-gulp-sass
    volumes:
      - ${DIR_SASS}:/site/sass
      - ${DIR_CSS}:/site/css
    environment:
      - SASS=${FILES_SASS}
      - GULP_DEBUG=${GULP_DEBUG}
    networks:
      - webdev

networks:
  webdev:
    driver: bridge
```


## What's next?

- Infrastructure as Code a Cloud Environment for different Provider (AWS, Digital Ocean, Alibaba Cloud ...)
- Create a CI/CD Template and Open Source it
- Documentation
- Publish Template


<!--
## Build Status

[![Deadlink Test](https://travis-ci.org/ellerbrock/hugo-awesome.svg?branch=master)](https://travis-ci.org/ellerbrock/awesome-koa)

**Info:** Green Build Status means there should be no Deadlinks in this List.<br>
You can find the Testfiles on [travis-deadlink-scanner](https://github.com/ellerbrock/travis-deadlink-scanner).
-->

## Contact

[![Github](https://github.frapsoft.com/social/github.png)](https://github.com/ellerbrock/)[![Docker](https://github.frapsoft.com/social/docker.png)](https://hub.docker.com/u/ellerbrock/)[![npm](https://github.frapsoft.com/social/npm.png)](https://www.npmjs.com/~ellerbrock)[![Twitter](https://github.frapsoft.com/social/twitter.png)](https://twitter.com/frapsoft/)[![Facebook](https://github.frapsoft.com/social/facebook.png)](https://www.facebook.com/frapsoft/)[![Google+](https://github.frapsoft.com/social/google-plus.png)](https://plus.google.com/116540931335841862774)[![Gitter](https://github.frapsoft.com/social/gitter.png)](https://gitter.im/frapsoft/frapsoft/)

## License 

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a> [![MIT license](https://badges.frapsoft.com/os/mit/mit-125x28.png?v=103)](https://opensource.org/licenses/mit-license.php)

This work by <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/ellerbrock" property="cc:attributionName" rel="cc:attributionURL">Maik Ellerbrock</a> is licensed under a <a rel="license" href="https://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a> and the underlying source code is licensed under the <a rel="license" href="https://opensource.org/licenses/mit-license.php">MIT license</a>.
