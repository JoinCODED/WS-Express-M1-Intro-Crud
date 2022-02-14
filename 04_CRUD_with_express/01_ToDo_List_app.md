In the upcoming sections, we will create our first `express` app. Which will be an api to serve a list of ToDos ✅ with the basic `CRUD` functionalities, what is `CRUD` 👂? let's find out!

**CRUD** stands for:

- **C**reate: creating new objects.
  _Example: adding a new task to our list of toDos._

- **R**etrieve: fetching existing data.
  _Example: retrieving the list of all toDos or one task from the list._

- **U**pdate: update existing objects.
  _Example: changing the name or state or even both of an existing task._

- **D**elete: delete an existing object.
  _Example: deleting a task from our list of toDos._

![crud](https://miro.medium.com/max/1400/1*2eBdh0vLZjUyCDF6x1EqvQ.png)

In your `express` app, create a new file called `tasks.js`.

```javascript
const tasks = [
  {
    id: 1,
    task: 'Create you first express app',
    done: false,
  },
  {
    id: 2,
    task: 'Finish React phase',
    done: true,
  },
  {
    id: 3,
    task: 'Become a javascript guru',
    done: true,
  },
];
```

Now export the tasks array:

```js
module.exports = tasks;
```

In your `app.js` import `tasks.js`:

```js
const tasks = require('./tasks');
```
