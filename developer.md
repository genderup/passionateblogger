---
layout: page
title: Developer Blog
permalink: /developer/
---
<div class="home">

 
   <ul class="posts">
      {% for post in site.categories['developer'] %}
      
      <li>
        <span class="post-date">{{ post.date | date: "%b %-d, %Y" }}</span>
        <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
       <p>{{ post.excerpt }}</p>
      </li>
     
    {% endfor %}
  </ul>

 


</div>

<div class="side-bar">
<p class="title">Apps by DTT</p>
<a href="{{ site.baseurl }}/justspeechy/"><img src="/JustSpeechy.png"></a> 

</div>

