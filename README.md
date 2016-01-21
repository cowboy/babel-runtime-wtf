# babel-runtime-wtf

## What am I doing wrong with babel-runtime?

```bash
$ npm install
...

# This makes sense to me:

$ node ./index
/private/tmp/test/index.js:1
(function (exports, require, module, __filename, __dirname) { let x = y
                                                              ^^^

SyntaxError: Block-scoped declarations (let, const, function, class) not yet supported outside strict mode
    at exports.runInThisContext (vm.js:53:16)
    at Module._compile (module.js:414:25)
    at Object.Module._extensions..js (module.js:442:10)
    at Module.load (module.js:356:32)
    at Function.Module._load (module.js:311:12)
    at Function.Module.runMain (module.js:467:10)
    at startup (node.js:134:18)
    at node.js:961:3

# This doesn't make sense to me. Why is the initial line number 3? Why does the
# code example show the transpiled code (var x = y;) instead of the original
# code (let x = y)?

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
```
