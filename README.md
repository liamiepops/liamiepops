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
