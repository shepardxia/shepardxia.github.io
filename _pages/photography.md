---
layout: default
title: photography
permalink: /photography/
description:
nav: true
nav_order: 4
---

{% for section in site.data.photography.sections %}
<div class="photo-section">
  <h2 class="photo-section-title">{{ section.name }}</h2>
  <div class="album-grid">
    {% for entry in section.albums %}
      {% assign album = site.photography | where: "slug", entry.album | first %}
      {% if album %}
        {% assign cover_id = entry.cover | default: album.photos.first %}
        <a href="{{ album.url | relative_url }}" class="album-card">
          <img src="https://res.cloudinary.com/{{ site.cloudinary_cloud }}/image/upload/w_800,h_500,c_fill,q_auto,f_auto/{{ album.cloud_folder }}/{{ cover_id }}.jpg" alt="{{ album.title }}">
          <div class="album-card-info">
            <span class="album-card-title">{{ album.title }}</span>
          </div>
        </a>
      {% endif %}
    {% endfor %}
  </div>
</div>
{% endfor %}

<script>
document.querySelectorAll('.album-grid').forEach(function(grid) {
  grid.addEventListener('wheel', function(e) {
    if (Math.abs(e.deltaX) > Math.abs(e.deltaY)) return;
    if (grid.scrollWidth <= grid.clientWidth) return;
    e.preventDefault();
    grid.scrollLeft += e.deltaY;
  }, { passive: false });
});
</script>
