---
title: Blog
url: /blog
---
{% for item in site.data.navigation.header %} \- [{{ item.title }}]({{site.baseurl}}{{ item.url }}){% endfor %} \-
# BLOG

{% for post in site.posts %} 
+  [{{post.title}}]({{post.url}})
{% endfor %}
