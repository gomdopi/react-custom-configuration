# Steps for creating your own React app from scratch with basic configuration

## Basics
### Create and move into your app directory
```
$ mkcd {dir-name} 
```
> mkcd = mkdir && cd
> 
>(https://github.com/gomdopi/dev-env-setup/blob/master/zsh/scripts.zsh)

## NPM
### Initialize NPM
```
$ npm init -y
```

## React
### Install React
```
$ npm install react react-dom
```

## Webpack
### Install Webpack
```
$ npm install --save-dev webpack webpack-dev-server webpack-cli
```

### Creating basic files
#### Start script
Add following to `package.json`:
```
"scripts": {
    "start": "webpack-dev-server --mode development",
   },
```

#### index.html
Create `index.html` like so:
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

#### index.js
Create `index.js` under `src` directory like so:
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

## Resources
[First website](https://www.codementor.io/@rajjeet/step-by-step-create-a-react-project-from-scratch-11s9skvnxv)

[Second website](https://www.freecodecamp.org/news/how-to-set-up-deploy-your-react-app-from-scratch-using-webpack-and-babel-a669891033d4/)

