Our first `CRUD` function we will use is `Read`

Which `HTTP` verbs you think fits our needs here?

- GET
- POST
- DELETE
- PUT

Answer:

- GET ✅
- POST ⭕
- DELETE ⭕
- PUT ⭕

`GET` is used to request data from a specified resource.

Next let's create a route that will serve the list of task to whom request them:

```js
app.get('/tasks', (req, res) => {});
```

So as we agreed we will send the list of `tasks` when someone requests this route, pass the `tasks` list that we imported in the `res.json` method:

```js
app.get('/tasks', (req, res) => {
  res.json(tasks);
});
```

Test your endpoint on your web browser: http://localhost:8000/tasks

Result:

![1](https://user-images.githubusercontent.com/84308096/153881375-65eacb39-1978-4f91-971a-37b50e265d0f.png)
