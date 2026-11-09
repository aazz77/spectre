# spectre-protocol

Core protocol implementation for **Spectre** — a censorship-resistant QUIC proxy protocol with JLS-style camouflage and Brutal congestion control.

This crate contains the **shared protocol core** extracted from the main Spectre project:

- Wire format (TCP Connect, Auth, Padding, UDP header)
- Address encoding
- Brutal-style congestion controller for `quinn`
- Packet-level obfuscation (`obfs`) and `ObfsRuntime` for `quinn`
- UDP session table, fragmentation / reassembly
- Simple bidirectional relay helper

## Installation

```toml
[dependencies]
spectre-protocol = "0.1"
```

## Features

| Module | Description |
|--------|-------------|
| `brutal` | Hysteria2-style target-rate congestion control (`Controller` for quinn) |
| `obfs` / `obfs_socket` | PSK-based packet obfuscation + quinn `Runtime` wrapper |
| `udp` | UDP association framing, fragmentation, session management |
| `relay` | Bidirectional stream relay helper |
| root | `Command`, `Address`, `TcpConnectRequest/Response`, `AuthRequest/Response`, padding helpers |

## Protocol Specification

See [PROTOCOL.md](PROTOCOL.md) for the full wire format specification (v0.1).

## Dependencies

This crate depends on the JLS-enabled QUIC stack:

- `quinn-jls` / `quinn-proto-jls`
- `socket2`

These are required because the Brutal controller and ObfsRuntime are tightly integrated with quinn's types.

## License

MIT

## Related

- Main project: [spectre](https://github.com/minexxa/spectre)
