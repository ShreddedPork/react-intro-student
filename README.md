# React intro

Welcome to the React Intro repo! This repo holds source files and branches to help get you up and running with React + Webpack.

# Getting started

The following commands will get you set up from scratch. Alternatively, you can opt-in to beginning at several stages of the boilerplate setup process by checking out the following branches:

`main`: contains only the `package.json, package-lock.json, .gitignore`, and `readme` for scratch setup

`webpack`: contains the `webpack.config.js` and `.babelrc` endpoints

`setup`: contains the folder and file structure for our React boilerplate, including `public` and `src` directories

# Bootstrapping from scratch

The following shell commands will get you up and running from scratch:

## Project initialization, adding deps, adding dev deps,

```bash
# create project structure, initialize config branch
mkdir react-intro && cd $_ && git init && npm init -y && git checkout -b main && git add . && git commit -m "init commit"

# checkout config branch for setup
git checkout -b config

# install deps
npm i react react-dom styled-components css-loader style-loader file-loader

# install dev deps
npm i -D @babel/core @babel/preset-env @babel/preset-react babel-loader babel-plugin-styled-components html-webpack-plugin webpack webpack-cli webpack-dev-server @babel/plugin-transform-runtime

# add .gitignore
printf ".DS_Store\nnode_modules\ndist" > .gitignore

# stage all and confirm
git status && git add . && git status

# commit deps
git commit -m "add: deps, dev deps"
```

## (Optional): gh client installation and remote repo initialization

```bash
# opt: install the gh client
brew install gh

# create a repo and push to remote
gh repo create 2201-fsa-core-react-intro --public --description "a react intro for 2201-fsa-core" --source=. --remote=origin

# confirm remote
git remote -v

# merge config with base
git checkout main && git merge config

# push to remote
git push -u origin main
```

## Webpack config

```bash
# create branch for webpack setup
git checkout -b webpack

# add these scripts to package.json script block
"dev":"webpack serve --port 3000",
"build":"webpack --config webpack.config.js",
"start":"npm run build && npm run dev",

# create webpack config
touch webpack.config.js
```

add the following content to your `webpack.config.js`:

```javascript
// add webpack config content
const path = require('path');
// generates the index.html and applies bundle, style assets
// https:#webpack.js.org/plugins/html-webpack-plugin/
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  mode: process.env.NODE_ENV || 'development',
  devServer: {
    historyApiFallback: true,
  },
  entry: path.join(__dirname, 'src', 'index.js'),
  output: {
    path: path.resolve(__dirname, 'dist'),
    publicPath: '/',
  },
  module: {
    rules: [
      {
        test: /\.?js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react'],
          },
        },
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(png|jp(e*)g|svg|gif)$/,
        use: ['file-loader'],
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, 'public', 'index.html'),
    }),
  ],
};
```

To wrap up our `webpack` setup, we'll create our `.babelrc` and add plugins to assist the transpilation process

```bash
# add .babelrc and content
printf '{"plugins": ["@babel/plugin-transform-runtime","babel-plugin-styled-components"]}' > .babelrc

# commit, merge to main, push to remote
git add . && git commit -m "add: webpack, babel configs" && git checkout main && git merge webpack && git push
```

## React project structure setup

```bash
# add react setup

git checkout -b setup && mkdir public && touch public/index.html && mkdir src && touch src/index.js src/index.css

# commit and merge
git add . && git commit -m "add: react boilerplate" && git checkout main && git merge setup && git push

# git branch check (type "q" to get out of vim)
git branch
```
