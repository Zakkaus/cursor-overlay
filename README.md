# Cursor Overlay for Gentoo

**English** | [繁體中文](README_zh-TW.md)

An unofficial Gentoo overlay providing the latest version of [Cursor](https://cursor.com/), the revolutionary AI-powered code editor built for productivity.ursor Overlay for Gentoo

An unofficial Gentoo overlay providing the latest [Cursor](https://cursor.com/) AI-powered code editor.

## 🎯 About

Cursor is a revolutionary AI-powered code editor that brings the future of coding to your fingertips. Built on top of VS Code's foundation, Cursor integrates cutting-edge AI capabilities directly into your development workflow.

### ✨ Key Features

- **🤖 AI-Powered Coding**: Intelligent code completion and generation powered by GPT-4 and other advanced models
- **💬 Chat with Your Code**: Ask questions about your codebase and get instant answers with context
- **🔄 Code Refactoring**: AI-assisted refactoring and optimization suggestions
- **📝 Natural Language Edits**: Describe changes in plain language and watch them happen
- **🎯 Context-Aware**: AI understands your entire project structure and dependencies
- **🚀 VSCode Compatible**: Full compatibility with VSCode extensions and workflows

### Why This Overlay?

This overlay provides:
- **🚀 Latest Versions**: Track official Cursor releases with quick updates
- **🔧 Native Integration**: Proper Gentoo package management and system integration
- **🎨 USE Flags**: Flexible feature configuration (Wayland, EGL, etc.)
- **🌏 Multi-Language**: Support for Chinese (Traditional/Simplified), English, and 30+ languages
- **🔐 Secure**: Official download sources with integrity verification

## 📦 Current Version

## 📦 Current Version

- **Latest Version**: `app-editors/cursor-1.7.52`
- **Supported Architectures**: `amd64` (x86_64), `arm64` (aarch64)
- **Electron Version**: 34.5.8
- **Node.js Version**: 132.0.6834.210
- **Release Date**: 2025-10-17

## 🚀 Installation

### Method 1: Using eselect-repository (Recommended)

```bash
# Add this overlay
sudo eselect repository add cursor-overlay git https://github.com/Zakkaus/cursor-overlay.git

# Sync
sudo emerge --sync cursor-overlay

# Install Cursor
sudo emerge -av app-editors/cursor
```

### Method 2: Manual Installation

```bash
# Clone this repository
git clone https://github.com/Zakkaus/cursor-overlay.git /var/db/repos/cursor-overlay

# Add to repos.conf
sudo tee /etc/portage/repos.conf/cursor-overlay.conf << 'EOF'
[cursor-overlay]
location = /var/db/repos/cursor-overlay
sync-type = git
sync-uri = https://github.com/Zakkaus/cursor-overlay.git
auto-sync = yes
EOF

# Sync and install
sudo emerge --sync cursor-overlay
sudo emerge -av app-editors/cursor
```

## 🔧 Configuration

### Accept Keywords

If you're on stable `amd64`, you may need to accept testing keywords:

```bash
echo "app-editors/cursor ~amd64" | sudo tee /etc/portage/package.accept_keywords/cursor
```

### USE Flags

Available USE flags:
- `egl` - Enable EGL support (recommended)
- `wayland` - Enable Wayland support (recommended for Wayland users)
- `kerberos` - Enable Kerberos authentication support

Example:
```bash
echo "app-editors/cursor wayland egl" | sudo tee /etc/portage/package.use/cursor
```

## 📝 Supported Languages

The ebuild includes support for multiple languages through `L10N`:
- Chinese (Simplified): `zh-CN`
- Chinese (Traditional): `zh-TW`
- English: `en-GB`
- And many more...

## 🔄 Updates

This overlay is updated regularly to track the latest Cursor releases. To update:

```bash
sudo emerge --sync cursor-overlay
sudo emerge -u app-editors/cursor
```

## 🐛 Issues and Contributing

### Reporting Issues

Found a bug or have a feature request? Please report it on [GitHub Issues](https://github.com/Zakkaus/cursor-overlay/issues).

When reporting, please provide:
- Gentoo version and architecture (`uname -a`)
- Cursor version (`cursor --version`)
- Error messages and logs
- Steps to reproduce

### Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details.

Quick start:
1. Fork this repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📚 Resources

### Cursor Official

- **Official Website**: https://cursor.com/
- **Documentation**: https://docs.cursor.com/
- **GitHub**: https://github.com/getcursor/cursor (Community)
- **Discord**: https://discord.gg/cursor

### Gentoo Resources

- **Gentoo Official**: https://www.gentoo.org/
- **Gentoo Wiki**: https://wiki.gentoo.org/
- **Overlays Guide**: https://wiki.gentoo.org/wiki/Overlay
- **ebuild Development**: https://devmanual.gentoo.org/

### Other Cursor Overlays

- **gentoo-zh**: https://github.com/microcai/gentoo-zh (Official Chinese overlay)

## ⚠️ Disclaimer

This is an **unofficial** overlay and is not affiliated with Cursor or Anysphere Inc.

- Cursor is proprietary software owned by Anysphere Inc.
- This overlay only provides installation ebuilds, not the Cursor application itself
- Use of Cursor is subject to their [Terms of Service](https://cursor.com/terms)
- This overlay is released under the MIT License

## 📜 License

### Overlay License

This overlay (ebuild scripts and configuration files) is licensed under the **MIT License**.

See [LICENSE](LICENSE) file for details.

### Cursor Software License

The Cursor application itself is proprietary software:
- Copyright © Anysphere Inc.
- Usage subject to Cursor [Terms of Service](https://cursor.com/terms)
- See https://cursor.com/ for details

## 🙏 Acknowledgments

- Thanks to [gentoo-zh](https://github.com/microcai/gentoo-zh) for the original ebuild reference
- Thanks to the Cursor team for creating an amazing AI-powered code editor
- Thanks to all contributors and users for their support

## 📞 Contact

- **Maintainer**: [Zakkaus](https://github.com/Zakkaus)
- **Email**: zakkauu@gmail.com
- **GitHub**: https://github.com/Zakkaus/cursor-overlay
- **Issue Tracker**: https://github.com/Zakkaus/cursor-overlay/issues

---

**Like this overlay?** Give it a ⭐️ Star!

**Have questions?** Open an [Issue](https://github.com/Zakkaus/cursor-overlay/issues/new)!

**Want to contribute?** Submit a [Pull Request](https://github.com/Zakkaus/cursor-overlay/pulls)!

## 🙏 Credits

- Based on ebuilds from [gentoo-zh](https://github.com/microcai/gentoo-zh)
- Maintained by [Zakkaus](https://github.com/Zakkaus)

## ⚠️ Disclaimer

This is an unofficial overlay and is not affiliated with Cursor or Anysphere Inc.
