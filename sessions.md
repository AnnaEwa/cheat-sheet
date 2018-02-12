# Sessions

```bash
$ npm install --save express-session connect-mongo
```

**app.js**

```javascript
const session = require("express-session");
const MongoStore = require("connect-mongo")(session);

...

app.use(session({
  secret: 'some-string',
  resave: true,
  saveUninitialized: true,
  cookie: { maxAge: 24 * 60 * 60 * 1000 },
  store: new MongoStore({
    mongooseConnection: mongoose.connection,
    ttl: 24 * 60 * 60 // 1 day
  })
}));

...
```

