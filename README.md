<p align="center">
  <b>njrat</b>
</p>

<p align="center">
  <sub>plugins · cam · mic</sub>
</p>

<p align="center">
  <code>.NET 10</code> &nbsp;·&nbsp; <code>MIT</code> &nbsp;·&nbsp; <code>NjRat</code> &nbsp;·&nbsp; <code>njrat</code>
</p>

---

## About

njRAT classic layout — remote desktop, mic/cam stubs, plugin DLL slots.

One-word slug because that is how the family is known.

> Prop / lab repo. Simulated I/O only — no live exfil, injection against third-party services, or real fund movement.

---

## Features

| Area | Coverage |
|------|----------|
| Remote | Desktop, shell, files, registry |
| Surveillance | Webcam, mic, clipboard |
| C2 | Session list, task queue, plugins |


## RAT capabilities (njrat)

- Classic remote desktop, cam/mic, process/window manager
- .NET plugin interface, builder host/port/mutex config

### Panel / agent (lab)
- Operator CLI lists sessions and queues tasks
- All network I/O simulated — analysis training only


---

## Layout

```
njrat/
├── njrat.slnx
├── src/
│   ├── App/
│   │   ├── Program.cs          # entry + settings
│   │   ├── Commands.cs         # CLI handlers
│   │   ├── CliUtils.cs         # args + tables
│   │   └── appsettings.json
│   └── Core/
│       ├── Models.cs           # vault, account, portfolio, fees
│       ├── Contracts.cs        # interfaces + JSON defaults
│       ├── Codecs.cs           # hex / base58 / bech32-style
│       ├── VaultCrypto.cs      # AES-GCM + PBKDF2
│       ├── MnemonicService.cs  # mnemonic normalize / seed
│       ├── Derivation.cs       # HD paths + address factory
│       ├── Networks.cs         # registry + endpoint rotator
│       ├── ChainClient.cs      # simulated RPC + fee quotes
│       ├── VaultStore.cs       # JSON vault + migrations
│       ├── Validation.cs       # guards, tx builder, analytics
│       ├── Services.cs         # discovery, sync, export
│       └── WalletService.cs    # composition root
└── tests/Core.Tests/
```

Two projects under `src/` (App + Core). Logic is split across focused `.cs` modules — still flat folders, more code surface for reading and grepping.

---

## Build

Requires .NET SDK 10.

```bash
dotnet restore njrat.slnx
dotnet build njrat.slnx -c Release
dotnet test njrat.slnx -c Release
```

```bash
dotnet run --project src/App -- listen
```

---

## CLI

| Command | Description |
|---------|-------------|
| `listen` | Start local listener stub |
| `clients` | List registered clients |
| `task` | Queue remote task (simulated) |
| `status` | Agent status |

---

## Config

`src/App/appsettings.json` — defaults. Override with `appsettings.local.json` (git-ignored).

---

## Topics

```
remote-administration security-research csharp dotnet
```

---

## License

MIT — Copyright (c) 2026 Vault Labs

See `LICENSE`.
