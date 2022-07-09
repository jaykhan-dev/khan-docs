---
tags:
  - vue js
  - javascript
  - marquee
  - plugin
  - npm
---

# Vue 3 Marquee

Using a marquee in Vue JS is really easy.  First you need to install the node package for Vue 3, include it in the `main.js` file, define the `data` and create a `v-for` loop in the HTML.

## Install

```bash
npm install vue3-marquee
```

## main.js

```js
//Vue3 Marquee
import Vue3Marquee from "vue3-marquee";
import "vue3-marquee/dist/style.css";

app.use(Vue3Marquee);
```

## HTML

```html
<Vue3Marquee class="overflow-hidden sm:w-full" id="marquee">
    <h3
        v-for="(word, index) in test"
        :key="index"
        :class="{ word: true, odd: index % 2 === 0, even: index % 2 === 1 }"
        class="font-bold text-8xl text-white text-opacity-10 uppercase p-4"
    >
        {{ word }}
    </h3>
</Vue3Marquee>
```


## Script
```js
export default {
  name: "VueEcosystem",
  components: {
    TabsEcosystem,
  },
  data() {
    return {
      test: [
        "Vue JS",
        " | ",
        "Satoshi Nakamoto ",
        " | ",
        "Algorand ",
        " | ",
        "Polygon ",
        " | ",
        "Carbon Neutral blockchain ",
        " | ",
        "E-Commerce ",
        " | ",
        "Web3 ",
        " | ",
        "Stablecoins ",
        " | ",
      ],
    };
  },
};
```