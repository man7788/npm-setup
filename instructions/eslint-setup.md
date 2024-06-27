# Setting up `ESlint` in `npm`

## Getting Started

### Install the `ESLint` package in your project:

```
npm install eslint --save-dev
```

### Add an `.eslintrc` file in one of the [supported configuration file formats](https://eslint.org/docs/v8.x/use/configure/configuration-files#configuration-file-formats).

```
# Create JavaScript configuration file
touch .eslintrc.js
```

### Add configuration to the `.eslintrc` file.

```
// .eslintrc.js example
module.exports = {
  "env": {
      "browser": true,
      "es2021": true
  },
  "extends": "eslint:recommended",
  "parserOptions": {
      "ecmaVersion": "latest",
      "sourceType": "module"
  },
}
```

### Adjust `.eslintrc.json` to customize rules

```
{
  "rules": {
      "eqeqeq": "off",
      "curly": "error",
      "quotes": ["error", "double"]
  }
}
```

### Lint code using the `ESLint CLI`:

```
npx eslint project-dir/ file1.js
```

## Install the `VS Code ESLint` extension

Automatic lint highlighting for your files as you write, without you needing to rerun the eslint command every time.

If your project also contains an ESLint configuration file, the extension will automatically use those rules for that project.

## Using `ESLint` community plugins and `Prettier` together

### Install `eslint-config-airbnb-base`

Our default export contains all of our ESLint rules, including ECMAScript 6+. It requires eslint and eslint-plugin-import.

1. Install the correct versions of each package, which are listed by the command:

```
npm info "eslint-config-airbnb-base@latest" peerDependencies
```

If using npm 5+, use this shortcut

```
npx install-peerdeps --dev eslint-config-airbnb-base
```

2. Add `"extends": "airbnb-base"` to your `.eslintrc`.

### Install `eslint-config-prettier`

Will turn off any of the ESLint rules that clash with Prettier. If you are using the default ESLint ruleset, you will not need this.

1. Install eslint-config-prettier:

```
npm install --save-dev eslint-config-prettier
```

2. Add eslint-config-prettier to your ESLint configuration to `eslintrc`.

   - Add `"prettier"` to the `"extends"` array in your `.eslintrc.*` file. Make sure to put it last, so it gets the chance to override other configs.

```
{
  "extends": [
    "some-other-config-you-use",
    "prettier"
  ]
}
```
