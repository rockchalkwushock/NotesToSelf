# NotesToSelf

# Purpose

A place to put those little nuggets of knowledge I have learned after being a complete dumbass and spending hours researching errors. This will grow...I just hope not exponentially!

## READ THE DOCS DUMMY!!!!

1) When using NYC for testing coverage the `babel-plugin-istanbul` package is only utilized with in a specific environment set in the `.babelrc`...don't be stupid and make sure that is the environment you are setting for testing or visa versa! Real smooth Clark!

**FYI THIS MUST BE === _TEST_**

**.bablerc example**
```
{
  "presets": [
    "es2015",
    "stage-0"
  ],
  "env": { <--- ENVIRONMENT
    "test": { <--- WHAT YOUR npm test SCRIPT SHOULD BE RUNNING IN! IT'S MAGIC!
      "plugins": [ "istanbul" ]
    }
  }
}
```
**npm test script example**

`"test": "cross-env NODE_ENV=test nyc --reporter=text --reporter=lcov _mocha",`

2) When using env vars and running CI...set the damn env vars in the CI!
