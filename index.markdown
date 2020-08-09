---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default #home
---
## Posts
{% for post in site.posts %}
<li>
    {% if post.url == page.url %}
    <string>{{ post.title }}</string>
    {% else %}
    <a href="{{site.baseurl}}{{ post.url }}">
        {{ post.title }}
    </a>
    {% endif %}
</li>
{% endfor %}