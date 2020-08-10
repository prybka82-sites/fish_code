---
layout: post
title:  "Notes on Markdown"
categories: notes
tags: notes markdown
---

**Jekyll Markdown**

Sources: 
- [Jekyll Markdown Quick Reference](https://gist.github.com/roachhd/779fa77e9b90fe945b0c)
- [Jekyll Markdown Support](https://www.markdownguide.org/tools/jekyll/)
- [Hot to link to part of the same document in Markdown](https://stackoverflow.com/questions/2822089/how-to-link-to-part-of-the-same-document-in-markdown)

## Basic formatting

{% highlight markdown %}
_italics_ *italics*

__bold__ **bold**

___bold and italics___ ***bold and italics***

~~strikethrough~~

`code` ``code``
{% endhighlight %}

_italics_ *italics*

__bold__ **bold**

___bold and italics___ ***bold and italics***

~~strikethrough~~

`code` ``code``

{% highlight markdown %}
{% raw %}
{% highlight csharp %}
int x = 5;
{% endhighlight %}
{% endraw %}
{% endhighlight %}

{% highlight csharp %}
int x = 5;
{% endhighlight %}

## Line breaks

{% highlight markdown %}
No
line
break

Line  
break  
tags (double trailing spaces)

Line

break
{% endhighlight %}

No
line
break

Line  
break  
tags (double trailing spaces)

Line

break

## Lists

Bulletted lists

{% highlight markdown %}
* item 1
* item 2
- item 1
- item 2
+ item 1
+ item 2
    - item 1
        * item 1
{% endhighlight %}

* item 1
* item 2
- item 1
- item 2
+ item 1
+ item 2
    - item 1
        * item 1

Ordered lists

{% highlight markdown %}
1. Item 1
2. Item 2
3. Item 3
{% endhighlight %}

1. Item 1
2. Item 2
3. Item 3

Setting the exact number (kramdown)

{% highlight markdown %}
{% raw %}
1. Item 1

{:start="5"}
3. Item 3
{% endraw %}
{% endhighlight %}

1. Item 1

{:start="5"}
3. Item 3

See: [Support starting numbered lists with arbritray number](https://github.com/gettalong/kramdown/issues/211#issuecomment-256508905)

## Paragraphs

{% highlight markdown %}
{% raw %}
## Header 2     # H1 is reserved for post titles!!!
### Header 3
#### Header 4
##### Header 5
###### Header 6
{% endraw %}
{% endhighlight %}

## Hyperlinks

- alternative text hyperlink:

{% highlight markdown %}
[Alternative text](http://actual-address.com)
{% endhighlight %}

[Alternative text](http://actual-address.com)

- literal link

{% highlight markdown %}
<http://actual-address.com>
{% endhighlight %}

<http://actual-address.com>

- referencing the headers within the document

{% highlight markdown %}
{% raw %}
[your link here](#line-breaks)
{% endraw %}
{% endhighlight %}

[your link here](#line-breaks)

- referencing ``<a/>`` anchrors: 

{% highlight markdown %}
{% raw %}
[your link here](#anchor-name)

<a name="anchor-name"></a>
{% endraw %}
{% endhighlight %}

[your link here](#anchor-name)

<a name="anchor-name"></a>

## Images

- from Web

{% highlight markdown %}
![alternative text](https://img.freepik.com/free-vector/vintage-logo-style-bear_225004-570.jpg?size=626&ext=jpg)
{% endhighlight %}
![alternative text](https://img.freepik.com/free-vector/vintage-logo-style-bear_225004-570.jpg?size=626&ext=jpg)

- from folder (``assets/images/example.jpg``)

{% highlight markdown %}
![alternative text]({{ site.baseurl }}/assets/images/example.jpg)
{% endhighlight %}

![alternative text]({{ site.baseurl }}/assets/images/example.jpg)

- setting size

{% highlight markdown %}
![pictue]({{ site.baseurl }}/assets/images/example.jpg){:height="90px" width="190px"}
{% endhighlight %}

![picute]({{ site.baseurl }}/assets/images/example.jpg){:height="90px" width="190px"}

See: [Changing image size in Markdown](https://stackoverflow.com/questions/14675913/changing-image-size-in-markdown).

## Quotes

{% highlight markdown %}
> Quote
>> Nested quote
>>> Nested quote
{% endhighlight %}

> Quote
>> Nested quote
>>> Nested quote

## Horizontal lines

{% highlight markdown %}
----

****
{% endhighlight %}

----

****

## Tables

{% highlight markdown %}
| Head1 | Head2 | Head3 |
| --- | --- | --- | 
| Value | Value | Value |
| Text | Text | Text |
{% endhighlight %}

| Head1 | Head2 | Head3 |
| --- | --- | --- | 
| Value | Value | Value |
| Text | Text | Text |

## Escape sequences

{% highlight markdown %}
\* `` ` `` \\ \` \_ \{ \} \[ \] \( \) \# \+ \- \. \! \|
{% endhighlight %}

\* `` ` `` \\ \` \_ \{ \} \[ \] \( \) \# \+ \- \. \! \|

