---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

<!-- TODO: Replace all sections below with your actual CV content.
     Publications, Talks, and Teaching sections are auto-generated from their
     respective collection files (_publications/, _talks/, _teaching/).
     All other sections (Education, Work, Skills, etc.) must be edited here directly. -->

Education
======
<!-- TODO: List your degrees in reverse chronological order, e.g.:
* Ph.D in [Field], [University], [Year]
* M.S. in [Field], [University], [Year]
* B.S. in [Field], [University], [Year]
-->

Work Experience
======
<!-- TODO: List positions in reverse chronological order, e.g.:
* [Year]-Present: [Title]
  * [Institution]
  * Duties: [Description]
-->

Skills
======
<!-- TODO: List your technical and other skills, e.g.:
* Programming: Python, R, MATLAB
* Tools: Git, Docker, LaTeX
* Languages: English (fluent), [other]
-->

Publications
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>

Talks
======
  <ul>{% for post in site.talks reversed %}
    {% include archive-single-talk-cv.html %}
  {% endfor %}</ul>

Teaching
======
  <ul>{% for post in site.teaching reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>

Service and Leadership
======
<!-- TODO: Add committee memberships, reviewing roles, mentoring, outreach, etc. -->
