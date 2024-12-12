---
layout: default
---
{% for post in site.posts %}
### [{{ post.title }}]({{ post.url }})
**{{ post.date | date: "%d %B %Y" }}**

<div class="tags">
  {% if post.tags %}
    {% for tag in post.tags %}
      <span class="tag">{{ tag }}</span>
    {% endfor %}
  {% endif %}
</div>

{{ post.excerpt }}
---
{% endfor %}