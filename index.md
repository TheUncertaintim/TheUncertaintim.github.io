---
layout: splash

header:
  image: "assets/images/Background.JPG"

classes:
  - landing
  - dark-theme

intro:
  - excerpt: '__I am Tim. I Make the Uncertainties in Life Become Certain.__'

feature_row2:
  - image_path: "/assets/images/about_me.jpg"
    alt: "placeholder image 2"
    title: "About Me"
    excerpt: 'About me, my shoes, my keyboard'
    url: /About/
    btn_label: "Read More"
    btn_class: "btn--primary"


---

{% include feature_row id="intro" type="center" %}

{% include feature_row id="feature_row2" type="left" %}
