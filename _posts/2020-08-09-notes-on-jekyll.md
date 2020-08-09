---
layout: post
title:  "Notes on Jekyll"
date:   2020-08-09 14:22:10 +0200
categories: notes
tags: notes linux windows jekyll
---
# Installation on Linux Mint

- Installing Ruby

{% highlight bash %}
sudo apt-get install ruby-full
{% endhighlight %}

or

{% highlight bash %}
sudo snap install ruby --classic
{% endhighlight %}

or

{% highlight bash %}
sudo snap switch ruby --channel=2.3/stable
sudo snap refresh
{% endhighlight %}

Checking Ruby version

{% highlight bash %}
ruby --version
{% endhighlight %}

Source: [Installing Ruby][installing-ruby]

[installing-ruby]: https://www.ruby-lang.org/en/documentation/installation/#rbenv

- Installing Jekyll

{% highlight bash %}
sudo gem install bundler jekyll
{% endhighlight %}

Checking Jekyll version

{% highlight bash %}
jekyll --version
{% endhighlight %}

# Installation on Windows

* Installing Ruby and Ruby Gems

For Windows installator see [RubyInstallers][rubyInstallers]

[rubyInstallers]: https://rubyinstaller.org/downloads/

During installation: 
- checkmark ``MSYS2`` installer
- choose 1, 2, and 3 in turn

Checking Ruby version

{% highlight bash %}
ruby -v
{% endhighlight %}

Checking Ruby Germs version: 

{% highlight bash %}
gem -v
{% endhighlight %}

Ruby Gems is a package manager for Ruby.

* Jekyll installation

{% highlight bash %}
gem install jekyll bundler
{% endhighlight %}

Checking Jekyll version:

{% highlight bash %}
jekyll -v
{% endhighlight %}

# New page

Generating

{% highlight bash %}
jekyll new PAGE_NAME
{% endhighlight %}

First run

{% highlight bash %}
cd PAGE_NAME
bundle exec jekyll serve
{% endhighlight %}

Stop the server with CTRL + C

Regenerating

{% highlight bash %}
jekyll serve
{% endhighlight %}

# Project structure

- ``_posts`` folder -- all posts
- ``_site`` folder -- the final version of the generated page (only for copying to the server: these files should not be edited)
- ``_config.yml`` file -- page configuration settings in YAML
- ``Gemfile`` file -- page dependencies
- ``about.md`` file -- the About page content
- ``index.md`` -- the main page

# File structure

Front matter

{% highlight yaml %}
---
layout: post
title: "Welcome to Jekyll!"
date: 2020-02-21 19:48:39 +0100
categories: jekyll update
---
{% endhighlight %}

Default front matter (one that does not need to be provided on every post and page) may be given in ``_config.yml`` file under ``Build settings``:

{% highlight yaml %}
defaults:
  -
    scope:
       path: "" # here you can set folders referenced by default values in front matter
       type: "posts" # document types referenced by defaults
    values:
      layout: "posts"
      title: "New post"
{% endhighlight %}

# Posts

Name must follow the format: ``RRRR-MM-DD-file-name.markdown`` or ``RRRR-MM-DD-file-name.md``.

Posts may be in HTML, but usually they are in markdown with front matter, e.g.

{% highlight yaml %}
---
layout: post
title: "Welcome to Jekyll!"
date: 2020-02-21 19:48:39 +0100
categories: jekyll update
---
{% endhighlight %}

Other supported formats are YAML, JSON.

The categories are used in routing, e.g.

``http://127.0.0.1:4000/jekyll/update/2020/02/21/welcome-to-jekyll.html``

It also possible to create own variables, e.g.

{% highlight yaml %}
author: Mike
tags: favourites
{% endhighlight %}

The date in the parameter must be equal to the one in the file name.

Posts may be grouped in subfolders.

# Drafts

They are stored in ``_drafts`` folder.

File name format is ``file-name.md`` (without the date).

This kind of files will not be presented unless the server is run with the following command:

{% highlight bash %}
jekyll serve --draft
{% endhighlight %}

Drafts are shown according to the file creation date. 

After moving the file from the ``_draft`` folder, a date must be added to its name.

# Pages

Pages may be stored in the main folder.

Page name format: ``page-name.md`` or ``page-name.html``.

They contain front matter indicating ``page`` layout:

{% highlight yaml %}
---
layout: "page"
---
{% endhighlight %}

