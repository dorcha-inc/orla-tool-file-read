# orla-tool-fs

A comprehensive file system operations tool for [Orla](https://github.com/dorcha-inc/orla) that provides reading, writing, listing, and managing files and directories.

---
[![Go Version](https://img.shields.io/badge/Go-1.21+-00ADD8?style=flat&logo=go)](https://golang.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Go Report Card](https://goreportcard.com/badge/github.com/dorcha-inc/orla-tool-fs)](https://goreportcard.com/report/github.com/dorcha-inc/orla-tool-fs)
[![Build](https://github.com/dorcha-inc/orla-tool-fs/actions/workflows/build.yml/badge.svg)](https://github.com/dorcha-inc/orla-tool-fs/actions/workflows/build.yml)
[![Coverage](https://codecov.io/gh/dorcha-inc/orla-tool-fs/branch/main/graph/badge.svg)](https://codecov.io/gh/dorcha-inc/orla-tool-fs)
---

## Installation

Install from the orla registry:

```bash
orla install fs
```

This will install the latest version from the default registry. To install a specific version:

```bash
orla install --version v0.3.0
```

Or to use a custom registry:

```bash
orla install fs --registry https://github.com/dorcha-inc/orla-registry
```

## Usage

Once installed, the tool will be available as an MCP tool. It supports common file system operations. All operations require the `operation` parameter to specify which operation to perform. The full parameter schema is defined in `tool.yaml` and will be automatically available through the MCP protocol.

As an example:

```json
{
  "operation": "read",
  "path": "/path/to/file.txt"
}
```

## Error Handling

All operations return a JSON response with a `success` field. If `success` is `false`, an `error` field will contain the error message.

**Example error response:**
```json
{
  "success": false,
  "error": "File not found: /path/to/file.txt"
}
```

## Development

To test locally before publishing:

1. Build the tool:
   ```bash
   make build
   ```
   This creates `bin/fs.tool`

2. Copy the tool to your orla project's tools directory:
   ```bash
   cp bin/fs.tool /path/to/orla/tools/fs.tool
   ```
   Replace `/path/to/orla` with the actual path to your orla project. The tool will be discovered by orla automatically.

3. Start orla (from the orla project directory):
   ```bash
   orla serve
   ```
   The tool will be automatically discovered and available.

## Publishing

To publish a new version to the registry:

1. Ensure all changes are committed to the main branch

2. Publish using the Makefile with a version number:
   ```bash
   make publish VERSION=0.3.0
   ```
   This will:
   - Update the version in `tool.yaml`
   - Build the binary
   - Commit the binary and updated `tool.yaml`
   - Create and push a git tag `v0.3.0`
   - Push commits to the main branch

3. Add the tool entry to the registry's `registry.yaml` file in the [orla-registry](https://github.com/dorcha-inc/orla-registry) repository

4. After publishing, the tool can be installed with:
   ```bash
   orla install fs --version v0.3.0
   ```

## Contributing

Contributions are welcome! Please see the Orla project's [contribution guide](https://github.com/dorcha-inc/orla/blob/main/CONTRIBUTING.md).