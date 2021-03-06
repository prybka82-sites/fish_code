---
layout: post
title:  "Adding table of contents in Jekyll"
categories: posts
tags: jekyll
---
How to add table of contents to Jekyll posts

## Solution 1: kramdown table of contents.

1. Set ``kramdown`` as markdown preprocessor in ``_config.yml``: 

{% highlight yaml %}
# Build settings
markdown: kramdown
{% endhighlight %}

Restart the Jekyll server (Ctrl + C and ``bundle exec jekyll serve``).

2. Insert the following code where the table of contents should be generated: 

{% highlight yaml %}
* Do not remove this line (it will not be displayed)
{:toc}
{% endhighlight %}

3. Optionally, some styles may be added, e.g.: 

{% highlight css %}
{% raw %}
/* Adding 'Contents' headline to the TOC */
#markdown-toc::before {
    content: "Contents";
    font-weight: bold;
}

/* Using numbers instead of bullets for listing */
#markdown-toc ul {
    list-style: decimal;
}

#markdown-toc {
    border: 1px solid #aaa;
    padding: 1.5em;
    list-style: decimal;
    display: inline-block;
}
{% endraw %}
{% endhighlight %}

## Solution 2: table of contents generated by JavaScript code.

1. Download JS script from [jekyll-table-of-contents](https://github.com/ghiculescu/jekyll-table-of-contents/archive/master.zip)

2. Create ``toc.js`` file in ``assets/js`` in your project and paste the JS script from the unzipped file. 

3. Initiate the script with the following code:

{% highlight html %}
<script src="{{ '/assets/js/toc.js' | relative_url }}"></script>

<script type="text/javascript">
$(document).ready(function() {
    $('#toc').toc();
});
</script>
{% endhighlight %}

The code should be added at the end of the page, because it looks for rendered headers. 

It is possible to limit the range of headers covered by the script in the following way: 

{% highlight html %}
$('#toc').toc({ headers: 'h1, h2, h3, h6' });
{% endhighlight %}

4. Generate the table of contents with the following code: 

{% highlight html %}
<div id="toc"></div>
{% endhighlight %}

An example post layout with table of contents: 

{% highlight html %}
{% raw %}
---
layout: default
---

<article class="post">
    <h1 class="post-title note info">{{ page.title }}</h1>
    <time datetime="{{ page.date | date_to_xmlschema }}" class="post-date">
        {{ page.date | date_to_string }}
    </time>
    <div id="toc"></div>
    {{ content }}
</article>

<script src="{{ '/assets/js/toc.js' | relative_url }}"></script>

<script type="text/javascript">
$(document).ready(function() {
    $('#toc').toc();
});
</script>
{% endraw %}
{% endhighlight %}

Source: [Jekyll Table of Contents - Wikipedia Look!](https://blog.webjeda.com/jekyll-toc/)