Routing to the page in main folder, e.g. 

``http://127.0.0.1:4000/page-name``

If the page is in a folder, e.g. ``_pages``, then the routing also is changed, e.g. 

``http://127.0.0.1:4000/pages/page-name``

# Categories

Categories are part of front matter, e.g. 

{% highlight yaml %}
---
layout: page
title: Some title
categories: cat1 cat2 cat3
---
{% endhighlight %}

A set of categories modify the routing, e.g. 

``http://127.0.0.1:4000/cat1/cat2/cat3/file-name``

# Permalinks

These are routing patterns set on each page in the front matter, e.g.

{% highlight yaml %}
---
layout: page
permalink: /folder/:basename
---
{% endhighlight %}

May contain predefined parameters: 

- ``:categories`` -- categories in front matter,
- ``:basename`` -- file name,
- ``:title`` -- the ``title`` parameter in the front matter,
- ``:year``, ``:month``, ``:day`` -- the year, month, and day from the ``date`` parameter in the front matter.

Documentation on permalins see [permalinks]

[permalinks]:https://jekyllrb.com/docs/permalinks/

It is also possible to add the extension of the parameter, e.g. 

{% highlight yaml %}
:title.html
{% endhighlight %}

# Motifs

See ``_config.yml`` file:

{% highlight yaml %}
# Build settings
theme: minima
{% endhighlight %}

Motif browser see [jekyll-themes]

[jekyll-themes]: https://rubygems.org/search?utf8=%E2%9C%93&query=jekyll-themes

Installing a new motif: 

