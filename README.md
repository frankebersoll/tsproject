﻿[![npm version](https://badge.fury.io/js/tsproject.svg)](http://badge.fury.io/js/tsproject)
# TsProject
TsProject is a Typescript bundle compiler which utilizes the Typescript project configuration file, tsconfig.json, to provide a compilation context for source files, module bundles and compile options.

TsProject produces a compiled output stream of vinyl files for further processing in the gulp build pipeline.

## Top Features

* Bundling of ES6 external Typescript modules
* Bundle minification with identifier shortening and whitespace removal
* Cache optimized incremental project builds
* File glob pattern matching for project files
 
## What's New

TsProject 1.2.0 supports Typescript 1.8.x.

TsProject 1.2.0 provides bundle minification by shortening identifiers and whitespace removal.

TsProject 1.2.0 provides bundle packaging support for library and component types.

TsProject 1.1.0 provides project watch support for cache optimized, incremental builds.

TsProject 1.1.0 supports Typescript 1.7!

TsProject 1.0.5 provides file glob pattern matching for specifying "files" in the tsconfig.json project file.

TsProject 1.0.5 is used to build TsProject. TsProject is a bundled, single file node module using ES6 module imports.

TsProject 1.0.1 bundles React (.tsx) file types. TsProject on github contains a [React based TodoMVC sample](https://github.com/ToddThomson/tsproject/tree/master/ReactTodoMVC) to help you get started.

## Why TsProject?

TsProject provides 2 new features:

1. **A single Typescript project build context**. TsProject uses the new tsconfig.json Typescript project file introduced in Typescript version 1.5 to configure source files, bundles and compile options.

2. **Single file typescript bundles and javascript bundles for packaging of Typescript, javascript and Typescript definition files**. TsProject bundles file dependencies of external Typescript modules at compilation time rather than relying on build tools (AMD Optimizer, r.js for example ) further down in the build pipeline.

## TsProject Wiki

Additional details can be found on the TsProject [wiki](https://github.com/ToddThomson/tsproject/wiki).

## Typescript ES6 External Module Bundles

TsProject supports a "bundles" property within the tsconfig.json project file. The "bundles" property may contain a list of named bundles. Each bundle must provide an array of source files and may optionally specify bundle configuration settings. 
The Typescript source file and its dependencies are packaged as a single Typescript file and output with the bundle name. The Typescript bundle is compiled to a single js javascript file and a single d.ts declaration file.

The following is a sample tsconfig.json showing the "bundles" property:

```
{
    "compilerOptions": {
        "module": "amd",
        "target": "es5",
        "noResolve": false,
        "declaration": true,
        "diagnostics": true
    },

    "files": [
        "index.ts",
        "page.ts",
        "common.ts",
		"plugin.ts"
    ],
    
    "bundles": {
        "app": {
            "files": [ "index.ts" ]
        },
        "components": {
            "files": [
                "page.ts",
                "plugin.ts"
            ],
            "config": {
			    "declaration": true,
                "outDir": "./bundles",
				"minify": true  
            }
        }
    }
}
```

## How to install

```
npm install tsproject
```

## API

    tsproject.src( projectConfigPath: string, settings: any )

Where:

**projectConfigPath** is a relative directory path to the default Typescript project file named "tsconfig.json".
Or,
**projectConfigPath** is a relative path to a named Typescript project file.   

## Usage - Gulp Build Pipeline

TsProject on github contains a [TodoMVC sample](https://github.com/ToddThomson/tsproject/tree/master/TsProjectTodoMVC) to help you get started.
The sample is built using Angular, Typescript ES6 modules and Require.

Here is a simple gulpfile.js:

```
var tsproject = require( 'tsproject' );
var gulp = require( 'gulp' );
gulp.task( 'build', function() {

    // path to directory of tsconfig.json provided
    tsproject.src( './src/project' )
        .pipe(gulp.dest('./build'));

    // path to named configuration file provided and optional settings specified 
    return tsproject.src( './src/project_a/myconfig.json',
		{ 
			logLevel: 1,
			compilerOptions: {
				listFiles: true
			} 
		})
        .pipe( gulp.dest( './mybuild' ) );

});
```

## Building TsProject

TsProject depends on [NPM](https://docs.npmjs.com/) as a package manager and 
[Gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md) as a build tool. 
If you haven't already, you'll need to install both these tools in order to 
build TsProject.

Once Gulp is installed, you can build it with the following commands:

```
npm install
gulp build
```  

