{% comment %}
  Translation Helper Include
  
  Usage in any layout/include/page:
    {% assign t = site.data.translations[page.lang | default: site.default_lang] %}
  
  Then use translations like:
    {{ t.nav.home }}
    {{ t.posts.read_time | replace: '%{time}', page.read_time }}
    {{ t.search.results_found | replace: '%{count}', results.size }}
  
  Helper macro usage:
    {% include i18n.html key="nav.home" %}
    {% include i18n.html key="posts.read_time" time=5 %}
    {% include i18n.html key="search.results_found" count=42 %}
{% endcomment %}

{% assign _lang = page.lang | default: site.default_lang %}
{% assign _t = site.data.translations[_lang] %}
{% assign _fallback = site.data.translations[site.default_lang] %}

{% comment %} Split key by dots to navigate nested YAML {% endcomment %}
{% assign _keys = include.key | split: "." %}
{% assign _val = _t %}
{% assign _fallback_val = _fallback %}

{% for _k in _keys %}
  {% assign _val = _val[_k] %}
  {% assign _fallback_val = _fallback_val[_k] %}
{% endfor %}

{% comment %} Fall back to default language if key missing {% endcomment %}
{% if _val == nil or _val == "" %}
  {% assign _val = _fallback_val %}
{% endif %}

{% comment %} Replace interpolation placeholders {% endcomment %}
{% if include.time %}
  {% assign _val = _val | replace: '%{time}', include.time %}
{% endif %}
{% if include.count %}
  {% assign _val = _val | replace: '%{count}', include.count %}
{% endif %}
{% if include.name %}
  {% assign _val = _val | replace: '%{name}', include.name %}
{% endif %}

{{ _val }}
