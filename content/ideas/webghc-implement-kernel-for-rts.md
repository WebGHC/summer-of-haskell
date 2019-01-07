---
title: WebGHC- Implement kernel execution environment to run RTS in WebAssembly / JavaScript
---

The [WebGHC][1] compiler has been able to create a working `wasm` executable, and even communicate with the browser using `jsaddle` library.
But so far the effort has been to try out a proof of concept and weed out potential issues.
Now it is required to create a proper kernel environment for haskell runtime, which works on the browser and non-browser environment (using `node`).

The idea will be to create a kernel in `TypeScript` which runs in the main thread, and communicates / controls the execution of `wasm` executable running in a worker thread.
This will involve creating communication channels and control structures to do data transfer between the threads, provide system level APIs like file read/write, polling, etc.

The work will be mainly in `TypeScript`/ `JavaScript`, occasionally hacking `RTS`, the compilation toolchain or the haskell compiler.
The intention here is to, as much as possible, reuse the existing `RTS` and `ghc` code, but occasionaly there might be need to do some modification.

Since it is expected that the `wasm` executable also runs in batch mode using `node`, it should be possible to run the test-suite of `ghc`, and other libraries.
This will provide a way to ensure the haskell compiler, `RTS` and kernel are working correctly.

Important resources to study for this project are the [WebAssembly][2], [Web Workers][3], and [Kernel system call APIs][4]

Mentors: Will Fancher, Divam Narula

Difficuly: Intermediate

[1]: https://github.com/WebGHC/wasm-cross/wiki
[2]: https://developer.mozilla.org/en-US/docs/WebAssembly
[3]: https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API
[4]: http://man7.org/linux/man-pages/dir_section_2.html
