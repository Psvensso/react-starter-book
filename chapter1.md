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

Browsers can't execute TypeScript directly. Typescript must be "transpiled" into JavaScript using the compiler, which requires some configuration, this is provided by the [tsconfig.json](https://raw.githubusercontent.com/Psvensso/react-starter/master/tsconfig.json) file in the root of you project. More about these options can be found on the [compiler options wiki page](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/Compiler Options.md).

##### Typings

Many JavaScript libraries, such as React, extend the JavaScript environment with features and syntax that the TypeScript compiler doesn't recognize natively. When the compiler doesn't recognize something, **it throws an error**.

Use [TypeScript type definition files](https://www.typescriptlang.org/docs/handbook/writing-declaration-files.html)—`d.ts files`—to tell the compiler about the modules you load.

TypeScript-aware editors leverage these same definition files to display type information about library features \(intellisense\).

##### lib.d.ts

TypeScript includes a special declaration file called [lib.d.ts](https://github.com/Microsoft/TypeScript/blob/master/lib/lib.d.ts). This file contains the ambient declarations for various common JavaScript constructs present in JavaScript runtimes and the DOM. Such as window, location Object

Based on the`--target`, TypeScript adds additional ambient declarations like`Promise`if the target is`es6`.

Since the were targeting es5, you can override the list of declaration files to be included:

```
"lib":["es2015","dom"]
```

Thanks to that, you have all the es6 typings even when targeting es5.

### Installable typings files {#installable-typings-files}

TypeScript has several strategies of finding you .d.ts definition files, one of the strategies is looking in the same folder as the module was imported from. However many libraries Jest, React Webpack and others do not include d.ts files in their npm packages. Fortunately, either their authors or community contributors have created separate d.ts files for these libraries and published them in well-known locations.

You can install these typings via `npm` \(more on what npm is later\) using the[`@types/*`scoped package](http://www.typescriptlang.org/docs/handbook/declaration-files/consumption.html) and Typescript, starting at 2.0, automatically recognizes them.

What `@types` are installed in the [starter project](https://github.com/Psvensso/react-starter)?

For instance, to install typings for react you could do  
`npm install @types/react --save`

Be sure to verify that the @types file is on the same version as the target library file.

For more resources on TypeScript go to their [GitHub Wiki](https://github.com/Microsoft/TypeScript/wiki)

The TSC \(type-script-compiler\) runs in Node so there is where we head of to in the next chapter.

