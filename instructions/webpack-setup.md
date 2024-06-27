# Setting up `webpack` in `npm`

## Getting Started

### Initialize `npm`, install `webpack` and `webpack-cli` locally

```
npm init -y
npm install webpack webpack-cli --save-dev
```

### Create a `.gitignore` file in your project

Include the following line in `.gitignore`

```
node_modules
```

### Create `/src` and `/dist` directories with the following content

- Create an `index.js` file in `/src`

If you are not using `HtmlWebpackPlugin`:

- Create an `index.html` file in `/dist`
- Link the filename `'bundle.js'` in a script tag in `index.html`

### Adjust `package.json` to `'private'`

Remove the `'main'` entry to prevent an accidental publish of your code:

```
{
  "name": "webpack-setup",
  "version": "1.0.0",
  "description": "",
  "private": true,
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "MIT",
  "devDependencies": {
    "webpack": "^5.38.1",
    "webpack-cli": "^4.7.2"
  }
}
```

### Create a `webpack.config.js` file

```
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(\_\_dirname, 'dist'),
  },
};
```

### Generate an optimized bundle

```
npx webpack --config webpack.config.js
```

### Adjust `package.json` by adding an npm script shortcut

```
{
  "name": "webpack-setup",
  "version": "1.0.0",
  "description": "",
  "private": true,
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^5.4.0",
    "webpack-cli": "^4.2.0"
  },
}
```

### `npm run build` can be used in place of the `npx webpack` command

```
npm run build
```

## Asset Management

### Install `style-loader` and `css-loader`

```
npm install --save-dev style-loader css-loader
```

### Add `style-loader` and `css-loader` to your `webpack.config.js`

```
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(\_\_dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
};
```

### Add the built-in image `Asset Modules` to your `webpack.config.js`

```
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(\_\_dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource',
      },
    ],
  },
};
```

### Add the built-in font `Asset Modules` to your `webpack.config.js`

```
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(\_\_dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource',
      },
      {
        test: /\.(woff|woff2|eot|ttf|otf)$/i,
        type: 'asset/resource',
      },
    ],
  },
};
```

## Output Management

### Install `HtmlWebpackPlugin`

```
npm install --save-dev html-webpack-plugin
```

### Adjust `webpack.config.js` for `HtmlWebpackPlugin`

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: {
    index: './src/index.js',
    print: './src/print.js',
  },
  plugins: [
    new HtmlWebpackPlugin({
      filename: 'template.html',
      template: './src/template.html',
      inject: 'head',
      scriptLoading: 'defer',
    }),
  ],
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(\_\_dirname, 'dist'),
  },
};
```

### Adjust `webpack.config.js` for cleaning up the `/dist` folder

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: {
    index: './src/index.js',
    print: './src/print.js',
  },
  plugins: [
    new HtmlWebpackPlugin({
      filename: 'template.html',
      template: './src/template.html',
      inject: 'head',
      scriptLoading: 'defer',
    }),
  ],
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(\_\_dirname, 'dist'),
    clean: true,
  },
};
```

## Development

### Adjust `webpack.config.js` to set mode to `'development'`

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  mode: 'development',
  entry: {
    index: './src/index.js',
    print: './src/print.js',
  },
  plugins: [
    new HtmlWebpackPlugin({
      filename: 'template.html',
      template: './src/template.html',
      inject: 'head',
      scriptLoading: 'defer',
    }),
  ],
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(\_\_dirname, 'dist'),
    clean: true,
  },
};
```

### Adjust `webpack.config.js` for `inline-source-map` option

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  mode: 'development',
  entry: {
    index: './src/index.js',
    print: './src/print.js',
  },
  devtool: 'inline-source-map',
  plugins: [
    new HtmlWebpackPlugin({
      filename: 'template.html',
      template: './src/template.html',
      inject: 'head',
      scriptLoading: 'defer',
    }),
  ],
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(\_\_dirname, 'dist'),
    clean: true,
  },
};
```

### Adjust `package.json` for using watch mode

```
{
  "name": "webpack-setup",
  "version": "1.0.0",
  "description": "",
  "private": true,
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "watch": "webpack --watch",
    "build": "webpack"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "html-webpack-plugin": "^4.5.0",
    "webpack": "^5.4.0",
    "webpack-cli": "^4.2.0"
  },
}
```

### Install `webpack-dev-server`

```
npm install --save-dev webpack-dev-server
```

