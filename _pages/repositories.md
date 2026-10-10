---
layout: page
permalink: /repositories/
title: repositories
description: Code on GitHub, grouped by topic.
nav: true
nav_order: 4
---

<style>
  .repo-group { margin-top: 2rem; }
  .repo-group h2 { margin-bottom: 0.2rem; }
  .repo-group .blurb { color: var(--global-text-color-light); margin-bottom: 1rem; }
  .repo-card {
    display: flex;
    gap: 1.25rem;
    align-items: center;
    padding: 1rem;
    border: 1px solid var(--global-divider-color);
    border-radius: 8px;
    background: var(--global-card-bg-color);
    transition: box-shadow 0.15s, transform 0.15s;
  }
  .repo-card:hover { box-shadow: 0 4px 14px rgba(0, 0, 0, 0.12); transform: translateY(-2px); }
  .repo-card img { width: 220px; flex-shrink: 0; border-radius: 6px; background: #fff; }
  .repo-card h3 { font-size: 1.15rem; margin: 0 0 0.4rem 0; }
  .repo-card p { margin: 0 0 0.6rem 0; text-align: justify; hyphens: auto; }
  .repo-tags span {
    display: inline-block;
    font-size: 0.75rem;
    padding: 0.1rem 0.55rem;
    margin: 0 0.3rem 0.3rem 0;
    border-radius: 999px;
    border: 1px solid var(--global-theme-color);
    color: var(--global-theme-color);
  }
  .repo-links a { margin-right: 1rem; font-size: 0.9rem; }
  @media (max-width: 576px) {
    .repo-card { flex-direction: column; align-items: stretch; }
    .repo-card img { width: 100%; }
  }
</style>

{% for group in site.data.repositories.groups %}

<div class="repo-group">
  <h2>{{ group.title }}</h2>
  <div class="blurb">{{ group.blurb }}</div>
  {% for repo in group.repos %}
    <div class="repo-card">
      <a href="{{ repo.url }}" target="_blank" rel="noopener"><img src="{{ repo.image | relative_url }}" alt="{{ repo.name }}"></a>
      <div>
        <h3><a href="{{ repo.url }}" target="_blank" rel="noopener"><i class="fa-brands fa-github"></i> {{ repo.name }}</a></h3>
        <p>{{ repo.description }}</p>
        <div class="repo-tags">{% for tag in repo.tags %}<span>{{ tag }}</span>{% endfor %}</div>
        <div class="repo-links">
          <a href="{{ repo.url }}" target="_blank" rel="noopener"><i class="fa-solid fa-code"></i> Code</a>
          {% if repo.project %}<a href="{{ repo.project | relative_url }}"><i class="fa-solid fa-flask"></i> Project page</a>{% endif %}
        </div>
      </div>
    </div>
  {% endfor %}
</div>
{% endfor %}
