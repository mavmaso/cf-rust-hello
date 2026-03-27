# cf-rust-hello

Worker simples em Rust para Cloudflare Workers usando `wrangler`.

## Requisitos

- Rust instalado
- target WebAssembly do Rust: `wasm32-unknown-unknown`
- Node.js disponível no ambiente
- `wrangler` instalado globalmente com npm

Este projeto separa as versoes de ferramenta assim:

- Rust: fixado em `rust-toolchain.toml`
- Node.js e `wrangler`: resolvidos por `.tool-versions` via `asdf`

## Setup

Instale o target do Rust, se ainda nao tiver:

```bash
rustup target add wasm32-unknown-unknown
```

Se voce usa `asdf`, este projeto ja inclui `.tool-versions` para o shim do `wrangler` funcionar neste diretorio.

## Rodando localmente

Para subir o worker em modo de desenvolvimento:

```bash
wrangler dev
```

Na primeira execucao, o `wrangler` vai instalar o `worker-build`, compilar o crate Rust para Wasm e gerar `build/worker/shim.mjs` antes de abrir a URL local.

Se quiser adiantar essa etapa manualmente, rode:

```bash
cargo install worker-build
worker-build --release
```

## Deploy

Para publicar no Cloudflare Workers:

```bash
wrangler deploy
```

Se o deploy pedir autenticacao, rode:

```bash
wrangler login
```

## Estrutura

- `src/lib.rs`: handler HTTP principal do worker
- `wrangler.toml`: configuracao do Cloudflare Workers
- `Cargo.toml`: dependencias e configuracao do crate Rust

## Resposta atual

O worker responde:

```text
Hello Worker from Rust 🚀
```