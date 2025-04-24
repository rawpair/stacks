# RawPair Stacks

This repo contains official Docker images for supported RawPair programming environments.

Each directory defines a language stack with the tools needed for live shared terminal sessions.

> These stacks are **not** part of RawPair's core infrastructure. They're sandboxed environments used inside terminal sessions.

## Example Stacks
- `elixir/` - Elixir, IEx, mix
- `node/` - Node.js through NVM
- `python/` - Python 3 with common support tools
...

## Usage
Each Dockerfile is intended to be used by RawPair internally. You can also test them standalone:

```bash
docker build -t rawpair/elixir ./stacks/elixir
```

## Contributing

Want to add a new stack? Check out [CONTRIBUTING.md](./CONTRIBUTING.md)
