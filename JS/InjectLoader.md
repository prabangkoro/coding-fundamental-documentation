# Inject-Loader

npm [package](https://www.npmjs.com/package/inject-loader)

## Why
This is particularly useful for writing tests where **mocking things inside your module-under-test** is sometimes necessary before execution.

`inject-loader` was inspired by, and builds upon ideas introduced in `jauco/webpack-injectable`.

## Usage

use inline text within your require => `require('inject-loader!MyModule')`, this will return a function that can used in test code to modify the injected module.

By default all require statements in an injected module will be altered to be replaced with an injector, though if a replacement it not specified the default values will be used.

### Examples

```js
// MyStore.js
 
var Dispatcher = require('lib/dispatcher');
var EventEmitter = require('events').EventEmitter;
var handleAction = require('lib/handle_action');
 
Dispatcher.register(handleAction, 'MyStore');
```

You can manipulate it’s dependencies when you come to write tests as follows:

```js
// If no flags are provided when using the loader then
// all require statements will be wrapped in an injector
MyModuleInjector = require('inject-loader!MyStore')
MyModule = MyModuleInjector({
  'lib/dispatcher': DispatcherMock,
  'events': EventsMock,
  'lib/handle_action': HandleActionMock
})
```