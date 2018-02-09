# Mongoose

mongoimport --db databaseName --collection collectionName --file fileName

# mongoose

* npm install --save mongoose
* object document mapper
* bring schemas into our use of mongodb
* see example schemas in
  `./snippets`
* types: String, Number, Date, Boolean, Array, Mixed, Objectid

## Setting up mongoose

```bash
$ npm install --save mongoose
```

Connect with mongoose and using promises.

**app.js**

```javascript
...
const mongoose = require('mongoose');

...

mongoose.Promise = Promise;
mongoose.connect('< URL >', {
  keepAlive: true,
  reconnectTries: Number.MAX_VALUE
}, (error) => {
  if (!error) { 
    console.log(`connected to ${<URL>}`);
  }
  console.error(`💣 ${err.name}: ${err.message}`);
  process.exit(-1);
});

...
```

⚠️ Don't forget to setup `<URL>` with `'mongodb://localhost:port/database-name'` or with `process.env.MONGODB_URI` .