### Adjust `package.json` for using `webpack-dev-server`

This tells `webpack-dev-server` to serve the files from the `/dist` directory on `localhost:8080`:

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  mode: 'development',
  entry: {
    index: './src/index.js',
    print: './src/print.js',
  },
  devtool: 'inline-source-map',
  devServer: {
    static: './dist',
    watchFiles: ['template.html']
  },
  plugins: [
    new HtmlWebpackPlugin({
      filename: 'template.html',
      template: './src/template.html',
      inject: 'head',
      scriptLoading: 'defer',
    }),
  ],
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(\_\_dirname, 'dist'),
    clean: true,
  },
   optimization: {
    runtimeChunk: 'single',
  },
};

```

### Adjust `package.json` for using `webpack-dev-server`

```
{
  "name": "webpack-setup",
  "version": "1.0.0",
  "description": "",
  "private": true,
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "watch": "webpack --watch",
    "start": "webpack serve --open",
    "build": "webpack"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "html-webpack-plugin": "^4.5.0",
    "webpack": "^5.4.0",
    "webpack-cli": "^4.2.0"
  },
}
```

## Production

### Install `webpack-merge`

```
npm install --save-dev webpack-merge
```

### Create the following seperate config files, and remove `webpack.config.js`

```
webpack.common.js
webpack.dev.js
webpack.prod.js
```

Make sure that any webpack commands you run use the `--config` option to specify which webpack configuration file to use. Otherwise, it will not bundle correctly looking for a missing `webpack.config.js`.

If you are using `ESlint`, `"import/no-extraneous-dependencies"` and `"import/extensions"` errors might show up.
Add the following rules to igonre the warnings.

```
 "rules": {
    "import/no-extraneous-dependencies": [
      "error",
      {
        "devDependencies": ["**/webpack.*.js"]
      }
    ],
    "import/extensions": ["error", { "js": "ignorePackages" }]

}
```

### Add the following code to `webpack.common.js`

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/template.html',
      inject: 'head',
      scriptLoading: 'defer',
    }),
  ],
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'dist'),
    clean: true,
  },
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource',
      },
      {
        test: /\.(woff|woff2|eot|ttf|otf)$/i,
        type: 'asset/resource',
      },
    ],
  },
};
```

### Add the following code to `webpack.dev.js`

```
const { merge } = require('webpack-merge');
const common = require('./webpack.common.js');

module.exports = merge(common, {
  mode: 'development',
  devtool: 'inline-source-map',
  devServer: {
    static: './dist',
    watchFiles: ['./src/template.html'],
  },
  optimization: {
    runtimeChunk: 'single',
  },
});
```

### Add the following code to `webpack.prod.js`

```
const { merge } = require('webpack-merge');
const common = require('./webpack.common.js');

module.exports = merge(common, {
  mode: 'production',
  devtool: 'source-map',
});
```

### Adjust `package.json` to use the new configuration files

```
{
  "name": "npm-setup",
  "version": "1.0.0",
  "description": "",
  "private": true,
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "watch": "webpack --watch --config webpack.dev.js",
    "start": "webpack serve --open --config webpack.dev.js",
    "build": "webpack --config webpack.prod.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "css-loader": "^6.7.2",
    "eslint": "^8.28.0",
    "eslint-config-airbnb-base": "^15.0.0",
    "eslint-config-prettier": "^8.5.0",
    "eslint-plugin-import": "^2.26.0",
    "html-webpack-plugin": "^5.5.0",
    "prettier": "2.8.0",
    "style-loader": "^3.3.1",
    "webpack": "^5.75.0",
    "webpack-cli": "^5.0.0",
    "webpack-dev-server": "^5.0.4",
    "webpack-merge": "^5.10.0"
  }
}
```

## Deploying a subfolder to GitHub Pages

### Make sure `git` knows about your subtree (the subfolder with your site)

```

git add dist && git commit -m "Initial dist subtree commit"

```

### Use `subtree push` to send it to the gh-pages branch on `GitHub`

```

git subtree push --prefix dist origin gh-pages

```

> Note: If your folder isn’t called `'dist'`, then you’ll need to change that in each of the commands above.

### Create an npm script to do the work

Inside your project’s `package.json` file, within the scripts section, add an additional entry

```
"scripts": { "YourScriptName": "git subtree push --prefix dist origin gh-pages" }
```

Now each time you need to update your project’s live preview, you `npm run <YourScriptName>` in your project’s terminal.
