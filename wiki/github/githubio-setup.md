---
layout: wiki
title: Setting up github-pages
---
These are some notes I took while setting up my own personal github-pages site.

Installed the specific version of ruby mentioned [here](https://pages.github.com/versions/) using the [ruby version manager](https://rvm.io/).

Remember to do [this](https://rvm.io/integration/gnome-terminal).
Still not really sure if that is the Right Thing To Do<sup>(TM)</sup>.

Started a new blank site with jekyll, because the supported themes did not interest me.

```
$ jekyll new <my-site-name> --blank
```
After running that command, a new folder called 'my-site-name' is created in the local folder.

Tested site by doing the following:

```
$ cd <my-site-name>
$ jekyll serve
```

Generating without an explicit theme still outputs some kind of stylesheet to /assets/css/style.css.

Looks like an older version of [normalize.css](https://necolas.github.io/normalize.css/).

Decided to use it for now, in addition to the custom css file I put in /assets/css/site.css.

Created two layout files in /_layouts folder (home.html and wiki.html).

Fiddled around until it looked acceptable.
