Our code has become long and harder to read and maintain 🤮

We need to clean it and have a proper files/folder structure to make it easier to add new routes and new functionalities in the future.

Start by creating a folder in your main directory, name it `api`.

Inside it, create a folder named `tasks`.

api
├── tasks

And inside the `tasks` folder create two files named: `tasks.controllers.js` and `tasks.routers.js`

api
├── tasks
├── tasks.controllers.js
└── tasks.routers.js

Open `tasks.routers.js` and let's create what is called `mini express applications` 👶

we will use a method from express called `Router()`, which is a complete router system that will handle all routing related to tasks for our express app. So, in `tasks.routers.js` we will require `express` and define our mini-app router.

```js
const express = require('express');
const router = express.Router();
```

Go back to `app.js` and cut ALL the routes and paste them in `api/tasks.routers.js`. Change all `app`'s to `router`'s. So, this `router` will be handling all the routes for now.

```js
// Task Create
router.post("/tasks", (req, res) => {...});

// Task List
router.get("/tasks", (req, res) => {...});

// Task Update
router.put("/tasks/:taskId", (req, res) => {...});

// Task Delete
router.delete("/tasks/:taskId", (req, res) => {...});
```

Require the tasks data file inside this file.

```js
let tasks = require('../../tasks');
```

Next, export your router at the bottom of the file.

```js
module.exports = router;
```

Require your router instance in `app.js`.

```js
const tasksRoutes = require('./api/tasks/tasks.routers.js');
```

Finally, under the middleware section of our `app.js`, we will call our `tasksRoutes` using the `app.use()` method.

```js
app.use(tasksRoutes);
```

Thats a lot of work, what have we done until now?

So what's happening now is that when a request is received, `express` will look inside `tasksRoutes` to look for the route with the path similar to the request's.

Test your routes, make sure all your routes are still working

Can this be even more cleaned up? Yes! Since all the routes in `tasksRoutes` start with the path `/tasks` we can modify our router call.

```js
app.use('/tasks', tasksRoutes);
```

And in our `tasks.routers.js` we can remove `/tasks`

```js
// Task Create
router.post("/", (req, res) => {...});

// Task List
router.get("/", (req, res) => {...});

// Task Update
router.put("/:taskId", (req, res) => {...});

// Task Delete
router.delete("/:taskId", (req, res) => {...});
```
