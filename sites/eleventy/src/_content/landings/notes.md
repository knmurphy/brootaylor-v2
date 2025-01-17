---
title: "Notes"
# Populates the `meta description` for a page
summary: "Quick notes, thoughts and ramblings."
bodyClass: "notes-home"

permalink: "{% if pagination.pageNumber > 0 %}/notes/{{ pagination.pageNumber + 1 }}/index.html{% else %}/notes.html{% endif %}"

pagination:
  data: collections.postNotes # This data is called using the `postNotes.js` collection script
  size: 15
  alias: notes

date: 2022-04-07T17:23:00
---

{# List of note posts #}
<ul role="list" class="notes__list | no-list | flow">
{% for note in notes -%}
  <li class="notes__list-item">
    <article class="note__summary">
      <h2 class="visually-hidden">{{ note.data.title }}</h2>
      <a href="{{ note.url }}">
        <time datetime="{{ note.date | dateTime }}">{{ note.date | dateTimeReadable("d LLLL y, ") }}{{ note.date | dateTimeReadable("t") | lower }}</time>
      </a>
      {{ note.templateContent | safe | trim }}
    </article>
  </li>
{% endfor -%}
</ul>

{# Pagination component --> (Maybe export this to its own component at some stage) #}
<nav class="pagination">
  <h3 class="visually-hidden">Pagination for note posts</h3>
  <span class="visually-hidden">Page: {{ pagination.pageNumber + 1 }} of {{ pagination.links | length  }}</span>
  <ul role="list" class="pagination__list | no-list">
    {% if pagination.nextPageHref -%}
      <li class="pagination__list-item">
        <i aria-hidden="true">&larr;</i>
        <a href="{{ pagination.nextPageHref }}">Older <span class="visually-hidden">posts</span></a>
      </li>
    {%- endif %}
    {%- if pagination.previousPageHref -%}
      <li class="pagination__list-item">
        <a href="{{ pagination.previousPageHref }}">Newer <span class="visually-hidden">posts</span></a>
        <i aria-hidden="true">&rarr;</i>
      </li>
    {%- endif %}
  </ul>
</nav>
