# Balance of Chaos

Turn-based geopolitical simulation. Tauri 2.x desktop app.
- Backend: Rust (game engine, state, AI)
- Frontend: SvelteKit + Svelte 5 + TypeScript (SSR disabled, adapter-static)
- Content: Lua 5.4 via mlua (deferred to Task 15)
- Styling: Tailwind CSS 3.x
- Data: TOML (config), JSON (saves)
- License: AGPL-3.0
- Repo: jmspring/boc

Architecture: Rust owns game logic. Lua provides content (events, personas).
Frontend calls Rust via Tauri IPC. No game logic in the frontend.

## Conventions
- Rust: no unwrap() on user paths, use Result/?. Clippy clean.
- TypeScript: strict mode, no `any` types.
- Engine code (src-tauri/src/engine/): pure Rust, no Tauri imports.
- IPC code (src-tauri/src/ipc/): thin layer, no game logic.
- Frontend: SvelteKit with Svelte 5 runes ($state, $derived, $effect), SSR disabled.
- Lua: content only. Returns data to Rust. Never mutates game state.
