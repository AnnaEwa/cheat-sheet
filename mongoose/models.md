# Models

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

Example:

```javascript
...

const classSchema = new Schema({
  ...
  students: [{
    type: Schema.Types.ObjectId,
    ref: 'User'
  }]
});

...
```

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



