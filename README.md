## aidb-webassembly-demo

🐶[Try Demo](https://www.hulk.show/aidb-webassembly-demo/)

## build and deploy

Prior to starting, make sure you have `cmake` installed.

* 1. Clone ai.deploy.box

```
https://github.com/TalkUHulk/ai.deploy.box.git
cd ai.deploy.box
mkdir build && cd build
```

* 2. Install emscripten

```shell
git clone https://github.com/emscripten-core/emsdk.git
cd emsdk
./emsdk install latest
./emsdk activate latest

source emsdk_env.sh
```

* 3. Build

```shell
cmake .. -DCMAKE_TOOLCHAIN_FILE=$EMSDK/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake -DWASM_FEATURE=basic -DENGINE_NCNN_WASM=ON -DENGINE_MNN=OFF -DENGINE_ORT=OFF -DENGINE_NCNN=OFF -DENGINE_TNN=OFF -DENGINE_OPV=OFF -DENGINE_PPLite=OFF
make -j4

cmake .. -DCMAKE_TOOLCHAIN_FILE=$EMSDK/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake -DWASM_FEATURE=simd -DENGINE_NCNN_WASM=ON -DENGINE_MNN=OFF -DENGINE_ORT=OFF -DENGINE_NCNN=OFF -DENGINE_TNN=OFF -DENGINE_OPV=OFF -DENGINE_PPLite=OFF
make -j4

cmake .. -DCMAKE_TOOLCHAIN_FILE=$EMSDK/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake -DWASM_FEATURE=threads -DENGINE_NCNN_WASM=ON -DENGINE_MNN=OFF -DENGINE_ORT=OFF -DENGINE_NCNN=OFF -DENGINE_TNN=OFF -DENGINE_OPV=OFF -DENGINE_PPLite=OFF
make -j4

cmake .. -DCMAKE_TOOLCHAIN_FILE=$EMSDK/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake -DWASM_FEATURE=simd-threads -DENGINE_NCNN_WASM=ON -DENGINE_MNN=OFF -DENGINE_ORT=OFF -DENGINE_NCNN=OFF -DENGINE_TNN=OFF -DENGINE_OPV=OFF -DENGINE_PPLite=OFF
make -j4
```

* 4. Deploy

Clone the project, create a folder named `aidb` in the root project directory and copy the following files into it:

```
# deploy files
aidb/
├── aidb-wasm-basic.js
├── aidb-wasm-basic.wasm
├── aidb-wasm-simd.js
├── aidb-wasm-simd-threads.js
├── aidb-wasm-simd-threads.wasm
├── aidb-wasm-simd-threads.worker.js
├── aidb-wasm-simd.wasm
├── aidb-wasm-threads.js
├── aidb-wasm-threads.wasm
└── aidb-wasm-threads.worker.js
```

Run local server:

```
python3 server.py
```

* 5. Access local server(chrome as a example)

```
# launch chrome browser, enter following command to address bar and press ENTER:
chrome://flags/#unsafely-treat-insecure-origin-as-secure

# enter following keyword to "Search flags" and press ENTER:
"insecure origins"
you will find "Insecure origins treated as secure" key

#enter local server url and click right side dropdown list, select "Enabled"
url example: http://localhost:12580

#relaunch chrome browser and access http://localhost:12580.
```

## Reference

感谢[nihui](https://github.com/nihui)大佬～

[跑在浏览器里的ncnn和webassembly](https://zhuanlan.zhihu.com/p/305601273)

[ncnn-webassembly-aidb-wasm](https://github.com/nihui/ncnn-webassembly-aidb-wasm)
