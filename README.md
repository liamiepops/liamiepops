### Liam O'Callaghan

Software engineer in Berlin. Most of my recent work is on language bindings and generated code.

### Pull requests merged, 2026

- [mozilla/uniffi-rs#2966](https://github.com/mozilla/uniffi-rs/pull/2966). Escaping `/*` and `*/` in generated Kotlin and Swift docstrings. Closed [#2411](https://github.com/mozilla/uniffi-rs/issues/2411), open since January 2025.
- [qdrant/qdrant#10209](https://github.com/qdrant/qdrant/pull/10209). `cc::Build::compile()` ran on targets with no SIMD source file, so the build failed before any Rust compiled. Affects `riscv64`, `s390x`, `powerpc64le`, 32-bit `arm` without NEON, and `wasm32`.
- [jhugman/uniffi-bindgen-react-native#438](https://github.com/jhugman/uniffi-bindgen-react-native/pull/438). The same escaping bug in the TypeScript backend. Found through 401 errors in one 12,000 line generated file.

Open: a documentation fix at [prisma/web](https://github.com/prisma/web), and [qdrant/qdrant#10226](https://github.com/qdrant/qdrant/issues/10226), Node bindings for Qdrant Edge, waiting on a maintainer decision.

### Projects

**[vaultbench](https://github.com/liamiepops/vaultbench)**. Five embedded vector search engines at 1k, 10k and 100k chunks of real markdown, recall measured against exact brute force. At 100k, Qdrant Edge queries in 0.52ms and stays exact; brute force takes 32.66ms. A plain array scan beats sqlite-vec and Orama above 1,000 chunks, and LanceDB's default index returns recall@10 of 0.500 without saying so.

**[portcall](https://github.com/liamiepops/portcall)**. Prisma 7 across Node, Bun, Deno and Cloudflare `workerd`. All four agree, because all four load the same WASM query compiler. The Workers target needs a second generator block, since the default client imports `node:process` at module scope.

**[Langsammm](https://github.com/liamiepops/Langsammm)**. A browser extension that plays music three semitones slower and lower, then puts the voices back. Slowing drags the spectral resonances down along with the pitch, so this lifts the envelope back where it started and leaves the pitch where it fell. Rust compiled to WebAssembly, around 40KB with no dependencies, running in an AudioWorklet. The envelope correction is a per-bin real gain on the original spectrum with the phases left alone, which is why transients survive it. Chrome and Firefox 128+, [published on addons.mozilla.org](https://addons.mozilla.org/en-US/firefox/addon/langsammm/).

**[geothermal-thermo-hydraulic-model](https://github.com/liamiepops/geothermal-thermo-hydraulic-model)**. Coupled physical models in Python for the questions that decide whether a deep or superhot-rock geothermal well is drillable, survivable, stable and worth the energy, with a tool that scores real candidate sites against all of them. IAPWS-95 water properties, 1-D and axisymmetric quasi-steady formulations, boundary-value solves for the coupled heat and stress fields. Closed-loop power comes out conduction-limited at roughly 3 to 4 MW, cold-quench drilling only survives in low-stress extensional crust, and at depth stress anisotropy binds hole stability before temperature does. Four European provinces scored: Pannonian Basin and Larderello go, Upper Rhine Graben conditional, United Downs no-go on stress anisotropy exceeding the fracture gradient. Order-of-magnitude models, built to locate binding constraints.
