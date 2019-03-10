---
layout: splash

header:
  image: "assets/images/Background.JPG"
  caption: "Photo credit: Wan-Yu Lee"

classes:
  - landing
  - dark-theme

believe:
  - excerpt: "Life is full of __Uncertainties__, and __Tim__ embraces as much as he can." 

feature_row:
    - image_path: "assets/images/Coder.png"
      alt: "placeholder image 1"
      title: "As a Programmer"
      excerpt: "Python and R are my favorites"
    - image_path: "assets/images/Cyclist.JPG"
      alt: "placeholder image 1"
      title: "As a climber"
      excerpt: "I have sent a V12 bouldering problem"
    - image_path: "assets/images/P1010513.JPG"
      alt: "placeholder image 1"
      title: "As a Research Associate"
      excerpt: "I study biometrics and emotions"

feature_row2:
  - image_path: "assets/images/about_me.JPG"
    alt: "placeholder image 2"
    title: "About Me"
    excerpt: 'About me, my shoes, my keyboard'
    url: /About/
    btn_label: "Read More"
    btn_class: "btn--primary"


---

{% include feature_row id="believe" type="center" %}

{% include feature_row %}

{% include feature_row id="feature_row2" type="center" %}
