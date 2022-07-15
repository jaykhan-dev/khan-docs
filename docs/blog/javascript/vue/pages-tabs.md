---
tags:
  - vue js
  - javascript
  - html
  - css
  - tabs
  - modular
---

# The following code is for creating tabs but without using Slots 

## `template`

```html
<template>
  <div class="flex space-x-4">
    <button @click="currentTabComponent = 'TabOne'">
      <p class="activeStyle">TAB1</p>
    </button>
    <button @click="currentTabComponent = 'TabTwo'">tab 2</button>
    <button @click="currentTabComponent = 'TabThree'">tab 3</button>
  </div>

  <keep-alive>
    <component :is="currentTabComponent" :style="activeStyle"></component>
  </keep-alive>
</template>
```

Using the composition API, we have to set a few variables and import pages.

## `<script>`
```html
<script>
import TabOne from "./TabOne.vue";
import TabTwo from "./TabTwo.vue";
import TabThree from "./TabThree.vue";
import { ref, reactive } from "vue";

export default {
  name: "App",
  components: {
    TabOne,
    TabTwo,
    TabThree,
  },
  setup() {
    const isActive = ref(true);
    const currentTabComponent = ref("TabOne");
    const activeStyle = reactive({
      color: "blue",
    });
    return {
      isActive,
      currentTabComponent,
      activeStyle,
    };
  },
};
</script>
```
