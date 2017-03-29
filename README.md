# NotesToSelf

## Purpose

A place to put those little nuggets of knowledge I have learned after being a complete dumbass and spending hours researching errors. This will grow...I just hope not exponentially!

## Table of Contents
- [IMPORTANT](#important)
- [NYC](#nyc)
- [CI](#ci)
- [Syntax](#syntax)
- [Dotenv](#dotenv)
- [Promises](#promises)
- [Mobile](#mobile)
- [Deploying](#deploying)
- [Fetch](#fetch)
- [CLI](#cli)
- [GIT](#git)
- [Lifecyles](#lifecyles)
- [Now](#now)
- [reduce](#reduce)
- [Semantic-Release](#semantic-release)
- [Create-React-App](#create-react-app)
- [Tail-Call](https://codetuts.tech/flatten-deep-nested-array-object/)
- [Jest](#jest)
- [GH-Issues](#gh-issues)

## IMPORTANT

**READ THE DOCS DUMMY!!!!** 

This will save you hours of headaches and guess what it's in English so you have no excuse!

### NYC
When using NYC for testing coverage the `babel-plugin-istanbul` package is only utilized with in a specific environment set in the `.babelrc`...don't be stupid and make sure that the environment you are setting for testing is **test**! Real smooth Clark!

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

### CI
When using env vars and running CI...set the damn env vars in the CI whether it be through CLI or GUI!

### Syntax
One of these things is not like the other...

```javascript
app.get('/api', [routes]);

app.use('/api', [routes]); // Real smooth Clark, real smooth!
```

### Dotenv
Setting up dotenv for env vars.

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

### Promises

## A Real Nugget of Knowledge brought to you by [@EQuimper](https://github.com/EQuimper)

`axios` is a _promise based HTTP client_ this being said what does it return on any _CRUD_ operation???

A promise!

```javascript
axios.post('/library', { result }); // returns a promise.
axios.get('/library'); // also returns a promise! Who'd have thought?
```

So when using something like `redux-pack` that is expecting a _promise_ **YAHTZEE**!!!

Also since `redux-promise-middleware` will handle the creation of a _new promise_ this is a win/win when it comes to using promises with `redux`.

### Mobile
Scrolling on mobile devices

Thanks to MR. Wesbos!

```css
 -webkit-overflow-scrolling: touch;
```

### Deploying
Deploying `create-react-app` projects to GH-Pages.

Don't be a dumbass! This is still webpack and bundles via the same exact principles.

For more info on my idiocy look at this [issue](https://github.com/facebookincubator/create-react-app/issues/1479).

### Fetch
Working with the native `fetch()`

`fetch()` will always return as a promise (just like `axios`) and this promise contains a _blob_ of information. Their will be no discernable data because _fetch_ does not know what I want the data to be. By looking under the _prototype_ you can find several methods to apply to the _blob_. Should I want to view the data from the `fetch()` as a json I simply can do the following:

```javascript
fetch(endpoint)
  .then(blob => blob.json())
  .then(data => console.log(data))
  
// OR using async/await

const fetchData = async () => {
  try {
    const res = await fetch(endpoint);
    const data = res.json();
    return data; // can perform deconstruction here.
  } catch (e) {
    console.log(e);
  }
}
```

### CLI
One of these things is not like the other...yep again!

```bash
$ yarn clean
```
`clean` is a keyword to the Yarn CLI so this will generate a _.yarnclean_ this is muy no bueno if you didn't mean to do this!
For more refer to [yarn clean](https://yarnpkg.com/en/docs/cli/clean).
```bash
$ yarn run clean
```
_package.json_
```json
"clean": "rimraf dist npm-debug.log.*"
```
For the most part you never need to use _run_ when working with Yarn but this is just like NPM numbnuts if it's a keyword and you had a script that is the same namesake not calling the _run_ keyword will cause you many a headaches!!!

### GIT
Something that is your friend when you are stupid...which is often.

```bash
$ git reset --hard <commit>
```
When you make a royal screw up, I mean epic, and it does not deal with Yarn or NPM you can reset the _cwd_ to the last commit.
If you make an epic ninja screw up remember the following experience:
```bash
$ git pull <REMOTE> <branch>
```
Notice how **REMOTE** is all caps? That's because that is the **REMOTE** numbnuts; **NOT** the URL!!!! It's okay have a beer, cry yourself to sleep, and come back strong tomorrow.


### Lifecyles
Utilizing React Lifecyle Methods for what they are worth...use them dummy!
**Coming very soon!**

### Now
Deploying with the `now` CLI interface from Ziet.

Do **NOT** add `NODE_ENV=production` as an envvar unless all _required_ packages are set as dependencies. Just like in Heroku the _production_ flag does not read dev-dependencies.

### Reduce
Very simple yet powerful use case for testing reducers using `[].reduce()`. For more on `.reduce()` checkout this [article](https://medium.com/javascript-scene/reduce-composing-software-fe22f0c39a1d#.s64k6pkg7).
```javascript
const ADD_VALUE = 'ADD_VALUE';
const summingReducer = (state = 0, action = {}) => {
  const { type, payload } = action;
  switch (type) {
    case ADD_VALUE:
      return state + payload.value;
    default: return state;
  }
};

const actions = [
  { type: 'ADD_VALUE', payload: { value: 1 } },
  { type: 'ADD_VALUE', payload: { value: 1 } },
  { type: 'ADD_VALUE', payload: { value: 1 } }
];

actions.reduce(summingReducer, 0); // 3
```

### Semantic-Release
When switching from a _private_ to _public_ repository the gh-token & npm-token will not transfer. You must reinitialize these values using:
```bash
semantic-release-cli setup
```

### Create-React-App
Any project built prior to `react-scripts@0.9.5` must be updgraded to `v0.9.5` or must downgrade `node` globally to `node < 7.7.2`:
- [The Issue](https://github.com/facebookincubator/create-react-app/issues/1776)
- [The PR](https://github.com/facebookincubator/create-react-app/pull/1783)
- [Version Release](https://github.com/facebookincubator/create-react-app/releases/tag/v0.9.5)
```bash
yarn upgrade react-scripts@0.9.5
# OR
npm update --save-dev react-scripts@0.9.5
# Verify
npm view react-scripts version # 0.9.5
```

### Tail-Call
[Tail-Call Optimized Recursion Call](https://codetuts.tech/flatten-deep-nested-array-object/)
```javascript
// First declare a function that will be checking
// that what we pass to it is cabaple of being
// concated.
const scalar = v => !Array.isArray(v);

// Second declare a function that accepts the nested array.
const flatten = (deep, flat = []) => {  
  // condition check for ending recursion
  if (deep.length === 0) return flat;
  // head is the current index in the array.
  // tail is the rest of the values.
  let [head, ...tail] = deep;
  // is the value able to be concatenated?
  if (scalar(head)) {
    return flatten(tail, flat.concat(head));
  } else {
    return flatten(tail, flat.concat(flatten(head)));
  }
}
```

### Jest
Fun fact `jest` sets `NODE_ENV=test` automatically under the hood :+1:

### GH Issues
Closing Github Issues and the keywords that must be used:

https://help.github.com/articles/closing-issues-via-commit-messages/
