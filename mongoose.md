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

### Models

All models should go inside `models` folder.

See documentation for schemas types

**model.js**

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const blogSchema = new Schema({
  name: String
}, {
  timestamps: {
    createdAt: "created_at",
    updatedAt: "updated_at"
  }
});

const Blog = mongoose.model('Blog', blogSchema);

module.exports = Blog;
```

### Schema for locations

```javascript
...

const restaurantSchema = new Schema({
  ...
  location: {
    type: {
      type: String
    },
    coordinates: [Number]
  }
  ...
});

restaurantSchema.index({ location: '2dsphere' });

...
```

#### 1 to 1 Relationship

Example: Users has one home

```javascript
...

const homeSchema = new Schema({
  ...
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

**review.js**

```js
const mongoose = require('mongoose');
const Schema   = mongoose.Schema;

const reviewSchema = new Schema({
    ...
});

const Review = mongoose.model('Review', reviewSchema);

module.exports = Review;
```

**product.js**

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



