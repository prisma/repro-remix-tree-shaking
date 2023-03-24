# Tree Shaking Bug (?)

This repro repo shows how Remix does not tree shake correctly (?) the server build.

The module `do-not-import-me` should be totally ignored by `remix build`, but it is not, leading to a an error about a node module being imported. Example

```
> npm run build
> remix build

Building Remix app in production mode...

✘ [ERROR] Could not resolve "node:perf_hooks"

    some-lib/do-not-import-me.ts:1:32:
      1 │ import { createHistogram } from 'node:perf_hooks'
        ╵                                 ~~~~~~~~~~~~~~~~~

  The package "node:perf_hooks" wasn't found on the file system but is built into node. Are you trying to bundle for node? You can use "platform: 'node'" to do that, which will remove this error.


Build failed with 1 error:
some-lib/do-not-import-me.ts:1:32: ERROR: Could not resolve "node:perf_hooks"
Error
    at Object.onCompileFailure (/Users/jasonkuhrt/projects/prisma/repro-remix-tree-shaking/node_modules/@remix-run/dev/dist/cli/commands.js:193:13)
    at Object.compile (/Users/jasonkuhrt/projects/prisma/repro-remix-tree-shaking/node_modules/@remix-run/dev/dist/compiler/remixCompiler.js:45:134)
    at processTicksAndRejections (node:internal/process/task_queues:96:5)
    at async Object.build (/Users/jasonkuhrt/projects/prisma/repro-remix-tree-shaking/node_modules/@remix-run/dev/dist/compiler/build.js:33:3)
    at async Object.build (/Users/jasonkuhrt/projects/prisma/repro-remix-tree-shaking/node_modules/@remix-run/dev/dist/cli/commands.js:188:3)
    at async Object.run (/Users/jasonkuhrt/projects/prisma/repro-remix-tree-shaking/node_modules/@remix-run/dev/dist/cli/run.js:456:7)
```
