You made a fully functional tasks api and you have all the endpoints.

Using `React` and `Axios`, create a frontend page that utilizes all functionalities we implemented in our api! 🖌️

You will also face a `CORS` error, so what is cors and how can we fix it? 🤔

`CORS` stands for `Cross-Origin Resource Sharing`. Doesn’t explain much, huh? Well, it’s really simple to understand.

`CORS` is a security mechanism built into (all) modern web-browsers. It basically blocks all the http requests from your front end to any API that is not in the same “Origin” (domain, protocol, and port—which is the case most of the time).

In order to fix this, start by installing `cors`:

```shell
npm i cors
```

Then in your `app.js` require it:

```js
const cors = require('cors');
```

Lastly, before all of your routes:

```js
app.use(cors());
```
