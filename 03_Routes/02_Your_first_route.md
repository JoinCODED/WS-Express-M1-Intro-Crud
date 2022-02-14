Let's start by writing the following code in your `app.js`

```js
app.get('/', (req, res) => {
  res.send({ message: 'Hello World!' });
});
```

Let’s dissect the above code:
It’s associated with an `HTTP` verb — in this case, it’s the `GET` verb.
It takes a `URL` path — in this case, it’s the homepage (/).
It takes a function which will be called when you access the endpoint.

Therefore, when a person makes a `GET` request to your homepage, `localhost:8000`, the arrow function is called and will display "Hello World!"

Now run the server, and in your browser, go to http://localhost:8000, and you should see the following message:

```json
{
  "message": "Hello World!"
}
```
