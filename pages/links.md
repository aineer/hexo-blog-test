---
layout: mypost
title: 友情链接
---

欢迎各位朋友与我建立友链，本站的友链信息如下

```
名称：{{ site.title }}
描述：{{ site.description }}
地址：{{ site.domainUrl }}{{ site.baseurl }}
头像：{{ site.domainUrl }}{{ site.baseurl }}/static/img/logo.jpg
```

<ul>
  {%- for link in site.links %}
  <li>
   <p>
      {{ link.url }}
      {{ site.description }}
      {{ site.domainUrl }}
      {{ site.baseurl }}
      {{ site.domainUrl }}
      {{ site.baseurl }}
   </p>
  </li>
  {%- endfor %}
</ul>