- in the ``Gemfile`` file change the ``minima`` and ``~> 2.5`` parameters to the name of the selected motif, e.g. ``jekyll-theme-midnight``,
- turn off the server (if it's on) using Ctrl + C
- use the command ``bundle install`` and install new motif
- change the motif in the ``_config.hml`` file, e.g. 

{% highlight yaml %}
# Build settings
theme: minima
{% endhighlight %}

to

{% highlight yaml %}
# Build settings
theme: jekyll-theme-midnight
{% endhighlight %}

- start the server using ``bundle exec jekyll serve`` command

# Layouts

Layouts are stored in the ``_layouts`` folder.

Name of the file must be in ``file-name.html`` format. 

Name of the file is used in particular pages and posts, e.g. the ``song`` layout:

{% highlight yaml %}
---
layout: song
---
{% endhighlight %}

A layout is an HTML file containing a reference to a markdown file in the {% raw %}``{{ content }}``{% endraw %} parameter located under the front matter.

**Layout inheritance**

If ``BBB.html`` layout inherits from ``AAA.html``, the files shoud be structrued as follows:

- ``AAA.html`` file:

{% highlight html %}
{% raw %}
Some elements...
{{ content }}
{% endraw %}
{% endhighlight %}

- ``BBB.html`` file:

{% highlight html %}
---
layout: AAA
---
Other elements...
{% endhighlight %}

# Variables

**Layout variables**: {% raw %}``{{ layout.variableName }}``{% endraw %}, e.g.

{% highlight html %}
{% raw %}
---
author: John
---
<h3>The author is {{ layout.author }}</h3>
{% endraw %}
{% endhighlight %}

**Page variables**: {% raw %}``{{ page.variableName }}``{% endraw %}, e.g. 

- layout ``mySite.html``:

{% highlight html %}
{% raw %}
---
---
<h3>The title is {{ page.title }}</h3>
<h4>Some custom variable is {{ page.customVariable }}</h4>
{% endraw %}
{% endhighlight %}

- a single post:

{% highlight yaml %}
---
layout: mySite
title: This is the title
customVar: This is my custom variable
---
Some content.
{% endhighlight %}

**Site** variable: {% raw %}``{{ site.variableName }}``{% endraw %}, e.g.

- ``_config.yml`` file:

{% highlight yaml %}
title: This is the title
myVar: This is my variable
{% endhighlight %}

- ``layout``

{% highlight html %}
{% raw %}
<div markdown = "0">
<h1>The title of my site is {{ site.title }}</h1> 
Some variable of my own design: {{ site.myVar }}.
</div>
{% endraw %}
{% endhighlight %}

# Includes

Includes are layout elements in HTML stored in ``_includes`` folder.

Adding to layout:

{% highlight html %}
{% raw %}
{$ include fileName.html $}
{% endraw %}
{% endhighlight %}

Passing variables:

- ``_includes/element.html`` file:

{% highlight html %}
{% raw %}
<h1 style="color: {{ include.color }}">...</h1>
{% endraw %}
{% endhighlight %}

- ``_layouts/some_page.html`` file:

{% highlight html %}
{% raw %}
{$ include element.html color="blue" $}
{% endraw %}
{% endhighlight %}

# Loops

_Example 1_

{% highlight html %}
{% raw %}
{% for post in site.posts %}
  {{ post.title }} 
  {{ post.url }} 
{% endfor %}
{% endraw %}
{% endhighlight %}

_Example 2_

{% highlight html %}
{% raw %}
{% for post in site.posts %}
<li>
  <a href="{{ post.url }}">
    {{ post.title }}
  </a>
<li>
{% endfor %}
{% endraw %}
{% endhighlight %}

_Example 3_ (loops within pages) 

{% highlight html %}
{% raw %}
{% for page in site.pages %}
{% endraw %}
{% endhighlight %}

# Conditional statements

{% highlight html %}
{% raw %}
{% if page.title == "Something" and page.title == "Nothing" %}
  Do sth if the condition is met.
{% elsif page.title == "Something else" or page.title == "Something strange" %}
  Do sth else.
{% else %} 
  Do it by default.
{% endif %}
{% endraw %}
{% endhighlight %}

Using conditional statements for styling hiperlinks:

{% highlight html %}
{% raw %}
{% for post in site.posts %}
  <li>
    <a style="{% if page.url = post.url %}color:red;{% endif %}" href="{{ post.url }}">
        {{ post.title }}
    </a>
  </li>
{% endfor %}
{% endraw %}
{% endhighlight %}

# Data files

Usually stored in ``_data`` folder. 

Supported formats: ``csv``, ``yaml``, ``json``.

Example

- data file ``people.yml``

{% highlight yaml %}
- name: "Mike"
  occupation: "student"
- name: "John"
  occupation: "teacher"
{% endhighlight %}

- presentation of data (``.html`` or ``.md``)

{% highlight yaml %}
{% raw %}
{% for person in site.data.people %}
<li>
{{ person.name }}, {{ person.occupation }}
<br />
</li>
{% endfor %}
{% endraw %}
{% endhighlight %}

# Static files

It could be any files, e.g. graphics, text, etc. They may be stored in any folder, e.g. ``assets``. 

Referencing all of them in a loop:

{% highlight yaml %}
{% raw %}
{% for file in site.static_files %}
  {{ file.path }} 
  {{ file.name }} 
  {{ file.basename }}
  {{ file.extname }} 
{% endfor %}
{% endraw %}
{% endhighlight %}

By default:
- static files are stored in a separate (sub)folder, e.g. ``assets/img``
- the ``_config.yml`` contains:

{% highlight yaml %}
plugins:
- jekyll-feed
defaults: 
  - scope: 
    path: assets/img
    values: 
      image: true
{% endhighlight %}

Using a static file:

{% highlight html %}
{% raw %}
{% for file in file.image %}
  {% if file.image %}
    {% file.image %}
    <img src="{{ file.path }}" /> 
  {% endif %}
{% endfor %}
{% endraw %}
{% endhighlight %}

# Hosting on GitHub pages

- create a repository in your GitHub account _without the ``README.md`` file_ (the ``Initialize this repository with a README`` option should be unchecked)
- modify the ``baseurl`` variable in ``_config.yml`` by inserting the remote repository name

``baseurl: "/REPO_NAME"``

- create a local repository

{% highlight bash %}
git init
{% endhighlight %}

- create ``gh-pages`` branch:

{% highlight bash %}
git checkout -b gh-pages
{% endhighlight %}

- stage all files: 

{% highlight bash %}
git add . 
{% endhighlight %}

- commit all files:

{% highlight bash %}
git commit -m "nazwa migawki"
{% endhighlight %}

- connect the local repo to the remote one:

{% highlight yaml %}
git remote add origin GIT_HUB_REPO_LINK
{% endhighlight %}

- check the remote repo

{% highlight yaml %}
git remote -v
{% endhighlight %}

- send files to the remote repo:

{% highlight yaml %}
git push origin gh-pages
{% endhighlight %}

- check for the link to your site in remote repo setting, GitHub Pages section, e.g. 

``https://KONTO-GITHUB-sites.github.io/NAZWA-STRONY/``

# Tutorials


