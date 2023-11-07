---
layout: post
title: "Free My Photos From Untappd"
date: 2023-11-06
---

This week at work is “craft week” (okay that really doesn’t translate smoothly from Norwegian) and we have a whole week intended for studying, experimenting, side projects, or anything else we choose to dive into. There’s no requirement of direct relevance to work — and so my first mission this week is the extremely important task of collecting 756 of my own photos of beer.

## CS50 final project

I registered my first beer on Untappd in 2013 when I attended [a conference in Nottingham](https://newadventuresconf.com/2013/). Last year, I&nbsp;decided 10 years of very active registration was enough — now I have completed a last farewell check&#8209;in, and exported all my data. I started playing around with this data for my final project when doing [CS50](https://cs50.harvard.edu/x/2021/), and created a travel journal for myself: [Wanderlust and 9 Years of Location Data]({{ '/2021/12/cs50/' | url }}).

## But what about my photos?

My data from Untappd is exported as JSON and as CSV. It contains a `photo_url` and now I want to write a script that lets me download them all. I may technically have the same photos on my phone already, but not in any structured way. Seems fun to download all the images I have in my Untappd account, and then be able to use these photos together with the rest of the data.

## Anchors can download!

When I started looking into approaches, I was surprised to learn the trusty and humble `<a>` element has an attribute I wasn’t familiar with. The `download` attribute makes the browser treat the link as a&nbsp;download, saving the file to the directory I have in my browser settings for downloads. I noticed that when opening a static `.html` locally, the browser will open the image in a new tab. But when running my project locally with a server, the file will download when I click something like this:

```html
<a href="photos/987.jpg" download="beer001.jpg">
    Download beer 001 as a jpg to your computer
</a>
```

This only works for [same-origin URLs](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) and that is not case for my needs now in freeing my photos from remote origins down to my computer. Is there a way around that? Yes! Especially since I’m looking for a way for me to download a batch of photos once, and learn something about browsers and JavaScript along the way. I’m not building an app where this is a feature, so note that YMMV.

## Fetch and Blob

The internet is overflowing with answers that suggest a combo of [using the Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) and the `fetch()` method — along with the [Blob object](https://developer.mozilla.org/en-US/docs/Web/API/Blob). Fun word, remind me MDN what a blob is?

> a file-like object of immutable, raw data; they can be read as text or binary data, or converted into a `ReadableStream` so its methods can be used for processing the data.

MDN can also explain that the `ReadableStream` interface is from the [Streams API](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API):

> The Streams API allows JavaScript to programmatically access streams of data received over the network and process them as desired by the developer.

I’m not entirely clear on why and how this all comes together. Does this approach basically create a new same&#8209;origin URL? 🤔 That is something for me to understand better another day. But _today_ I have successfully downloaded all the photos from my account with this function:

```js
function downloadPhotos() {
  // loop though myArray of beer check-ins with photos
  myArray.forEach(function (item, index) {
    fetchWithAnchorElement(item, index);

    async function fetchWithAnchorElement() {
      // each item in myArray has this photo_url key  
      const img = await fetch(item.photo_url); 
      const imgBlob = await img.blob();
      const imgUrl = URL.createObjectURL(imgBlob);

      const anchor = document.createElement("a");
      anchor.href = imgUrl;
      anchor.download = `beer${index}.jpg`;
      document.body.appendChild(anchor);
      anchor.click();
      document.body.removeChild(anchor);
    }
  });
}
```

I started working with a limited `test-data.json` and when switching to my full data set, I initially intended to limit the first run. But I messed up how I called `slice()` on my array, and before I knew it I had downloaded files `beer0.jpg` — `beer755.jpg`. Browsers are amazing! 🎉
