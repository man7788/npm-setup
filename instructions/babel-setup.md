# Setting Up `Babel-Loader` in `npm`

## Getting Started

### Install Babel

```
- npm install -D babel-loader @babel/core @babel/preset-env webpack
```

## Within your webpack configuration object, you'll need to add the babel-loader to the list of modules

```
module: {
  rules: [
    {
      test: /\.(?:js|mjs|cjs)$/,
      exclude: /node_modules/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: [
            ['@babel/preset-env', { targets: "defaults" }]
          ]
        }
      }
    }
  ]
}
```

## Config File

### If you want to reduce config files in project root, you can specify browsers in package.json with browserslist key:

```
{
  "private": true,
  "dependencies": {
    "autoprefixer": "^6.5.4"
  },
  "browserslist": [
    "last 1 version",
    "> 1%",
    "not dead"
  ]
}
```

If you don’t use Google Analytics then a good default can be to support all browsers with a market share of 0.25% or higher like this: 

```
> 0.25%
```