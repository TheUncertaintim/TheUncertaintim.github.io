---
date: 2021-12-01
header:
  teaser: /assets/images/the-lost-passage/teaser.png
  image: /assets/images/the-lost-passage/header-image2.png
---

A collaborative artwork that aims to raise awareness for climate emergency

# Origin

[**The Lost Passage**](https://thelostpassage.art) was a collaborative project that came out of an online fellowship program called [BeFantastic Together](https://befantastic.in/together/overview/) in 2021. The fellowship program, which I was part of, explores the on-going climate emergency with projects using with Art & Technology.

The core idea of this project, cited from the [project page](https://befantastic.in/together/the-lost-passage/):

> “The Lost Passage” is a digitally reconstructed environment of a swarm of artificial passenger pigeons, which went extinct in the early 20th century. In this digital space, they inhabit a never-ending, sublime, yet destitute memory of a lost landscape. However, on closer inspection, they are actually confined within the four walls of this space.

Together with a New-Media Artist from USA, a cultural producer and a mentor from Singapore, we drafted the idea and each contributed to this project.

# Contribution

With a background in [Animal Science & Bionics/Biomimetics](/about/), I volunteered working on the flocking behavior of the pigeons.

## Initial implementation

First, I followed a [Cinder tutorial](https://libcinder.org/docs/guides/flocking/chapter1.html) and demonstrated the team how the swarm could look like. I just love the organic look and feel of the swarm. Notice also how it disperses from the imaginary red, triangular predators!

{% include video id='869180572' provider='vimeo' %}

## Improvements

With the help of [Amay Kataria](https://amaykataria.com/#/), we ported and adapted the behavior implementation from C++ to [Three.js](https://threejs.org/). Since the pigeon is supposed to be _trapped_ in the virtual box, I edited the behavior model to make them "boundary-aware". Finally, after adding the 3D pigeon model to the virtual world, the flock looked even more realistic than before.

{% include video id='869179355' provider='vimeo' %}

<br>

# Final thoughts

Switching from the C++ world to JavaScript the very first time was challenging yet fun experience. As the time given for the implementation was limited, the interactive web experience is only available on non-mobile devices. You can give it a try [here](https://thelostpassage.art).
