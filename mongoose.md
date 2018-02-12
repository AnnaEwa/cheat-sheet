# Mongoose

mongoimport --db databaseName --collection collectionName --file fileName

[Link Mongoose](http://mongoosejs.com)

## Setting up connection

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




