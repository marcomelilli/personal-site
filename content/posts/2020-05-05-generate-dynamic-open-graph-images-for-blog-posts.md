---
template: post
title: Generate dynamic open graph images for blog posts
slug: generate-dynamic-open-graph-images-blog-post-title
draft: true
date: 2020-05-05T12:29:56.500Z
description: >-
  Learn how to generate social cards for Twitter, Facebook, Slack with the blog
  post title, using og-image service by Vercel. And how to integrate it in a
  gatsbyjs blog.
category: SEO
tags:
  - web
  - social
  - opengraph
  - gatsbyjs
---
**Open graph tags** are very useful and everybody have to know them because they help to optimize your content for social sharing. Look this example from this blog:

![og dynamic image comparison](/media/og-dynamic-image.png "og dynamic image")

To obtain the second image you need to configure the `og` tags in the section `<head />` of your blog page.

There are lots of Open Graph properties, but the most importants are:

* **og:title** – The title of your object as it should appear within the graph, e.g., “My blog title
* **og:type** – The type of your object, e.g., “video.movie”. Depending on the type you specify, other properties may also be required.
* **og:image** – An image URL which should represent your object within the graph.
* **og:url** – The canonical URL of your object that will be used as its permanent ID in the graph, e.g., “[m](http://www.imdb.com/title/tt0117500/)ysite.com/my-awesome-blog-post“

## How to generate an awesome card with a title

It would take a long time to design an image for every single blog post, right? And we don't want the exact same image for every blog post because that wouldn't make the article stand out when it was shared to Twitter.

To obtain the second image I used this [og-image service by Vercel](https://github.com/zeit/og-image) that is available and free on github.\
Here you can see a [live preview](https://og-image.now.sh/) to how it works: you can make a get request to the service passing parameters like the *title text* and an *image url*, and it automagically creates a **card image** that you can add to your `og:image` tag.

**How it works?**\
\
To use the service you need to self hosted your own version. You can follow the official guide to deploy for free on Vercel (Zeit) or you can decide to host where you want:

1. Go to the [github project](https://github.com/zeit/og-image) and click the fork button at the top right of GitHub
2. Clone the repo to your local machine with`git clone URL_OF_FORKED_REPO_HERE`
3. Make some changes to configure your own version:

   * File `now.js`: if you want to use the Vercel free plan, you need to remove all the properties except `"rewrites"`
   * File `api/_lib/parser.ts`: At row 61 you need 

     ```javascript
     ... 
         if (!images[0].startsWith('https://assets.vercel.com/') && !images[0].startsWith('https://assets.zeit.co/')) {
     ...
     ```

     and replace with your own domain if you want to limit the other people can use your self hosted version:

     ```javascript
      ... 
         if (!images[0].startsWith('https://marcomelilli.com/')) {`
      ... 
     ```
   * In `api/_lib/parser.ts`: you can edit and restyle the card css as you wish.
4. run `npm install -g now`
5. Run locally with `now dev`and visit [localhost:3000](http://localhost:3000/) to test it. Eg: [localhost:3000](http://localhost:3000/)/my-title-example
6. Deploy to the cloud by running `now`and you'll get a unique URL

Now you can generate images using the following **url**:

`https://<MY_UNIQUE_URL>.now.sh/my%20blog%20post%20title?images=https://url-logo.svg`

## Integrate in a GatsbyJs blog