# Running in the browser and WASI

In the browser, WebAssembly runs inside the JavaScript engine: the page fetches a .wasm module, the engine compiles and instantiates it, and JavaScript calls its exported functions. Outside the browser, wasm runs on standalone runtimes, and WASI, the WebAssembly System Interface, gives it a controlled way to touch files, the clock, and other system resources. Same module format, two very different hosts.

## In the browser

A page loads wasm through the browser's WebAssembly API. It fetches the module bytes, the engine compiles them, and instantiation produces an object whose exports are callable from JavaScript like ordinary functions. The wasm module has no direct access to the page, the network, or storage; it only exposes functions and shares a block of memory. JavaScript orchestrates: it hands data in, calls exported functions, and reads results back out.

## Outside the browser with WASI

Wasm is useful beyond the browser as a portable, sandboxed unit of compute, on servers, at the edge, and in plugin systems. But a bare wasm module cannot open a file or read the clock on its own, by design. WASI is a standard set of host functions that a runtime can grant, giving the module a portable way to do system tasks such as reading files or getting the time, without binding it to one operating system.

## Capability-based access

The important part of WASI is that access is granted, not assumed. A runtime hands a module only the specific capabilities it chooses to allow, for example one directory rather than the whole filesystem. A module cannot reach anything it was not explicitly given. This makes wasm plus WASI a strong fit for running untrusted or third-party code on a server: the module gets exactly the doors you open and no others, which is a stronger default than most native processes.
