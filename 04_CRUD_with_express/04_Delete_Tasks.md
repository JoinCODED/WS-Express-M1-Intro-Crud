We will delete a task by its `ID`, which will be sent in the `URL`

We will use the `delete` verb. The client must specify which task they want to delete by sending the task `ID` in the `URL`

So the url will be something like this:

http://localhost:8000/tasks/1

Let's implement that with code:

```js
app.delete('/tasks/1', (req, res) => {
  tasks = tasks.filter((task) => task.id !== 1);
  console.log('tasks', tasks);
});
```

Try it out in `Postman`, and to make sure it works send a request to the `tasks` list endpoint, the task is gone, but wait.. if you have like a 100 task, will we create a separate route for each task? 😱

## Route Parameter 🦸

`Route parameters` are named `URL` segments. We use them to capture the values specified at their position in the `URL`. To create a route parameter in a `URL`, we add a `colon` followed with the `name` of your parameter.

Let's start using route params to solve our problem

```javascript
app.delete('/tasks/:taskId', (req, res) => {
  tasks = tasks.filter((task) => task.id !== 1);
  console.log('tasks', tasks);
});
```

So we are capturing what ever value coming in the place of `taskId` in the `URL`
if the user requested http://localhost:8000/tasks/3 , the `taskId` param will be equal to `3`

but how to access this value inside of our code? we will use `req.params` as follows:

```js
app.delete('/tasks/:taskId', (req, res) => {
  const { taskId } = req.params;
  tasks = tasks.filter((task) => task.id !== taskId);
  console.log('tasks', tasks);
});
```

Try now to delete the task with the `id` of 2, hmm.. it's not working, thats because the `taskId` type is `String` and `task.id` is of type `Int`.

## 👾 Challenge!

Fix it so both `taskId` and `task.id` are of the same type!

## 📖 Solution:

```js
app.delete('/tasks/:taskId', (req, res) => {
  const { taskId } = req.params;
  tasks = tasks.filter((task) => task.id !== +taskId);
  console.log('tasks', tasks);
});
```

Lastly we need to send a response, and the response code for deleting elements is `204`.

```js
app.delete('/tasks/:taskId', (req, res) => {
  const { taskId } = req.params;
  tasks = tasks.filter((task) => task.id !== +taskId);
  console.log('tasks', tasks);
  res.status(204);
});
```

⚠️ Beware: we always have to end our response, previously we didn't because `res.json` method automatically ends the response for us, but since we are not sending anything, we need to tell express to end this response and not to wait for something to send.

```js
res.status(204).end();
```

But what if we requested to delete a task with an id of 16, it does'nt exist. We should return an error to the user.

```js
app.delete('/tasks/:taskId', (req, res) => {
  const { taskId } = req.params;
  const foundTask = tasks.find((task) => task.id === +taskId);
  if (foundTask) {
    tasks = tasks.filter((task) => task.id !== +taskId);
    console.log('tasks', tasks);
    res.status(204);
  } else {
    res.status(404).json({ message: 'Task not found' });
  }
});
```

If the `task` is found within our `tasks` list, we will `delete` it, and if it does'nt we will send a message for the user "Task not found" with a `404` status code which means a specific resource was not found.
