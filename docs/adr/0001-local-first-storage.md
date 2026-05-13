# ADR-0001: Local-first storage with a sync extension point

**Status:** Accepted  
**Date:** 2026-05-13

## Context

The app needs to persist state across sessions and eventually across devices (laptop + phone). Two approaches were considered at the outset: local-only storage (localStorage/IndexedDB) and a cloud backend (Supabase, Turso, etc.).

## Decision

Start local-only. All state lives in the browser via Zustand's `persist` middleware backed by `localStorage`. No backend, no auth, no network dependency in v1.

Each Zustand store is structured around a plain serialisable state shape so the storage adapter can be swapped later (e.g. a custom storage adapter that syncs to Supabase) without rewriting business logic.

## Consequences

- **Positive:** Zero infrastructure to maintain; works offline immediately; no auth complexity; fast to ship.
- **Positive:** Data is private by default — never leaves the device.
- **Negative:** Data is not shared across devices until a sync layer is added.
- **Negative:** Clearing browser storage deletes all data — export/backup feature needed before cross-device sync is worthwhile.
- **Extension point:** When adding sync, replace the `persist` storage option per store. The state shape and selectors remain unchanged.
