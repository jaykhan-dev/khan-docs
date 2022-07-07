---
sidebar: auto
---

# Creating Tabs
The following snippets of code are a reference for creating tabs entirely with Vue JS.  It requires at least 3 components and uses the composition API and slots.

## Tabs

```html
<template>
  <div class="tab-content" v-show="title == selectedTitle">
    <slot />
  </div>
</template>

<script>
import { inject } from "vue";
export default {
  props: ["title"],
  setup() {
    const selectedTitle = inject("selectedTitle");
    return {
      selectedTitle,
    };
  },
};
</script>
```

## Tabs Wrapper

```html
<template>
  <div class="tabs grid place-items-center">
    <ul class="tabs__header flex my-2 items-center">
      <li
        v-for="title in tabTitles"
        :key="title"
        @click="selectedTitle = title"
        :class="{ selected: title == selectedTitle }"
        class="p-2 border-b-4 mx-2 border-gray-700 hover:border-b-blue-600 duration-300 cursor-pointer"
      >
        {{ title }}
      </li>
    </ul>
    <slot />
  </div>
</template>

<script>
import { ref, provide } from "vue";
export default {
  setup(props, { slots }) {
    const tabTitles = ref(slots.default().map((tab) => tab.props.title));
    const selectedTitle = ref(tabTitles.value[0]);
    provide("selectedTitle", selectedTitle);
    return {
      selectedTitle,
      tabTitles,
    };
  },
};
</script>

<style>
.tabs__header li.selected {
  border-bottom: 8;
  border-bottom-color: green;
}
</style>
```

## Tabs usage

```html
<template>
  <section class="text-white flex justify-center">
    <div class="">
      <TabsWrapper>
        <TabsEach title="Vue">
          TEXT FOR TAB 1
        </TabsEach>
        <TabsEach title="E-comm"
         TEXT FOR TAB 2
        </TabsEach>
      </TabsWrapper>
    </div>
  </section>
</template>

<script setup>
import TabsWrapper from "./TabsWrapper.vue";
import TabsEach from "./TabsEach.vue";
</script>
```