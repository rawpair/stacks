# RawPair Stacks

This repository provides official Docker images for development environments used with [RawPair](https://github.com/rawpair/rawpair). These stacks are designed for **collaborative, short-lived sessions**—where convenience matters more than minimalism.

Each image includes:
- A **full toolchain** for a specific language (e.g., Elixir, Ada, Prolog)
- **Sane defaults** and ready-to-use configuration
- Everything needed to get started without manual setup

These images are intended for **ephemeral, sandboxed sessions**, not public-facing or production deployments.

They prioritize **developer convenience** over strict hardening: full toolchains, common tools pre-installed, minimal setup required.  
This makes them ideal for short-lived environments where speed and simplicity matter most—like live coding, pair programming, or onboarding sessions.

They are **not security-hardened** for internet exposure or long-term persistence, and we strongly recommend against using them outside controlled environments.

---

## Required Components

To integrate properly with RawPair, each container **must include**:

- `bash` — shell consistency
- `tmux` — terminal multiplexing
- `supervisor` — process management
- `vector` — log streaming to the host
- `ttyd` — exposes the terminal over HTTP

These enable RawPair's real-time terminal access, session orchestration, and logging. Without them, your container **will not function correctly** inside the system.

---

## Required Config Files

Each image must also include three configuration files:

- `supervisord.conf`
- `ttyd-wrapper.sh`
- `vector.toml`

These are provided in the [docker/](https://github.com/rawpair/rawpair/tree/main/docker) folder of the main repo. You should copy them into your image during the build process.

---

## 💡 Customizing Stacks

You’re free to build your own stacks, but make sure to keep the required components.  
In short: **build your own, but build smart.**

## Supported Tech Stacks

The majority of the Docker images in this repo are available on https://hub.docker.com/u/rawpair

| Stack                                                    | Docker Repository                                                                     | Notes                                          |
|----------------------------------------------------------|---------------------------------------------------------------------------------------|------------------------------------------------|
| **[Ada](https://www.gnu.org/software/gnat/)**            | [rawpair/ada](https://hub.docker.com/r/rawpair/ada)                                   | Includes GNU GNAT                              |
| **[Chicken Scheme](https://www.call-cc.org/)**           | [rawpair/chicken-scheme](https://hub.docker.com/r/rawpair/chicken-scheme)             | Includes csi, csc, and chicken-install         |
| **[Clojure](https://clojure.org/)**                      | [rawpair/clojure](https://hub.docker.com/r/rawpair/clojure)                           | Runs on Temurin (OpenJDK)                      |
| **[CBQN](https://github.com/dzaima/CBQN/)**              | [rawpair/cbqn](https://hub.docker.com/r/rawpair/cbqn)                                 |                                                |
| **[COBOL](https://gnucobol.sourceforge.io/)**            | [rawpair/gnucobol](https://hub.docker.com/r/rawpair/gnucobol)                         | Includes GNU COBOL                             |
| **[Elixir](https://elixir-lang.org/)**                   | [rawpair/elixir](https://hub.docker.com/r/rawpair/elixir)                             | Includes Mix and Hex                           |
| **[Gambit Scheme](https://gambitscheme.org/)**           | [rawpair/gambit-scheme](https://hub.docker.com/r/rawpair/gambit-scheme)               | Includes gsi and gsc                           |
| **[Guile](https://www.gnu.org/software/guile/)**         | [rawpair/gnuguile](https://hub.docker.com/r/rawpair/gnuguile)                         |                                                |
| **[Haskell](https://www.haskell.org/)**                  | [rawpair/haskell](https://hub.docker.com/r/rawpair/haskell)                           | Includes GHC                                   |
| **[Janet](https://janet-lang.org/)**                     | [rawpair/janet](https://hub.docker.com/r/rawpair/janet)                               | Includes Janet CLI and jpm                     |
| **[Julia](https://julialang.org/)**                      | [rawpair/julia](https://hub.docker.com/r/rawpair/julia)                               | REPL and package manager built-in              |
| **[.NET](https://dotnet.microsoft.com/)**                | [rawpair/dotnet](https://hub.docker.com/r/rawpair/dotnet)                             | Includes C#, F#, VB.NET, Mono                  |
| **[Liberty Eiffel](https://www.liberty-eiffel.org/)**    | [rawpair/liberty-eiffel](https://hub.docker.com/r/rawpair/liberty-eiffel)             | Compiled from [source](https://github.com/LibertyEiffel/Liberty) |
| **[Metasploit](https://www.metasploit.com/)**            | [rawpair/metasploit](https://hub.docker.com/r/rawpair/metasploit)                     | Metasploit Framework                           |
| **[MIT/GNU Scheme](https://www.gnu.org/software/mit-scheme/)** | [rawpair/mit-gnu-scheme](https://hub.docker.com/r/rawpair/mit-gnu-scheme)       |                                                |
| **[Nim](https://nim-lang.org/)**                         | [rawpair/nim](https://hub.docker.com/r/rawpair/nim)                                   | Includes nimble                                |
| **[Node.js](https://nodejs.org/)**                       | [rawpair/node](https://hub.docker.com/r/rawpair/node)                                 | Managed via NVM                                |
| **[OCaml](https://ocaml.org/)**                          | [rawpair/ocaml](https://hub.docker.com/r/rawpair/ocaml)                               | Includes OPAM, OCaml 4.14.1, Dune, Menhir      |
| **[PHP](https://www.php.net/)**                          | [rawpair/php](https://hub.docker.com/r/rawpair/php)                                   | Includes FPM/CLI; PHP 8.0–8.3                  |
| **[Python](https://www.python.org/)**                    | [rawpair/python](https://hub.docker.com/r/rawpair/python)                             | 2 base images available: Trixie; NVIDIA CUDA   |
| **[Racket](https://racket-lang.org/)**                   | [rawpair/racket](https://hub.docker.com/r/rawpair/racket)                             | Includes raco and CLI REPL                     |
| **[Ruby](https://www.ruby-lang.org/en/)**                | [rawpair/ruby](https://hub.docker.com/r/rawpair/ruby)                                 | Includes RubyGems                              |
| **[Rust](https://www.rust-lang.org/)**                   | [rawpair/rust](https://hub.docker.com/r/rawpair/rust)                                 |                                                |
| **[Smalltalk](https://www.gnu.org/software/smalltalk/)** | [rawpair/gnusmalltalk](https://hub.docker.com/r/rawpair/gnusmalltalk)                 | Includes GNU Smalltalk                         |
| **[Steel Bank Common Lisp](https://www.sbcl.org/)**      | [rawpair/sbcl](https://hub.docker.com/r/rawpair/sbcl)                                 | Includes SBCL and Quicklisp                    |
| **[Zig](http://ziglang.org/)**                           | [rawpair/zig](https://hub.docker.com/r/rawpair/zig)                                   |                                                |

Can't see your favourite stack? Submit a PR or create an issue.

## Usage
Each Dockerfile is intended to be used by RawPair internally. You can also test them standalone:

### Render list of all possible permutations:

```bash
cd stacks
./build-images.sh --dry-run
```

### Example: generating Elixir images

```bash
cd stacks
./build-images.sh --filter=elixir
```

### Generating multi-arch images

Some Docker images support multi-arch. Although dockerx can build arm64 images via QEMU, this is not recommended as it is painfully slow. Instead, we recommend getting hold of a Raspberry Pi or an ARM server.

Assuming the main docker node is amd64 arch:

`docker buildx create --name multiarch --use --platform linux/amd64`

Optionally append arm64 remote builder:

`docker buildx create --append --name multiarch --platform linux/arm64 arm-vps`

Inspect:

`docker buildx inspect rawpair-builder --bootstrap`

`cd stacks` 

#### Ada (GNAT)

##### Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/ada:bookworm -f ./ada/bookworm/Dockerfile --push .`

##### Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/ada:trixie -f ./ada/trixie/Dockerfile --push .`

#### Chicken Scheme

##### Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/chicken-scheme:bookworm -f ./chicken-scheme/bookworm/Dockerfile --push .`

##### Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/chicken-scheme:trixie -f ./chicken-scheme/trixie/Dockerfile --push .`

#### Clojure

##### Temurin 21 - Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/clojure:temurin-21-bookworm -f ./clojure/clojure:temurin-21-bookworm/Dockerfile --push .`

##### Temurin 22 - Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/clojure:temurin-22-bookworm -f ./clojure/clojure:temurin-22-bookworm/Dockerfile --push .`

##### Temurin 23 - Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/clojure:temurin-23-bookworm -f ./clojure/clojure:temurin-23-bookworm/Dockerfile --push .`

##### Temurin 24 - Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/clojure:temurin-24-bookworm -f ./clojure/clojure:temurin-24-bookworm/Dockerfile --push .`

#### Elixir - Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/elixir:bookworm -f ./elixir/bookworm/Dockerfile --push .`

#### Gambit Scheme

##### Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/gambit-scheme:bookworm -f ./gambit-scheme/bookworm/Dockerfile --push .`

##### Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/gambit-scheme:trixie -f ./gambit-scheme/trixie/Dockerfile --push .`

#### CBQN

##### Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/cbqn:bookworm -f ./cbqn/bookworm/Dockerfile --push .`

#### GNU COBOL

##### Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/gnucobol:bookworm -f ./gnucobol/bookworm/Dockerfile --push .`

##### Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/gnucobol:trixie -f ./gnucobol/trixie/Dockerfile --push .`

#### GNU Guile

##### Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/gnuguile:bookworm -f ./gnuguile/bookworm/Dockerfile --push .`

##### Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/gnuguile:trixie -f ./gnuguile/trixie/Dockerfile --push .`

#### GNU Smalltalk - Ubuntu 24.04

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/gnusmalltalk:trixie -f ./gnusmalltalk/trixie/Dockerfile --push .`

#### Haskell - Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/haskell:trixie -f ./haskell/trixie/Dockerfile --push .`

#### Janet - Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/janet:bookworm -f ./janet/bookworm/Dockerfile --push .`

#### Julia - Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/julia:trixie -f ./julia/trixie/Dockerfile --push .`

#### Liberty Eiffel - Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/liberty-eiffel:bookworm -f ./liberty-eiffel/bookworm/Dockerfile --push .`

#### Metasploit Framework - 6.4.0

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/metasploit:6.4.0 -f ./metasploit/6.4.0/Dockerfile --push .`

#### MIT/GNU Scheme

##### Debian Bookworm

`docker buildx build --platform linux/amd64 -t rawpair/mit-gnu-scheme:bookworm -f ./mit-gnu-scheme/bookworm/Dockerfile --push .`

#### Nim - Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/nim:trixie -f ./nim/trixie/Dockerfile --push .`

#### Node - Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/node:trixie -f ./node/trixie/Dockerfile --push .`

#### OCaml - Ubuntu 24.04

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/ocaml:ubuntu-2404 -f ./ocaml/ubuntu-2404/Dockerfile --push .`

#### PHP - Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/php:trixie -f ./php/trixie/Dockerfile --push .`

#### Python - Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/python:trixie -f ./python/trixie/Dockerfile --push .`

#### Racket - Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/racket:trixie -f ./racket/trixie/Dockerfile --push .`

#### Ruby - Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/ruby:trixie -f ./ruby/trixie/Dockerfile --push .`

#### Rust - Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/rust:trixie -f ./rust/trixie/Dockerfile --push .`

#### Steel Bank Common Lisp - Debian Trixie

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/sbcl:trixie -f ./sbcl/trixie/Dockerfile --push .`

#### Zig - Debian Bookworm

`docker buildx build --platform linux/amd64,linux/arm64 -t rawpair/zig:bookworm -f ./zig/bookworm/Dockerfile --push .`

### Generating images through background jobs

Wrap the command with `nohup <command> > build.log 2>&1 &`.
