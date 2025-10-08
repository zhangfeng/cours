---
title: Projet apprentissage
layout: page
---

# Apprentissage et astuces

L'apprentissage est l'art d'acquérir de nouvelles connaissances et de
nouvelles et de mettre à l'épreuve notre capacité de déduction.

Ici, je propose de la matière qui, je l'espère, vous aideront dans votre
apprentissage.

VOici les différents domainesd'apprentissage qui m'intéressent et où j'ai pu écrire quelques articles:

{% for c in site.collections | sort: "label" -%}
{% if c.label != "posts"}
{% assign index_page = c.docs | where: "layout", "collection_index" | first -%}
- [{{c.label}}]({{index_page.url}})
{% endfor %}

