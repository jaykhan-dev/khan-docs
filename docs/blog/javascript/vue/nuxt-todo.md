---
tags:
  - nuxt
  - vue
  - todo
---

# Nuxt

## `store.js`

```js
export const state = () => ({
  tasks: [],
});

export const mutations = {
  ADD_TASK(state, task) {
    state.tasks = [{ content: task, done: false }, ...state.tasks];
  },
  REMOVE_TASK(state, task) {
    state.tasks.splice(state.tasks.indexOf(task), 1);
  },
  TOGGLE_TASK(state, task) {
    task.done = !task.done;
  },
};
```

## `index.vue`

```html
<template>
  <main class="grid place-items-center">
    <NuxtLogo />
    <ComponentOne />
    <h1 class="text-4xl font-bold">Task Board</h1>
    <p class="text-2xl">Create a list of tasks</p>

    <div class="create-new my-8">
      <input
        v-model="newTask"
        type="text"
        class="border border-black p-2 rounded font-mono"
        placeholder="Add a new task"
        @keypress.enter="addTask"
      />
      <button
        class="p-2 bg-green-500 text-white rounded hover:bg-blue-500 duraiton-300"
        @click="addTask"
      >
        Add
      </button>
    </div>

    <div class="tasks">
      <TaskAdd v-for="(task, i) in $store.state.tasks" :key="i" :task="task" />
    </div>

    <div>
      <nuxt-link to="/NewPage">New Page test</nuxt-link>
    </div>
  </main>
</template>

<script>
  import NuxtLogo from "~/components/NuxtLogo.vue";
  import ComponentOne from "~/components/ComponentOne.vue";
  export default {
    components: { NuxtLogo, ComponentOne },
    data() {
      return {
        newTask: "",
      };
    },
    methods: {
      addTask() {
        if (this.newTask) {
          this.$store.commit("ADD_TASK", this.newTask);
          this.newTask = "";
        }
      },
    },
  };
</script>
```

## `TaskAdd.vue`

```html
<template>
  <div :class="`task ${task.done ? 'is-complete' : ''}`">
    <div class="content">{{ task.content }}</div>
    <div class="buttons">
      <button @click="toggleDone">{{ task.done ? 'Undo' : 'Done' }}</button>
      <button @click="removeTask" class="delete">Delete</button>
    </div>
  </div>
</template>

<script>
  export default {
    props: ["task"],
    methods: {
      toggleDone() {
        this.$store.commit("TOGGLE_TASK", this.task);
      },
      removeTask() {
        this.$store.commit("REMOVE_TASK", this.task);
      },
    },
  };
</script>

<style></style>
```

## `eslintrs.js`

```js
module.exports = {
  root: true,
  env: {
    browser: true,
    node: true,
  },
  parserOptions: {
    parser: "@babel/eslint-parser",
    requireConfigFile: false,
  },
  extends: ["@nuxtjs", "plugin:nuxt/recommended", "prettier"],
  plugins: [],
  // add your custom rules here
  rules: {
    "vue/multi-word-component-names": "off",
  },
};
```

## `default.vue` in `layouts` folder

```html
<template>
  <div>
    <NavBar />
    <Nuxt />
  </div>
</template>

<script>
  import NavBar from "../components/NavBar.vue";
  export default {
    components: {
      NavBar,
    },
  };
</script>
```

## `NavBar.vue`

```html
<template>
  <nav
    class="flex justify-center space-x-4 bg-black text-green-500 py-4 font-mono"
  >
    <nuxt-link to="/">Home</nuxt-link>
    <nuxt-link to="/NewPage">About</nuxt-link>
  </nav>
</template>
```
