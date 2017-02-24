# How to Set Up D3.js with Webpack and Babel

This repository accompanies my [tutorial](https://medium.com/code-like-a-girl/how-to-set-up-d3-js-with-webpack-and-babel-7bd3f5e20df7#.dv1hfry3g) on Medium. Follow along!   

Before you begin, make sure you have node and npm installed. Use a node version higher than 6. Also, note that all terminal commands are for Mac. Please use the equivalent commands for your OS.

The other day I was setting up a D3.js project when I ran into the classic developer conundrum — if I wanted to set up the project without using a CDN, I’d need to learn a couple of other auxiliary technologies. I had been meaning to learn to use webpack anyways, so I was happy to find a reason to get a jump on it. I didn’t find an existing tutorial for these three technologies, so thought I would share how I set up my project with you!

Here we go!

## Step 1: Set up your package.json file.

1. Create a new directory for this project.
2. While inside of your directory, type `npm init` into your terminal.
3. Follow the steps that appear on your screen. For the sake of this tutorial, it’s perfectly fine to use the defaults each time. Once you have done that, take a look at your package.json file. This is what mine looks like:

```
{
  "name": "d3-webpack-babel-tutorial", 
  "version": "1.0.0", 
  "description": "", 
  "main": "index.js", 
  "scripts": { 
    "test": "echo \"Error: no test specified\" && exit 1" 
  }, 
  "author": "", 
  "license": "ISC"
}
```

Yours should look similar, but with whatever information you have inputted, rather than the information I inputted!

## Step 2: Install Webpack

1. Type `npm install webpack webpack-dev-server` into your terminal.
2. Create a webpack configuration file by typing `touch webpack.config.js` into your terminal.
3. Then, copy the code below into your `webpack.config.js` file.

```
const path = require('path'); 

module.exports = { 
  entry: './src/index.js', 
  output: {
    path: path.resolve('dist'), 
    filename: 'index_bundle.js' 
  }, 
  module: {
    loaders: [
      { test: /\.js$/, loader: 'babel-loader', exclude: /node_modules/ }
     ]
 }  
} 
```

As you can see above, you’ve specified an entry and an output.
* In this case, the input is an index.js file that lives inside of a src folder.
* The output describes where the javascript code is going to be saved.
* The loaders allow you to require other build tools. In this case, we are going to be loading Babel.

## Step 3: Install Babel
1. Type npm `install --save-dev babel-cli` into your terminal.
2. Once you’ve finished installing, your package.json file will look like this:

```
{
  "name": "my-project", 
  "version": "1.0.0", 
  "devDependencies": { 
    "babel-cli": "^6.0.0"
  }
}
```

3. Add a build script to your npm scripts by adding these lines to your `package.json` file: `"build": "babel src -d lib"`. It should look like this:

```
"scripts": { 
  "build": "babel src -d lib" 
} 
```

4. Run `npm build`.
5. Next, type `npm install babel-loader babel-core babel-preset-es2015`. This will allow us to load all of the dependencies we need to get this working.
6. We will then need to create a `.babelrc file`. To do so, type `touch .babelrc` into your terminal.
7. Type `npm install babel-preset-env --save-dev` into your terminal and add these lines to your `.babelrc` file.

```
{ 
  "presets":["env"] 
}
```

## Step 4: Set up the Structure of your Application
1. Create a folder called `src` by typing `mkdir src` in your terminal.
2. Create a new file inside of your `src` folder. If you’re on a mac, you can `cd` into your `src` file and then create an `index.js` and an `index.html` file with the command `touch index.js index.html`.
3. In your `index.js file`, add a `console.log` to test if it is working later.

```
console.log("working");
```

4. Add the `!DOCTYPE` to your `index.html` file. I’ve also added an `<h1>` tag with the word “Hi” in it. My `index.html` file looks like this:

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>D3 Webpack Babel</title>
</head>
<body>
  <h1>Hi</h1>
</body>
</html>
```

## Step 5: Setup HTML Webpack Plugin
1. To install the `HTML Webpack plugin`, type `npm install html-webpack-plugin`.
2. To configure it, you can copy and paste the code below into your `webpack.config.js` file.

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const HtmlWebpackPluginConfig = new HtmlWebpackPlugin({
  template: './src/index.html',
  filename: 'index.html',
  inject: 'body'
})
module.exports = { 
  entry: './src/index.js', 
  output: { 
    path: path.resolve('dist'), 
    filename: 'index_bundle.js'
  }, 
  module: { 
    loaders: [ 
      { test: /\.js$/, loader: 'babel-loader', exclude: /node_modules/ }
    ]
  }, 
  plugins: [HtmlWebpackPluginConfig]
}
```

## Step 6: Run the Application
1. Head into your `package.json` file and add a start script to your npm scripts. Inside of scripts replace the line that begins with "test" and replace it with: `"start": “webpack-dev-server"`. It will look like this:

```
{
  "name": "d3-webpack-babel",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "build": "babel src -d lib", 
    "start": "webpack-dev-server"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "babel-cli": "^6.23.0",
    "babel-preset-env": "^1.1.8"
  }
}
```

2. In your terminal, run `npm start`. Your app should start running. Check in your browser to make sure everything is working correctly.

## Step 7: Install D3
1. Run `npm install d3` in your terminal.
2. Add an `svg` like this to your `index.html` file:

```
<svg width="300px" height="150px">
  <rect x="20" y="20" width="20px" height="20" rx="5" ry="5" />
  <rect x="60" y="20" width="20px" height="20" rx="5" ry="5" />
  <rect x="100" y="20" width="20px" height="20" rx="5" ry="5"/>
 </svg>
```

You should see three black squares appear in your browser. 

3. In your `index.js` file, add an import statement to include D3 in the file: `import * as d3 from 'd3';`.
4. To test to be sure that D3 is loaded correctly, try using it by changing the color of the three rectangles you see on your screen. You can copy and paste the code below into your `index.js` file.

```
import * as d3 from 'd3';

const square = d3.selectAll("rect");
square.style("fill", "orange");

```

If you’ve done it correctly, you should see the three little squares turn orange!

If you’ve followed all of these steps, you should find that you now have Webpack, Babel, and D3 correctly installed and functional. Please post an issue if you run into any problems. 













