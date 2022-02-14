![routing diagram](https://i.imgur.com/pN3x62G.png)

In the simplest terms, a `route` represents an endpoint which people can access. A route is associated with an `HTTP` verb (e.g. `GET`, `POST`, and so on), and it takes a URL path. It also takes a function which is called when the endpoint is accessed.

A `route`'s syntax looks like this:

```javascript
app.someMethod(routePath, someHandler);
```

- `app` is the instance of our express application.
- `someMethod` represents the HTTP method of the route, such as `get`, `post`, etc.
- `routePath` is the path on the server. It defines the endpoints at which requests can be made.
- `someHandler` is a callback function that will be executed when the client sends a request to this route.

To read more about this topic, [click here](https://expressjs.com/en/starter/basic-routing.html).
