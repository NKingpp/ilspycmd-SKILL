# ilspycmd SKILL

<p align="center">
<em>Trae IDE Skill for ilspycmd — the .NET assembly decompiler CLI.</em>
</p>

<p align="center">
<a href="#english">English</a> · <a href="#中文">中文</a>
</p>

---

## English

### Overview

A [Trae IDE](https://trae.ai) Skill that provides comprehensive guidance for using **ilspycmd**, the command-line .NET assembly decompiler from the [ILSpy](https://github.com/icsharpcode/ILSpy) project. It covers installation, usage, and common workflows across Windows, macOS, and Linux.

### What is ilspycmd?

ilspycmd can decompile .NET assemblies (DLL/EXE) back into C# source code, generate portable PDBs, list types, export full compilable projects, and produce interactive HTML class diagrams. It supports .NET Framework, .NET Core, and .NET 5+ assemblies.

### Install the Skill

**Option 1 — via npx (recommended)**:

```bash
npx skills add NKingpp/ilspycmd-SKILL
```

**Option 2 — manual copy**:

```bash
mkdir -p ~/.trae/skills/ilspycmd
cp SKILL.md ~/.trae/skills/ilspycmd/SKILL.md
```

Then restart Trae IDE or reload the window for the skill to take effect.

### Quick Start (ilspycmd tool itself)

Requires [.NET SDK](https://dotnet.microsoft.com/download) 6.0+.

```bash
dotnet tool install --global ilspycmd
```

Decompile an assembly:

```bash
ilspycmd sample.dll
```

Decompile as a full project:

```bash
ilspycmd -p -o ./output sample.dll
```

For the full option reference and OS-specific examples, see [SKILL.md](SKILL.md).

---

## 中文

### 概述

一个 [Trae IDE](https://trae.ai) Skill，提供 **ilspycmd**（来自 [ILSpy](https://github.com/icsharpcode/ILSpy) 项目的 .NET 程序集命令行反编译器）的完整使用指南。涵盖安装、用法以及 Windows、macOS 和 Linux 上的常见工作流。

### ilspycmd 是什么？

ilspycmd 可以将 .NET 程序集（DLL/EXE）反编译为 C# 源代码、生成便携式 PDB 调试文件、列出类型、导出完整可编译项目，以及生成交互式 HTML 类图。支持 .NET Framework、.NET Core 和 .NET 5+ 程序集。

### 安装 Skill

**方式一 — 通过 npx 安装（推荐）**：

```bash
npx skills add NKingpp/ilspycmd-SKILL
```

**方式二 — 手动复制**：

```bash
mkdir -p ~/.trae/skills/ilspycmd
cp SKILL.md ~/.trae/skills/ilspycmd/SKILL.md
```

然后重启 Trae IDE 或重新加载窗口，skill 即可生效。

### 快速开始（ilspycmd 工具本身）

需要安装 [.NET SDK](https://dotnet.microsoft.com/download) 6.0+。

```bash
dotnet tool install --global ilspycmd
```

反编译程序集：

```bash
ilspycmd sample.dll
```

反编译为完整项目：

```bash
ilspycmd -p -o ./output sample.dll
```

完整的参数说明和各操作系统示例，请参阅 [SKILL.md](SKILL.md)。

---

## License

[Apache License 2.0](LICENSE)
