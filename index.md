---
title: première ébauche
layout: default
---

# Apprentissage et astuces

L'apprentissage est l'art d'acquérir de nouvelles connaissances et de
nouvelles et de mettre à l'épreuve notre capacité de déduction.

Ici, je propose de la matière qui, je l'espère, vous aideront dans votre
apprentissage.

{% for c in site.collections | }sort: "label" -%}
## Section: {{ c.label }}

{% for p in c.docs | sort: "name" %}
- [{{ p.title }}]({{ p.url }})

{% endfor %}
{% endfor %}
