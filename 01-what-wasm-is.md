# What wasm is

WebAssembly is a compact binary instruction format that runs on a stack-based virtual machine at close to native speed. It is a compilation target: you write code in a language like Rust or C, compile it to a .wasm module, and any host with a wasm engine can run it. The problem it solves is giving the web, and other sandboxed hosts, a fast, portable, low-level target that is not tied to JavaScript.

## A compilation target, not a language

Nobody writes WebAssembly by hand for real work. It is the output of a compiler, the same role that machine code plays for a native program, except wasm stays portable across machines. The module is a stream of typed instructions operating on a virtual stack, plus a chunk of linear memory. Because the format is low-level and predictable, engines can validate and compile it quickly.

## Near-native speed

Wasm runs fast for two reasons. Its instructions map cleanly onto real processor operations, so the engine can turn them into machine code with little overhead. And it uses simple numeric types and a flat block of memory, avoiding the dynamic type checks and garbage-collection pauses that general scripting incurs. The result is predictable performance suited to tight numeric loops.

## Portable and validated

A single .wasm file runs unchanged on any compliant engine, whether in a browser on Windows, a browser on a phone, or a server runtime. Before running, the engine validates the module against strict rules, rejecting malformed or unsafe modules up front. This combination, one portable binary plus mandatory validation, is what lets untrusted code from the web run quickly without putting the host at risk, which the security section covers in more detail.
