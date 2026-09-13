### Liam O'Callaghan

Software engineer in Berlin. Most of my recent work is on language bindings and numerical models.

### Open source, 2026

- **[Mozilla, UniFFI bindings generator](https://github.com/mozilla/uniffi-rs/pull/2966).** UniFFI generates the bindings that let Firefox ship one Rust codebase to both Android and iOS. Fixed a code generation fault in the Kotlin and Swift backends that emitted source which would not compile, closing [an issue open since January 2025](https://github.com/mozilla/uniffi-rs/issues/2411).
- **[Qdrant, core repo](https://github.com/qdrant/qdrant/pull/10209).** A vector database with 34,000 stars, run as infrastructure under AI search and retrieval products. Fixed a build failure that stopped the project compiling at all on RISC-V, s390x and WebAssembly.
- **[uniffi-bindgen-react-native](https://github.com/jhugman/uniffi-bindgen-react-native/pull/438).** UniFFI carried to TypeScript for React Native, Node and the browser, funded by Mozilla, LiveKit and Filament. Fixed the same class of fault in the TypeScript generator, found while generating bindings for a 12,000 line interface.
- **[Prisma, documentation site](https://github.com/prisma/web).** Their Cloudflare deployment guide had regressed to a deprecated setting during a documentation migration. Traced it to the commit that lost the original fix and restored it.
- **[Qdrant Edge, Node.js bindings](https://github.com/qdrant/qdrant/issues/10226).** Built and demonstrated end to end: shard creation, write, read, close, and reopen from disk. Awaiting a decision from the maintainers on which language bindings belong in the core repository.

### Projects

**[geothermal-thermo-hydraulic-model](https://github.com/liamiepops/geothermal-thermo-hydraulic-model)**

Five coupled models in Python covering coolant-loop heat export, quench fracturing, drilling-thermal optimisation, hole stability under cooling and breakout from the ground reaction curve. The models are low-dimensional and mostly quasi-steady, solving as boundary-value problems across the coupled heat and stress fields, with water properties from IAPWS-95.

Run against four European provinces, it clears Pannonian Basin and Larderello, passes Upper Rhine Graben on conditions, and rules out United Downs, where anisotropy exceeds the fracture gradient. Those verdicts come from the limits the models find: conduction caps a closed-loop well near 3 to 4 MW, cold-quench spallation works only in low-stress extensional crust below the brittle-ductile transition, and elsewhere lowers the cutting energy without breaking the rock, and past a certain depth the rock closes the hole through stress anisotropy before heat becomes the problem. These are order-of-magnitude models, built to find where a site becomes economically viable.

**[Langsammm](https://github.com/liamiepops/Langsammm)**

Plays music three semitones slower and lower, then puts the voices back. Slowing normally drags vocal resonance down with the pitch and singers sound slurred. Lifts the spectral envelope back where it started while leaving the pitch down.

The DSP is Rust compiled to WebAssembly, 40KB with no dependencies, and runs inside a Web Audio AudioWorklet. It takes a cepstral envelope of each frame and applies a per-bin real gain to the original spectrum, leaving the phases alone. Ships for Chrome and Firefox 128+, [published on addons.mozilla.org](https://addons.mozilla.org/en-US/firefox/addon/langsammm/).

**[vaultbench](https://github.com/liamiepops/vaultbench)**

Five embedded vector search engines at personal-knowledge-base scale, measured on latency, memory, disk and recall against exact ground truth, across 1k, 10k and 100k document sample sets.

A plain array scan beats two of the four indexed engines above 1,000 documents. One engine's default configuration returns half the expected recall, with nothing in the output to indicate it. At 100k chunks Qdrant Edge answers in 0.52ms and stays exact, where brute force takes 32.66ms.

**[portcall](https://github.com/liamiepops/portcall)**

Ran Prisma 7 through the same eleven steps on Node, Bun, Deno and Cloudflare `workerd`. All four returned byte-identical output, which stops being interesting once you notice they load the same WASM query compiler. Cloudflare Workers was the exception: its default client imports `node:process` at module scope, so that target needs a generator block of its own.
