## The issue

First, to prove that everything works without paths, we have `index1.ts`
which imports like this:

`import { Greeter } from "./src/lib/greeter/index.js";`

When we run the code:

```bash
NODE_OPTIONS="--loader ts-node/esm" node index1.ts
```

you'll see an output like this:

```bash
this is something Hello There
```

Then, we have `index2.ts`, which imports like this:

`import { Greeter } from "$lib/greeter/index.js";`

When we run this code:

```bash
NODE_OPTIONS="--loader ts-node/esm" node index2.ts
```

it gives:

```bash
/home/marko/dev/ts-node-tsconfig-path-debug/node_modules/ts-node/dist-raw/node-esm-resolve-implementation.js:774
  throw new ERR_MODULE_NOT_FOUND(packageName, fileURLToPath(base));
        ^
CustomError: Cannot find package '$lib' imported from /home/marko/dev/ts-node-tsconfig-path-debug/index2.ts
    at packageResolve (/home/marko/dev/ts-node-tsconfig-path-debug/node_modules/ts-node/dist-raw/node-esm-resolve-implementation.js:774:9)
    at moduleResolve (/home/marko/dev/ts-node-tsconfig-path-debug/node_modules/ts-node/dist-raw/node-esm-resolve-implementation.js:815:18)
    at Object.defaultResolve (/home/marko/dev/ts-node-tsconfig-path-debug/node_modules/ts-node/dist-raw/node-esm-resolve-implementation.js:929:11)
    at /home/marko/dev/ts-node-tsconfig-path-debug/node_modules/ts-node/src/esm.ts:228:33
    at entrypointFallback (/home/marko/dev/ts-node-tsconfig-path-debug/node_modules/ts-node/src/esm.ts:179:34)
    at resolve (/home/marko/dev/ts-node-tsconfig-path-debug/node_modules/ts-node/src/esm.ts:227:12)
    at Loader.resolve (node:internal/modules/esm/loader:89:40)
    at Loader.getModuleJob (node:internal/modules/esm/loader:242:28)
    at ModuleWrap.<anonymous> (node:internal/modules/esm/module_job:73:40)
    at link (node:internal/modules/esm/module_job:72:36)```
