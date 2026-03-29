{% comment %}
  Multilingual SEO Head Include
  Outputs hreflang link tags for SEO.
  Add {% include i18n-head.html %} inside your <head> or in _includes/head/custom.html
{% endcomment %}

{% assign current_lang = page.lang | default: site.default_lang %}

{% comment %} Self-referencing hreflang {% endcomment %}
<link rel="alternate" hreflang="{{ current_lang }}" href="{{ page.url | absolute_url }}" />

{% comment %} Alternate language hreflang tags {% endcomment %}
{% if page.lang_alts %}
  {% for alt in page.lang_alts %}
    <link rel="alternate" hreflang="{{ alt[0] }}" href="{{ alt[1] | absolute_url }}" />
  {% endfor %}
{% endif %}

{% comment %} x-default points to the default language version {% endcomment %}
{% if site.default_lang == current_lang %}
  <link rel="alternate" hreflang="x-default" href="{{ page.url | absolute_url }}" />
{% elsif page.lang_alts[site.default_lang] %}
  <link rel="alternate" hreflang="x-default" href="{{ page.lang_alts[site.default_lang] | absolute_url }}" />
{% endif %}

{% comment %} Set lang attribute context for this page {% endcomment %}
<meta name="language" content="{{ current_lang }}">
