# _Libraries_

---

# _Functionality_

## _dotenv_

- https://docs.travis-ci.com/user/encryption-keys/
- A zero-dependency module that loads environment variables from a `.env` file into [`process.env`](https://nodejs.org/docs/latest/api/process.html#process_process_env)
- Use for API keys

* `npm install dotenv`
* Create a `.env` file at the root directory of your application and add the variables to it

```
// .env
SECRET_KEY=abcd1234
```

- Add `.env` to `.gitignore`
- Add the following line to your app

```
require('dotenv').config()
```

```
// access `SECRET_KEY`
process.env.SECRET_KEY
```

---

## _isomorphic-fetch_

- https://www.npmjs.com/package/isomorphic-fetch
- https://github.com/matthew-andrews/isomorphic-fetch
- `npm install --save isomorphic-fetch es6-promise`
- Adds a global `fetch` polyfill
  - since babel doesn't have one

---

## _Isomorphic Unfetch_

- Switches between [unfetch](https://github.com/developit/unfetch) & [node-fetch](https://github.com/bitinn/node-fetch) for client & server
- https://www.npmjs.com/package/isomorphic-unfetch
- https://github.com/developit/unfetch/tree/master/packages/isomorphic-unfetch
- `npm install --save isomorphic-unfetch`

---

# _CryptoCurrency_

## _CCXT_

- Might need to have Python 2 installed
- `npm install --global`--production`windows-build-tools`
- `npm` ` install ``--global ` ` --production ``windows-build-tools `--add-python-to-path='true' --debug ``
- `npm install ccxt`

---

# _Methods_

## _Lodash_

- https://lodash.com/
- A modern JavaScript utility library delivering modularity, performance & extras
- Makes JavaScript easier by taking the hassle out of working with arrays, numbers, objects, strings, etc
- Lodash’s modular methods are great for:
  - Iterating arrays, objects, & strings
  - Manipulating & testing values
  - Creating composite functions

### _Functions_

### debounce

- Creates a debounced function that delays invoking `func` until after `wait` milliseconds have elapsed since the last time the debounced function was invoked
- https://www.npmjs.com/package/lodash.debounce
- `npm i lodash.`debounce ``
- `import debounce from 'lodash.debounce';`
- ``debounce`(func, [wait=0], [options={}])`

### _Objects_

### pickBy

- Creates an object composed of the `object` properties `predicate` returns truthy for
- Basically `filter` for object properties
- https://www.npmjs.com/package/lodash.pickby
- `npm i`lodash.pickby``
- `import`pickBy `from '`lodash.pickby`';`
- ``pickBy```(object, [predicate=_.identity])`

---

## _Underscore_

- https://underscorejs.org/
- Provides a whole mess of useful functional programming helpers without extending any built-in objects
- `npm install underscore`

---

## _Immutable.js_

- http://facebook.github.io/immutable-js/
- https://github.com/facebook/immutable-js
- Immutable data cannot be changed once created, leading to much simpler application development, no defensive copying, and enabling advanced memoization and change detection techniques with simple logic
- Pairs well with React

---

## _Moment.js_

- Parse, validate, manipulate, and display dates and times in JavaScript
- https://momentjs.com/

---

# _Code quality_

## _ESLint_

- `npm install eslint --save-dev`

* To ignore a file, add to the top of the file
  - `/* eslint-disable */`
  - ` /*`` eslint-disable max-len ``*/ `
  - - or -
  - add a `.eslintignore` file to the project root
  - `/node_modules/* and /bower_components/*` in the project root are ignored by default

```
!/*.js
/tests/**/*.js
!/tests/**/jsfmt.spec.js
!/**/.eslintrc.js
/test.js
/dist/
**/node_modules/**
```

- To disable a line
  - `// eslint-disable-next-line max-len`

* To initialize:
  - `eslint --init`

### Scripts

- `"lint": "./node_modules/eslint/bin/eslint.js ./*.js"`
- `"lint": "./node_modules/eslint/bin/eslint.js ./src/"`
- `"lint": "./node_modules/eslint/bin/eslint.js ./src/ --ignore-pattern *.test.js"`
- `"lint": "./node_modules/eslint/bin/eslint.js`./src/`--ignore-pattern node_modules/"`
- `"lint": "./node_modules/eslint/bin/eslint.js ./client/src/ server.js"`
- `"lintWin": "eslint . --ignore-pattern node_modules/"`

### Configs

- If you are using `ESLint` globally, you have to install the plugin globally too
- Otherwise, install it locally

* Node
  - https://www.npmjs.com/package/eslint-plugin-node
  - `npm install --save-dev eslint-plugin-node`
  - `"`extends` "``````: ` ` [`````"```eslint:recommended```"`````,``` `"`plugin:node/recommended`"`]`,```

```
"env": {
    "node": true,
  },
```

- React
  - https://www.npmjs.com/package/eslint-plugin-react
  - https://github.com/turingschool-examples/javascript/blob/master/linters/module-3/.eslintrc
  - `npm install eslint-plugin-react --save-dev`
  - `"`extends` "``````: ` ``[`````"```eslint:recommended```"`````,``` ``"```plugin:react/recommended```"`````]```,```

```````
{
  ```"```extends```"``````:``` ````[`````"```eslint:recommended```"`````,``` ``"```plugin:react/recommended```"`````]````,
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "plugins": ["react"],
  "rules": {
    "react/jsx-uses-react": "error",
    "react/jsx-uses-vars": "error"
  }
}
```````

- Jest

```
`"env": {`
`  "jest": true`
`}`
```

- babel-eslint
  - https://www.npmjs.com/package/babel-eslint
  - Allows you to lint ALL valid Babel code
  - `npm install` ```babel-eslint --save-dev`
  - `npm install babel-eslint --save-dev`

```
`"parser": "babel-eslint"`
```

- ???

```
{
  "extends": ["react-app", "plugin:jsx-a11y/recommended"],
  "plugins": ["jsx-a11y"]
}
```

### Templates

```
{
  "env": {
    "browser": true,
    "commonjs": true,
    "es6": true,
    "mocha": true
  },
  "extends": "eslint:recommended",
  "parserOptions": {
    "sourceType": "module"
  },
  "rules": {
    "brace-style": "error",
    "comma-spacing": [
      "warn",
      {
        "before": false,
        "after": true
      }
    ],
    "curly": "error",
    "semi-spacing": [
      "error",
      {
        "before": false,
        "after": true
      }
    ],
    "indent": ["error", 2],
    "key-spacing": [
      "error",
      {
        "beforeColon": false,
        "afterColon": true
      }
    ],
    "keyword-spacing": [
      "error",
      {
        "before": true,
        "after": true
      }
    ],
    "linebreak-style": ["error", "unix"],
    "max-len": ["error", 80],
    "new-cap": [
      "error",
      {
        "newIsCap": true
      }
    ],
    "newline-after-var": ["error", "always"],
    "object-shorthand": ["error", "always"],
    "space-before-blocks": [
      "error",
      {
        "functions": "always",
        "keywords": "always",
        "classes": "always"
      }
    ],
    "space-infix-ops": [
      "error",
      {
        "int32Hint": false
      }
    ]
  }
}
```

```
{
  "parser": "babel-eslint",
  "env": {
    "browser": true,
    "node": true,
    "commonjs": true,
    "es6": true,
    "mocha": true,
    "jest": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:node/recommended",
    "plugin:react/recommended"
  ],
  "plugins": ["react"],
  "parserOptions": {
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "rules": {
    "react/jsx-uses-react": "error",
    "react/jsx-uses-vars": "error",
    "linebreak-style": 0
  }
}
```

```
{
  "env": {
    "browser": true,
    "node": true,
    "es6": true
  },

  "parser": "babel-eslint",

  "plugins": ["react"],

  "ecmaFeatures": {
    "arrowFunctions": true,
    "binaryLiterals": true,
    "blockBindings": true,
    "classes": true,
    "defaultParams": true,
    "destructuring": true,
    "forOf": true,
    "generators": true,
    "modules": true,
    "objectLiteralComputedProperties": true,
    "objectLiteralDuplicateProperties": true,
    "objectLiteralShorthandMethods": true,
    "objectLiteralShorthandProperties": true,
    "octalLiterals": true,
    "regexUFlag": true,
    "regexYFlag": true,
    "spread": true,
    "superInFunctions": true,
    "templateStrings": true,
    "unicodeCodePointEscapes": true,
    "globalReturn": true,
    "jsx": true
  },

  "rules": {
    //
    //Possible Errors
    //
    // The following rules point out areas where you might have made mistakes.
    //
    "comma-dangle": 2, // disallow or enforce trailing commas (recommended)
    "no-cond-assign": 2, // disallow assignment in conditional expressions (recommended)
    "no-console": 2, // disallow use of console (recommended)
    "no-constant-condition": 2, // disallow use of constant expressions in conditions (recommended)
    "no-control-regex": 2, // disallow control characters in regular expressions (recommended)
    "no-debugger": 2, // disallow use of debugger (recommended)
    "no-dupe-args": 2, // disallow duplicate arguments in functions (recommended)
    "no-dupe-keys": 2, // disallow duplicate keys when creating object literals (recommended)
    "no-duplicate-case": 2, // disallow a duplicate case label. (recommended)
    "no-empty": 2, // disallow empty block statements (recommended)
    "no-empty-character-class": 2, // disallow the use of empty character classes in regular expressions (recommended)
    "no-ex-assign": 2, // disallow assigning to the exception in a catch block (recommended)
    "no-extra-boolean-cast": 2, // disallow double-negation boolean casts in a boolean context (recommended)
    "no-extra-parens": 2, // disallow unnecessary parentheses
    "no-extra-semi": 2, // disallow unnecessary semicolons (recommended) (fixable)
    "no-func-assign": 2, // disallow overwriting functions written as function declarations (recommended)
    "no-inner-declarations": 2, // disallow function or variable declarations in nested blocks (recommended)
    "no-invalid-regexp": 2, // disallow invalid regular expression strings in the RegExp constructor (recommended)
    "no-irregular-whitespace": 2, // disallow irregular whitespace outside of strings and comments (recommended)
    "no-negated-in-lhs": 2, // disallow negation of the left operand of an in expression (recommended)
    "no-obj-calls": 2, // disallow the use of object properties of the global object (Math and JSON) as functions (recommended)
    "no-regex-spaces": 2, // disallow multiple spaces in a regular expression literal (recommended)
    "no-sparse-arrays": 2, // disallow sparse arrays (recommended)
    "no-unexpected-multiline": 2, // Avoid code that looks like two expressions but is actually one (recommended)
    "no-unreachable": 2, // disallow unreachable statements after a return, throw, continue, or break statement (recommended)
    "use-isnan": 2, // disallow comparisons with the value NaN (recommended)
    "valid-jsdoc": 2, // Ensure JSDoc comments are valid
    "valid-typeof": 2, // Ensure that the results of typeof are compared against a valid string (recommended)


    //
    // Best Practices
    //
    // These are rules designed to prevent you from making mistakes.
    // They either prescribe a better way of doing something or help you avoid footguns.
    //
    "accessor-pairs": 2, // Enforces getter/setter pairs in objects
    "array-callback-return": 2, // Enforces return statements in callbacks of array's methods
    "block-scoped-var": 2, // treat var statements as if they were block scoped
    "complexity": 0, // specify the maximum cyclomatic complexity allowed in a program
    "consistent-return": 2, // require return statements to either always or never specify values
    "curly": 2, // specify curly brace conventions for all control statements
    "default-case": 2, // require default case in switch statements
    "dot-location": [2, "property"], // enforces consistent newlines before or after dots
    "dot-notation": 2, // encourages use of dot notation whenever possible
    "eqeqeq": 2, // require the use of === and !==
    "guard-for-in": 2, // make sure for-in loops have an if statement
    "no-alert": 2, // disallow the use of alert, confirm, and prompt
    "no-caller": 2, // disallow use of arguments.caller or arguments.callee
    "no-case-declarations": 2, // disallow lexical declarations in case clauses (recommended)
    "no-div-regex": 2, // disallow division operators explicitly at beginning of regular expression
    "no-else-return": 2, // disallow else after a return in an if
    "no-empty-function": 2, // disallow use of empty functions
    "no-empty-pattern": 2, // disallow use of empty destructuring patterns (recommended)
    "no-eq-null": 2, // disallow comparisons to null without a type-checking operator
    "no-eval": 2, // disallow use of eval()
    "no-extend-native": 2, // disallow adding to native types
    "no-extra-bind": 2, // disallow unnecessary function binding
    "no-extra-label": 2, // disallow unnecessary labels
    "no-fallthrough": 2, // disallow fallthrough of case statements (recommended)
    "no-floating-decimal": 2, // disallow the use of leading or trailing decimal points in numeric literals
    "no-implicit-coercion": 2, // disallow the type conversions with shorter notations
    "no-implicit-globals": 2, // disallow var and named functions in global scope
    "no-implied-eval": 2, // disallow use of eval()-like methods
    "no-invalid-this": 2, // disallow this keywords outside of classes or class-like objects
    "no-iterator": 2, // disallow usage of __iterator__ property
    "no-labels": 2, // disallow use of labeled statements
    "no-lone-blocks": 2, // disallow unnecessary nested blocks
    "no-loop-func": 2, // disallow creation of functions within loops
    "no-magic-numbers": 0, // disallow the use of magic numbers
    "no-multi-spaces": 2, // disallow use of multiple spaces (fixable)
    "no-multi-str": 2, // disallow use of multiline strings
    "no-native-reassign": 2, // disallow reassignments of native objects
    "no-new": 2, // disallow use of the new operator when not part of an assignment or comparison
    "no-new-func": 2, // disallow use of new operator for Function object
    "no-new-wrappers": 2, // disallows creating new instances of String,Number, and Boolean
    "no-octal": 2, // disallow use of octal literals (recommended)
    "no-octal-escape": 2, // disallow use of octal escape sequences in string literals, such as var foo = "Copyright \251";
    "no-param-reassign": 2, // disallow reassignment of function parameters
    "no-process-env": 0, // disallow use of process.env
    "no-proto": 2, // disallow usage of __proto__ property
    "no-redeclare": 2, // disallow declaring the same variable more than once (recommended)
    "no-return-assign": 2, // disallow use of assignment in return statement
    "no-script-url": 2, // disallow use of javascript: urls.
    "no-self-assign": 2, // disallow assignments where both sides are exactly the same (recommended)
    "no-self-compare": 2, // disallow comparisons where both sides are exactly the same
    "no-sequences": 2, // disallow use of the comma operator
    "no-throw-literal": 2, // restrict what can be thrown as an exception
    "no-unmodified-loop-condition": 2, // disallow unmodified conditions of loops
    "no-unused-expressions": 2, // disallow usage of expressions in statement position
    "no-unused-labels": 2, // disallow unused labels (recommended)
    "no-useless-call": 2, // disallow unnecessary .call() and .apply()
    "no-useless-concat": 2, // disallow unnecessary concatenation of literals or template literals
    "no-void": 2, // disallow use of the void operator
    "no-warning-comments": 0, // disallow usage of configurable warning terms in comments - e.g. TODO or FIXME
    "no-with": 2, // disallow use of the with statement
    "radix": 2, // require use of the second argument for parseInt()
    "vars-on-top": 2, // require declaration of all vars at the top of their containing scope
    "wrap-iife": 2, // require immediate function invocation to be wrapped in parentheses
    "yoda": 2, // require or disallow Yoda conditions


    //
    // Strict Mode
    //
    // These rules relate to using strict mode.
    //
    "strict": 0, // controls location of Use Strict Directives. 0: required by babel-eslint


    //
    // Variables
    //
    // These rules have to do with variable declarations.
    //
    "init-declarations": 0, // enforce or disallow variable initializations at definition
    "no-catch-shadow": 2, // disallow the catch clause parameter name being the same as a variable in the outer scope
    "no-delete-var": 2, // disallow deletion of variables (recommended)
    "no-label-var": 2, // disallow labels that share a name with a variable
    "no-restricted-globals": 0, // restrict usage of specified global variables
    "no-shadow": 2, // disallow declaration of variables already declared in the outer scope
    "no-shadow-restricted-names": 2, // disallow shadowing of names such as arguments
    "no-undef": 2, // disallow use of undeclared variables unless mentioned in a /*global */ block (recommended)
    "no-undef-init": 2, // disallow use of undefined when initializing variables
    "no-undefined": 2, // disallow use of undefined variable
    "no-unused-vars": [2, {"argsIgnorePattern": "^_", "varsIgnorePattern": "^_"}], // disallow declaration of variables that are not used in the code (recommended)
    "no-use-before-define": 2, // disallow use of variables before they are defined

    //
    // Node.js and CommonJS
    //
    // These rules are specific to JavaScript running on Node.js or using CommonJS in the browser.
    //
    "callback-return": 2, // enforce return after a callback
    "global-require": 0, // enforce require() on top-level module scope
    "handle-callback-err": 2, // enforce error handling in callbacks
    "no-mixed-requires": 2, // disallow mixing regular variable and require declarations
    "no-new-require": 2, // disallow use of new operator with the require function
    "no-path-concat": 2, // disallow string concatenation with __dirname and __filename
    "no-process-exit": 0, // disallow process.exit()
    "no-restricted-imports": 0, // restrict usage of specified node imports
    "no-restricted-modules": 0, // restrict usage of specified node modules
    "no-sync": 2, // disallow use of synchronous methods
    //
    // Stylistic Issues
    //
    // These rules are purely matters of style and are quite subjective.
    //
    "array-bracket-spacing": [2, "never"], // enforce spacing inside array brackets (fixable)
    "block-spacing": [2, "always"], // disallow or enforce spaces inside of single line blocks (fixable)
    "brace-style": 2, // enforce one true brace style
    "camelcase": 2, // require camel case names
    "comma-spacing": [2, {"before": false, "after": true}], // enforce spacing before and after comma (fixable)
    "comma-style": [2, "last"], // enforce one true comma style
    "computed-property-spacing": [2, "never"], // require or disallow padding inside computed properties (fixable)
    "consistent-this": [2, "_this"], // enforce consistent naming when capturing the current execution context
    "eol-last": 2, // enforce newline at the end of file, with no multiple empty lines (fixable)
    "func-names": 0, // require function expressions to have a name
    "func-style": 0, // enforce use of function declarations or expressions
    "id-blacklist": 0, // blacklist certain identifiers to prevent them being used
    "id-length": 0, // this option enforces minimum and maximum identifier lengths (variable names, property names etc.)
    "id-match": 0, // require identifiers to match the provided regular expression
    "indent": [2, 2, {"SwitchCase": 1}], // specify tab or space width for your code (fixable)
    "jsx-quotes": [2, "prefer-double"], // specify whether double or single quotes should be used in JSX attributes (fixable)
    "key-spacing": [2, {"beforeColon": false, "afterColon": true}], // enforce spacing between keys and values in object literal properties
    "keyword-spacing": [2, {"before": true, "after": true}], // enforce spacing before and after keywords (fixable)
    "linebreak-style": [2, "unix"], // disallow mixed 'LF' and 'CRLF' as linebreaks
    "lines-around-comment": [2, {"beforeBlockComment": true, "afterBlockComment": false, "afterLineComment": false}], // enforce empty lines around comments
    "max-depth": [2, 3], // specify the maximum depth that blocks can be nested
    "max-len": [2, 100, 2], // specify the maximum length of a line in your program
    "max-nested-callbacks": [2, 3], // specify the maximum depth callbacks can be nested
    "max-params": [2, 5], // limits the number of parameters that can be used in the function declaration
    "max-statements": 0, // specify the maximum number of statement allowed in a function
    "new-cap": [2, {"newIsCap": true, "capIsNew": false}], // require a capital letter for constructors
    "new-parens": 2, // disallow the omission of parentheses when invoking a constructor with no arguments
    "newline-after-var": [2, "always"], // require or disallow an empty newline after variable declarations
    "newline-per-chained-call": 0, // enforce newline after each call when chaining the calls
    "no-array-constructor": 2, // disallow use of the Array constructor
    "no-bitwise": 2, // disallow use of bitwise operators
    "no-continue": 2, // disallow use of the continue statement
    "no-inline-comments": 2, // disallow comments inline after code
    "no-lonely-if": 2, // disallow if as the only statement in an else block
    "no-mixed-spaces-and-tabs": 2, // disallow mixed spaces and tabs for indentation (recommended)
    "no-multiple-empty-lines": [2, {"max": 2}], // disallow multiple empty lines
    "no-negated-condition": 2, // disallow negated conditions
    "no-nested-ternary": 2, // disallow nested ternary expressions
    "no-new-object": 2, // disallow the use of the Object constructor
    "no-plusplus": 2, // disallow use of unary operators, ++ and --
    "no-restricted-syntax": [2, "WithStatement"], // disallow use of certain syntax in code
    "no-spaced-func": 2, // disallow space between function identifier and application (fixable)
    "no-ternary": 0, // disallow the use of ternary operators
    "no-trailing-spaces": 2, // disallow trailing whitespace at the end of lines (fixable)
    "no-underscore-dangle": 2, // disallow dangling underscores in identifiers
    "no-unneeded-ternary": 2, // disallow the use of ternary operators when a simpler alternative exists
    "no-whitespace-before-property": 2, // disallow whitespace before properties
    "object-curly-spacing": [2, "never"], // require or disallow padding inside curly braces (fixable)
    "one-var": [2, "never"], // require or disallow one variable declaration per function
    "one-var-declaration-per-line": 2, // require or disallow an newline around variable declarations
    "operator-assignment": [2, "never"], // require assignment operator shorthand where possible or prohibit it entirely
    "operator-linebreak": [2, "after"], // enforce operators to be placed before or after line breaks
    "padded-blocks": [2, "never"], // enforce padding within blocks
    "quote-props": [2, "as-needed"], // require quotes around object literal property names
    "quotes": [2, "single"], // specify whether backticks, double or single quotes should be used (fixable)
    "require-jsdoc": 0, // Require JSDoc comment
    "semi": [2, "always"], // require or disallow use of semicolons instead of ASI (fixable)
    "semi-spacing": [2, {"before": false, "after": true}], // enforce spacing before and after semicolons (fixable)
    "sort-imports": 0, // sort import declarations within module
    "sort-vars": 0, // sort variables within the same declaration block
    "space-before-blocks": [2, "always"], // require or disallow a space before blocks (fixable)
    "space-before-function-paren": [2, {"anonymous": "always", "named": "never"}], // require or disallow a space before function opening parenthesis (fixable)
    "space-in-parens": [2, "never"], // require or disallow spaces inside parentheses (fixable)
    "space-infix-ops": 2, // require spaces around operators (fixable)
    "space-unary-ops": [2, {"words": true, "nonwords": false}], // require or disallow spaces before/after unary operators (fixable)
    "spaced-comment": [2, "always"], // require or disallow a space immediately following the // or /* in a comment
    "wrap-regex": 0, // require regex literals to be wrapped in parentheses
    //
    // ECMAScript 6
    //
    // These rules are only relevant to ES6 environments and are off by default.
    //
    "arrow-body-style": [2, "as-needed"], // require braces in arrow function body
    "arrow-parens": [2, "as-needed"], // require parens in arrow function arguments
    "arrow-spacing": 2, // require space before/after arrow function's arrow (fixable)
    "constructor-super": 2, // verify calls of super() in constructors (recommended)
    "generator-star-spacing": [2, "before"], // enforce spacing around the * in generator functions (fixable)
    "no-class-assign": 2, // disallow modifying variables of class declarations (recommended)
    "no-confusing-arrow": 0, // disallow arrow functions where they could be confused with comparisons
    "no-const-assign": 2, // disallow modifying variables that are declared using const (recommended)
    "no-dupe-class-members": 2, // disallow duplicate name in class members (recommended)
    "no-new-symbol": 2, // disallow use of the new operator with the Symbol object (recommended)
    "no-this-before-super": 2, // disallow use of this/super before calling super() in constructors (recommended)
    "no-useless-constructor": 2, // disallow unnecessary constructor
    "no-var": 2, // require let or const instead of var
    "object-shorthand": 2, // require method and property shorthand syntax for object literals
    "prefer-arrow-callback": 2, // suggest using arrow functions as callbacks
    "prefer-const": 2, // suggest using const declaration for variables that are never modified after declared
    "prefer-reflect": 0, // suggest using Reflect methods where applicable
    "prefer-rest-params": 2, // suggest using the rest parameters instead of arguments
    "prefer-spread": 2, // suggest using the spread operator instead of .apply()
    "prefer-template": 2, // suggest using template literals instead of strings concatenation
    "require-yield": 2, // disallow generator functions that do not have yield
    "template-curly-spacing": 2, // enforce spacing around embedded expressions of template strings (fixable)
    "yield-star-spacing": 2, // enforce spacing around the * in yield* expressions (fixable)
    //
    // eslint-plugin-react
    //
    // List of supported rules
    //
    "react/display-name": 0, // Prevent missing displayName in a React component definition
    "react/forbid-prop-types": [2, {"forbid": ["any", "array"]}], // Forbid certain propTypes
    "react/no-danger": 2, // Prevent usage of dangerous JSX properties
    "react/no-deprecated": 2, // Prevent usage of deprecated methods
    "react/no-did-mount-set-state": 2, // Prevent usage of setState in componentDidMount
    "react/no-did-update-set-state": 2, // Prevent usage of setState in componentDidUpdate
    "react/no-direct-mutation-state": 2, // Prevent direct mutation of this.state
    "react/no-is-mounted": 2, // Prevent usage of isMounted
    "react/no-multi-comp": 0, // Prevent multiple component definition per file
    "react/no-set-state": 0, // Prevent usage of setState
    "react/no-string-refs": 2, // Prevent using string references in ref attribute.
    "react/no-unknown-property": 2, // Prevent usage of unknown DOM property (fixable)
    "react/prefer-es6-class": 0, // Enforce ES5 or ES6 class for React Components
    "react/prefer-stateless-function": 0, // Enforce stateless React Components to be written as a pure function
    "react/prop-types": 2, // Prevent missing props validation in a React component definition
    "react/react-in-jsx-scope": 2, // Prevent missing React when using JSX
    "react/require-extension": [1, {"extensions": [".js"]}], // Restrict file extensions that may be required
    "react/self-closing-comp": 2, // Prevent extra closing tags for components without children
    "react/sort-comp": 2, // Enforce component methods order
    "react/wrap-multilines": 2, // Prevent missing parentheses around multilines JSX (fixable)
    //
    // JSX-specific rules
    //
    "react/jsx-boolean-value": [2, "always"], // Enforce boolean attributes notation in JSX (fixable)
    "react/jsx-closing-bracket-location": [2, {"selfClosing": "after-props", "nonEmpty": "after-props"}], // Validate closing bracket location in JSX
    "react/jsx-curly-spacing": [2, "never"], // Enforce or disallow spaces inside of curly braces in JSX attributes (fixable)
    "react/jsx-equals-spacing": 2, // Enforce or disallow spaces around equal signs in JSX attributes
    "react/jsx-handler-names": [2, {"eventHandlerPrefix": "on", "eventHandlerPropPrefix": "on"}], // Enforce event handler naming conventions in JSX
    "react/jsx-indent-props": [2, 2], // Validate props indentation in JSX
    "react/jsx-indent": [2, 2], // Validate JSX indentation
    "react/jsx-key": 2, // Validate JSX has key prop when in array or iterator
    "react/jsx-max-props-per-line": [2, {"maximum": 4}], // Limit maximum of props on a single line in JSX
    "react/jsx-no-bind": [2, {"allowArrowFunctions": true}], // Prevent usage of .bind() and arrow functions in JSX props
    "react/jsx-no-duplicate-props": [2, {"ignoreCase": true}], // Prevent duplicate props in JSX
    "react/jsx-no-literals": 0, // Prevent usage of unwrapped JSX strings
    "react/jsx-no-undef": 2, // Disallow undeclared variables in JSX
    "react/jsx-pascal-case": 2, // Enforce PascalCase for user-defined JSX components
    "react/jsx-sort-prop-types": 0, // Enforce propTypes declarations alphabetical sorting
    "react/jsx-sort-props": 2, // Enforce props alphabetical sorting
    "react/jsx-space-before-closing": [2, "always"], // Validate spacing before closing bracket in JSX (fixable)
    "react/jsx-uses-react": 2, // Prevent React to be incorrectly marked as unused
    "react/jsx-uses-vars": 2 // Prevent variables used in JSX to be incorrectly marked as unused
  }
}
```

---

## _Prettier_

- `package.json` script
  - ` "`prettier`"```: ```"`prettier --config .prettierrc --write `\"`src/**/*.js`\" `"``
- config file
  - `.prettierrc`

```
{
    "bracketSpacing": false,
    "jsxBracketSameLine": true,
    "parser": "flow",
    "printWidth": 80,
    "proseWrap": "never",
    "singleQuote": true,
    "trailingComma": "all"
}
```

---

## _Style lint_

- config file
  - `.prettierrc`

```
{
  "rules": {
    "at-rule-no-unknown": true,
    "block-no-empty": true,
    "color-no-invalid-hex": true,
    "comment-no-empty": true,
    "declaration-block-no-duplicate-properties": [
      true,
      {
        "ignore": [
          "consecutive-duplicates-with-different-values"
        ]
      }
    ],
    "declaration-block-no-shorthand-property-overrides": true,
    "font-family-no-duplicate-names": true,
    "font-family-no-missing-generic-family-keyword": true,
    "function-calc-no-unspaced-operator": true,
    "function-linear-gradient-no-nonstandard-direction": true,
    "keyframe-declaration-no-important": true,
    "media-feature-name-no-unknown": true,
    "no-descending-specificity": true,
    "no-duplicate-at-import-rules": true,
    "no-duplicate-selectors": true,
    "no-empty-source": true,
    "no-extra-semicolons": true,
    "no-invalid-double-slash-comments": true,
    "property-no-unknown": true,
    "selector-pseudo-class-no-unknown": true,
    "selector-pseudo-element-no-unknown": true,
    "selector-type-no-unknown": true,
    "string-no-newline": true,
    "unit-no-unknown": true,
    "at-rule-empty-line-before": [
      "always",
      {
        "except": [
          "blockless-after-same-name-blockless",
          "first-nested"
        ],
        "ignore": [
          "after-comment"
        ]
      }
    ],
    "at-rule-name-case": "lower",
    "at-rule-name-space-after": "always-single-line",
    "at-rule-semicolon-newline-after": "always",
    "block-closing-brace-empty-line-before": "never",
    "block-closing-brace-newline-after": "always",
    "block-closing-brace-newline-before": "always-multi-line",
    "block-closing-brace-space-before": "always-single-line",
    "block-opening-brace-newline-after": "always-multi-line",
    "block-opening-brace-space-after": "always-single-line",
    "block-opening-brace-space-before": "always",
    "color-hex-case": "lower",
    "color-hex-length": "short",
    "comment-empty-line-before": [
      "always",
      {
        "except": [
          "first-nested"
        ],
        "ignore": [
          "stylelint-commands"
        ]
      }
    ],
    "comment-whitespace-inside": "always",
    "custom-property-empty-line-before": [
      "always",
      {
        "except": [
          "after-custom-property",
          "first-nested"
        ],
        "ignore": [
          "after-comment",
          "inside-single-line-block"
        ]
      }
    ],
    "declaration-bang-space-after": "never",
    "declaration-bang-space-before": "always",
    "declaration-block-semicolon-newline-after": "always-multi-line",
    "declaration-block-semicolon-space-after": "always-single-line",
    "declaration-block-semicolon-space-before": "never",
    "declaration-block-single-line-max-declarations": 1,
    "declaration-block-trailing-semicolon": "always",
    "declaration-colon-newline-after": "always-multi-line",
    "declaration-colon-space-after": "always-single-line",
    "declaration-colon-space-before": "never",
    "declaration-empty-line-before": [
      "always",
      {
        "except": [
          "after-declaration",
          "first-nested"
        ],
        "ignore": [
          "after-comment",
          "inside-single-line-block"
        ]
      }
    ],
    "function-comma-newline-after": "always-multi-line",
    "function-comma-space-after": "always-single-line",
    "function-comma-space-before": "never",
    "function-max-empty-lines": 0,
    "function-name-case": "lower",
    "function-parentheses-newline-inside": "always-multi-line",
    "function-parentheses-space-inside": "never-single-line",
    "function-whitespace-after": "always",
    "indentation": 2,
    "length-zero-no-unit": true,
    "max-empty-lines": 1,
    "media-feature-colon-space-after": "always",
    "media-feature-colon-space-before": "never",
    "media-feature-name-case": "lower",
    "media-feature-parentheses-space-inside": "never",
    "media-feature-range-operator-space-after": "always",
    "media-feature-range-operator-space-before": "always",
    "media-query-list-comma-newline-after": "always-multi-line",
    "media-query-list-comma-space-after": "always-single-line",
    "media-query-list-comma-space-before": "never",
    "no-eol-whitespace": true,
    "no-missing-end-of-source-newline": true,
    "number-leading-zero": "always",
    "number-no-trailing-zeros": true,
    "property-case": "lower",
    "rule-empty-line-before": [
      "always-multi-line",
      {
        "except": [
          "first-nested"
        ],
        "ignore": [
          "after-comment"
        ]
      }
    ],
    "selector-attribute-brackets-space-inside": "never",
    "selector-attribute-operator-space-after": "never",
    "selector-attribute-operator-space-before": "never",
    "selector-combinator-space-after": "always",
    "selector-combinator-space-before": "always",
    "selector-descendant-combinator-no-non-space": true,
    "selector-list-comma-newline-after": "always",
    "selector-list-comma-space-before": "never",
    "selector-max-empty-lines": 0,
    "selector-pseudo-class-case": "lower",
    "selector-pseudo-class-parentheses-space-inside": "never",
    "selector-pseudo-element-case": "lower",
    "selector-pseudo-element-colon-notation": "double",
    "selector-type-case": "lower",
    "unit-case": "lower",
    "value-list-comma-newline-after": "always-multi-line",
    "value-list-comma-space-after": "always-single-line",
    "value-list-comma-space-before": "never",
    "value-list-max-empty-lines": 0
  }
}
```

---

# _System_

## Windows-Build-Tools

- `npm install --global windows-build-tools`
- Downloads and installs Visual C++ Build Tools, provided free of charge by Microsoft
- These tools are [required to compile popular native modules](https://github.com/nodejs/node-gyp)
  - If not already installed, it will also install Python 2.7, configuring your machine and npm appropriately
- Install this if you get this error:

```
if not defined npm_config_node_gyp (node "C:\Program Files\nodejs\node_modules\npm\node_modules\npm-lifecycle\node-gyp-bin\\..\..\node_modules\node-gyp\bin\node-gyp.js" rebuild )  else (node "C:\Program Files\nodejs\node_modules\npm\node_modules\node-gyp\bin\node-gyp.js" rebuild )
gyp ERR! configure error
gyp ERR! stack Error: Can't find Python executable "python", you can set the PYTHON env variable.
```

---

## _nodemon_

- https://github.com/remy/nodemon
- `npm i -g nodemon`
- Will auto-reload your Node server any time you make changes so you can see them take effect immediately
- Monitor for any changes in your node.js application and automatically restart the server
- `npm install --save-dev nodemon`
  - If using in an npm script, install locally
- To start a server, use:
  - `nodemon server.js`

---

## _PM2_

- A production process manager for Node.js applications with a built-in load balancer
- It allows you to keep applications alive forever, to reload them without downtime and to facilitate common system admin tasks
- https://www.npmjs.com/package/pm2
- Install globally to access pm2 command
  - `npm install pm2 -g`
- `npm i` ```pm2`
- script
  - `"dev": "pm2 start lib/server.js --watch",`

---

## _**http-server**_

- https://www.npmjs.com/package/http-server
- `npm install -g http-server`

* to start
  - `http-server`

---

## _**Browsersync**_

- https://www.browsersync.io/
- `npm install -g browser-sync`

* to view UI:
  - http://localhost:3001/

- to live inject html/css/js:
  - `browser-sync start --server --files "./*.html" "css/*.css" "js/*.js"`

---

## _concurrently_

- Run multiple npm script commands concurrently
- `npm install -g concurrently`
- Does not need to be installed locally
- Add these npm scripts to be able to start the backend and frontend at the same time using `npm run app`

```
`"server": "cd server && nodemon server.js",
 "client": "cd client && npm start",
 "app": "concurrently --kill-others-on-fail \"npm run server\" \"npm run client\""`
```

- The `–kill-others-on-fail` flag will kill other processes if one exits with a non zero status code

---

## _cross-env_

- Run scripts that set and use environment variables across platforms
- https://www.npmjs.com/package/cross-env
- `npm install --save-dev cross-env`

```
{
  "scripts": {
    "test": "cross-env NODE_ENV=test mocha --exit",
    "build": "cross-env NODE_ENV=production webpack --config build/webpack.config.js"
  }
}
```

---

# _Development_

---

# _Deployment_

## _Gulp_

- http://alferov.github.io/awesome-gulp/

* Installing
  - `npm install --global gulp-cli`

- Creating a Gulp Project:

  1. Initialize your project directory:
     1. `npm init`
  2. Install gulp in your project devDependencies:
     1. `npm install --save-dev gulp`
  3. Create a gulpfile.js at the root of your project:
     1. `var gulp = require('gulp');`

```
gulp.task('default', function() {
  // place code for your default task here
});
```

- Plugins:
  - http://gulpjs.com/plugins/
  - LiveReload - browser is refreshed automatically on save (requires Chrome extension)
    - `npm install --save-dev gulp-livereload`
  - gulp-util - a runnable task that visibly shows it executed
    - `npm install --save-dev gulp-util`

* Functions:
  - gulp.task
    - defines your tasks. Its arguments are name, deps and fn.

````
`gulp.``task``(``'mytask'``, ``function``() {`
``  ```//do stuff`
`});`
` `
`gulp.``task``(``'dependenttask'``, [``'mytask'``], ``function``() {`
``  ```//do stuff after 'mytask' is done.`
`});`
````

    * gulp.src
        * points to the files we want to use. Its parameters are globs and an optional options object. It uses .pipe for chaining its output into other plugins.
    * gulp.dest
        * points to the output folder we want to write files to.
    * gulp.src and gulp.dest
        * used to simply copy files

````
`gulp.``task``(``'copyHtml'``, ``function``() {`
``  ```// copy any html files in source/ to public/`
``  `gulp.``src``(``'source/*.html'``).``pipe``(gulp.``dest``(``'public'``));`
`});`
````

    * gulp.watch - like gulp.task has two main forms. Both of which return an EventEmitter that emits change events.
        * `gulp.``watch``('source/javascript``/**/``*.js``', ['``jshint']);`

- Tasks:
  - Javascript concat and minify

---

# _Performance_

## lru cache

- A cache object that deletes the least-recently-used items
- https://github.com/isaacs/node-lru-cache

---

# _Babel_

- http://ccoenraets.github.io/es6-tutorial/setup-babel/
- https://github.com/babel/example-node-server
- Install either as a dependency or devDependency depending on if the code is compiled locally or on a production server through source control
- Base
  - `npm i`@babel/cli`@babel/core @babel/node @babel/polyfill @babel/register babel-loader`
- Presets
  - `npm i @babel/preset-react @babel/preset-env`
- Plugins
  - `npm i @babel/plugin-proposal-class-properties @babel/plugin-proposal-object-rest-spread`
- Install ESlint option
  - `npm i -D babel-eslint`
- Install Jest option
  - `npm i ``babel-jest```
  - If using babel 7
    - `npm i core@^7.0.0-bridge.0`

* Allows
  - imports
  - JSX

- Update package.json

```
"scripts": {
  "dev": "nodemon --exec babel-node lib/server.js",
  "babel-node": "babel-node --presets=/*a*/ --ignore='foo|bar|baz'"
},
"babel": {
  "presets": [
    "@babel/preset-react",
    "@babel/preset-env"
  ],
  "plugins": [
    "@babel/plugin-proposal-class-properties",
    "`@babel/plugin-proposal-object-rest-spread`"
  ]
},
```

    * Add babel-node interpreter flag to starting script
        * `--interpreter babel-node`
        *  `"dev": "pm2 start lib/server.js --watch --interpreter babel-node",`

### Building Node

- You should not run `babel-node` in production
- If you are using JS features not nativity supported by node, you must compile Node before running it in production
- Add a new script to `package.json`
  - `"build-node": "babel lib -d build --copy-files",`
  - Compiles files from `/lib/` into `/build/`
  - `--copy-files` will include non-JS files as well
- There are also differences between features supported by browsers and Node
  - Babel will need 2 different configs, one for each
- Update babel `presets` config for `@babel/preset-env`
  - May not work

```
[
  "@babel/preset-env",
  {
    "targets": {
      "node": "current"
    }
  }
]
```

- In order to compile differently for the browser, we override the babel settings with Webpack
- In `webpack.config.js` under the `module.rules` property, add:

```
options: {
  presets: ['react', 'env']
}
```

- Running `npm run build-webpack` will create bundles files configured for browsers
- Running `npm run build-node` will create a `/build/` folder with a natively compiled Node

---

# _Webpack_

- `npm install webpack --save-dev`
- `npm install eslint-loader --save-dev`
- `npm install babel-loader --save-dev`
- http://ccoenraets.github.io/es6-tutorial/setup-webpack/
- https://createapp.dev/

### Source map

- Insert to show errors in your pre-compiled JS files:

```
module.exports = {
  devtool: 'inline-source-map',
},
```

### Hot reloading

- only components can be hot-reloaded

### Scripts

- `"start": "webpack-dev-server --mode development —open"`
- `"build": "webpack --mode production"`

### Config

```
const path = require('path');

const config = {
  entry: ['@babel/polyfill', './lib/components/index.js'],
  output: {
    path: path.resolve(__dirname, 'public'),
    filename: 'bundle.js'
  },
  module: {
    rules: [{ test: /\.js$/, exclude: /node_modules/, loader: 'babel-loader' }]
  }
};

module.exports = config;
```

### _Bundles_

### Cache

- Browsers are caching your code
- Every time you make a change, the file containing it has to be re-downloaded by all of the people visiting your site
- You probably don’t change your dependencies that much, though
- If you split them into a separate file, visitors would not have to download it again then

* Using Webpack to bundle, we can configure it to produce 2 bundles
  - one for the vendor files, and one for the app codebase
* This will allow the dependency cache to remain valid until there is an actual dependency change

- Use the SplitChunksPlugin
  - https://webpack.js.org/plugins/split-chunks-plugin/
- In `webpack.config.js` add:
  - This will split everything in `/node_modules/`

```
optimization: {
    splitChunks: {
      cacheGroups: {
        commons: {
          test: /[\\/]node_modules[\\/]/,
          name: 'vendors',
          chunks: 'all'
        }
      }
    }
  },
  output: {
    path: path.resolve(__dirname, 'public'),
    filename: '[name].bundle.js'
  },
```

- Update `index.html` to include both bundles
  - `<script src="/main.bundle.js" charset="utf-8"></script>`
  - `<script src="/vendors.bundle.js" charset="utf-8"></script>`
  - Might need version control on the files to let browsers know they changed
    - `src="/main.bundle.js?version=1.0.0"`
    - `src="/vendors.bundle.js`?version=1.0.0`"`
- Update `.gitignore` to include both bundles
  - `public/main.bundle.js`
  - `public/vendors.bundle.js`

### Minimize

- Create a new script and add the `p` flag to Webpack run command
- `"build-webpack": "webpack -p",`

### Examples

- https://github.com/tr1s/tris-webpack-boilerplate

---

# Database

## _objection.js_

- An SQL-friendly ORM for Node.js
- Built on an SQL query builder called knex
- https://github.com/Vincit/objection.js

---

# _Security_

## _bcrypt.js_

- Helps you hash passwords
- https://github.com/dcodeIO/bcrypt.js/
- `npm install bcryptjs`
- `const bcrypt = require('bcryptjs');`

## _jsonwebtoken_

- A compact, URL-safe means of representing claims to be transferred between two parties
- https://github.com/auth0/node-jsonwebtoken
- `npm install jsonwebtoken`
- `const jwt = require('jsonwebtoken');`

## _cookie-parser_

- Parse HTTP request cookies
- https://github.com/expressjs/cookie-parser
- `npm install cookie-parser`
- `const cookieParser = require('cookie-parser')`

## _Passport_

- Simple, unobtrusive authentication for Node.js
- https://github.com/jaredhanson/passport
- https://github.com/passport-next/passport
- https://github.com/jwalton/passport-api-docs

## _express-validator_

- An express.js middleware for validator.js
- String validation
- https://github.com/express-validator/express-validator

---

# _Misc_

## _Nodemailer_

- Send e-mails with Node.JS – easy as cake!
- https://github.com/nodemailer/nodemailer
- `npm install nodemailer --save`
- `const nodemailer = require('nodemailer');`

---

# _UI_

## _NProgress_

- For slim progress bars like on YouTube, Medium, etc
- https://github.com/rstacruz/nprogress
- `npm install --save nprogress`
- `import NProgress from 'nprogress';`

---

## _Font Awesome_

- https://fontawesome.com/how-to-use/on-the-web/setup/getting-started

### Node

- https://fontawesome.com/how-to-use/use-with-node-js

* `npm i --save @fortawesome/fontawesome`
* `npm i --save @fortawesome/react-fontawesome`

- `npm i --save @fortawesome/fontawesome-free-solid`
- `npm i --save @fortawesome/fontawesome-free-regular`
- `npm i --save @fortawesome/fontawesome-free-brands`

* `import fontawesome from '@fortawesome/fontawesome'`
* `import FontAwesomeIcon from '@fortawesome/react-fontawesome'`

- `import brands from '@fortawesome/fontawesome-free-brands'`
- `import faCheckSquare from '@fortawesome/fontawesome-free-solid/faCheckSquare'`

* `fontawesome.library.add(brands, faCheckSquare)`

- `<FontAwesomeIcon icon="check-square" />`
- `<FontAwesomeIcon icon={['fab', 'apple']} />`

### React

- https://github.com/FortAwesome/react-fontawesome

1. Install Font Awesome
   1. `npm i --save @fortawesome/react-fontawesome`
   2. `npm i --save @fortawesome/fontawesome-svg-core`
   3. May need to restart server in order to get it working
2. Install icon package as needed
   1. `npm i --save @fortawesome/free-solid-svg-icons`
   2. `npm i --save @fortawesome/free-brands-svg-icons`
   3. `npm i --save @fortawesome/free-regular-svg-icons`
3. In App.js
   1. import Font Awesome
      1. `import { FontAwesomeIcon } from '@fortawesome/react-fontawesome'`
   2. Import library
      1. `import { library } from '@fortawesome/fontawesome-svg-core'`
   3. Import icons
      1. Either individually
         1. `import { faCheckSquare, faCoffee } from '@fortawesome/free-solid-svg-icons'`
      2. Or all icons in package
         1. `import { fab } from '@fortawesome/free-brands-svg-icons'`
   4. Add icons to library to use anywhere in app
      1. `library.add(fab, faCheckSquare, faCoffee)`
4. In every component that uses FA icons
   1. `import { FontAwesomeIcon } from '@fortawesome/react-fontawesome'`
5. Use

```
<FontAwesomeIcon icon="check-square" />
<FontAwesomeIcon icon="coffee" />
<FontAwesomeIcon icon={['fab', 'microsoft']} />
<FontAwesomeIcon icon={['fab', 'google']} />
```

### Testing

- `src/__mocks__/@fortawesome/react-fontawesome.js`

```
import React from 'react'

export function FontAwesomeIcon(props) {
  return <i className="fa" />
}
```

---

# _Interesting_

- https://github.com/palantir/blueprint
- https://github.com/marmelab/react-admin

---
