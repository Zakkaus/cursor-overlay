# Contributing Guide

**English** | [繁體中文](CONTRIBUTING_zh-TW.md)

Thank you for considering contributing to Cursor Overlay! This document provides guidelines for the contribution process and best practices.

## How to Contribute

### Reporting Issues
- Check if the issue already exists
- Provide detailed information about your system and the problem
- Include error messages and logs if applicable

### Submitting Pull Requests

1. Fork the repository
2. Create a new branch for your feature/fix
3. Make your changes
4. Test your changes locally
5. Submit a pull request with a clear description

### Updating Cursor Version

To add a new Cursor version:

1. Copy the latest ebuild:
   ```bash
   cp app-editors/cursor/cursor-1.7.52.ebuild app-editors/cursor/cursor-X.Y.Z.ebuild
   ```

2. Update the `BUILD_ID` in the new ebuild:
   - Check the Cursor download page or GitHub releases
   - The BUILD_ID is usually a git commit hash

3. Generate the Manifest:
   ```bash
   ebuild cursor-X.Y.Z.ebuild manifest
   ```

4. Test the installation:
   ```bash
   emerge -av =app-editors/cursor-X.Y.Z
   ```

5. Submit a pull request

## Code Style

- Follow Gentoo ebuild guidelines
- Use tabs for indentation in ebuilds
- Keep ebuild comments clear and concise

## Testing

Before submitting, please test:
- Installation on clean system
- Upgrade from previous version
- Uninstallation

## Questions?

Open an issue for any questions or concerns.
