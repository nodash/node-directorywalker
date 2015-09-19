DirectoryWalker for NodeJS
==========================

[![Build Status](https://travis-ci.org/scravy/node-directorywalker.svg)](https://travis-ci.org/scravy/node-directorywalker)

Walk directories recursively and event based.

Usage
-----

    npm install --save directorywalker

Example:

```JavaScript
var DirectoryWalker = require('directorywalker');
var walker = new DirectoryWalker({ /* optional options object */ });

walker.on('file', function (file) { console.log(file); });

walker.walk(__dirname);
```

API
---

### Options

    fileFilter: function (path, callback(err, boolean))

The `fileFilter` is invoked every time a file is encountered.
If the result (gathered asynchronously, the callback takes an error as
its first argument and the verdict as its second argument) is trueish
the `file` event will be emitted for the given file.

    dirFilter: function (path, callback(err, boolean))

The `dirFilter` is invoked every time a dir is encountered.
If the result (gathered asynchronously, the callback takes an error as
its first argument and the verdict as its second argument) is trueish
the `dir` event will be emitted for the given file. **If the event is
not trueish, the event will not be emitted and
_the directory will not be descended into_.**

### Events

```JavaScript
walker.on('file', function (path) { ... })
```

Emitted each time a file is encountered and accepted by
the `fileFilter` (if any).

```JavaScript
walker.on('dir', function (path) { ... })
```

Emitted each time a directory is encountered and accepted by
the `dirFilter` (if any).

```JavaScript
walker.on('error', function (path, err) { ... })
```

Emitted each time an error occurs (for example when statting a file,
invoking a filter, ...).

```JavaScript
walker.on('entry', function (path) { ... })
```

Emitted each time a directory entry (be it a file, a directory,
anything) is encountered.

```JavaScript
walker.on('stats', function (path, stats) { ... })
```

Emitted each time a directory entry is statted. The event also
carries the stats for that directory entry.

