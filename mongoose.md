# Mongoose

mongoimport --db databaseName --collection collectionName --file fileName

# mongoose

* npm install --save mongoose
* object document mapper
* bring schemas into our use of mongodb
* see example schemas in
  `./snippets`
* types: String, Number, Date, Boolean, Array, Mixed, Objectid

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

### Models

All models should go inside `models` folder.

**model.js**

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const blogSchema = new Schema({
  name:    String,
  binary:  Buffer,
  living:  Boolean,
  updated: { type: Date, default: Date.now },
  age:     { type: Number, min: 18, max: 65 },
  mixed:   Schema.Types.Mixed,
  _someId: Schema.Types.ObjectId,
  array:      [],
  ofString:   [String],
  ofNumber:   [Number],
  ofDates:    [Date],
  ofBuffer:   [Buffer],
  ofBoolean:  [Boolean],
  ofMixed:    [Schema.Types.Mixed],
  ofObjectId: [Schema.Types.ObjectId],
  ofArrays:   [[]],
  ofArrayOfNumbers: [[Number]],
  nested: {
    stuff: { type: String, lowercase: true, trim: true }
  }
}, {
  timestamps: {
    createdAt: "created_at",
    updatedAt: "updated_at"
  }
});

const Blog = mongoose.model('Blog', blogSchema);

module.exports = Blog;
```

### Relations between models

#### 1 to 1 Relationship

Example: Users has one home

```javascript
...
  const homeSchema = new Schema({
    name: String,
    owner: {
      type: Schema.Types.ObjectId,
      ref: 'User'
    }
  });
...
```

#### 1 to N Relationship

Example: Users has one home

#### Model with subschema or embedded documents

Example: Products has reviews

```js
...
const Review   = require('./review');

const productSchema = new Schema({
  name       : String,
  price      : Number,
  imageUrl   : String,
  description: String,
  reviews    : [Review.schema]
});

...
```





