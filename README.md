---
layout: default
title: Mucomplex Diary
---
<h4>What hackers do is figure out technology and experiment with it in ways many people never imagined. They also have a strong desire to share this information with others and to explain it to people whose only qualification may be the desire to learn. - Emmanuel Goldstein</h4>

<ul>
  {% for post in site.posts %}
    <li>
      <h2><a href="/mucomplex/{{ post.url }}">{{ post.title }}</a></h2>
      <p>{{ post.description }}</p>
    </li>
  {% endfor %}
</ul>
