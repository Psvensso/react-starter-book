# TypeScript {#typescript}

> TypeScript is a free and open-source programming language developed and maintained by Microsoft. It is a strict superset of JavaScript, and adds optional **static typing** and class-based object-oriented programming to the language.
>
> TypeScript is designed for development of large applications and transcompiles to JavaScript.  
> As TypeScript is a superset of JavaScript, any existing JavaScript programs are also valid TypeScript programs.  
> [Wikipedia](https://www.gitbook.com/book/psvensso/react/edit#)

There are two main goals of TypeScript:

* Provide an optional type system for JavaScript.
* Provide planned features from future JavaScript editions to current JavaScript engines

[TypeScript Design Goals](https://github.com/Microsoft/TypeScript/wiki/TypeScript-Design-Goals#non-goals)



Browsers can't execute TypeScript directly. Typescript must be "transpiled" into JavaScript using the compiler, which requires some configuration, this is provided by the [tsconfig.json](https://raw.githubusercontent.com/Psvensso/react-starter/master/tsconfig.json) file in the root of you project. More about these options can be found on the [compiler options wiki page](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/Compiler%20Options.md).

##### Typings

Many JavaScript libraries, such as React, extend the JavaScript environment with features and syntax that the TypeScript compiler doesn't recognize natively. When the compiler doesn't recognize something, it throws an error.

Use [TypeScript type definition files](https://www.typescriptlang.org/docs/handbook/writing-declaration-files.html)—`d.ts files`—to tell the compiler about the modules you load.

TypeScript-aware editors leverage these same definition files to display type information about library features \(intellisense\).



##### lib.d.ts

TypeScript includes a special declaration file called [lib.d.ts](https://github.com/Microsoft/TypeScript/blob/master/lib/lib.d.ts). This file contains the ambient declarations for various common JavaScript constructs present in JavaScript runtimes and the DOM. Such as window, location Object

Based on the`--target`, TypeScript adds _additional _ambient declarations like`Promise`if the target is`es6`.

Since the QuickStart is targeting`es5`, you can override the list of declaration files to be included:

```
"lib":["es2015","dom"]
```

Thanks to that, you have all the`es6`typings even when targeting`es5`.



##### Syntactic downleveling

Turns TypeScript code into JavaScript code. An example use of syntactic downleveling is the destructuring pattern or the arrow function syntax when targeting ES2015.

```js
var foo = {x: "TypeSCript", y: 50}  
var { x, y } = foo;
const helloFunc = () => "Hello world";
```

compiles to

```ts
var foo = { x: "TypeSCript", y: 50 };
var x = foo.x, y = foo.y;
var helloFunc = function () { return "Hello world"; };
```

##### 

##### Polyfilling / Shimming

TypeScript does not polyfill itself, this is something we must provide to the browser. TypeScript is mostly pared with core-js polyfill library.

