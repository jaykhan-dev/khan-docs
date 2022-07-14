---
tags:
  - javascript
  - web framework
  - node js
  - express js
  - server
---

# Express JS

[Official website](http://expressjs.com/)

>Fast, unopinionated, minimalist web framework for Node.js

Below is the very simple setup for an Express app.  It is used mainly for the backend.  My interest is in authentication which will be covered in a different blog.

```bash
mkdir express-test
cd express-test
npm init -y
npm i express
touch server.js
```

`server.js` file

```js
const express = require("express");
const app = express();

app.get("/", (request, response) => {
    response.send("Hi there");
});

app.get("/about", (request, response) => {
    response.send("<h1>About</h1>");
});

app.listen(4000, () => {
    console.log("Listen on the port 4000...");
});
```

To run this file type `node server.js` into the terminal

