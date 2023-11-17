---
layout: mypost
title: 友情链接
---

欢迎各位朋友与我建立友链，本站的友链信息如下:

```
名称：{{ site.title }}
地址：{{ site.domainUrl }}{{ site.baseurl }}
描述：{{ site.description }}
```

<ul>
  {%- for link in site.links %}
  <li>
    <p>{{ link.title }}<br> </p>
    <p>-> <a href="{{ link.url }}" title="{{ link.desc }}" target="_blank" >{{ link.url }}</a></p>
    <p>描述：{{ link.desc }}</p>
  </li>
  {%- endfor %}
</ul>
