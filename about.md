---
layout: page
title: About
permalink: /about/
---

Discuss The Times is a current events blog. We also publish iPhone apps such as <a href="{{ site.baseurl }}/justspeechy/">Just Speechy</a> 

 <ul class="posts">
    {% for post in site.posts %}
      <li>
        <span class="post-date">{{ post.date | date: "%b %-d, %Y" }}</span>
        <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>