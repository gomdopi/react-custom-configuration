# Steps for creating your own React app from scratch with basic configuration

## Initialization/Installation
### Create and move into your app directory
```
$ mkcd {dir-name} 
```
> mkcd = mkdir && cd
> 
>(https://github.com/gomdopi/dev-env-setup/blob/master/zsh/scripts.zsh)

### NPM
#### Initialize NPM
```
$ npm init -y
```

### React
#### Install React
```
$ npm install react react-dom
```

### Webpack
#### Install Webpack
```
$ npm install --save-dev webpack webpack-dev-server webpack-cli
```

#### Creating basic files
##### Start script
- Add following to `package.json`:
```
"scripts": {
  "start": "webpack-dev-server --mode development",
},
```
- Usage:
```
$ npm run start
```

##### index.html
- Create `index.html` like so:
```
<!DOCTYPE html>
<html>
  <head>
    <title>My React Configuration Setup</title>
  </head>
  <body>     
    <div id="root"></div>
      <script src="./dist/bundle.js"></script>
  </body>
</html>
```

- Make sure `index.html` & `bundle.js` are in specified directory in `webpack.config.js`:
```
output: {
  path: path.resolve(__dirname , 'build'),
  filename: 'bundle.js'
},
```
> HTMLWebpackPlugin can take care of the above by adding correct
> script tag with src as entry file configured in `webpack.config.js`

##### index.js
- Create `index.js` in `src/` like so:
```
import React from "react";
import ReactDOM from "react-dom";

class Welcome extends React.Component {
  render() {
    return <h1>Hello World from React boilerplate</h1>;
  }
}

ReactDOM.render(<Welcome />, document.getElementById("root"));
```

### Babel
#### Install Babel
```
$ npm install --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader
```

#### Create/configure basic files
##### webpack.config.js
- Create `webpack.config.js` in root like so:
```
module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'build'),
    publicPath: '/',
    filename: 'bundle.js'
  },
  devServer: {
    contentBase: './build',
  },
  module: {
    rules: [
    {
      test: /\.(js|jsx)$/,
      exclude: /node_modules/,
      use: ['babel-loader']
    }
    ]
  },
};
```

##### .babelrc
- Create `.babelrc` in root like so:
```
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}
```

### Prettier
#### Install Prettier
```
$ npm install --save-dev --save-exact prettier
```

#### Create configuration file
- Create `.prettierrc` in root like so:
```
{
  "semi": true,
  "singleQuote": true,
  "trailingComma": "es5"
}
```

#### Usage
##### CLI
```
$ npx prettier --write "src/**/*.js"
```

##### Script
- Add script to `package.json`
```
"scripts": {
  "format": "prettier --write \"src/**/*.js\"",
},
```
- Usage:
```
$ npm run format
```

### Source Map
- Add source map for better error logging:
```
module.exports = {
  devtool: 'inline-source-map',
  // … the rest of the config
};
```

### ESLint
#### Install ESLint
```
$ npm --save-dev install eslint eslint-loader babel-eslint eslint-config-react eslint-plugin-react
```

#### Configure webpack
- Modify `webpack.config.js`:
```
module.exports = {
  // modify the module
  module: {
    rules: [{
      test: /\.(js|jsx)$/,
      exclude: /node_modules/,
      use: ['babel-loader', 'eslint-loader'] // include eslint-loader
    }]
  },
};
```

#### Create config file
- Create `.eslintrc` in root like so:
```
{
  "parser": "babel-eslint",
  "extends": "react",
  "env": {
    "browser": true,
    "node": true
  },
  "settings": {
    "react": {
      "version": "detect"
    }
  }
}
```

#### Add eslint script
```
"scripts": {
  "eslint-fix": “eslint --fix \"src/**/*.js\"", // the eslint script,
},
```
- Usage:
```
$ npm run eslint-fix
```

### CSS LESS
#### Installation
```
$ npm install --save-dev less less-loader css-loader style-loader
```

#### Create basic files
- Create `header.less` in `src/style/` like so:
```
.header {
  background-color: #3d3d;
}
```

- Create `main.less` in `src/style/` like so:
```
@import "header.less";
@color: #f5adad;
body {
  background-color: @color;
}
```

#### Using the styles found in the less file(s)
- Import `main.less` into `index.js`:
```
import './style/main.less';
```

### HTMLWebpackPlugin
#### Installation
```
npm install --save-dev html-webpack-plugin
```

#### Configuration
- Configure `webpack.config.js`:
```
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: //…
  output: {
    //…
  },
  devServer: {
    //…
  },
  module: {
    //…
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve('./index.html'),
    }),
  ]
};
```

## Resources
[First website](https://www.codementor.io/@rajjeet/step-by-step-create-a-react-project-from-scratch-11s9skvnxv)

[Second website](https://www.freecodecamp.org/news/how-to-set-up-deploy-your-react-app-from-scratch-using-webpack-and-babel-a669891033d4/)

