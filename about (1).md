{% comment %}
  _includes/masthead.html (override)
  
  This overrides the Minimal Mistakes masthead to inject the language switcher.
  Copy the original masthead from the MM theme and add {% include language-switcher.html %}
  where you want it (shown below in the nav area).
  
  To get the original: 
    bundle info --path minimal-mistakes-jekyll
    Then copy: _includes/masthead.html from that path into your project.
  
  Below is a complete masthead with language switcher integrated.
{% endcomment %}

<div class="masthead">
  <div class="masthead__inner-wrap">
    <div class="masthead__menu">
      <nav id="site-nav" class="greedy-nav">
        {% if site.logo %}
          <a class="site-logo" href="{{ '/' | relative_url }}">
            <img src="{{ site.logo | relative_url }}" alt="{{ site.masthead_title | default: site.title }}">
          </a>
        {% endif %}

        <a class="site-title" href="{{ '/' | relative_url }}">
          {{ site.masthead_title | default: site.title }}
          {% if site.subtitle %}<span class="site-subtitle">{{ site.subtitle }}</span>{% endif %}
        </a>

        <ul class="visible-links">
          {%- for link in site.data.navigation.main -%}
            {% assign current_lang = page.lang | default: site.default_lang %}
            {% assign t = site.data.translations[current_lang] %}

            <li class="masthead__menu-item">
              <a href="{{ link.url | relative_url }}"{% if link.description %} title="{{ link.description }}"{% endif %}>
                {% comment %} Translate nav labels if key matches t.nav keys {% endcomment %}
                {% if link.title == "Home" %}{{ t.nav.home }}
                {% elsif link.title == "About" %}{{ t.nav.about }}
                {% elsif link.title == "Blog" %}{{ t.nav.blog }}
                {% elsif link.title == "Contact" %}{{ t.nav.contact }}
                {% else %}{{ link.title }}
                {% endif %}
              </a>
            </li>
          {%- endfor -%}
        </ul>

        {% comment %} Language Switcher {% endcomment %}
        {% include language-switcher.html %}

        <button class="greedy-nav__toggle hidden" type="button">
          <span class="visually-hidden">{% include i18n.html key="ui.menu_label" %}</span>
          <div class="navicon"></div>
        </button>

        <ul class="hidden-links hidden"></ul>
      </nav>
    </div>
  </div>
</div>
