# cf-rust-hello

Simple Rust worker for Cloudflare Workers using `wrangler`.

## Requirements

- Rust installed
- Rust WebAssembly target: `wasm32-unknown-unknown`
- Node.js available in your environment
- `wrangler` installed globally with npm

This project manages tool versions as follows:

- Rust: pinned in `rust-toolchain.toml`
- Node.js and `wrangler`: use your local environment version manager

## Setup

Install the Rust target if you do not have it yet:

```bash
rustup target add wasm32-unknown-unknown
```

If you use `asdf`, do not commit `.tool-versions` in this repository because Cloudflare build environments may try to install tools from it and fail.

For local development with `asdf`, create `.tool-versions` only on your machine (it is ignored by Git), for example:

```text
nodejs 24.3.0 .npm
```

## Run Locally

Start the worker in development mode:

```bash
wrangler dev
```

On the first run, `wrangler` installs `worker-build`, compiles the Rust crate to Wasm, and generates `build/worker/shim.mjs` before opening the local URL.

If you want to run this step manually first:

```bash
cargo install worker-build
worker-build --release
```

## Deploy

Publish to Cloudflare Workers:

```bash
wrangler deploy
```

If deployment asks for authentication:

```bash
wrangler login
```

## Project Structure

- `src/lib.rs`: main worker HTTP handler
- `wrangler.toml`: Cloudflare Workers configuration
- `Cargo.toml`: Rust crate dependencies and settings

## Current Response

The worker currently responds with:

```text
Hello Worker from Rust 🚀
```