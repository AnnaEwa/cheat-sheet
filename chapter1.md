# Express

## Express-generator

Install `express-generator` package

```bash
$ npm install -g express-generator
```

```bash
$ express <nameOfProject> --view=ejs --git
$ cd <nameOfProject>
$ npm install
```

### Setup nodemon

```bash
$ npm install --save-dev nodemon
```

**Package.json**

```json
{
    ...
    "scripts": {
        "start-dev": "nodemon ./bin/www",
        "start": "node ./bin/www"
    },
    ...
}
```

### ENV environment

```bash
$ npm install --save dotenv
```

Create a file call \`.env\`

**.env**

```txt
DOMAIN=http://localhost:3000
```

### ESLint Config

Execute `eslint --init` in your terminal folder or add `.eslintrc.json`

```bash
$ npm install --save-dev eslint eslint-config-airbnb-base eslint-plugin-import
```

**.eslintrc.json**

```js
{
  "env": {
    "node": true
  },
  "extends": "airbnb-base",
  "rules": {
    "max-len": "off",
    "radix": "off",
    "object-curly-newline": "off",
    "newline-per-chained-call": "off",
    "import/newline-after-import": "off",
    "no-unused-vars": "off"
  }
}
```

### Setting up Layouts Partials and helpers

[Link to express-ejs-layouts](https://github.com/Soarez/express-ejs-layouts)

Assuming that you use `EJS` as view engine

```bash
$ npm install --save express-ejs-layouts
```

**app.js**

```javascript
const expressLayouts = require('express-ejs-layouts');

...
app.set('view engine', 'ejs');

app.set("layout extractScripts", true) // see Documentation
app.set("layout extractStyles", true) // see Documentation
app.set("layout extractMetas", true) // see Documentation
app.set('layout', 'layouts/main'); // custom layout

app.use(expressLayouts); 
...
```

create the layout view `main.ejs` in `views/layouts/` folder

create the following structure

```
views
├── ...
├── partials
│   ├── navbar.ejs
│   └── footer.ejs
└── layouts
    ├── main.ejs
    └── secondLayout.ejs
```



