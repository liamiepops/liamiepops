# Liam O'Callaghan

I work at the seams between systems. Most of what I fix lives in generated code, where two toolchains have quietly disagreed for a year and the compiler is the first one to mention it.

I studied applied mathematics before I wrote software for a living, and I work from Berlin.

## Upstream, 2026

**Escaping comment markers in Kotlin and Swift docstrings.** [mozilla/uniffi-rs#2966](https://github.com/mozilla/uniffi-rs/pull/2966), merged August 2026.

Rust doc comments were emitted straight into generated `/** ... */` blocks with no escaping, so a `*/` in the source closed the docstring early and a `/*` opened one that never closed, taking the rest of the file with it. Both languages allow nested `/* ... */`, so it only broke when a marker had no partner, which is part of why it lasted as long as it did. Closed [#2411](https://github.com/mozilla/uniffi-rs/issues/2411), open since January 2025.

**Building Qdrant on architectures with no SIMD backend.** [qdrant/qdrant#10209](https://github.com/qdrant/qdrant/pull/10209), merged August 2026.

`lib/quantization/build.rs` called `cc::Build::compile()` outside its architecture branching, so on any target without a SIMD source file the archiver ran against an object that was never created. The build died before a single line of Rust compiled. Reproduced on `riscv64gc-unknown-linux-gnu`, and it also reaches `s390x`, `powerpc64le`, 32-bit `arm` without NEON, and `wasm32`.

**The same defect in the TypeScript generator, where it does more damage.** [jhugman/uniffi-bindgen-react-native#438](https://github.com/jhugman/uniffi-bindgen-react-native/pull/438), merged August 2026.

TypeScript has no nested block comments, so one stray `*/` runs to the end of the file. This surfaced while I was generating Node bindings for `qdrant-edge-ffi`: 401 TypeScript errors spread across a 12,000 line generated file, all of them traceable to a single docstring.

**A documentation fix that a migration ate.** [prisma/web](https://github.com/prisma/web), open.

The Cloudflare deployment page still told you to set `node_compat = true`, which Cloudflare had deprecated, while Prisma's own newer guide already used `nodejs_compat`. It had been fixed correctly in February and lost nine days later when the docs moved to Fumadocs in a commit touching 3,630 files. The corrected file was renamed into the v6 archive, and the page people actually read was copied from a version that still had the old flag.

**Node bindings for Qdrant Edge.** [qdrant/qdrant#10226](https://github.com/qdrant/qdrant/issues/10226).

`lib/edge/ffi` is a hand-annotated UniFFI surface built for Swift and Kotlin, with no JavaScript target. I have it working end to end through generated Napi bindings: create a shard, upsert a point carrying a dense vector and a JSON payload, query it back, unload, reopen from the same path on disk, query again. Which language bindings belong in the core repository is still an open question for the maintainers, and they have asked that no pull request be opened until they decide.

## Published

### [vaultbench](https://github.com/liamiepops/vaultbench)

Five embedded vector search engines benchmarked at personal knowledge base scale, on real markdown pulled from four public documentation repositories, at 1k, 10k and 100k chunks. Embeddings are computed once and loaded byte identically into every engine. Recall is measured against exact brute force ground truth.

What came out of it:

- A plain `Float32Array` scan beats both sqlite-vec and Orama at every size above 1,000 chunks.
- LanceDB's default index returns recall@10 of 0.500 at 10k and 100k, and nothing in the output tells you.
- Filters buy sqlite-vec nothing. At 1% selectivity it runs 184x slower than brute force.
- `save()` in Orama produces output that cannot be `JSON.stringify`d at 100k.
- Qdrant Edge is fastest at every size and stays exact throughout.

The failure mode I went in expecting, search then discard under a filter, showed up in none of them, which is a clean negative result and worth as much as the rest.

### [portcall](https://github.com/liamiepops/portcall)

Prisma 7 probed across Node, Bun, Deno and Cloudflare `workerd`. All four pass all eleven steps with byte identical output, which turns out to be close to guaranteed once you notice that all four load the same WASM query compiler. The one real difference is the Workers target, which needs a second generator block, because the default client imports `node:process` at module scope.

This is also where the stale Prisma documentation above came from.

### Langsammm

A Firefox extension that slows browser audio down without turning everyone into a chipmunk. Real time pitch shifting with formant preservation in the Web Audio API: playback slows, and the spectral envelope is corrected back to where it started, so voices keep the character you recognise them by. It draws the spectrum live while it runs, and it hooks into YouTube, YouTube Music, SoundCloud and Bandcamp. Everything stays on the machine, with no network calls and no telemetry. Passed Mozilla add-on review and published on addons.mozilla.org.
