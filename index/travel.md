---
layout: page
title: Travel
subtitle: Places I've been & moments captured
---

{%- comment -%} Collect and sort all images from the /travel/ folder dynamically {%- endcomment -%}
{%- assign travel_images = "" | split: "" -%}
{%- for file in site.static_files -%}
  {%- if file.path contains '/travel/' -%}
    {%- assign travel_images = travel_images | push: file -%}
  {%- endif -%}
{%- endfor -%}
{%- assign travel_images = travel_images | sort: "path" -%}

{%- comment -%} Month name helper {%- endcomment -%}
{%- assign month_names = "January,February,March,April,May,June,July,August,September,October,November,December" | split: "," -%}

{%- if travel_images.size == 0 -%}
  <p style="text-align: center; font-style: italic; color: #999;">No travel photos yet. Check back soon!</p>
{%- else -%}
<div class="travel-gallery">
  <div class="gallery-grid">
  {%- for img in travel_images -%}
    {%- assign basename = img.basename -%}
    {%- assign y = basename | slice: 0, 4 -%}
    {%- assign m_str = basename | slice: 4, 2 -%}
    {%- assign m = m_str | plus: 0 | minus: 1 -%}
    {%- assign d = basename | slice: 6, 2 | plus: 0 -%}
    {%- assign month_name = month_names[m] -%}
    <div class="gallery-item">
      <a href="{{ img.path | relative_url }}" target="_blank">
        <img src="{{ img.path | relative_url }}" alt="{{ month_name }} {{ d }}, {{ y }}" loading="lazy">
        <div class="gallery-overlay">
          <span class="gallery-date">{{ month_name }} {{ d }}, {{ y }}</span>
        </div>
      </a>
    </div>
  {%- endfor -%}
  </div>
</div>
{%- endif -%}
