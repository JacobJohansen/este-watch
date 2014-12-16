# este-watch [![Build Status](https://secure.travis-ci.org/steida/este-watch.png?branch=master)](http://travis-ci.org/steida/este-watch) [![Dependency Status](https://david-dm.org/steida/este-watch.png?theme=shields.io)](https://david-dm.org/steida/este-watch)

> Fast and reliable Node.js files watcher.

- It's fast, because it wraps fs.watch which does not use pooling.
- It's reliable, because it supports only that behavior that works reliable across all OS's.

## Why yet another file watcher?

There are zilions Node.js file watchers. No one is perfect. The most feature rich is probably [gaze](https://github.com/shama/gaze), but it burns CPU because it uses pooling fs.watchFile. 
This watcher uses only fs.watch so it has limited functionality (can't detect deleted files), but it works. And it's fast
even for thousands of files. Read more [here](https://github.com/wearefractal/glob-watcher/issues/1#issuecomment-31232567) and [here](http://tech.nitoyon.com/en/blog/2013/10/10/grunt-watch-slow/).

## Basic Usage

Create a watcher to watch all files in the directories "foo" and "bar":

```javascript
function onWatch(file) {
  // Relative path to file that was changed or created
  console.log(file.filepath);

  // File Extension
  console.log(file.extension);
}

var esteWatch = require('este-watch');

var watcher = esteWatch(['foo', 'bar'], onWatch);

// Start the watcher
watcher.start()
```

## Options

A third argument can be passed to the esteWatch function to specify options.

Three options are available:

* filter: (RegExp) only fire watcher callback for files where the full relative filepath matches this pattern
* ignoreFiles: (RegExp) prevent watcher callback from firing for files where the full relative filepath matches this pattern
* ignoreDirectories: (RegExp) prevent watcher from even starting for directories where the full relative directory path matches this pattern

```javascript
esteWatch(['foo', 'bar'], onWatch, {
  filter: /\.js$/,
  ignoreFiles: /\.min\.js$/,
  ignoreDirectories: /node_modules/,
}).start();
```
