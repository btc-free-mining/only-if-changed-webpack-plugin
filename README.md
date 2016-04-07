
# only-if-changed-webpack-plugin

Webpack plugin to only run build if dependent files have changed

## Example

```js
var path = require('path');

var opts = {
  rootDir: process.cwd(),
  devBuild: process.env.NODE_ENV !== 'production',
};

module.exports = {
  output: {
    filename: 'bundle.js',
    path: path.join(opts.rootDir, 'build'),
    pathinfo: opts.devBuild,
  },
  plugins: [
    new OnlyIfChangedPlugin({
      cacheDirectory: path.join(opts.rootDir, 'tmp/cache'),
      cacheIdentifier: opts, // all variable opts/environment should be used in cache key
    })
  ],
};
```

After an initial build, all subsequent builds will skip compiling and emitting 
assets until a dependent file or output asset of the build is modified or deleted.
