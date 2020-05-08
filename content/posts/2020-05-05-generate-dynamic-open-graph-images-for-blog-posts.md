---
template: post
title: Generate dynamic open graph images for blog posts
slug: generate-dynamic-open-graph-images-blog-post-title
draft: false
date: 2020-05-06T16:00:56.500Z
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

* **og:title** – The title of your object as it should appear within the graph, e.g. “My blog title"
* **og:image** – An image URL which should represent your object within the graph.
* **og:url** – The canonical URL of your object that will be used as its permanent ID in the graph, e.g., “mysite.com/my-awesome-blog-post“

## How to generate an awesome card with a text

It would take a long time to design an image for every single blog post, right? And we don't want the exact same image for every blog post because that wouldn't make the article stand out when it was shared to Twitter.

To obtain the second image I used this [og-image service by Vercel](https://github.com/zeit/og-image) that is available and free on github.\
Here you can see a [live preview](https://og-image.now.sh/) to how it works: you can make a get request to the service passing parameters like the *title text* and an *image url*, and it automagically creates a **card image** that you can add to your `og:image` tag.

**How it works?**\
\
To use the service you need to self host your own version. You can follow the official guide to deploy for free on Vercel (Zeit) or you can decide to host where you want:

1. Go to the [github project](https://github.com/zeit/og-image) and click the fork button at the top right of GitHub
2. Clone the repo to your local machine with`git clone URL_OF_FORKED_REPO_HERE`
3. Make some changes to configure your own version:

   * File `now.js`: if you want to use the Vercel free plan, you need to remove all the properties except `"rewrites"`
   * File `api/_lib/parser.ts`: At row 61 you need to find the following lines and remove them. This is a check that limits other sites to use your instance, infact it'll replace every custom image you'll pass in the params with the default one (the Vercel logo).

     ```javascript
     ... 
         if (!images[0].startsWith('https://assets.vercel.com/') && !images[0].startsWith('https://assets.zeit.co/')) {
            images[0] = defaultImage;
         }
     ...
     ```

     In my case I hosted all the images that I want to use (programming logos) in my blog, so I decided to replace the condition with my **domain name:**

     ```javascript
      ... 
         if (!images[0].startsWith('https://marcomelilli.com/')) {`
      ... 
     ```
   * Finally in `api/_lib/parser.ts`you can edit and restyle the card as you wish (it's all html and css)
4. Run `npm install -g now`
5. Run locally with `now dev`and visit [localhost:3000](http://localhost:3000/) to test it. Eg: [localhost:3000](http://localhost:3000/)/my-title-example
6. Deploy to the cloud by running `now` and you'll get a unique URL

Finally you can generate images using the following **url**:

`https://<MY_UNIQUE_URL>.now.sh/my%20blog%20post%20title?images=https://url-logo.svg`

## Integrate og-image in a GatsbyJs blog

You can use that url to fill the tag `og:image` in your post page. If you use a static site generator like **GatsbyJs,** it's very easy to implement. To set **meta tags headers** in a page, the best solution is [gatsby-plugin-react-helmet](https://www.gatsbyjs.org/packages/gatsby-plugin-react-helmet/) that lets you control your document head using their React component.

This is an example that you can use in your **Post layout template**:

```javascript
...

const Layout = () => {
  ...
  const metaImageUrl = category ? 
    (category ? ("https://<MY_UNIQUE_URL>.now.sh/" + postTitle + "?images=https://mysite.com/media/"+category.toLowerCase()+".svg") 
      : author.photo);
  ...

  return (
    <div className={styles.layout}>
      <Helmet>
        <html lang="en" />
        <title>{title}</title>
        <meta name="description" content={description} />
        <meta property="og:site_name" content={title} />
        <meta property="og:image" content={metaImageUrl} />
        <meta name="twitter:card" content="summary_large_image" />
        <meta name="twitter:title" content={title} />
        <meta name="twitter:description" content={description} />
        <meta name="twitter:image" content={metaImageUrl} />
      </Helmet>
      {children}
    </div>
  );
};
...
```

In this example I put all my category images in the folder *media* in my site, and in this way I'ill autogenerate an og image with the `postTitle` and the `category logo` for every article:

`https://<MY_UNIQUE_URL>.now.sh/" + postTitle + "?images=https://mysite.com/media/"+category.toLowerCase()+".svg`

You are free to generate the images you want according to your needs.



__Note__: If you did everithing correctly but still have __some issues__ with Facebook and Twitter preview, you can read [this article](https://marcomelilli.com/posts/gatsby-react-helmet-og-meta-tags-are-not-recognized) about how I fixed an annoying problem with gatsby-plugin-react-helmet