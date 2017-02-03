# NotesToSelf

## Purpose

A place to put those little nuggets of knowledge I have learned after being a complete dumbass and spending hours researching errors. This will grow...I just hope not exponentially!

## READ THE DOCS DUMMY!!!!

1) When using NYC for testing coverage the `babel-plugin-istanbul` package is only utilized with in a specific environment set in the `.babelrc`...don't be stupid and make sure that is the environment you are setting for testing or visa versa! Real smooth Clark!

**FYI THIS MUST BE === _TEST_**

**.bablerc example**
```json
{
  "presets": [
    "es2015",
    "stage-0"
  ],
  "env": { 
    "test": {
      "plugins": [ "istanbul" ]
    }
  }
}
```
**npm test script example**
```json
"test": "cross-env NODE_ENV=test nyc --reporter=text --reporter=lcov _mocha",
```

2) When using env vars and running CI...set the damn env vars in the CI!

3) One of these things is not like the other...

```javascript
app.get('/api', [routes]);

app.use('/api', [routes]); // Real smooth Clark, real smooth!
```

4) Setting up dotenv for env vars.

#### PROTECTING YOUR ENVIRONMENT
```bash
yarn add dotenv
touch .env
```
_.env_
```plaintext
API_KEY='YOUR API_KEY HERE'
API_SECRET='YOUR API_SECRET HERE'
```
_entryPointToProject.js_
```javascript
import 'dotenv/config';

const key = process.env.API_KEY;
const secret = process.env.API_SECRET;

const somefunction = () => {
  const url = `http://someapi.com/${key, secret}`; // this is a very poor example, but you get the idea.
}
```

**NOTE**: When using `create-react-app` all developer created env vars must begin with the prefix `REACT_APP_`.

For more information: [Environment Variables in CRA](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-custom-environment-variables)

**NOTE**: `create-react-app` has `dotenv` built into the `build` & `start` scripts. No need to import into project.

For more information: [Dotenv in React-Scripts](https://github.com/facebookincubator/create-react-app/blob/v0.8.5/packages/react-scripts/scripts/build.js#L19)

_.env_example_
```paintext
NODE_ENV=development
REACT_APP_SECRET_CODE=123
```

5) Promises Promises Promises.

## A Real Nugget of Knowledge brought to you by @EQuimper

`axios` is a _promise based HTTP client_ this being said what does it return on any _CRUD_ operation class???

A promise!

```javascript
axios.post('/library', { result }); // returns a promise.
axios.get('/library'); // also returns a promise! Who'd have thought?
```

So when using something like `redux-pack` that is expecting a _promise_ YAHTZEE!!!

Also since `redux-promise-middleware` will handle the creation of a _new promise_ this is a win/win when it comes to using promises with `redux`.

6) Scrolling on mobile devices

Thanks to MR. Wesbos!

```css
 -webkit-overflow-scrolling: touch;
```

7) Deploying create-react-app projects to GH-Pages.

Don't be a dumbass! This is still webpack and bundles via the same exact principles.

For more info on my idiocy look at this [issue](https://github.com/facebookincubator/create-react-app/issues/1479).
