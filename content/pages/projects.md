---
template: page
title: Projects
socialImage: ''
slug: projects
draft: true
---
This is the list of projects I developed in my free time:

## Products Box

[Products Box](https://productsbox.dev) is a chrome extension that helps you to organize all your projects and products.

<img src="https://productsbox.dev/static/logo-6a24baa9faf55025db35aafd35d5a687.png"/> 

You can add your projects and create 3 types of actions for every product:

* **Navigation**: bookmarks to open new tabs
* **Webhooks**: to send http requests to webhooks (launch a build on netlify, a task on zapier, add a task log on makerlog, etc..)
* **Cards**: You can create a mini dashboard adding cards with important informations (number of users, revenue, etc..)

It's was developed in [Reactjs](https://it.reactjs.org/), [Userbase](https://userbase.com) and [Firebase Cloud Functions](https://firebase.com)

## Big Bench App

<img style="float: left; height: 300px; margin-right: 20px;" src="https://scontent.fmxp6-1.fna.fbcdn.net/v/t1.0-9/117826788_1026341171130506_8947142900720440714_o.png?_nc_cat=101&ccb=2&_nc_sid=09cbfe&_nc_ohc=KoCJ1xjKSOcAX-xZR7x&_nc_ht=scontent.fmxp6-1.fna&oh=069b43fd02a485167c7b5a082baa0930&oe=6044CA5C"/> 

From 2018 to 2021 I worked on **Big Bench App**, a mobile app for Android and iOS that helped people to find giant benches (tourist attractions) in Italy. The app had more than 15k downloads between the stores and more than 8k of subscribed users. I worked on the mobile app and on the backend, and it was a great experience.\
The project consisted of a hybrid mobile app built with Ionic, a backend in NestJs (a nodejs framework) and a website in ReactJs.\
\
Press:

* https://radiogold.it/cronaca/179840-grandi-panchine-finiscono-tutte-in-unapp/\
* https://xantarmob.altervista.org/big-bench-lapp-per-trovare-le-panchine-con-i-panorami-piu-belli/amp/\
* https://www.lacascatadeisapori.it/big-bench-le-grandi-panchine-nelle-langhe/

<div style="clear:both"></div>

## Nestjs email authentication

<img style="float: left; height: 200px; margin-right: 20px;" src="https://d33wubrfki0l68.cloudfront.net/e937e774cbbe23635999615ad5d7732decad182a/26072/logo-small.ede75a6b.svg"/> 

This project is an example of implementation of a user **email authentication** with [Nestjs](https://nestjs.com/) v5.0, [MongoDB](https://www.mongodb.com/) and [PassportJs](http://www.passportjs.org)

It can be used as base of a nestjs project: it implements API for login/registration of a user in a database and features of **email verification**, **forgotten password**, **reset password**, **update profile** and **settings**. It implments a DockerFile to run it in a container. [Link to the project](https://github.com/marcomelilli/nestjs-email-authentication). 200+ stars on Github   

## ATM Bot Notifier

<img style="float: left; height: 200px; margin-right: 20px;" src="/media/atm_channel.jpg"/> 

I made a little **telegambot** that updates you every morning with the news of the ATM metro and during the day notifies you about status changes. 

It could be useful to know in real time if the subway is suspended and quickly look for alternatives. 

Link to the [channel](https://t.me/metro_atm)    

<div style="clear:both"></div>

## HomeAssistant

I started to develop a **homeautomation system** for my home using a Raspberry and [Homeassistant](https://www.home-assistant.io/). 

![image1.png](https://raw.githubusercontent.com/marcomelilli/homeassistant-config/master/www/screenshots/image1.png)

This is my [configuration](https://github.com/marcomelilli/homeassistant-config)

## Four in a row - AI

This project is an implementation in javascript of the algorithm [minimax](https://en.wikipedia.org/wiki/Minimax) with [Alpha-Beta pruning](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning) applied to the game **Connect Four**.

![game screenshot](https://github.com/marcomelilli/four-in-a-row-js-minimax/raw/master/img/game-screen.png) It uses [EaselJs](https://www.createjs.com/easeljs) for drawing the board, as support for working with the HTML5 Canvas element. You can find the project [here](https://github.com/marcomelilli/four-in-a-row-js-minimax) and a [live demo](http://connectfour.marcomelilli.com)!