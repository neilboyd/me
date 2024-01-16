# me

<ul class="page-list">
{% assign sorted-pages = site.pages | where_exp: 'page', 'page.title' | sort: 'url' | reverse %}
{% for p in sorted-pages %}
  <li>
    <a href="{{ site.url }}{{ p.url }}">{{ p.title }}</a>
  </li>
{% endfor %}
</ul>
