# Using `Prettier` in `npm`

## Getting Started

### Install Prettier locally

```
npm install --save-dev --save-exact prettier
```

### Create an empty config file to let editors and other tools know you are using Prettier

```
node --eval "fs.writeFileSync('.prettierrc','{}\n')"
```

### Adjust .prettierrc.json to add rules

```
{
  "singleQuote": true
}
```

### Create a `.prettierignore` file to let the Prettier CLI and editors know which files to **_not_** format

```
# Ignore artifacts:
build
coverage
```

> Prettier will follow rules specified in .gitignore if it exists in the same directory from which it is run. You can also base your .prettierignore on .eslintignore (if you have one).

> If your project isn’t ready to format, say, HTML files yet, add \*.html

## `Prettier Formatter for Visual Studio Code` Extension

## Install

Install through VS Code extensions. Search for `Prettier - Code formatter`

Can also be installed in VS Code: Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.

```
ext install esbenp.prettier-vscode
```

## Default Formatter

### Adjust `setting.json` to use Prettier as the default formatter

```
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

### Adjust `setting.json` to enable auto format

```
{
  "[javascript]": {
    "editor.formatOnSave": true
  }
}
```
