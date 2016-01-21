# babel-runtime-wtf

_(Should have been named babel-register-wtf, whoops)_

## What am I doing wrong with babel-register?

* Issue filed at <https://phabricator.babeljs.io/T7018>

```bash
$ npm install
...

# This error doesn't make sense to me. Why is the initial line number 3? Why
# does the code example show the transpiled code (var x = y;) instead of the
# original code (let x = y)?

$ node -r babel-register ./index
/private/tmp/test/index.js:3
var x = y;
        ^

ReferenceError: y is not defined
    at Object.<anonymous> (index.js:1:9)
    at Module._compile (module.js:435:26)
    at loader (/private/tmp/test/node_modules/babel-register/lib/node.js:130:5)
    at Object.require.extensions.(anonymous function) [as .js] (/private/tmp/test/node_modules/babel-register/lib/node.js:140:7)
    at Module.load (module.js:356:32)
    at Function.Module._load (module.js:311:12)
    at Function.Module.runMain (module.js:467:10)
    at startup (node.js:134:18)
    at node.js:961:3

# If I compile index.js to compiled.js and then (in a separate step) run the
# compiled code with sourcemap support, I get the stack trace I'm looking for.
# Why don't I see this when compiling on-the-fly with babel-register?

$ ./node_modules/.bin/babel --source-maps inline index.js --out-file compiled.js

$ node -r source-map-support/register ./compiled

index.js:1
let x = y
        ^
ReferenceError: y is not defined
    at Object.<anonymous> (index.js:1:9)
    at Module._compile (module.js:435:26)
    at Object.Module._extensions..js (module.js:442:10)
    at Module.load (module.js:356:32)
    at Function.Module._load (module.js:311:12)
    at Function.Module.runMain (module.js:467:10)
    at startup (node.js:134:18)
    at node.js:961:3
```
