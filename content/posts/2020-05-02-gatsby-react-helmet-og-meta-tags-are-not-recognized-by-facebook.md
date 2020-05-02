---
template: post
title: Gatsby react helmet og meta tags are not recognized
slug: gatsby-react-helmet-og-meta-tags-are-not-recognized
draft: false
date: 2020-05-02T12:39:51.164Z
description: >-
  What to do when facebook or twitter don't find OpenGraph meta tags generated
  by gatsby-plugin-react-helmet
category: GatsbyJs
tags:
  - gatsbyjs
  - opengraph
---
The plugin [gatsby-plugin-react-helmet](https://www.gatsbyjs.org/packages/gatsby-plugin-react-helmet/) is helpful to generate `og` meta tags but I recently noticed that **facebook** and **twitter** stopped to recognize the meta tags in my site. 

Looking for a solution, I discovered that other people had the same issue and infact there is an [open issue](https://github.com/gatsbyjs/gatsby/issues/22908) on github, at the moment I'm writing this article.

The main problem is that this plugin put all the tags at the **bottom of the header** and in some projects, when **large style tag** being placed before the meta tags, Facebook does not always parse the `og`tags if they come too late in the head. So the easiest way to resolve the problem is to prioritize Helmet tags in the `<head />` tag.

An elegant workaround proposed by [ttstauss](https://github.com/ttstauss) and [Ciantic](https://github.com/Ciantic) in this [issue](https://github.com/gatsbyjs/gatsby/issues/22206):

Create a `gatsby-ssr.js` in the root of your gatsbyjs project with the following content:

```javascript
const React = require("react")
const { Helmet } = require("react-helmet")

exports.onRenderBody = (
  { setHeadComponents, setHtmlAttributes, setBodyAttributes },
  pluginOptions
) => {
  const helmet = Helmet.renderStatic()
  setHtmlAttributes(helmet.htmlAttributes.toComponent())
  setBodyAttributes(helmet.bodyAttributes.toComponent())
  setHeadComponents([
    helmet.title.toComponent(),
    helmet.link.toComponent(),
    helmet.meta.toComponent(),
    helmet.noscript.toComponent(),
    helmet.script.toComponent(),
    helmet.style.toComponent(),
  ])
}

exports.onPreRenderHTML = ({ getHeadComponents, replaceHeadComponents }) => {
  const headComponents = getHeadComponents()
  headComponents.sort((x, y) => {
    if (x.props && x.props["data-react-helmet"]) {
      return -1
    } else if (y.props && y.props["data-react-helmet"]) {
      return 1
    }
    return 0
  })
  replaceHeadComponents(headComponents)
}
```

More info about Gatsby Server Rendering APIs and `OnPreRenderHTML`function [here](https://www.gatsbyjs.org/docs/ssr-apis/#onPreRenderHTML)

Note: the content of *gatsby-ssr.js* worked for me only after `gatsby build` in production, not with the `gatsby develop` command