Next, lets explore the `Create` `CRUD` function:

And the `HTTP` verb that fits our needs is the `POST` verb

```js
app.post('/tasks', (req, res) => {});
```

We will send the new task's data through the `body` of the request. What will our data look like?

Let's add it in `Postman`
Step 1: Open `Postman`, and create new `POST` request at the top.
Step 2: Copy and paste this url in `Postman` http://localhost:8000/tasks.
Step 3: Under the `URL` field, click on `Body` and choose `raw`.
Step 4: In `Body`, `raw`, choose data type: `json` and copy and paste this data:

```json
{
  "task": "Create a new task through Postman",
  "done": true
}
```

But how do we receive the new task's data? Let's `console.log` the request `req`:

```js
app.post('/tasks', (req, res) => {
  console.log(req);
});
```

Note that we can't find the data. For `Express` to handle the `body` of a `url`, we will use a `middleware`, we will learn more about `middleware`s later

In `app.js` we will call `app.use` which is a `middleware`, and inside it we will call `express.json()` method which will parse the `body` as `JSON` data and before your routes so that it will be applied to all routes.

```js
const app = express();

app.use(express.json());

[...]
```

Let's send a request to the route again. As you can see the new task data is saved inside `req.body`.

What's missing from the client side is the `ID` of the new task which should be generated from the backend.

## 👾 Challenge!

generate an `ID`, get the `ID` of the last task element in `tasks` and add 1 to it.

## 📖 Solution:

```js
app.post('/tasks', (req, res) => {
  const id = tasks[tasks.length - 1].id + 1;
});
```

Then we will create an object that has the generated ID and the data sent from the client.

```js
app.post('/tasks', (req, res) => {
  const id = tasks[tasks.length - 1].id + 1;
  const newTask = { id, ...req.body };
});
```

Now we will add `newTask` to our array using `.push` and we will send the `newTask` as a response.

```js
app.post('/tasks', (req, res) => {
  const id = tasks[tasks.length - 1].id + 1;
  const newTask = { id, ...req.body };
  newTask.push(newTask);
  res.json(newTask);
});
```

Test your new endpoint in `Postman` and to make sure all is working, send a request to the `tasks` list endpoint on `Postman` to check if the new task was added.

Result:

![]()

Note that the default success response status is `200`, we will change it to `201` which means that the item is created successfully.

```js
res.status(201).json(newTask);
```
