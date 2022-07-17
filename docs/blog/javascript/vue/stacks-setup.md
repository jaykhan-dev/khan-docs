---
tags:
  - vue js
  - blockchain
  - bitcoin
  - vite
  - install
  - setup
  - stacks blockchain
  - stacks
  - layer 1
  - vue 3
  - javascript
  - html
  - css
  - tailwind css
  - eslint
  - prettier
  - axios
  - vue router
  - pinia
  - node js
  - hiro wallet
  - web3
  - nft
  - defi
---

# Vue + Stacks

Stacks has a Vue starter npm package which can be created with the following commans:

```bash
npm create stacks
cd project-name
npm install
npm start
```
This comes with Stacks.JS plugins that allow a user to connect their Hiro Wallet. 

However, it requires additional plugins to make it more robust and fully functional as a Vue 3 app

## npm installs

```bash
npm i axios pinia gsap @vueuse/motion vue-router 
npm i --save-dev @rushstack/eslint-patch @vue/eslint-config-prettier @vue/test-utils cypress eslint eslint-plugin-cypress eslint-plugin-vue jsdom prettier start-server-and-test vitest
```

See [Tailwind](/blog/javascript/vue/tailwind-css/) for how to setup the css

## Cypress

In a `cypress.config.js` file, put the following code :

```js
// eslint-disable-next-line no-undef
const { defineConfig } = require("cypress");
// eslint-disable-next-line no-undef
module.exports = defineConfig({
  e2e: {
    specPattern: "cypress/e2e/**/*.{cy,spec}.{js,jsx,ts,tsx}",
    baseUrl: "http://localhost:4173",
  },
});
```


## `.gitignore`

```
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*
lerna-debug.log*

node_modules
.DS_Store
dist
dist-ssr
coverage
*.local

/cypress/videos/
/cypress/screenshots/

# Editor directories and files
.vscode/*
!.vscode/extensions.json
.idea
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?
```

## `package.json`

```js
"scripts": {
    "start": "vite",
    "build": "vite build",
    "preview": "vite preview --port 5050",
    "test:unit": "vitest --environment jsdom",
    "test:e2e": "start-server-and-test preview http://127.0.0.1:4173/ 'cypress open --e2e'",
    "test:e2e:ci": "start-server-and-test preview http://127.0.0.1:4173/ 'cypress run --e2e'",
    "lint": "eslint . --ext .vue,.js,.jsx,.cjs,.mjs --fix --ignore-path .gitignore"
  },
```

## ESLint and Prettier

Create a `.eslintrc.cjs` file and put the following code:

```js
/* eslint-env node */
require("@rushstack/eslint-patch/modern-module-resolution");

module.exports = {
  root: true,
  extends: [
    "plugin:vue/vue3-essential",
    "eslint:recommended",
    "@vue/eslint-config-prettier",
  ],
  env: {
    "vue/setup-compiler-macros": true,
  },
  overrides: [
    {
      files: ["cypress/e2e/**.{cy,spec}.{js,ts,jsx,tsx}"],
      extends: ["plugin:cypress/recommended"],
    },
  ],
};
```

## `router.js`

```js
import { createRouter, createWebHistory } from "vue-router";
import HomeView from "../views/HomeView.vue";

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  linkActiveClass: "activeClass",
  routes: [
    {
      path: "/",
      name: "home",
      component: HomeView,
    },
    {
      path: "/about",
      name: "about",
      component: () => import("../views/AboutView.vue"),
    },
  ],
});

export default router;
```
## Sample Store

```js
import { defineStore } from "pinia";
import axios from "axios";

export const SongsStore = defineStore("SongsStore", {
  state: () => ({
    songs: [],
    loading: true,
  }),
  getters: {
    getSongs(state) {
      return state.songs;
    },
  },
  actions: {
    async fetchSongs() {
      try {
        const data = await axios.get(
          "https://khanquest.herokuapp.com/api/v2/pages/?type=songs.SongPage&fields=title,artist_name,album,date,song_key,bpm,writers,tags,categories(name),song_catalog,song_history,song_file,song_image_thumbnail"
        );
        this.songs = data.data;
        this.loading = false;
      } catch (error) {
        alert(error);
        console.log(error);
      }
    },
  },
});
```

## `main.js`

```js
import { createApp } from "vue";
import App from "./App.vue";
import "./index.css";
import { MotionPlugin } from "@vueuse/motion";
import { createPinia } from "pinia";
import router from "./router";

import { Buffer } from "@stacks/common";

window.Buffer = window.Buffer || Buffer;

const app = createApp(App);

app.use(MotionPlugin);
app.use(createPinia());
app.use(router);

app.mount("#app");
```

