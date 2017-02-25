# Building development environment with webpack and bable

## 1. Install dependency

> brew install yarn  
> yarn add webpack webpack-dev-server path  
> yarn add babel-loader babel-core babel-preset-es2015 babel-preset-react --dev  
> yarn add react react-dom  
> yarn add html-webpack-plugin  
> yarn add reactstrap react-addons-transition-group react-addons-css-transition-group  
> yarn add bootstrap@4.0.0-alpha.6  
> yarn add extract-text-webpack-plugin@^2.0.0-beta

## 2. Config

* package.js  

  ```javascript  
  /*
    ./package.json  
  */  
  {  
  "name": "hello-world-react",  
  "version": "1.0.0",  
  "main": "index.js",  
  "license": "MIT",

  // add the scripts key to your package.json

  "scripts": {  
    "build": "webpack",  
    "start": "webpack-dev-server"  
  },

  "dependencies": {  
  ...  
  },  
  "devDependencies": {  
  ...  
  }  
  }

  * webpack.config.js
  
    ```js
    /*
        ./webpack.config.js
    */
    const path = require('path');

    const HtmlWebpackPlugin = require('html-webpack-plugin');
    const HtmlWebpackPluginConfig = new HtmlWebpackPlugin({
      template: './client/index.html',
      filename: 'index.html',
      inject: 'body'
    })

    const ExtractTextPlugin = require('extract-text-webpack-plugin');
    const ExtractTextPluginConfig = new ExtractTextPlugin({
      filename: 'build.min.css'
    })
    const ExtractTextPluginCSSLoader = ExtractTextPlugin.extract({
      use: 'css-loader'
    })
    module.exports = {
        entry: './client/index.js',
        output: {
            path: path.resolve('dist'),
            filename: 'index_bundle.js'
        },
        module: {
            loaders: [
                {
                    test: /\.js$/,
                    loader: 'babel-loader',
                    exclude: /node_modules/
                }, {
                    test: /\.jsx$/,
                    loader: 'babel-loader',
                    exclude: /node_modules/
                }, {
                    test: /\.css$/,
                    loader: ExtractTextPluginCSSLoader
                }
            ]
        },
        plugins: [HtmlWebpackPluginConfig,ExtractTextPluginConfig]
    }

* .babelrc

  ```js
  /* 
    ./.babelrc
  */  
  {
    "presets":[
        "es2015", "react"
    ]
  }
  ```

* folder tree

  ```
  |-client /*include all src for client site*/
  |----index.js
  |----index.html
  |----App.jsx
  |-dist /*include all webpack output file for page*/
  |-webpack.config.js
  |-package.json
  |-yarn.lock
  |-.babelrc
  ```



