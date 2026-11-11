# Kavro — experimental low-level language & Aqua Studio

**Status: v0.4 / M2 preview — under active development. NOT production-ready.**

Kavro is an experimental programming language inspired by HolyC, C, x86-64 Assembly and systems programming. The companion **Kavro Studio** is an offline, retro-styled development environment influenced by the classic Mac OS X Aqua aesthetic and Frutiger Aero.

## What works today

- A browser-based educational compiler: lexer, parser, static type checker, three-address KIR, bytecode and bounded JavaScript VM.
- A standalone Windows launcher (`KavroStudio.exe`) that opens the offline Studio in Edge/Chrome app mode.
- **New in M2 preview:** a direct **Windows x86-64 PE32+** code generator (JavaScript implementation) that writes real machine code and PE headers without an external linker, for a deliberately limited set of Kavro programs.
- Integrated editor, shell, token/bytecode/KIR inspectors, PE metadata inspector, custom cursors, Aqua UI and a 10-lesson interactive PT-BR academy.
- Automated static tests; Windows native execution checks are defined for the GitHub Actions Windows runner, and their status must be verified there.

## Getting started on Windows 11

1. Download and extract the distribution ZIP **in full**. Do not run the launcher inside the archive.
2. Open `KavroStudio.exe` (it uses your installed Edge or Chrome).
3. For VM mode, open any example and press `Ctrl+Enter`.
4. For **native compilation**, open `native_hello.kvr` in the Explorer and click **EXE x64**. The browser will save `native_hello.exe` in Downloads.
5. Run that generated `.exe` from **Windows Terminal / PowerShell** to see its output. Native code is outside the VM sandbox; run only code you trust.

The native backend currently supports `fn main()`, `i64` and `bool` values, immutable/mutable local variables, `+ - * %`, comparisons, logical operators with short-circuit, `if`, bounded `while`, literal strings and integer/boolean `print`, and `assert`. No helper functions, recursion, floating point, arrays, pointers, FFI, string interpolation, or inline Assembly **in generated native binaries yet**. These features remain available only where documented for the VM.

**Caveat:** The VM uses JavaScript safe integers; the experimental native backend operates on signed 64-bit integers with overflow traps. Its semantics are not fully unified yet. See [M2 backend reference](docs/COMPILADOR_NATIVO_M2.md).

## Developer CLI (requires Node.js 20+)

```powershell
node cli/kavro.js check examples/native_hello.kvr
node cli/kavro.js run examples/native_hello.kvr
node cli/kavro.js native examples/native_hello.kvr native_hello.exe
node tests/native-m2.test.js
```

The exported `native_hello.exe` does **not** require Node, Chrome, or the Kavro VM at runtime. The **Studio launcher** itself still requires Edge/Chrome.

## Documentation

- [Comece aqui — Windows 11](README_COMECE_AQUI.md)
- [Aprenda Kavro (PT-BR)](docs/APRENDA_KAVRO.md)
- [Referência da linguagem](docs/REFERENCIA_DA_LINGUAGEM.md)
- [Backend nativo M2: implementação, limites e segurança](docs/COMPILADOR_NATIVO_M2.md)
- [Arquitetura KIR](docs/ARQUITETURA_KIR.md)
- [Roadmap](ROADMAP.md)
- [Security guidance](docs/SEGURANCA.md)

## Quality and security

- No `eval` or remote package fetch required to compile a `.kvr` file in Studio.
- VM execution includes step/time/output limits. Native binaries **do not run in the VM** and may use host OS resources; the current M2 generator inserts a loop iteration budget and arithmetic overflow checks.
- M2 is a research compiler, not a hardened compiler or verified toolchain. Check generated binaries and never disable Windows security protections to run them.
- Source and tests are intended to be reproducible; generated `.exe`, keys, build folders and ZIP files are not normally committed.
- **License:** not yet selected. Until a LICENSE is published, normal copyright rules apply; please discuss licensing before external reuse or contributions.

Repository: [axrobert/kavro-lang](https://github.com/axrobert/kavro-lang)
