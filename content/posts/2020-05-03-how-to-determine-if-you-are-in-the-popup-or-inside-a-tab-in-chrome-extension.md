---
template: post
title: How to determine if you are in the popup or inside a tab in chrome extension
slug: chrome-extension-determine-if-inside-popup-or-tab
draft: false
date: 2020-05-03T13:23:11.402Z
description: >-
  How to find out is the user is in the popup or in a tab to handle different
  actions
category: ChromeExtension
tags:
  - chrome
---
During the development of a chrome extension you can execute the content of "popup.html" inside the **popup**, or open the content in a new **tab**. Sometimes you need to **know where the user is**, so you can handle different actions for different contexts. How to determine it? 

This simple function returns true if you are inside the popup otherwise false:

```javascript
 const isInPopup = function() {
     return (typeof chrome != undefined && chrome.extension) ?
         chrome.extension.getViews({ type: "popup" }).length > 0 : null;
 }

if(isInPopup()){
  //Open the popup content in a new tab
  chrome.tabs.create({url: chrome.extension.getURL('popup.html')});
} else {
  //If you are already in the tab, do something else 
  ...
}
```