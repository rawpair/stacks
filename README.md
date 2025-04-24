# RawPair Stacks

This repo contains official Docker images for supported RawPair programming environments.

Each directory defines a language stack with the tools needed for live shared terminal sessions.

> These stacks are **not** part of RawPair's core infrastructure. They're sandboxed environments used inside terminal sessions.

## Supported Tech Stacks

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

```bash
docker build -t rawpair/elixir ./stacks/elixir
```

## Contributing

Want to add a new stack? Check out [CONTRIBUTING.md](./CONTRIBUTING.md)
