# Responsive Nav

The following code snippets is a reference code for creating a top nav bar that works for desktop and mobile. 

There is no styling, only the `HTML` and the `JavaScript`.

```html
<template>
  <div
    class="bg-slate-900/80 fixed top w-full shadow z-50 backdrop-blur-md p-2"
  >
    <nav
      class="container py-2 mx-auto md:flex md:justify-between md:items-center"
    >
      <div class="flex items-center justify-between">
        <router-link to="/" class="hover:text-green-600">
          <img src="../assets/endeavr-logo.svg" alt="" width="50" />
        </router-link>

        <!-- MOBILE MENU BUTTON -->
        <div @click="toggleNav" class="flex md:hidden">
          <button
            type="button"
            class="text-gray-500 hover:text-orange-400 focus:outline-none focus:text-gray-900"
          >
            <svg viewBox="0 0 24 24" class="w-6 h-6 fill-current">
              <path
                fill-rule="evenodd"
                d="M4 5h16a1 1 0 0 1 0 2H4a1 1 0 1 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2z"
              ></path>
            </svg>
          </button>
        </div>
      </div>

      <!-- MOBILE OPEN -->
      <div
        :class="showMenu ? 'flex' : 'hidden'"
        class="flex-col mt-8 space-y-4 md:flex md:space-y-0 md:flex-row md:items-center md:space-x-10 md:mt-0 text-white text-sm"
        @click="showMenu == !showMenu"
      >
        <router-link to="/about" class="hover:text-blue-500">About</router-link>
        <router-link to="/music" class="hover:text-blue-500">Music</router-link>
        <router-link to="/blog" class="hover:text-blue-500">Blog</router-link>
        <!-- 
        <router-link to="/wallet" class="hover:text-blue-500"
          >Invest</router-link
        >
        -->
        <router-link to="/wallet" class="hover:text-blue-500">Vote</router-link>
        <router-link to="/collab" class="hover:text-blue-500"
          >Collaborate</router-link
        >
        <a
          href="https://endeavr-docs.netlify.app"
          target="_blank"
          rel="noopener noreferrer"
          class="hover:text-blue-500"
          >Docs</a
        >
      </div>
    </nav>
  </div>

  <router-view />
</template>
```

```html
<script>
import { ref } from "vue";

export default {
  setup() {
    let showMenu = ref(false);
    const toggleNav = () => (showMenu.value = !showMenu.value);
    return { showMenu, toggleNav };
  },
};
</script>
```