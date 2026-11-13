# WebAssembly Basics

A plain-language reference on WebAssembly, or wasm. It covers what wasm is, how it runs in the browser and outside it through WASI, the boundary between wasm and JavaScript, when wasm helps versus when plain JavaScript is the better choice, which languages compile to it, and how its sandbox keeps code contained. It is honest about what wasm is not.

## The core idea

WebAssembly is a compact binary instruction format that runs at near-native speed inside a safe sandbox, giving the web a fast compilation target for languages other than JavaScript. It is not a replacement for JavaScript; it runs alongside it, shines at CPU-heavy work, and reaches the page and the network only by calling into JavaScript. Think of it as a fast engine you drop in for the heavy lifting, wired to the rest of the app through a deliberate boundary.

## What is inside

- [01-what-wasm-is.md](01-what-wasm-is.md) the binary format, the virtual machine, and what problem it solves.
- [02-running-in-browser-and-wasi.md](02-running-in-browser-and-wasi.md) how wasm loads in the browser and runs outside it.
- [03-the-wasm-js-boundary.md](03-the-wasm-js-boundary.md) how wasm and JavaScript pass data and calls.
- [04-when-wasm-helps-and-when-not.md](04-when-wasm-helps-and-when-not.md) the honest trade-offs on speed and complexity.
- [05-languages-and-security.md](05-languages-and-security.md) what compiles to wasm and how the sandbox contains it.

## The stance

This reference treats wasm as a specialized tool, not a silver bullet. It is excellent for compute-bound work and for reusing existing native code on the web, and it is beside the point for ordinary interface code. Reaching for it where plain JavaScript would do adds a boundary and a build step for no gain.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Copyright RBL Industries LLC 2026.
