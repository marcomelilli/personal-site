---
template: post
title: Generate dynamic open graph images for blog posts
slug: generate-dynamic-open-graph-images-blog-post-title
draft: true
date: 2020-05-05T12:29:56.500Z
description: >-
  Learn how to generate social cards for Twitter, Facebook, Slack with the blog
  post title, using og-image service by Vercel
category: SEO
tags:
  - web
  - social
  - opengraph
---
**Open graph tags** are very useful and everybody have to know them because they help to optimize your content for social sharing. Look this example from this blog:

![og dynamic image comparison](/media/og-dynamic-image.png "og dynamic image")

To obtain the second image you need to configure the `og` tags in the section `<head />` of your blog page.

There are lots of Open Graph properties, but the most importants are:

* **og:title** – The title of your object as it should appear within the graph, e.g., “My blog title
* **og:type** – The type of your object, e.g., “video.movie”. Depending on the type you specify, other properties may also be required.
* **og:image** – An image URL which should represent your object within the graph.
* **og:url** – The canonical URL of your object that will be used as its permanent ID in the graph, e.g., “[m](http://www.imdb.com/title/tt0117500/)ysite.com/my-awesome-blog-post“

The image