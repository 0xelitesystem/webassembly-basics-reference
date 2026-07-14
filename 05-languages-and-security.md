# Languages and security

Many languages compile to WebAssembly, with Rust, C, and C plus plus among the most common, alongside Go, AssemblyScript, and others. Wasm's safety comes from its sandbox: a module runs in an isolated memory space, cannot reach the host except through functions it was explicitly given, and is validated before it runs. That containment is what makes running untrusted web code practical.

## Languages that compile to wasm

Systems languages fit best because they compile to compact, fast modules without a heavy runtime. Rust is popular for its strong tooling and safety, C and C plus plus for reusing decades of existing libraries, and Go and others are supported with varying runtime overhead. AssemblyScript offers a TypeScript-like syntax that compiles to wasm directly. Languages that need a large garbage-collected runtime can target wasm too, but the module ships more baggage.

## The sandbox

A wasm module executes in a sandbox with its own linear memory, separate from the host and from other modules. It cannot read or write host memory, cannot see other modules' memory, and cannot call into the operating system on its own. Its only outward reach is the set of imported functions the host chose to provide. If the host imports nothing, the module can only compute and return values. This deny-by-default posture is the heart of wasm security.

## Validation and its limits

Before execution, the engine validates the module against strict structural and type rules, rejecting anything malformed, so a broken or malicious module fails to load rather than misbehaving. Memory access is bounds-checked against the module's own linear memory, so a stray access cannot escape into the host. The honest limit: the sandbox protects the host from the module, but it does not make the code inside correct. A bug in the source, such as a logic error or a mishandled input, still produces a wrong answer; it just cannot break out of the sandbox to harm the host.
