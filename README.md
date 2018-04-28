# Relay Compiler Webpack Plugin

[![npm version](https://badge.fury.io/js/relay-compiler-webpack-plugin.svg)](https://badge.fury.io/js/relay-compiler-webpack-plugin)
[![Build Status](https://travis-ci.org/danielholmes/relay-compiler-webpack-plugin.svg?branch=master)](https://travis-ci.org/danielholmes/relay-compiler-webpack-plugin)

Are you running Relay Modern? Are you annoyed with constantly running the `relay-compiler` to generate code, especially if you're already running Webpack?

Well be annoyed no more! Simply install this plugin to automatically hook into Webpack's build process to generate these files for you.

## Installation

  1. Add this to your project:

```sh
  yarn add --dev relay-compiler-webpack-plugin
  # Or if you're using npm
  npm install --save-dev relay-compiler-webpack-plugin
```

  2. Add the plugin to your Webpack configuration:
  
```javascript
const RelayCompilerWebpackPlugin = require('relay-compiler-webpack-plugin')
const path = require('path')

module.exports = {
  // ... Your existing Webpack configuration
  plugins: [
    // ...
    new RelayCompilerWebpackPlugin({
      schema: path.resolve(__dirname, './relative/path/to/schema.graphql'), // or schema.json or a GraphQLSchema instance
      src: path.resolve(__dirname, './relative/path/to/source/files'),
    })
  ]
  // ...
}
```

  3. :tada:

### Gotchas

If there are multiple versions of GraphQL in your dependency tree it will cause schema validation errors. To get around
this, ensure you have the same graphql version as your relay-compiler version depends on. To assist this you can 
[install dependencies as flat](https://yarnpkg.com/lang/en/docs/cli/install/#toc-yarn-install-flat) which ensures only 
one version of each dependency.
  
### TODOs

Currently, the `relay-compiler` is undergoing a lot of work.
Various modules required by this library aren't modular enough to truly inject the generated files into Webpack's file hierarchy.
We'll be working with the `relay-compiler` to make it more modular in this regard as well as updating this project accordingly.

However it is still better than manually running the `relay-compiler` whenever anything changes.
Currently Webpack may build a few times once it picks up the files generated by this plugin.

 - Set up some tests. See [lodash webpack plugin](https://github.com/lodash/lodash-webpack-plugin/blob/master/.travis.yml)
   for example of testing with multiple webpack versions

## License

Relay Compiler Webpack Plugin may be redistributed according to the [BSD 3-Clause License](LICENSE).

Copyright 2018
