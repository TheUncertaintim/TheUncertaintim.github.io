---
layout: splash

header:
  image: "assets/images/Background.JPG"
  caption: "Photo credit: Wan-Yu Lee"

classes:
  - landing
  - dark-theme

subtitle:
  - excerpt: 'The Uncertainties in Stats, Engineering, Psychology are just out there in our daily life. This personal site talks about how I understand it, and visualize them with code.'

Recent_Project:
  - title: "Recent Project"

NatureWithKivy:
  - image_path: /assets/images/Nature_with_kivy.jpg
    title: "Nature With Kivy"
    excerpt: 'Visualize nature phenomenon with python based on the book *Nature of Code* written by Daniel Shiffman'
    url: /NatureWithKivy/Intro/
    btn_label: "Read More"
    btn_class: "btn--primary"

---

{% include feature_row id="subtitle" type="center" %}

{% include feature_row id="Recent_Project" type="center" %}

{% include feature_row id="NatureWithKivy" type="left" %}
