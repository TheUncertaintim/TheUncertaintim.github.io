---
date: 2023-06-30
header:
  teaser: /assets/images/yjsh-day/teaser.png
  image: /assets/images/yjsh-day/header-image.png
  caption: "Photo credit: [SuperColeRolls](https://supercolerolls.pixieset.com/)"

gallery:
  - url: /assets/images/yjsh-day/figma-home-page.png
    image_path: /assets/images/yjsh-day/figma-home-page.png
    alt: "Figma design for home page"
    title: "Deign for home page"
  - url: /assets/images/yjsh-day/figma-tell-us.png
    image_path: /assets/images/yjsh-day/figma-tell-us.png
    alt: "Figma design for guestbook"
    title: "Design for guestbook"
  - url: /assets/images/yjsh-day/figma-photos.png
    image_path: /assets/images/yjsh-day/figma-photos.png
    alt: "Figma design for photo gallery"
    title: "Design for gallery"
---

A home-made, digital wedding guestbook

# Origin

In early 2023, my wife (back then fiancée) and I started planning our wedding reception to be held in June. In addition to hosting a wedding banquet, we also wanted to add a bit of interactive element and fun into it. After all, it's a once in a lifetime experience. :)

We were looking for inspirations online, and came across the idea of handing out marriage advice cards to the guests. The idea of receiving heart-warming messages and advice from our friends and family sounded awesome, so we decided to design and print the cards ourselves. Essentially, we were making a guestbook.

The problem? We also like to keep the photos taken on the actual day to be shared with everyone. Of course, services like Facebook or Instagram could have been used for this purpose. But since we were designing the marriage advice cards already, we might as well push it a little further, making it our own online guestbook instead.

# yjsh.day

We took our initials and bought a domain name [yjsh.day](https://yjsh.day), then got right down to work.

## Design

### Physical Cards

SH sketched out 5 different designs for the physical cards to be printed and handed out on the actual day. They are:

- **Advice** --- General marriage advice
- **Share** --- Share a memory with us
- **Suggest** --- Suggest an date night idea
- **Tell** --- Tell us something we don't know
- **Predict** --- Predict our future

For example, the physical version of the first card (**Advice**) looks like this:

{% include figure image_path="/assets/images/yjsh-day/physical-advice-card.png" alt="A printed marriage advice card on the table" caption="Physical marriage advice card" %}

### Web application

For the design of the web application, SH started out with a sketch in Figma.

{% include gallery caption="Figma design for **yjsh.day**" %}

In addition to the landing page (leftmost image), the web app consists of two main features:

- **Tell Us** --- digital guestbook
- **Photos** --- photo gallery

### Tell Us

Instead of writing the physical cards, the idea here is that our guest can fill out any advice card on their mobile device, and submit it directly to us. The messages submitted will be displayed on the web app right away, sharing it with everyone else.

### Photos

If there is any photo that our guests would like to share, this page provides a mean for them to upload it directly to us. The photos in the gallery will be updated as the submissions coming in.

## Implementation

As the design was being settled and finalized, I started looking into how to structure the app, and what tools to use.

### Tools and frameworks

I had some professional experience developing desktop application using JavaFX framework, but building a web application was my first time. I quickly went through the fundamentals of [Web Development](https://developer.mozilla.org/en-US/docs/Learn), and picked up [React.js](https://react.dev/learn) and [Next.js](https://nextjs.org/docs) in 2 months. In hindsight, going with React and Next.js was a correct and safe decision. These are very popular choices in modern web development, which makes it easy to find resources and helps online.

### Architecture

As Google Cloud Platform (GCP) was offering new customers a 90-day free trial (with $400 USD worth of credits), I decided to build the application around these GCP services:

- [**Datastore**](https://cloud.google.com/datastore/docs) --- NoSQL database for storing messages
- [**Cloud Storage**](https://cloud.google.com/storage/docs) --- Object storage for photos
- [**Cloud Function**](https://cloud.google.com/functions/docs) --- Serverless execution environment for thumbnail generation
- [**Google App Engine**](https://cloud.google.com/appengine/docs/nodejs) --- Fully managed environment for app deployment

For example, the text messages received from the guest were stored in Google Datastore, a NoSQL database. The photos shared by our guest were uploaded to Cloud Storage. For every photo uploaded, a Cloud Function was triggered to scale down the image to a thumbnail. The Google [Cloud Client Libraries](https://cloud.google.com/nodejs/docs/reference) were used to build the [API Routes](https://nextjs.org/docs/pages/building-your-application/routing/api-routes) in Next.js. And finally, the application itself was deployed in the Google App Engine (GAE).

{% include figure image_path="/assets/images/yjsh-day/architecture.png" alt="A diagram showing the GCP services used by the web app" caption="**Yjsh.day** is built with GCP services" %}

The reason I deployed the app in Google App Engine instead of on [Vercel](https://vercel.com/) is because that I was also preparing for [Google Cloud Associate Engineer Certification](https://cloud.google.com/learn/certification/cloud-engineer) and simply wanted to get some hands-on experience[^1].

### Dependencies

In addition to the GCP client libraries, two additional libraries were installed: [SWR](https://swr.vercel.app/) and [Photoswipe for React](https://photoswipe.com/react-image-gallery/).

- **SWR** --- A React Hooks library to perform Client-side data fetching without jeopardizing the performance
- **Photoswipe** -- A React component wrapper that offers ready-made interface for the user to browse the pictures in a gallery.

## Results

It took me around a month to build, test, debug and finally deploy the web app. Just like every other product in real life, the final implementation is never the same as the initial design. But it's close enough! This is how the landing page looked when it's implemented.

{% include figure image_path="/assets/images/yjsh-day/website-screenshot.png" alt="screenshot of the website" caption="Landing page of yjsh.day" %}

On the actual day, we received a handful of messages and numerous photos through the app. Seeing the application working, bringing in all the messages from our guest was fantastic. To me, it was a successful experiment!

I disabled the features for uploading photos and messages sometime after the wedding. But you can still visit the website at [yjsh.day](https://yjsh.day). The source code can be found in my [Github](https://github.com/TheUncertaintim/yjsh-day).

<!-- ### Hidden feature

One hidden feature baked into the app is to animate the messages received being written down one after another. This came in handy on the actual day, as the guests not using their mobile devices could choose to read the text messages on a TV instead.

{% include figure image_path="/assets/images/yjsh-day/handwriting-animation.gif" alt="Animation of messages being written down on a card" caption="Animating the text messages received" %}

You can still see it happening [here](https://yjsh.day/animate). The code for animating the text was adapted from [this SO answer](https://stackoverflow.com/questions/29911143/how-can-i-animate-the-drawing-of-text-on-a-web-page). -->

# Final thoughts

I couldn't be more happy about how the idea came about, and that it finally got implemented and was running as desired. I have learned a lot about web development during the process, and certainly gained more experience working with the cloud.

Many thanks to my wife SH for working with me on this project, it would not have been possible without her.

[^1]: I passed the [Associate Cloud Engineer certification exam](https://google.accredible.com/7cfc739f-27ef-4e2d-85a2-38c82dd99391) 2 months after the project.
