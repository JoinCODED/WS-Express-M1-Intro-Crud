And the last `CRUD` function, `update` and we will use the `put` `HTTP` verb with it.

Create a route for updating a task

```js
app.put('/tasks/:taskId', (req, res) => {});
```

Now for updating a task, it can be done with many ways, maybe the user wants to update only one specific field, many fields, or all fields.

Start with finding the task and making sure it exists:

```js
app.put('/tasks/:taskId', (req, res) => {
  const { taskId } = req.params;
  const foundTask = tasks.find((task) => task.id === +taskId);
});
```

If the task does'nt exist, send an error message and a `404` status code like we did with the delete tasks

```js
app.put('/tasks/:taskId', (req, res) => {
  const { taskId } = req.params;
  const foundTask = tasks.find((task) => task.id === +taskId);
  if (foundTask) {
  } else {
    res.status(404).json({ message: 'Task not found' });
  }
});
```

We have 2 things coming from our request, the first one is the `taskId` that needs to be updated, and also we have the new data in the `req.body`

We can extract the values of the `foundTask` and replace it with the data coming in the request body:

```js
app.put('/tasks/:taskId', (req, res) => {
  const { taskId } = req.params;
  const foundTask = tasks.find((task) => task.id === +taskId);
  if (foundTask) {
    foundTask.task = req.body.task;
    foundTask.done = req.body.done;
  } else {
    res.status(404).json({ message: 'Task not found' });
  }
});
```

But what if we have too many fields, a more clever way is to iterate over the `foundTask` object and replace everything at once

```js
app.put('/tasks/:taskId', (req, res) => {
  const { taskId } = req.params;
  const foundTask = tasks.find((task) => task.id === +taskId);
  if (foundTask) {
    for (const key in req.body) foundTask[key] = req.body[key];
  } else {
    res.status(404).json({ message: 'Task not found' });
  }
});
```

Finally send a response with a status code of `204` which indicates that a resource was updated successfully 👏

```js
if (foundTask) {
  for (const key in req.body) foundTask[key] = req.body[key];
  res.status(204).end();
}
```
