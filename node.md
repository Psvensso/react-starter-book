# Node JS

> **Node.js **is an open-source, cross-platform JavaScript runtime environment for developing a diverse variety of server tools and applications. Although Node.js is not a JavaScript framework, many of its basic modules are written in JavaScript, and developers can write new modules in JavaScript. The runtime environment interprets JavaScript using Google's V8 JavaScript engine.

[Wikipedia](https://en.wikipedia.org/wiki/Node.js)

We use tools written in javascript, running in Node, to both build our app but also to host a webserver that serves our static files.

### NPM - Node package manager

The node package manager NPM came with the installation of Node and is used as a CLI tool, it works like most other [package managers](https://en.wikipedia.org/wiki/Package_manager). It has a [repository](https://www.npmjs.com/) with available packages and you use it to "pull" packages to you local machine. The external packages are most often, but doesn't have to be, javascript snippets or libraries. The configuration file, placed in the root of you project, called [package.json](https://raw.githubusercontent.com/Psvensso/react-starter/master/package.json) keeps track of what other modules/packages it has as dependencies and very importantly what versions they are and what dependencies they in turn have.

_What dependencies does our starter app have?_

_And what dependencies does React have?_

---

How NPM figures out dependency tree by tree shaking etc. is a too big topic for this short intro. Dependency problems between our packages are not a rare problem unfortunately so digging into this is often needed. I recommend the official documentation linked below. Also bare in mind that NPM has been under several version upgrades lately so old examples might be invalid, another reason to use the official documentation.

Although NPM is mainly about installing external package dependencies but we can also leverage it to run scripts in node, this makes our life a little bit later and you will see how we run scripts and defines tasks in the package.json file later on.

[NPM documentation](https://docs.npmjs.com/getting-started)  
[Package.json documentation](https://docs.npmjs.com/files/package.json)

In conjunction with NPM one can use the newer, hipper, package manager system from Facebook and other called [Yarn](https://yarnpkg.com). I recommend that one first get familiarized with NPM and then potentially moves on to using Yarn.

That is the basics of what ships with node and how the package manager looks like.

Now let's dive into how we use Node to server and package our app.

### Express

The [express js](https://expressjs.com/) is a small web server framework for node and is by far the most popular one. Since we will only write a small demo application we stick to express. In react-starter on the master branch we only use Express to server a [index.html](https://github.com/Psvensso/react-starter/blob/master/Tools/index.html) file, it adds some development tooling support and server static files from disk to the browser, it's all handled in the [server.js](https://github.com/Psvensso/react-starter/blob/master/Tools/server.js) file.  
For development with react this setup is very nice and provides good developer tool support. The back-end api and controllers can easily be swapped out for something more robust later on when running a production scenario.

### Webpack

Webpack is another Node package we use to both build our sources \(typescript, styling etc.\) and to use as a develop/package manager. The tool is configured using a webpack.config.\*.js file located in the Tools folder. There are several files depending on for what target your building. The dev version includes debugging and module hot swapping capabilities whiles the production version includes minification etc. to the bundle. The output of the tool is a bundle.js file that gets copied into the Scripts/dist folder \(not included in Git, you must build it yourself\).

##### How webpack bundles

Quickly explained webpack works by providing one or many entry points, in our case our entry point is main.ts in the Scripts folder. Webpack scans the file content, traces its dependencies and builds up a dependency graph then all of those files gets added into a single js file and server to the client.

##### Different file content

When using webpack we can "load" different kinds of files, other than just TypeScript \(.ts\) files or JavaScript \(ts\) files. We will go into how to load/require files in javascript when we get to the ES6 and TypeSCript syntaxes later on but just know that when importing for example stylesheets like this, in main.ts.

```
import "../Content/styles/main.scss";
```

Webpack then matches the file type from its "rules" configuration and figures out how to transpile, \(or compile or whatever plugin your using for that file type\) it should do with the file.

For example:  
.scss files gets turned into css using the sass-loader and then piped into a bunch of other plugins.  
.ts files gets compiled with the ts-loader  
... and so on.

They then all end up in the bundle.js file \(yes even the css\) together with some injected Webpack scripts.

_Can you find the rules and the names of the loaders/plugins in the _[_config file_](https://github.com/Psvensso/react-starter/blob/master/Tools/webpack.config.dev.js)_? _  
_Can you find your modules in the bundle.js file?     
_

**TL;DR;**

We run webpack like this, from the base of our project.

```
webpack -p --config tools/webpack.config.release.js
or
webpack -p --config tools/webpack.config.dev.js
```

Or use the npm script tasks \(`npm run build` or `npm run build:dev`\).

_Can you find where the NPM tasks are defined in the _[_config.json_](https://github.com/Psvensso/react-starter/blob/master/package.json)_?_

[Webpack documentation](https://webpack.js.org/)

### NOTE! Webpack is in v2.\*

Webpack has undergone some [big changes to the config file](https://webpack.js.org/guides/migrating/) structure and their internal workings. Make sure that documentation and examples you'r looking at are the correct version. Were using the latest and greatest v2.\* in the startup project.









That's it, all the boring tooling talks are done!   
First i recommend a short break, stretch your legs and try not to get overwhelmed by all the information with the tooling. Next its time to have a look at into the source code structure, or at least how i like to have it, and then we can finally start hacking some React components!

