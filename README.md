# React from Scratch

Boilerplate template for building react apps from scratch without using CRA.

## Instructions

---

### Initialize the project using `npm` and `git`

1. `cd react-boilerplate`
2. `npm init` - creates a `package.json`
3. `git init` - initalizes `git` repository

---

### Set the structure of the app directory

Create the following folders

- `public`
- `src`

---

### Install runtime dependencies

- `npm install react react-dom`

---

### Installing development dependencies

#### Install a transpiler (Babel)

A transpiler converts ECMAScript 2015+ code into backwards-compatible version of javascript (Older browser compatibility). Babel also transpiles JSX.

- `npm install @babel/core @babel/preset-env @babel/preset-react babel-loader css-loader style-loader --save-dev`

#### Install a bundler (Webpack)

- `npm instal webpack webpack-cli webpack-dev-server html-webpack-plugin --save-dev`

---

#### Create Webpack and Babel config files

- `touch webpack.config.js .babelrc`

#### Basic webpack config:

```
const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");

module.exports = {
  output: {
    path: path.resolve(__dirname, "build"),
    filename: "bundle.js",
  },
  resolve: {
    modules: [path.join(__dirname, "src"), "node_modules"],
    alias: {
      react: path.join(__dirname, "node_modules", "react"),
    },
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
        },
      },
      {
        test: /\.css$/,
        use: [
          {
            loader: "style-loader",
          },
          {
            loader: "css-loader",
          },
        ],
      },
    ],
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./public/index.html",
    }),
  ],
};

```

Add the `index.html` in the public folder

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>React Boilerplate</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
```

#### Configure babelrc file

```
{
    "presets": [
        "@babel/preset-env",
        "@babel/preset-react"
    ]
}
```

---

#### Create a basic `index.js` file

```
import React from "react"
import ReactDom from "react-dom"
const root = document.getElementById('root')
const App = () => {
return (
<h1>Hello from React</h1>
)
}
ReactDom.render(<App />, root)
```

---

#### Adding scripts in the `package.json`

The following scripts allows to run the following commands:

- `npm start`
- `npm build`

```
"scripts: {
"start": "webpack serve  --mode=development --open --hot",
"build": "webpack --mode=production"
}
```
