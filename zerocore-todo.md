- [ ] Remove nacelle. Move into a separate repo


- [ ] The component model

  - [ ] Read the component model explainer https://github.com/WebAssembly/component-model/blob/main/design/mvp/Explainer.md
  - [x] Implement export interface that can be used from the world.
  - [x] Understanding the wasi:io (streams, polls, etc.) https://github.com/bytecodealliance/wasmtime/tree/main/crates/wasi/wit/deps/io

- [ ] Support only components nacelle and nacelle-cli

  - [ ] Checking the file to see if it is a component. if not, give directions on how to make it a component.

    ```
    0x0 | 00 61 73 6d | version 13 (Component)
        | 0d 00 01 00
    ```

    The 7th byte being set to 0x01 indicates that this is a component. Ignore the version as it will keep increasing pre-standardization and it will set back to 0x01 when it is standardized.

  - [ ] `wit_component::ComponentEncoder` for converting core modules to components with the ability to adapt it for wasi_snapshot_preview1.

- [ ] Zerodb

  - [ ] API Design

    ```rust
    use zerosdk::zeroproxy::{zeroproxy, Request, Response};

    #[zeroproxy::handler]
    pub fn handler(_req: &mut Request) -> impl Response {
        "Hello, World!".into()
    }
    ```

- [ ] Zero Developer Experience

  - [ ] Support for mono-repo
  - [ ] Support for single library containing multiple triggers

- [ ] Capabilities

  - [ ] `[ucan]` custom section in the wasm binary
  - [ ] Embed the ucan in the component. -> `component.zero.wasm`
  - [ ] fs - path, read, write, delete, create (resource granularity = file, directory)
  - [ ] database - path, read, write, delete, create (resource granularity = db, table)

- [ ] Identities (DIDs)

  - [ ] Admin - Allows communication with other node. Can create a tenant partition. etc.
  - [ ] Owner - Delegated by admin. Can own a tenant partition
  - [ ] Node

- [ ] The Core

  - [ ] The core runtime - `zerocore`
  - [ ] Minimum Provider Requirement - `zerofs`
    - [ ] When `zerocore` recieves a request from `zeroproxy`, it asks `zerofs` for the wasm code, providing the users credentials.
    - [ ] `zerofs` checks if the user has access to the file and returns the wasm code.
    - [ ] `zerocore` then executes the wasm code and sends the response back to `zeroproxy`.
  - [ ] Wasi Preview 2 API support
    - [ ] `wasi:io` (zerowasi)
    - [ ] `wasi:random` (zerowasi)
    - [ ] `wasi:clocks` (zerowasi)
  - [ ] `Provider` trait
    - [ ] To be implemented by most providers
    - [ ] Mostly IPC communication
    - [ ] Some providers like zerofs require shared memory
    - [ ] IMPORTANT: Add protection on the shared memory
    - [ ] Behaviors
      - [ ] Multitenancy
      - [ ] Capabilities
      - [ ] Distributed
  - [ ] `EventProvider: Provider` trait
  - `stdout` and `stderr` gets redirected to the logs

- [ ] Providers

  - [ ] Move http-server (proxy) to a provider
  - [ ] Design Provider Contract Language (PCL)
  - [ ] Figure Provider/Core communication method (IPC)
  - [ ] Add support for main providers and their contracts
    - [ ] zeroproxy (`wasi:http`)
    - [ ] zerodb (`zero:db`)
    - [ ] zerofs (shared memory, `wasi:filesystem`)
    - [ ] zerochrono (`zero:chrono`)
    - [ ] zerobrowser (`zero:browser`)
    - [ ] zeroml (`zero:ml`)
    - [ ] zerovm (firecracker) (replaces zeroci/zerobuild) `zero:vm`
    - [ ] zerocache (`zero:cache`)
  - [ ] Two types of providers
    - [ ] Event Providers (e.g. zeroproxy)
    - [ ] Resource Providers (e.g. zerofs)

- [ ] General Configuration File

  - [ ] `zerocore.toml` - The configuration file for the core and providers

- [ ] Distributed System Design

  - [ ] Common distributed semantics (They all use zeroraft so they share a common config)
  - [ ] Coreless nodes (The core sets up the node and exits)

- [ ] Catching panics in request handlers

- [ ] Optimizations
  - [ ] AOT compilation

- [ ] Tests

  - [ ] proptests
  - [ ] fuzzing
  - [ ] jepsen
