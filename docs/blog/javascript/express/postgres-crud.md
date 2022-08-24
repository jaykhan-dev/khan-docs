---
tags:
  - node
  - express
  - server
  - javascript
  - vue
  - full-stack
  - postgres
  - sql
---

# PostgreSQL

## Create a table

```sql
CREATE TABLE tasks(
  id SERIAL PRIMARY KEY,
  task VARCHAR(255) NOT NULL,
  description TEXT,
  completed BOOLEAN
)
```

## Add data

```sql
INSERT INTO tasks VALUES
(DEFAULT, 'create express backend', 'Using node, express and postgres for the backend', FALSE);
```

## Express JS

### Install express

```bash
mkdir express-backend
cd express-backend
npm init -y
npm i express pg cors
```

### `index.js`

```js
const express = require('express');
const cors = require('cors');
const bodyParser = require('body-parser');
const db = require('./queries');
const app = express();

const port = 4000

app.use(bodyParser.json());
app.use(
  bodyParser.urlencoded({
    extended: true
  });
);

//OPEN TO ALL REQUESTS
app.use(cors());

app.get('/', (request, response) => {
  response.json({info: 'NodeJS, Express, and PostgreSQL'})
});

//ENDPOINTS FOR queries
app.get('/tasks', db.getTasks)
app.get('/taks/:id', db.getTasksByID)
app.post('/tasks', db.createTask)
app.put('/tasks/:id', db.updateTask)
app.delete('/tasks/:id', db.deleteTask)

app.listen(port, () => {
  console.log(`App is listening on port ${port}`)
});

```

### `queries.js`

```js
const Pool = require("pg").Pool;
const pool = new Pool({
  user: "****",
  host: "localhost",
  database: "***",
  password: "*******",
  port: 5432,
});

// GET ALL TASKS
const getTasks = (request, response) => {
  pool.query("SELECT * FROM tasks", (error, results) => {
    if (error) {
      throw error;
    }
    response.status(200).json(results.rows);
  });
};
```
