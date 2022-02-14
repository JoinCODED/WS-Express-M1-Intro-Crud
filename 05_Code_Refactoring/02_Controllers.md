What we did until now, is that our `app.js` is clean, but our routes file is messy, and we can clean it using `controllers`

In your `tasks.controllers.js` import the the tasks data file:

```js
let tasks = require('../../tasks');
```

Let's start with the task create route. Copy the `callback` function from your create route and assign it to a function called `taskCreate` as shown below. And to make things easier, export it directly

```js
exports.taskCreate = (req, res) => {
  const id = tasks[tasks.length - 1].id + 1;
  const newTask = { id, ...req.body };
  tasks.push(newTask);
  res.status(201).json(newTask);
};
```

Now to use this controller in `tasks.routers.js`, require the method from `tasks.controllers.js` and pass to the route.

```js
const { taskCreate } = require('./tasks.controllers');

// Task Create
router.post('/', taskCreate);
```

Do the same for the other routes, our code now is clean ✨
