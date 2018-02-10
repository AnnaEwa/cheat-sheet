# Flash Notifications

[link connect-flash](https://github.com/jaredhanson/connect-flash)

```bash
$ npm install --save connect-flash
```

**connect-flash** use session in order to work.

**app.js**

```javascript
const flash = require('connect-flash');
...

// session configuration middleware 

app.use(flash());

// passport configuration middleware 

...
```

Examples in routes

```javascript
router.get('/flash', function(req, res){
  // Set a flash message by passing the key, followed by the value, to req.flash().
  req.flash('info', 'Flash is back!')
  res.redirect('/');
});

router.get('/', function(req, res){
  
  // Get an array of flash messages by passing the key to req.flash()
  res.render('index', { messages: req.flash('info') });
});
```



