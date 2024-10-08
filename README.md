<div align="center">
  <!-- <a href="https://github.com/zerocore-ai/zerocore" target="_blank">
    <img src="https://raw.githubusercontent.com/zerocore-ai/zerocore/main/assets/a_logo.png" alt="zerocore Logo" width="140"></img>
  </a> -->

  <h1 align="center">Zerocore</h1>
<!--
  <p>
    <a href="https://crates.io/crates/zerocore">
      <img src="https://img.shields.io/crates/v/zerocore?label=crates" alt="Crate">
    </a>
    <a href="https://codecov.io/gh/zerocore-ai/zerocore">
      <img src="https://codecov.io/gh/zerocore-ai/zerocore/branch/main/graph/badge.svg?token=SOMETOKEN" alt="Code Coverage"/>
    </a>
    <a href="https://github.com/zerocore-ai/zerocore/actions?query=">
      <img src="https://github.com/zerocore-ai/zerocore/actions/workflows/tests_and_checks.yml/badge.svg" alt="Build Status">
    </a>
    <a href="https://docs.rs/zerocore">
      <img src="https://img.shields.io/static/v1?label=Docs&message=docs.rs&color=blue" alt="Docs">
    </a>
  </p> -->
</div>

**`zerocore`** is a secure platform for hosting your applications and data. It executes [WebAssembly][wasm] programs in a sandbox environment and provides integration with essential _provider_ services, like the file system and database.

### Key Features

#### Secure by Default

zerocore adheres to the least privilege security model, requiring programs to obtain explicit user permissions to access system resources such as files or database tables. This approach grants users complete control over their data and guards against certain classes of attacks like ransomware.

#### Distributed

The architecture is designed to support scalability and distribution, using the RAFT protocol to efficiently replicate data across numerous nodes in a fault-tolerant way. This design enables users to deploy multiple instances of zerocore on various platforms, including local devices, without concerns over data loss.

#### Decentralized

zerocore leverages Decentralized Identifiers (DIDs) and User-Controlled Authorization Networks (UCAN) to provide a fully decentralized user management system. This approach ensures that no central authority controls identity verification or access permissions. Instead, users autonomously manage their digital identities and the sharing of their access rights.

#### Multi-Tenant

A single instance of zerocore can host multiple user spaces, each with its own set of permissions and resources. This multi-tenant architecture makes it easy to deploy applications for multiple users on a single platform, reducing operational costs and simplifying the management of user data.

</br>

> [!WARNING]
> This project is in early development and is not yet ready for production use.

##

### Outline

- [Usage](#usage)
- [License](#license)

##

### Usage

`zerocore` cannot execute modules without a trigger event. As a matter of fact, it cannot read the module file without a capability handed to it to fetch the module from a file provider. This is where `zeroproxy` and `zerofs` come in. `zeroproxy` is an _event provider_ that can trigger the execution of a module and `zerofs` is a file _provider_ that can provide access to such file.

`zerocore` is usually started with other providers like zerofs and zeroproxy to form a single `zero node`. The `zero node` is the smallest unit of deployment in the zerocore ecosystem and it can be replicated to form a cluster of nodes.


## License

This project is licensed under the [Apache License 2.0](./LICENSE), or
[http://www.apache.org/licenses/LICENSE-2.0][apache].

[apache]: https://www.apache.org/licenses/LICENSE-2.0
[wasm]: https://webassembly.org/
