---
layout: page
title: Bayard Randel's Blog
tagline: Code, banjos, and divers Antipodean curiosities
---
{% include JB/setup %}

<h3>Recent Posts</h3>
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

<div>
  <p>
    Github: {{ site.author.github }}
  </p>
  <p>
    Twitter: {{ site.author.twitter }}
  </p>
</div>

