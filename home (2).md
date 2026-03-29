{% comment %}
  Language Switcher Include
  Usage: {% include language-switcher.html %}
  
  Requires front matter on each page:
    lang: en          # current language
    lang_alts:        # alternate language versions
      de: /de/about/
      ne: /ne/about/
{% endcomment %}

{% assign current_lang = page.lang | default: site.default_lang %}
{% assign t = site.data.translations[current_lang] %}

<nav class="language-switcher" aria-label="Language selection">
  <ul class="language-switcher__list">
    {% for lang_code in site.languages %}
      {% assign lang_data = site.data.translations[lang_code] %}
      {% if lang_code == current_lang %}
        <li class="language-switcher__item language-switcher__item--active" aria-current="true">
          <span class="language-switcher__current">
            {{ lang_data.lang_flag }} {{ lang_data.lang_name }}
          </span>
        </li>
      {% else %}
        {% comment %} Try to find alternate URL for this language {% endcomment %}
        {% if page.lang_alts[lang_code] %}
          {% assign alt_url = page.lang_alts[lang_code] %}
        {% elsif lang_code == site.default_lang %}
          {% assign alt_url = "/" %}
        {% else %}
          {% assign alt_url = "/" | append: lang_code | append: "/" %}
        {% endif %}
        <li class="language-switcher__item">
          <a class="language-switcher__link" href="{{ alt_url | relative_url }}" hreflang="{{ lang_code }}" lang="{{ lang_code }}">
            {{ lang_data.lang_flag }} {{ lang_data.lang_name }}
          </a>
        </li>
      {% endif %}
    {% endfor %}
  </ul>
</nav>
