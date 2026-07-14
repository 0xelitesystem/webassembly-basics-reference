# The wasm and JavaScript boundary

WebAssembly and JavaScript talk across a narrow, explicit boundary. Wasm exports functions that JavaScript calls, and JavaScript can pass functions in for wasm to call back. They natively exchange only numbers; anything larger, such as strings, arrays, or objects, is passed by sharing wasm's linear memory and agreeing on how to read it. Crossing this boundary has a cost, so good designs cross it rarely with big chunks of work.

## Numbers cross directly

The clean case is numbers. A wasm module can export a function like add(a, b) that takes two integers and returns one. In JavaScript you call it as instance.exports.add(2, 3) and get back 5. The four wasm numeric types map straightforwardly, and these calls are cheap. If your data is numeric and your work is a self-contained calculation, the boundary barely gets in the way.

## Bigger data goes through shared memory

Wasm has a single block of linear memory that JavaScript can also read and write as a typed array. To pass a string, JavaScript writes the bytes into that shared memory, then calls a wasm function with the offset and length; wasm reads the bytes from the same memory. Results come back the reverse way: wasm writes into memory, JavaScript reads the bytes out. Both sides must agree on layout, so tools generate this glue code, but the underlying mechanism is always numbers plus a shared buffer.

## No direct page or network access

Wasm cannot touch the DOM, make a network request, or read storage on its own. Every such action goes through JavaScript. To change the page, wasm computes a result and returns it, and JavaScript updates the DOM. To fetch data, JavaScript fetches and hands the bytes to wasm. Because each crossing has overhead, the winning pattern is coarse-grained: hand wasm a large job, let it run entirely inside its own memory, and read one result out, rather than chattering back and forth for small operations.
