---
tags:
  - vue js
  - javascript
  - framework
  - user interface
  - spa
  - ssr
  - progressive
  - web
  - open source
  - pwa
  - typescript
  - vuex
  - vue router
  - vite
  - pinia
  - nuxt
  - vuepress
---

# Vue JS

## JavaScript framework

[See official site](https://vuejs.org/)

Vue JS is a modern JavaScript framework that uses Node, webpack bundling, and ES modules.  It is great for creating user interfaces because Vue falls into the "View" category of the [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) model of modern web development.  It's possible to add third party libraries like Three JS, GSAP to add more sophisticated animations and 3D spaces.

The simplicity of Vue JS is what attracted me to it.  It is intuitive and easy to setup and deploy.  Being similar to other frameworks like React and Angular, Vue is not backed by a mega corporation but rather by the online community of developers who decided to improve Vue out of appreciation.  It's open source and has a robust ecosystem.   

## The ecosystem
The Vue JS ecosystem is growing everyday.  Though not the most popular JavaScript framework (that honor belongs to React), it is attracting developers due its inherent simplicity and developer satisfaction.

### VueX/Pinia
VueX is the official state management for Vue.  When an application gets more and more complicated, it's necessary to use a vuex store to get the data from an API and commit mutations when a change occurs in the backend.  The frontend then gets updated automatically.  Think of state management as the **source of truth**.  

[VueX Docs](https://vuex.vuejs.org/) - is the first version of state management that is based on Redux by React.

[Pinia Docs](https://pinia.vuejs.org/) - the new way of state management that is being maintained by the core Vue JS developers.

### Vue Router
[Vue Router docs](https://router.vuejs.org/)

The official router for Vue JS. A single page app requires a different kind of routing system than the traditional method of loading a new page for each link.  In SPA's, there is only one page that gets loaded but the DOM can be manipulated with JavaScript.  This is great if you want a site that feels like a **real time** application, similar to [AJAX](https://www.w3schools.com/xml/ajax_intro.asp).

### Vite
[Vite Docs](https://vitejs.dev/)

From the official docs:
>Vite (French word for "quick", pronounced /vit/, like "veet") is a build tool that aims to provide a faster and leaner development experience for modern web projects.

The two main parts are the **dev server** and uses the **Rollup** bundling tool to make servers super fast. I use Vite with all my projects because the developer experience is much nicer. 

### Nuxt
[Official site](https://nuxtjs.org/)

Nuxt is a framework built on top of Vue JS.  It has many features that make it a production ready framework which is great for building modern applications.  It's SEO friendly, and can use most modern UI frameworks like [Tailwind CSS](https://tailwindcss.com/).


### VuePress
[Official docs](https://v2.vuepress.vuejs.org/)

This site is built with VuePress which is a great way of building static sites.  Working with data is essential in todays world but how that data is rendered on the client is something every UX designer must take into consideration.  

Speed is a major issue with all websites and applications and compromising can lead to lost business.  In this case, I wanted a site that would *load fast*, and has a great UX and easy development environments.

If SEO is a matter of concern, then VuePress is built to be SEO-friendly.

Installing a VuePress site is as simple as running the following commands:

1. Create a folder
```bash
mkdir vuepress-site
cd vuepress-site
```

2. Initialize git and npm
```bash
git init
npm init
```

3. Install VuePress
```bash
npm install -D vuepress@next
```

After this the steps are more involved and requires an understanding of basic JavaScript.

## Mobile
Building mobile apps is a big thing these days.  So many users first look up information on their phones and so having a mobile native app can be a great way of connecting with them. There are several frameworks which make it easy to build mobile native apps for iOS and Android.  

Below is a link to Ionic which is intuitive and easy to setup.  There is a learning curve but being familiar with Vue JS it's not a big hurdle.   
### Ionic
[Official website](https://ionicframework.com/)

## E-Commerce
It is possible to use Vue for popular e-commerce platforms.  The preferred way is to use a [headless CMS](https://jamstack.org/headless-cms/) with a REST API and hook it up to the frontend with Vue.

### Vue Storefront
[Official website](https://www.vuestorefront.io/)

## Web3
The fact that Vue JS can be used with web3 is a major plus in my book.  I plan on using it a lot to build dapps, especially for Ethereum and Algorand.  See below for the respective links.
