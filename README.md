# Elm loader [![Version](https://img.shields.io/npm/v/elm-webpack-loader.svg)](https://www.npmjs.com/package/elm-webpack-loader) [![Travis build Status](https://travis-ci.org/rtfeldman/elm-webpack-loader.svg?branch=master)](http://travis-ci.org/rtfeldman/elm-webpack-loader) [![AppVeyor build status](https://ci.appveyor.com/api/projects/status/7a5ws36eenwpdvgc/branch/master?svg=true)](https://ci.appveyor.com/project/rtfeldman/elm-webpack-loader/branch/master)

Webpack loader for the [Elm](http://elm-lang.org/) programming language.


## Installation

```sh
$ npm install --save elm-webpack-loader
```


## Usage

[Documentation: Using loaders](http://webpack.github.io/docs/using-loaders.html)

In your `webpack.config.js` file:

```js
module.exports = {
  module: {
    loaders: [{
      test: /\.elm$/,
      exclude: [/elm-stuff/, /node_modules/],
      loader: 'elm-webpack'
    }]
  }
};
```

See the [examples](#example) section below for the complete webpack configuration.

### Options

#### Cache (default false)

You can add `cache=true` to the loader:

```js
  ...
  loader: 'elm-webpack?cache=true'
  ...
```

If you add this, when using `npm run watch`, the loader will only load the
dependencies at startup. This could be performance improvement, but know that
new files won't be picked up and so won't be watched until you restart webpack.

This flag doesn't matter if you don't use watch mode.

#### cwd (default null)

You can add `cwd=elmSource` to the loader:
```js
var elmSource = __dirname + '/elm/path/in/project'
  ...
  loader: 'elm-webpack?cwd=' + elmSource
  ...
```

You can use this to specify a custom location within your project for your elm files. Note, this
will cause the compiler to look for **all** elm source files in the specified directory.

#### Upstream options

All options are sent down as an `options` object to node-elm-compiler. For example, you can explicitly pick the local `elm-make` binary by setting the option `pathToMake`:

```js
  ...
  loader: 'elm-webpack?pathToMake=node_modules/.bin/elm-make',
  ...
```

For a list all possible options, [consult the source](https://github.com/rtfeldman/node-elm-compiler/blob/5a4cc71/index.js#L11-L19).

## Notes

### Example

You can find an example in the `example` folder.
To run:

```
npm install
npm run build
```

You can have webpack watch for changes with: `npm run watch`

You can run the webpack dev server with: `npm run dev`

For a full featured example project that uses elm-webpack-loader see [pmdesgn/elm-webpack-starter](https://github.com/pmdesgn/elm-webpack-starter) .

### noParse

Webpack can complain about precompiled files (files compiled by `elm-make`).
You can silence this warning with [noParse](https://webpack.github.io/docs/configuration.html#module-noparse). You can see it in use in the example.

```js
  module: {
    loaders: [...],
    noParse: [/.elm$/]
  }
```

## Revisions

### 3.0.0

Support Elm 0.17, and remove obsolete `appendExport` option.

### 2.0.0

Change `warn` to be a pass-through compiler flag rather than a way to specify
logging behavior.

### 1.0.0

Initial stable release.
