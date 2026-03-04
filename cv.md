---
title: CV
permalink: /cv

---
{% for item in site.data.navigation.header %}
- [{{ item.title }}]({{ item.url }})
{% endfor %}


{ {% pdf "/downloads/2026_02_24_resume.pdf" %}}
