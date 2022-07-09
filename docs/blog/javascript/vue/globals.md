---
tags:
  - vue js
  - javascript
  - globals
  - lottie
  - css
  - netlify
---

# Global code snippets

## Netlify
When visiting Vue JS apps, this code snippet will make sure that you can go to any page without having to go through the home page. 

```toml
# The following redirect is intended for use with most SPA's that handles routing internally.
[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

## CSS
Use this code if you want to use GSAP and not mess up the page overflow.  

```css
body,
html {
  display: block;
  width: 100%;
  margin: 0px;
  padding: 0px;
  overflow-x: hidden;
}
```

## Scripts
Some scripts I use to add icons and Lottie files.

```html
<!-- LOTTIE -->
<script src="https://unpkg.com/@lottiefiles/lottie-player@latest/dist/lottie-player.js"></script>
<!-- FONT AWESOME -->
<link 
    rel="stylesheet" 
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/css/all.min.css" 
    integrity="sha512-KfkfwYDsLkIlwQp6LFnl8zNdLGxu9YAA1QvwINks4PhcElQSvqcyVLLD9aMhXd13uQjoXtEKNosOWaZqXgel0g==" 
    crossorigin="anonymous" 
    referrerpolicy="no-referrer" />
```