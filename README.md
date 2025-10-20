# Cursor Overlay for Gentoo

An unofficial Gentoo overlay providing the latest [Cursor](https://cursor.com/) AI-powered code editor.

## 🎯 About

This overlay provides up-to-date ebuilds for Cursor, the AI-first coding environment. The official `gentoo-zh` repository often lags behind the latest releases, so this overlay aims to provide the newest versions quickly.

## 📦 Current Version

- **Latest**: `app-editors/cursor-1.7.52`
- **Architecture**: `amd64`, `arm64`

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

## 🐛 Issues & Contributions

Found a bug or want to contribute? Please open an issue or pull request on [GitHub](https://github.com/Zakkaus/cursor-overlay).

## 📜 License

This overlay follows Gentoo's licensing. Individual ebuilds are GPL-2+.

The Cursor application itself is proprietary software. See [cursor.com](https://cursor.com/) for details.

## 🙏 Credits

- Based on ebuilds from [gentoo-zh](https://github.com/microcai/gentoo-zh)
- Maintained by [Zakkaus](https://github.com/Zakkaus)

## ⚠️ Disclaimer

This is an unofficial overlay and is not affiliated with Cursor or Anysphere Inc.
