# wasm
```
./build.sh
cp em.js wasmminer.js wasmminer.wasm worker.js ../../wasmminer/js
```

## how to emcc

```
wget 'https://s3.amazonaws.com/mozilla-games/emscripten/releases/emsdk-portable.tar.gz' | tar xzf -
cd emsdk-portable
./emsdk update
./emsdk install latest
./emsdk activate latest
source ./emsdk_env.sh
```

