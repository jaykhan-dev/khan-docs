---
tags:
  - javascript
  - gsap
  - animation
  - scrolling
  - vue js
---

# GSAP

[Official website](https://greensock.com/)

[Cheat Sheet](https://greensock.com/cheatsheet/)

GSAP is a great JavaScript library for creating modern animations on the web.  I use it pretty much for all my Vue JS projects because it's powerful and intuitive.  

## Scroll Trigger

The following code are references for scrolling animation techniques. 

### Imports

```js
// GSAP
import { gsap } from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";
import { onMounted } from "@vue/runtime-core";
gsap.registerPlugin(ScrollTrigger);
```
### Vue Component

This snippet scales up an `#element` as the user scrolls by.  The opacity and scale are set to `0` and starts animating at the bottom of the page.  When the page is halfway through, the `#element` is fully scaled and the opacity is set to `1` which is 100%. 

```js
export default {
  setup() {
    onMounted(() => {
      //IMAGE
      gsap.set("#element", { scale: 0, opacity: 0 });
      gsap.to("#element", {
        scrollTrigger: {
          trigger: "#element",
          scrub: 1,
          start: "top bottom",
          end: "top center",
        },
        scale: 1,
        opacity: 1,
        ease: "none",
        duration: 3,
      });
     
    });
  },
};
```

Based on this simple code reference, it is possible to switch it up by using `x,y` values for `position` and other cool effects.  This is just the tip of the iceberg. 

