# PassportJS

* config \(see snippet\)

* * serialize
  * deserialize
  * use\(new Strategy\)
  * app.use\(...\);
  * app.use\(...\);
* req.login\(newUser\)
* req.logout\(\)
* if \(!req.user\) { ... }
* if \(!req.isAuthenticated\(\)\) { ... }

## Setting up passportJS

⚠️ **You need to setup sessions before using passport !!!!!!!**

```javascript
$ npm install --save passport passport-local bcrypt
```

Create `helpers` folder and the file `passport.js` in it.

## Local Strategy

**passport.js**

```javascript
const bcrypt = require('bcrypt');
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;

// Import the model that we will use for login
const User = require('../models/user');

function configurePassport() {
  // What we save in session
  passport.serializeUser((user, cb) => {
    cb(null, user._id);
  });

  // Get what we got from session
  passport.deserializeUser((id, cb) => {
    User.findOne({ '_id': id }, (err, user) => {
      if (err) { return cb(err); }
      cb(null, user);
    });
  });

  // Strategy that we follow locally
  passport.use(new LocalStrategy((username, password, next) => {
    User.findOne({ username }, (err, user) => {
      if (err) {
        return next(err);
      }
      if (!user) {
        return next(null, false, { message: 'Incorrect username' });
      }
      if (!bcrypt.compareSync(password, user.password)) {
        return next(null, false, { message: 'Incorrect password' });
      }

      return next(null, user);
    });
  }));
}

module.exports = configurePassport;
```

⚠️ Information from form in variables `username` and `password`

**app.js**

```javascript
...
const passport = require('passport');
const configurePassport = require('./helpers/passport');

...
configurePassport();
app.use(flash());
app.use(passport.initialize());
app.use(passport.session());

...
```

## handlers functions

`req.login(newUser, function(error){ ...`}`)` -&gt; Used to establish a login session.

`req.user` -&gt; If authentication succeeds, the next handler will be invoked and the `req.user` property will be set to the authenticated user.

`req.logout()` -&gt; Can be called from any route handler which needs to terminate a login session. will remove the `req.user` property and clear the login session \(if any\).

`req.isAuthenticated()` -&gt; Return if an user is authenticated or not.

## Protecting routes \(manual version\)

Setting up middleware using passport concept of middleware

Inside `helpers` create file `middlewares.js` .

**middleware.js**

```javascript
exports.isLoggedIn = redirect => (req, res, next) => {
  if (req.isAuthenticated()) {
    next();
  } else {
    res.redirect(redirect);
  }
};
```

use

```javascript
const isLoggedIn = require('path/middlewares').isLoggedIn

app.use( isLoggedIn('/login') ); // Example
```



