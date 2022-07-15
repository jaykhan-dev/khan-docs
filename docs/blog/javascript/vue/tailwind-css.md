---
tags:
  - tailwind css
  - post css
  - vue js
  - css
  - html
  - setup
  - install
---

# Tailwind CSS

[Official Website](https://tailwindcss.com/)

## Setup

### Install commands

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

### Configure

```js
module.exports = {
  content: [
    "./index.html",
    "./src/**/*.{vue,js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

### `index.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### `main.js`

```js
import { createApp } from 'vue'
import App from './App.vue'
import './index.css'

createApp(App).mount('#app')
```

### run application

```bash
npm run dev
```