---
layout: page
permalink: /publications/
title: publications
description: Reverse-chronological, with venue and topic tags. Use the filters to narrow by area.
years: [2026,2025,2024,2023,2022,2021,2020,2019,2018,2016]
nav: true
nav_order: 1
---
<!-- _pages/publications.md -->

<div class="pub-filters" id="pub-filters">
  <button type="button" class="pub-filter active" data-tag="">All</button>
  <button type="button" class="pub-filter t-machine-learning" data-tag="Machine Learning">Machine Learning</button>
  <button type="button" class="pub-filter t-blockchain" data-tag="Blockchain">Blockchain</button>
  <button type="button" class="pub-filter t-cryptography" data-tag="Cryptography">Cryptography</button>
  <span class="pub-filter-sep"></span>
  <button type="button" class="pub-filter t-security-and-privacy" data-tag="Security and Privacy">Security and Privacy</button>
  <button type="button" class="pub-filter t-decentralisation" data-tag="Decentralisation">Decentralisation</button>
  <button type="button" class="pub-filter t-pre-training" data-tag="Pre-Training">Pre-Training</button>
  <button type="button" class="pub-filter t-post-training" data-tag="Post-Training">Post-Training</button>
  <button type="button" class="pub-filter t-model-merging" data-tag="Model Merging">Model Merging</button>
  <button type="button" class="pub-filter t-inference" data-tag="Inference">Inference</button>
  <button type="button" class="pub-filter t-verifiability" data-tag="Verifiability">Verifiability</button>
  <button type="button" class="pub-filter t-incentives" data-tag="Incentives">Incentives</button>
</div>

<div class="publications">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>

<script>
(function () {
  var bar = document.getElementById('pub-filters');
  if (!bar) return;
  var buttons = bar.querySelectorAll('.pub-filter');

  function apply(tag) {
    document.querySelectorAll('.publications ol.bibliography').forEach(function (list) {
      var shown = 0;
      list.querySelectorAll('li').forEach(function (li) {
        var row = li.querySelector('[data-tags]');
        var tags = row ? row.getAttribute('data-tags').split(', ') : [];
        var show = !tag || tags.indexOf(tag) !== -1;
        li.hidden = !show;
        if (show) shown++;
      });
      list.hidden = shown === 0;
      var heading = list.previousElementSibling;
      while (heading && !heading.classList.contains('year')) heading = heading.previousElementSibling;
      if (heading) heading.hidden = shown === 0;
    });
  }

  buttons.forEach(function (btn) {
    btn.addEventListener('click', function () {
      buttons.forEach(function (b) { b.classList.remove('active'); });
      btn.classList.add('active');
      apply(btn.getAttribute('data-tag'));
    });
  });
})();
</script>
