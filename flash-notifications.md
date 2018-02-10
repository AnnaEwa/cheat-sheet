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



