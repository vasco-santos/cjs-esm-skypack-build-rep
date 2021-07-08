# cjs module with esm first dependency skypack build

> Skypack is failing to build cjs projects where a given dependency exports esm (and other) builds.

This cjs module, which simply requires `multiformats` (exports esm + cjs), aims to replicate the skypack build failure.

## Build content

The skypack build result looks like:

```js
import require$$0 from "/-/multiformats@v9.2.0-7XY1SMf0M7olnt6nKPTy/dist=es2020,mode=imports/optimized/multiformats/cid.js";
const {CID} = require$$0;
var cjsEsmSkypackBuildRep = () => {
  const cid2 = CID.parse("bagaaierasords4njcts6vs7qvdjfcvgnume4hqohf65zsfguprqphs3icwea");
  return cid2;
};
export default cjsEsmSkypackBuildRep;
```

Where `/-/multiformats@v9.2.0-7XY1SMf0M7olnt6nKPTy/dist=es2020,mode=imports/optimized/multiformats/cid.js` source obtained in the browser is:

```js
class CID {
  // ...
}
// ...

export {CID};
```

## Running

Runnable code: https://codepen.io/vascosantos/pen/gOWMbLM

```js
import sth from 'https://cdn.skypack.dev/cjs-esm-skypack-build-rep'
```

Results on

```sh
Uncaught TypeError: Cannot destructure property 'CID' of 'require$$0' as it is null.
    at cjs-esm-skypack-build-rep.js:2
```
