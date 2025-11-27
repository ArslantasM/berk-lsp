# BERK Language Server Protocol (LSP)

**Official Language Server for BERK Programming Language**

[![License](https://img.shields.io/badge/License-GPL--3.0-blue.svg)](https://github.com/ArslantasM/berk/blob/main/LICENSE)
[![Made in Turkey](https://img.shields.io/badge/Made%20in-Turkey%20🇹🇷-E30A17?style=flat&labelColor=FFFFFF)](https://github.com/ArslantasM/berk)
[![BERK Version](https://img.shields.io/badge/BERK-v0.9.1-E30A17)](https://github.com/ArslantasM/berk)

## 🌟 What is BERK LSP?

BERK LSP is the official Language Server Protocol implementation for [BERK Programming Language](https://github.com/ArslantasM/berk) - the world's first dual-language (Turkish/English) systems programming language.

This language server provides rich IDE features for BERK in any LSP-compatible editor (VS Code, Neovim, Emacs, etc.).

## ✨ Features

### Core Language Features
- ✅ **Real-time Diagnostics**: Syntax and semantic error detection as you type
- ✅ **Code Completion**: Context-aware suggestions for both Turkish and English keywords
- ✅ **Hover Information**: Type signatures, documentation, and parameter hints
- ✅ **Go to Definition (F12)**: Jump to function/variable declarations across files 🆕
- ✅ **Find All References (Shift+F12)**: Find all usages of a symbol workspace-wide 🆕
- ✅ **Rename Symbol (F2)**: Safe refactoring with keyword protection 🆕

### Bilingual Support
- Full IntelliSense for Turkish keywords (`fonksiyon`, `değişken`, `eğer`, etc.)
- Full IntelliSense for English keywords (`function`, `let`, `if`, etc.)
- Mixed-language code support in the same file
- Smart context switching between languages

### Performance
- Fast startup time (<1s)
- Incremental parsing for large files
- Low memory footprint (~50MB typical)
- 310/310 tests passing (100% reliability)

## 📥 Installation

### Windows

1. **Download** the latest release:
   ```powershell
   # Download berk-lsp.exe from Releases
   # https://github.com/ArslantasM/berk-lsp/releases/latest
   ```

2. **Install** to a directory in your PATH:
   ```powershell
   # Option 1: System-wide (requires admin)
   Move-Item berk-lsp.exe "C:\Program Files\BERK\"
   # Add C:\Program Files\BERK to PATH
   
   # Option 2: User directory
   Move-Item berk-lsp.exe "$env:USERPROFILE\.berk\bin\"
   # Add to PATH: $env:Path += ";$env:USERPROFILE\.berk\bin"
   ```

3. **Verify** installation:
   ```powershell
   berk-lsp --version
   # Output: BERK Language Server v0.9.0
   ```

### Linux / macOS

1. **Download** the binary:
   ```bash
   # For Linux x64
   wget https://github.com/ArslantasM/berk-lsp/releases/latest/download/berk-lsp-linux-x64
   
   # For macOS (Intel)
   wget https://github.com/ArslantasM/berk-lsp/releases/latest/download/berk-lsp-macos-x64
   
   # For macOS (Apple Silicon)
   wget https://github.com/ArslantasM/berk-lsp/releases/latest/download/berk-lsp-macos-arm64
   ```

2. **Make executable** and install:
   ```bash
   chmod +x berk-lsp-*
   sudo mv berk-lsp-* /usr/local/bin/berk-lsp
   ```

3. **Verify** installation:
   ```bash
   berk-lsp --version
   ```

## 🔧 Editor Setup

### VS Code (Recommended)

Install the official [BERK extension](https://marketplace.visualstudio.com/items?itemName=ArslantasM-tools.berk-lang):

```bash
# From VS Code Marketplace
code --install-extension ArslantasM-tools.berk-lang
```

The extension will automatically detect and use `berk-lsp` if it's in your PATH.

**Manual Configuration:**
```json
// settings.json
{
  "berk.languageServerPath": "C:\\path\\to\\berk-lsp.exe"
}
```

### Neovim

Using `nvim-lspconfig`:

```lua
-- ~/.config/nvim/lua/lsp/berk.lua
local lspconfig = require('lspconfig')
local configs = require('lspconfig.configs')

-- Define BERK LSP
if not configs.berk_lsp then
  configs.berk_lsp = {
    default_config = {
      cmd = { 'berk-lsp' },
      filetypes = { 'berk' },
      root_dir = lspconfig.util.root_pattern('.git', 'berk.toml'),
      settings = {},
    },
  }
end

-- Activate
lspconfig.berk_lsp.setup {}
```

### Emacs

Using `lsp-mode`:

```elisp
;; ~/.emacs.d/init.el
(with-eval-after-load 'lsp-mode
  (add-to-list 'lsp-language-id-configuration '(berk-mode . "berk"))
  (lsp-register-client
   (make-lsp-client
    :new-connection (lsp-stdio-connection '("berk-lsp"))
    :major-modes '(berk-mode)
    :server-id 'berk-lsp)))
```

### Sublime Text

Using LSP package:

```json
// LSP.sublime-settings
{
  "clients": {
    "berk-lsp": {
      "enabled": true,
      "command": ["berk-lsp"],
      "selector": "source.berk"
    }
  }
}
```

## 🚀 Usage

The LSP server runs automatically when you open a `.berk` file in a configured editor.

### Command Line Options

```bash
berk-lsp [OPTIONS]

Options:
  --version        Print version and exit
  --help           Show this help message
  --stdio          Use stdio transport (default)
  --tcp <PORT>     Use TCP transport on specified port
  --log <FILE>     Log output to file (for debugging)
```

### Debugging

Enable verbose logging:

```bash
# Log to file
berk-lsp --log /tmp/berk-lsp.log

# In VS Code, check Output panel:
View → Output → BERK Language Server
```

## 📊 LSP Capabilities

| Feature | Status | Since |
|---------|--------|-------|
| Text Document Sync | ✅ Full | v0.8.0 |
| Diagnostics | ✅ Full | v0.8.0 |
| Code Completion | ✅ Full | v0.8.0 |
| Hover | ✅ Full | v0.8.0 |
| Go to Definition | ✅ Full | v0.9.1 |
| Find References | ✅ Full | v0.9.1 |
| Rename | ✅ Full | v0.9.1 |
| Signature Help | 🚧 Planned | v1.0.0 |
| Code Actions | 🚧 Planned | v1.0.0 |
| Semantic Tokens | 🚧 Planned | v1.5.0 |
| Inlay Hints | 🚧 Planned | v1.5.0 |
| Code Lens | 🚧 Planned | v1.5.0 |

## 🏗️ Building from Source

Prerequisites:
- Rust 1.70+
- LLVM 17.0.6+
- Git

```bash
# Clone repository
git clone https://github.com/ArslantasM/berk.git
cd berk/berk-lang

# Build LSP server
cargo build --release --bin berk-lsp

# Binary location
target/release/berk-lsp.exe  # Windows
target/release/berk-lsp      # Linux/macOS
```

## 🧪 Testing

The LSP server has comprehensive test coverage:

```bash
# Run all LSP tests
cd berk-lang
cargo test --features llvm lsp

# Test statistics:
# - 310/310 unit tests passing
# - 7 LSP capabilities tested
# - JSON-RPC 2.0 protocol compliance
```

## 📚 Documentation

- **BERK Language Guide**: https://arslantasm.github.io/berk_pages/
- **Standard Library API**: https://arslantasm.github.io/berk-stdlib-docs/
- **Main Repository**: https://github.com/ArslantasM/berk
- **VS Code Extension**: https://marketplace.visualstudio.com/items?itemName=ArslantasM-tools.berk-lang
- **LSP Specification**: https://microsoft.github.io/language-server-protocol/

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](https://github.com/ArslantasM/berk/blob/main/CONTRIBUTING.md) in the main repository.

### Development Setup

1. Fork and clone the main BERK repository
2. Make changes in `berk-lang/src/lsp/`
3. Test with `cargo test lsp`
4. Submit a pull request

## 📋 Requirements

- **Windows**: Windows 10+ (x64)
- **Linux**: glibc 2.31+ (Ubuntu 20.04+, Fedora 32+)
- **macOS**: macOS 11+ (Big Sur)

## 🐛 Troubleshooting

### LSP Not Starting

```bash
# Check if binary exists
which berk-lsp  # Linux/macOS
where berk-lsp  # Windows

# Check permissions
chmod +x berk-lsp  # Linux/macOS

# Test manually
berk-lsp --version
```

### Connection Issues

1. Check editor's LSP logs
2. Ensure `berk-lsp` is in PATH
3. Verify firewall settings (if using TCP)
4. Try `--log` option for debugging

### Performance Issues

- Close unused BERK files
- Increase editor's LSP timeout settings
- Check system resources (RAM/CPU)
- Report large file issues on GitHub

## 📄 License

GPL-3.0 - Same as BERK Programming Language

See [LICENSE](https://github.com/ArslantasM/berk/blob/main/LICENSE) for details.

## 🔗 Links

- **Main Project**: https://github.com/ArslantasM/berk
- **Language Documentation**: https://arslantasm.github.io/berk_pages/
- **Standard Library**: https://arslantasm.github.io/berk-stdlib-docs/
- **VS Code Extension**: https://marketplace.visualstudio.com/items?itemName=ArslantasM-tools.berk-lang
- **Report Issues**: https://github.com/ArslantasM/berk/issues
- **Discussions**: https://github.com/ArslantasM/berk/discussions

---

**Made with ❤️ in Turkey 🇹🇷**

*BERK LSP v0.9.1 - Released November 28, 2025*
