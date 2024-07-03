# Using `Jest` in `npm` 

## Getting Started

### Install Jest using your favorite package manager:

```
npm install --save-dev jest
```

## Add the following section to your `package.json`:

```
{
  "scripts": {
    "test": "jest --watch"
  }
}
```

## Using ES6 import statements with Jest
By default, the current version of Jest will not recognize ES6 import statements. In order for you to be able to use ES6 modules for this project you may follow the Jest instructions for using Babel.

To use Babel, install required dependencies:

```
npm install --save-dev babel-jest @babel/core @babel/preset-env
```

Configure Babel to target your current version of Node by creating a ```babel.config.js``` file in the root of your project:

```
module.exports = {
  presets: [['@babel/preset-env', {targets: {node: 'current'}}]],
};
```





