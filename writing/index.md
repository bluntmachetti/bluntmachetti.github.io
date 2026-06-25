---
layout: page
title: "Writing"
label: "ESSAYS"
subtitle: "Personal essays on building, learning, and the intersection of AI, resilience, and decision-making."
---

<div class="log">
  <div class="log-head">
    <h2>Essays</h2>
    {% assign essays = site.posts | where: "category", "writing" %}
    <span class="count">{% assign n = essays | size %}{% if n < 10 %}0{% endif %}{{ n }} POSTED</span>
    <span class="rule"></span>
  </div>

  {% for post in essays %}
  <a class="entry" href="{{ post.url | relative_url }}">
    <div class="entry-idx">
      {% if post.log %}<span class="entry-num">LOG-{{ post.log }}</span>{% endif %}
      <span class="entry-date">{{ post.date | date: "%Y.%m.%d" }}</span>
      {% if post.read %}<span class="entry-read">{{ post.read | upcase }}</span>{% endif %}
    </div>
    <div class="entry-body">
      {% if post.flags %}
      <div class="entry-flags">
        {% for f in post.flags %}<span class="flag {{ f.kind }}">{{ f.text }}</span>{% endfor %}
      </div>
      {% endif %}
      <h3 class="entry-title">{{ post.title }}</h3>
      <p class="entry-excerpt">{{ post.summary | default: post.description }}</p>
      <span class="entry-more">Read essay <span class="arr">→</span></span>
    </div>
  </a>
  {% endfor %}
</div>
