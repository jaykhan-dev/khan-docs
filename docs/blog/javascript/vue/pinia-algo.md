---
sidebar: auto
---

# Pinia
Pinia is the new state management for Vue JS.  It basically the next iteration of VueX.  The main difference is that there is no 'mutations' which was deemed to be *extremely* verbose.  The following snippet is a reference to get the Algo price from the Cryptocompare API in USD and display it in a Vue JS template.

## Pinia Store

```js
import { defineStore } from "pinia";
import axios from "axios";

export const usePriceStore = defineStore("price", {
  state: () => ({
    price: "",
  }),
  getters: {
    getPrice(state) {
      return state.price;
    },
  },
  actions: {
    async fetchPrice() {
      try {
        const data = await axios.get(
          "https://min-api.cryptocompare.com/data/price?fsym=ALGO&tsyms=USD"
        );
        this.price = data.data;
      } catch (error) {
        alert(error);
        console.log(error);
      }
    },
  },
});
```

## Display Price

```html
<template>
  <section class="flex justify-center bg-gray-900 text-white py-20">
    <div class="lg:w-2/4 grid lg:grid-cols-4 place-items-center text-center">
        <!-- GRID COL1 -->
      <div>
        <h1 class="lg:text-6xl font-bold text-2xl" v-if="price">
          {{ price.USD }}
        </h1>
        <p class="uppercase my-4">{{ msg }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, computed } from "vue";
import { usePriceStore } from "../stores/price";

const store = usePriceStore();
const msg = ref("Algo USD");
const price = computed(() => {
  return store.price;
});

onMounted(() => {
  store.fetchPrice();
});
</script>
```