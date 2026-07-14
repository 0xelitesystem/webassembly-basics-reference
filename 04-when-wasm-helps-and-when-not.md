# When wasm helps and when not

WebAssembly helps most for CPU-heavy work: sustained numeric computation where predictable speed matters and where the job can run in a tight loop without constantly crossing back to JavaScript. For ordinary interface code, event handling, DOM updates, and light logic, plain JavaScript is simpler and usually just as fast. Choosing wasm is a trade of added complexity for compute speed, and it only pays off when there is real compute to speed up.

## Where wasm wins

Good fits are image and video processing, audio and signal work, compression and encryption, physics and simulation, 3D and game engines, and porting an existing C, C plus plus, or Rust library to the web instead of rewriting it. These share a shape: heavy, self-contained computation over numeric data, with few boundary crossings. In that shape wasm delivers steady, near-native throughput that JavaScript's dynamic nature struggles to match.

## Where plain JavaScript wins

For most web code, JavaScript is the right tool. Reading and updating the DOM, wiring up events, calling APIs, and gluing components together are dominated by the boundary and the page, not by raw compute, so wasm adds a build step and a data-marshaling cost for no benefit. JavaScript also has direct DOM and browser access, a huge library ecosystem, and no compile step, which makes it faster to write and easier to debug for interface work.

## The honest trade-off

Wasm is not automatically faster; for boundary-heavy or light-compute code it can be slower once you count the cost of moving data across the wasm and JavaScript line. It adds a toolchain, a compile step, and harder debugging. Reach for it when profiling shows a genuine compute bottleneck or when you have existing native code worth reusing. Otherwise, plain JavaScript is the simpler and often faster choice. Wasm complements JavaScript; it does not replace it.
