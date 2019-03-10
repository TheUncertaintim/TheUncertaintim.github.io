---
layout: splash

header:
  image: "assets/images/Background.JPG"

classes:
  - landing
  - dark-theme

intro:
  - excerpt: '__I am Tim. I Make the Uncertainties in Life Become Certain.__'

feature_row:
  - image_path: "assets/images/Coder.png"
    alt: "placeholder image 1"
    title: "As a Coder"
    excerpt: "I code in Python and R"
  - image_path: "assets/images/Cyclist.JPG"
    alt: "placeholder image 1"
    title: "As a Boulder"
    excerpt: "I climb V12"
  - image_path: "assets/images/P1010513.jpg"
    alt: "placeholder image 1"
    title: "As a Research Associate"
    excerpt: "See my publications"

feature_row2:
  - image_path: "assets/images/about_me.JPG"
    alt: "placeholder image 2"
    title: "About Me"
    excerpt: 'About me, my shoes, my keyboard'
    url: /About/
    btn_label: "Read More"
    btn_class: "btn--primary"


---

{% include feature_row id="intro" type="center" %}

{% include feature_row %}

{% include feature_row id="feature_row2" type="center" %}
