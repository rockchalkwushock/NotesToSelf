# NotesToSelf

# Purpose

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

#### PROTECTING YOUR ENVIRONMENT
```bash
yarn add dotenv
touch .env
mkdir config
cd config
touch envConfig.js
```
_.env_
```plaintext
API_KEY='YOUR API_KEY HERE'
API_SECRET='YOUR API_SECRET HERE'
```
_envConfig.js_
```javascript
import dotenv from 'dotenv';

// Configure Envvars.
dotenv.config();

// Bring in Envvars from .env.
const envVariables = [
  'API_KEY',
  'API_SECRET'
];

// Check that Envvars are set.
envVariables.forEach((env) => {
  if (!process.env[env]) {
    throw new Error(`Env variable ${env} not set.`);
  }
});
```
_file.js_
```javascript
import '/config/envConfig';

const key = process.env.API_KEY;
const secret = process.env.API_SECRET;

const somefunction = () => {
  const url = `http://someapi.com/${key, secret}`; // this is a very poor example, but you get the idea.
}
```
