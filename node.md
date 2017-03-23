# Node JS

> **Node.js **is an open-source, cross-platform JavaScript runtime environment for developing a diverse variety of server tools and applications. Although Node.js is not a JavaScript framework, many of its basic modules are written in JavaScript, and developers can write new modules in JavaScript. The runtime environment interprets JavaScript using Google's V8 JavaScript engine.

[Wikipedia](https://en.wikipedia.org/wiki/Node.js)

We use tools written in javascript, running in Node, to both build our app but also to host a webserver that serves our static files.

### NPM - Node package manager

The node package manager NPM came with the installation of Node and is used as a CLI tool, it works like most other [package managers](https://en.wikipedia.org/wiki/Package_manager). It has a [repository](https://www.npmjs.com/) with available packages and you use it to "pull" packages to you local machine. The external packages are most often, but doesn't have to be, javascript snippets or libraries. The configuration file, placed in the root of you project, called [package.json](https://raw.githubusercontent.com/Psvensso/react-starter/master/package.json) keeps track of what other modules/packages it has as dependencies and very importantly what versions they are and what dependencies they in turn have. $$x = y$$  


_**What dependencies does our starter app have?   
And what dependencies does React have?  
**_  
How NPM figures out dependency tree by tree shaking etc. is a too big topic for this short intro. Dependency problems between our packages are not a rare problem unfortunately so digging into this is often needed. I recommend the official documentation linked below. Also bare in mind that NPM has been under several version upgrades lately so old examples might be invalid, another reason to use the official documentation.

Although NPM is mainly about installing external package dependencies but we can also leverage it to run scripts in node, this makes our life a little bit later and you will see how we run scripts and defines tasks in the package.json file later on.

[NPM documentation](https://docs.npmjs.com/getting-started)  
[Package.json documentation](https://docs.npmjs.com/files/package.json)

In conjunction with NPM one can use the newer, hipper, package manager system from Facebook and other called [Yarn](https://yarnpkg.com). I recommend that one first get familiarized with NPM and then potentially moves on to using Yarn.

  
That is the basics of what ships with node and how the package manager looks like. Now lets dive into how we use Node to server and package our app.





