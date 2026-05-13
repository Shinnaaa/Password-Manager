# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-file, zero-dependency local password manager (`index.html`). The entire application — HTML, CSS, and JavaScript — lives in one self-contained file. Open it directly in a browser; no build step, no server, no npm.

## Running the App

Open `index.html` in any modern browser (Chrome, Safari, Firefox, Edge). No build or install step required.

## Architecture

Everything is in `index.html`. The file is structured as:

1. **CSS** (`<style>`) — All styles inline, using CSS custom properties (`--primary`, `--bg`, etc.) for theming.
2. **HTML** — Static shell: lock screen, main app with tabs (generator / vault / health), modals (add/edit entry, delete confirm, import, export).
3. **JavaScript** (`<script>`) — Single `'use strict'` block. No modules, no frameworks.

### Security model

- Master password → PBKDF2 (210,000 iterations, SHA-256) → AES-256-GCM key via `crypto.subtle`
- Vault is encrypted as `{ salt, iv, ct }` (all base64) and stored in `localStorage` under key `pwm_vault_v1`
- All randomness uses `crypto.getRandomValues()` with rejection sampling (no modulo bias)
- Auto-lock after 5 minutes of inactivity; clipboard auto-cleared after 30 seconds

### Entry data model

Two entry kinds stored in `vault.entries[]`:

**Password entry:**
```js
{ id, kind:'password', site, username, password, totpSecret, notes, tags[], createdAt, updatedAt }
```
Entries without `kind` are treated as passwords (backward compat).

**Secret entry:**
```js
{ id, kind:'secret', site, secretType, secretValue, envs[], platform, expiresAt, notes, tags[], createdAt, updatedAt }
```
`secretType` is one of: `API Key`, `Token`, `SSH Private Key`, `Connection String`, `其他`.
`expiresAt` is an ISO date string `YYYY-MM-DD` from `<input type="date">`.

### Key state variables

```js
cryptoKey       // CryptoKey (AES-GCM), null when locked
vault           // { entries: [] } — decrypted in memory only
activeTypeFilter  // null | 'password' | 'secret'
activeTagFilter   // null | string
editingKind       // 'password' | 'secret' — current modal kind
editingEnvs       // Set of selected environment names
editingTags       // Set of selected tag names
cbTimers          // Map: key -> { endTime, defaultText } for clipboard countdown
totpCodes         // Map: entry id -> current 6-digit code string
```

### Global tick

A single `setInterval` (1s) drives both clipboard countdown display and TOTP progress bars. TOTP codes are regenerated once per 30-second window (detected by comparing `Math.floor(Date.now()/1000/30)` to `lastTotpWindow`).

### UI language

All UI text is Simplified Chinese. Entry modal switches between password and secret modes via `setEditKind(kind)`, which toggles `#ef-pw-section` / `#ef-secret-section` visibility.

### Vault persistence flow

`unlock()` → PBKDF2 derive key → AES-GCM decrypt localStorage blob → populate `vault`
Any mutation → `persistVault()` → AES-GCM encrypt → write back to localStorage
