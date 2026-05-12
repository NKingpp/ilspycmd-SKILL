---
name: "ilspycmd"
description: ".NET assembly decompiler CLI tool. Invoke when user needs to decompile DLL/EXE files, reverse engineer .NET assemblies, extract C# source code from compiled binaries, or analyze .NET metadata."
---

# ilspycmd - .NET Assembly Decompiler

ilspycmd is the command-line frontend for ILSpy, the open-source .NET assembly browser and decompiler. It can decompile .NET assemblies back into C# source code, generate portable PDBs, list types, and export full compilable projects. It runs on Windows, macOS, and Linux via the .NET SDK.

## Installation

Requires the [.NET SDK](https://dotnet.microsoft.com/download) (6.0+) installed.

```bash
dotnet tool install --global ilspycmd
```

To update to the latest version:

```bash
dotnet tool update --global ilspycmd
```

### OS-Specific Notes

**Windows**: After install, the tool is available in `PowerShell` or `cmd`. The global tool path is `%USERPROFILE%\.dotnet\tools`.

**macOS / Linux**: After install, ensure `~/.dotnet/tools` is in your `PATH`:

```bash
export PATH="$PATH:$HOME/.dotnet/tools"
```

Add the line above to your shell profile (`~/.zshrc`, `~/.bashrc`, or `~/.bash_profile`) for persistence.

## Basic Usage

```
ilspycmd [options] <Assembly file name(s)>
```

The assembly file argument is mandatory. Multiple assemblies can be specified. Use OS-native path separators (`\` on Windows, `/` on macOS/Linux).

## Common Operations

### Decompile entire assembly to stdout

```bash
ilspycmd sample.dll
```

### Decompile to output directory (single file)

**Windows**:

```powershell
ilspycmd -o .\decompiled sample.dll
```

**macOS / Linux**:

```bash
ilspycmd -o ./decompiled sample.dll
```

### Decompile as compilable project (one .cs per type)

**Windows**:

```powershell
ilspycmd -p -o .\decompiled-project sample.dll
```

**macOS / Linux**:

```bash
ilspycmd -p -o ./decompiled-project sample.dll
```

### Decompile a specific type

```bash
ilspycmd -t "MyNamespace.MyClass" sample.dll
```

### List all classes and interfaces

```bash
ilspycmd -l c,i sample.dll
```

### Show IL code instead of C#

```bash
ilspycmd -il sample.dll
```

### Generate PDB symbols

```bash
ilspycmd -genpdb sample.dll
```

### Decompile with PDB variable names

```bash
ilspycmd -usepdb -o ./output sample.dll
```

## Full Option Reference

| Option | Description |
|---|---|
| `-v\|--version` | Show version of ICSharpCode.Decompiler |
| `-h\|--help` | Show help information |
| `-o\|--outputdir <dir>` | Output directory (omit to write to stdout) |
| `-p\|--project` | Decompile as compilable project (requires `-o`) |
| `-t\|--type <name>` | Fully qualified type name to decompile |
| `-il\|--ilcode` | Show IL code instead of C# |
| `--il-sequence-points` | Show IL with sequence points (implies `-il`) |
| `-genpdb\|--generate-pdb` | Generate portable PDB |
| `-usepdb\|--use-varnames-from-pdb` | Use variable names from PDB |
| `-l\|--list <types>` | List entities: c(lass), i(nterface), s(truct), d(elegate), e(num) |
| `-lv\|--languageversion <ver>` | C# language version: CSharp1–CSharp12_0, Preview, Latest (default: Latest) |
| `-r\|--referencepath <path>` | Dependency search path (can be repeated) |
| `--no-dead-code` | Remove dead code from output |
| `--no-dead-stores` | Remove dead stores from output |
| `-d\|--dump-package` | Dump NuGet package assemblies (requires `-o`) |
| `--nested-directories` | Use namespace-based nested directory structure |
| `--disable-updatecheck` | Disable automatic update check |
| `--generate-diagrammer` | Generate interactive HTML class diagrammer |
| `--generate-diagrammer-include <regex>` | Whitelist types for diagrammer by regex on Type.FullName |
| `--generate-diagrammer-exclude <regex>` | Blacklist types for diagrammer by regex on Type.FullName |
| `--generate-diagrammer-report-excluded` | Output report of excluded diagrammer types |
| `--generate-diagrammer-docs <path>` | Path to XML documentation comments file |
| `--generate-diagrammer-strip-namespaces <namespaces>` | Strip namespaces from XML doc comments |

## Typical Workflows

### Reverse engineer a library

**Windows**:

```powershell
ilspycmd -p --nested-directories -r C:\path\to\dependencies -o .\src C:\path\to\Library.dll
```

**macOS / Linux**:

```bash
ilspycmd -p --nested-directories -r /path/to/dependencies -o ./src /path/to/Library.dll
```

### Inspect a single class with IL

```bash
ilspycmd -il -t "Namespace.ClassName" sample.dll
```

### Batch decompile multiple assemblies

**Windows**:

```powershell
ilspycmd -o .\output lib1.dll lib2.dll lib3.dll
```

**macOS / Linux**:

```bash
ilspycmd -o ./output lib1.dll lib2.dll lib3.dll
```

### Generate class diagram HTML app

```bash
ilspycmd --generate-diagrammer -o ./diagrams sample.dll
```

### Decompile to specific C# version

```bash
ilspycmd -lv CSharp8_0 -o ./output sample.dll
```

### Decompile a .NET bundle / single-file app

```bash
ilspycmd -d -o ./extracted MyApp.exe
```

## Key Notes

- When using `-p` (project mode), `-o` (output directory) is **required**.
- The `-r` option can be specified multiple times to add several dependency search paths.
- Entity types for `-l`: `c` (class), `i` (interface), `s` (struct), `d` (delegate), `e` (enum). Combine with commas: `-l c,i,s`.
- Language versions range from `CSharp1` to `CSharp12_0`, plus `Preview` and `Latest`.
- For fully automated/CI scenarios, use `--disable-updatecheck` to avoid network calls.
- The tool supports .NET Framework, .NET Core, .NET 5+ assemblies, and NuGet packages.
- On Windows, paths use backslashes (`\`); on macOS/Linux, paths use forward slashes (`/`).
- The tool behaves identically across all operating systems — only paths and shell syntax differ.
