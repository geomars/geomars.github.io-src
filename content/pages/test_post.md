Title: Setting up my pelican blog on github 
Date: 2016-01-10 11:35
Modified: 2016-05-05 19:30
Category: Tech
Subcategory: Blogging
Authors: geomars
Tags: pelican, python
Summary: blog setup

There's a lot of better tutorial out there regarding how to set up a Pelican based blog, some of them are on the reference, but this is a simple documentation on how I build my Pelican blog on Github. 

## Create virtualenv 


```language
tarzan@cave:~/auuow$ mkdir banana && cd banana
tarzan@cave:~/auuow/banana$ virtualenv pelicanpy2
New python executable in /home/tarzan/banana/pelicanpy2/bin/python
Installing setuptools, pip, wheel...done.

tarzan@cave:~/auuow/banana$ source pelicanpy2/bin/activate
```
 
 
 
## Install pelican and additional libraries

```language
(pelicanpy2) tarzan@cave:~/auuow/banana$ pip install pelican
(pelicanpy2) tarzan@cave:~/auuow/banana$ pip install markdown fabric beautifulsoup4 lxml pillow typogrify
(pelicanpy2) tarzan@cave:~/auuow/banana$ pip freeze > requirements.txt
```
    
 
 
## Add pelican plugins and themes

```language
(pelicanpy2) tarzan@cave:~/auuow/banana$ git init
(pelicanpy2) tarzan@cave:~/auuow/banana$ git add .
(pelicanpy2) tarzan@cave:~/auuow/banana$ git commit -m "Initial commit"
(pelicanpy2) tarzan@cave:~/auuow/banana$ git submodule add https://github.com/getpelican/pelican-plugins.git plugins
(pelicanpy2) tarzan@cave:~/auuow/banana$ git submodule add https://github.com/getpelican/pelican-themes.git themes
(pelicanpy2) tarzan@cave:~/auuow/banana$ git add .
(pelicanpy2) tarzan@cave:~/auuow/banana$ git commit -m "Add plugins and themes"
```


## Start building blog

```language
(pelicanpy2) tarzan@cave:~/auuow/banana$ pelican-quickstart

Welcome to pelican-quickstart v3.7.1.
This script will help you create a new Pelican-based website.
Please answer the following questions so this script can generate the files
needed by Pelican.   
> Where do you want to create your new web site? [.] 
> What will be the title of this web site? geoblog 
> Who will be the author of this web site? geomars
> What will be the default language of this web site? [en] 
> Do you want to specify a URL prefix? e.g., http://example.com   (Y/n) 
> What is your URL prefix? (see above example; no trailing slash) https://geomars.github.io
> Do you want to enable article pagination? (Y/n)
> How many articles per page do you want? [10] 5
> What is your time zone? [Europe/Paris] Asia/Jakarta
> Do you want to generate a Fabfile/Makefile to automate generation and publishing? (Y/n) 
> Do you want an auto-reload & simpleHTTP script to assist with theme and site development? (Y/n) 
> Do you want to upload your website using FTP? (y/N) 
> Do you want to upload your website using SSH? (y/N) 
> Do you want to upload your website using Dropbox? (y/N) 
> Do you want to upload your website using S3? (y/N) 
> Do you want to upload your website using Rackspace Cloud Files? (y/N) 
> Do you want to upload your website using GitHub Pages? (y/N) y
> Is this your personal page (username.github.io)? (y/N) y
Done. Your new project is available at /home/tarzan/cave/auuow/banana

(pelicanpy2) tarzan@cave:~/auuow/banana$ git add .
(pelicanpy2) tarzan@cave:~/auuow/banana$ git commit -m "Initialize pelican"
 
```


## Setup pelican configuration
```language
(pelicanpy2) tarzan@cave:~/auuow/banana$ mkdir content/pages
(pelicanpy2) tarzan@cave:~/auuow/banana$ mkdir content/images
(pelicanpy2) tarzan@cave:~/auuow/banana$ mkdir content/extra
(pelicanpy2) tarzan@cave:~/auuow/banana$ mkdir content/pdfs
(pelicanpy2) tarzan@cave:~/auuow/banana$ mkdir content/downloads
(pelicanpy2) tarzan@cave:~/auuow/banana$ git add .
(pelicanpy2) tarzan@cave:~/auuow/banana$ git commit -m "Add static directories"
```

edit pelicanconf.py
```language
# Path-specific metadata
EXTRA_PATH_METADATA = {
    'extra/robots.txt': {'path': 'robots.txt'},
    }

# Static path    
STATIC_PATHS = ['pages', 'extra', 'images', 'pdfs', 'downloads']

# Posts settings
ARTICLE_PATHS = ['pages']

# Plugins
PLUGIN_PATHS = ['plugins']
PLUGINS = ['assets', 'sitemap', 'extract_toc', 'gravatar']
```


```language
(pelicanpy2) tarzan@cave:~/auuow/banana$ git add .
(pelicanpy2) tarzan@cave:~/auuow/banana$ git commit -m "Edit configuration"
(pelicanpy2) tarzan@cave:~/auuow/banana$ touch content/pages/test_post.md
```


```language
(pelicanpy2) tarzan@cave:~/auuow/banana$ pelican content
(pelicanpy2) tarzan@cave:~/auuow/banana$ echo "/output" >> .gitignore
(pelicanpy2) tarzan@cave:~/auuow/banana$ echo "/__pycache__" >> .gitignore
(pelicanpy2) tarzan@cave:~/auuow/banana$ git add .
(pelicanpy2) tarzan@cave:~/auuow/banana$ git commit -m "Add gitignore"
```


## References:

(1) The long road to building a static blog with pelican from **[notionsandnotes][1].** 

[1]: https://www.notionsandnotes.org/tech/web-development/pelican-static-blog-setup.html
 
