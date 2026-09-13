### Liam O'Callaghan

Software engineer in Berlin. Most of my recent work is on language bindings and generated code.

### Projects

**[vaultbench](https://github.com/liamiepops/vaultbench)**. Five embedded vector search engines at 1k, 10k and 100k chunks of real markdown, recall measured against exact brute force. At 100k, Qdrant Edge queries in 0.52ms and stays exact; brute force takes 32.66ms. A plain array scan beats sqlite-vec and Orama above 1,000 chunks, and LanceDB's default index returns recall@10 of 0.500 without saying so.

**[portcall](https://github.com/liamiepops/portcall)**. Prisma 7 across Node, Bun, Deno and Cloudflare `workerd`. All four agree, because all four load the same WASM query compiler. The Workers target needs a second generator block, since the default client imports `node:process` at module scope.
