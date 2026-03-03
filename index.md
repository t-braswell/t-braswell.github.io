---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
title: Homepage
# layout: home doesnt work
menus: header
permalink: /
---
{% for item in site.data.navigation.header %}
- [{{ item.title }}]({{site.baseurl}}{{ item.url }})
{% endfor %}

