# How to Set Up D3.js with Webpack and Babel

This repository accompanies my [tutorial](https://medium.com/code-like-a-girl/how-to-set-up-d3-js-with-webpack-and-babel-7bd3f5e20df7#.dv1hfry3g) on Medium. Follow along!   

Before you begin, make sure you have node and npm installed. Use a node version higher than 6. Also, note that all terminal commands are for Mac. Please use the equivalent commands for your OS.

The other day I was setting up a D3.js project when I ran into the classic developer conundrum — if I wanted to set up the project without using a CDN, I’d need to learn a couple of other auxiliary technologies. I had been meaning to learn to use webpack anyways, so I was happy to find a reason to get a jump on it. I didn’t find an existing tutorial for these three technologies, so thought I would share how I set up my project with you!

Here we go!

## Step 1: Set up your package.json file.

1. Create a new directory for this project.
2. While inside of your directory, type npm init into your terminal.
3. Follow the steps that appear on your screen. For the sake of this tutorial, it’s perfectly fine to use the defaults each time. Once you have done that, take a look at your package.json file. This is what mine looks like:

```{
  "name": "d3-webpack-babel-tutorial", 
  "version": "1.0.0", 
  "description": "", 
  "main": "index.js", 
  "scripts": { 
    "test": "echo \"Error: no test specified\" && exit 1" 
  }, 
  "author": "", 
  "license": "ISC"
}```


