# buyco-client-app-flow-to-ts-strategy

[[app architecture graph]](dependency-graph/app.html)

## Context
buyco-client-app needs to move from flow to TypeScript. Best approach is to replace the `.js` files to `.ts` files from leaves to root. The objectif of the repo is to host and present the dependencies graph of the different modules that could be replaced.

## Graph generation
The project [dependency-cruiser](https://github.com/sverweij/dependency-cruiser) is used to generate the graphs. Run the following in the `buyco-client-app` project to see the dependencies of the module `packages/app/src/Modal`:

```bash
npx depcruise --progress  -x node_modules --config .dependency-cruiser.js  --output-type dot --include-only \"^packages/app/src\" --  packages/app/src/Modal | dot -T svg  | depcruise-wrap-stream-in-html > dependencygraph.html
```

The config file `.dependency-cruiser.js` can be found in this repo [here](.dependency-cruiser.js).
The graph will be generated as a HTML file named `dependencygraph.html`.

## Strategy
The following list orders the modules to be replaced (the order must be respected).

1. packages/app/src/DateTime [[graph]](dependency-graph/DateTime.html)
2. packages/app/src/i18n [[graph]](./dependency-graph/I18n.html)
3. packages/app/src/StorageModule
4. packages/app/src/Modal [[graph]](dependency-graph/Modal.html)
5. **/*.i18n.js (≃10 files)
6. packages/app/src/Notification/models [[graph]](dependency-graph/Notification.html)
7. packages/app/src/Me/models [[graph]](dependency-graph/Me.html)
8. 