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
| **[Ada](https://www.gnu.org/software/gnat/)**            | [rawpair/ada](https://hub.docker.com/repository/docker/rawpair/ada)                   | Includes GNU GNAT                              |
| **[Clojure](https://clojure.org/)**                      | [rawpair/clojure](https://hub.docker.com/repository/docker/rawpair/clojure)           | Runs on Temurin (OpenJDK)                      |
| **[COBOL](https://gnucobol.sourceforge.io/)**            | [rawpair/gnucobol](https://hub.docker.com/repository/docker/rawpair/gnucobol)         | Includes GNU COBOL                             |
| **[Elixir](https://elixir-lang.org/)**                   | [rawpair/elixir](https://hub.docker.com/repository/docker/rawpair/elixir)             |                                                |
| **[Haskell](https://www.haskell.org/)**                  | [rawpair/haskell](https://hub.docker.com/repository/docker/rawpair/haskell)           | Includes GHC                                   |
| **[Julia](https://julialang.org/)**                      | [rawpair/julia](https://hub.docker.com/repository/docker/rawpair/julia)               |                                                |
| **[.NET](https://dotnet.microsoft.com/)**                | [rawpair/dotnet](https://hub.docker.com/repository/docker/rawpair/dotnet)             | Includes C#, F#, VB.NET, Mono                  |
| **[Liberty Eiffel](https://www.liberty-eiffel.org/)**    | [rawpair/liberty-eiffel](https://hub.docker.com/repository/docker/rawpair/liberty-eiffel) | Compiled from [source](https://github.com/LibertyEiffel/Liberty) |
| **[Node.js](https://nodejs.org/)**                       | [rawpair/node](https://hub.docker.com/repository/docker/rawpair/node)                 | Managed via NVM                                |
| **[OCaml](https://ocaml.org/)**                          | [rawpair/ocaml](https://hub.docker.com/repository/docker/rawpair/ocaml)               | Includes OPAM, OCaml 4.14.1, Dune, Menhir      |
| **[PHP](https://www.php.net/)**                          | [rawpair-php](https://hub.docker.com/repository/docker/rawpair/php)                   | Includes FPM/CLI; PHP 8.0–8.3                  |
| **[Python](https://www.python.org/)**                    | [rawpair/python](https://hub.docker.com/repository/docker/rawpair/python)             | 2 base images available: Trixie; NVIDIA CUDA   |
| **[Ruby](https://www.ruby-lang.org/en/)**                | [rawpair/ruby](https://hub.docker.com/repository/docker/rawpair/ruby)                 |                                                |
| **[Rust](https://www.rust-lang.org/)**                   | [rawpair/rust](https://hub.docker.com/repository/docker/rawpair/rust)                 |                                                |
| **[Smalltalk](https://www.gnu.org/software/smalltalk/)** | [rawpair/gnusmalltalk](https://hub.docker.com/repository/docker/rawpair/gnusmalltalk) | Includes GNU Smalltalk                         |
| **[Steel Bank Common Lisp](https://www.sbcl.org/)**      | [rawpair/sbcl](https://hub.docker.com/repository/docker/rawpair/sbcl)                 | Includes SBCL and Quicklisp                    |

Can't see your favourite stack? Submit a PR or create an issue.

## Usage
Each Dockerfile is intended to be used by RawPair internally. You can also test them standalone:

Generates list of all possible permutations:

```bash
cd stacks
./build-images.sh --dry-run
```

Generates Elixir images:

```bash
cd stacks
./build-images.sh --filter=elixir
```

