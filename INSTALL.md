# lixPresentr — Installation Guide

This document describes the lixPresentr Windows installer behavior, command-line options, and return codes. It is referenced by the Microsoft Store certification process to interpret installer exit codes.

## Installer overview

- **Product:** lixPresentr (Bible projection desktop app by Creativlix Tech)
- **Installer type:** NSIS (Win32 executable installer)
- **Installer name:** `lixPresentr-Setup-X.Y.Z.exe`
- **Install scope:** Per-user (no administrator privileges required)
- **Execution level:** `asInvoker`
- **Default install location:** `%LOCALAPPDATA%\Programs\lixPresentr\`
- **User data location:** `%APPDATA%\lixPresentr\` (preserved on uninstall)
- **Architectures supported:** x64

## Command-line options

The installer is built with electron-builder NSIS and supports the standard NSIS command-line switches.

| Switch | Description |
|---|---|
| `/S` | Silent install (no UI). All defaults are accepted automatically. |
| `/D=<path>` | Set the installation directory. Must be the **last** parameter and **not** quoted, even if the path contains spaces. |
| `/allusers` | Install for all users (requires administrator elevation). |
| `/currentuser` | Install for the current user only (default). |

### Examples

```cmd
:: Silent install with defaults (per-user)
lixPresentr-Setup-1.0.5.exe /S

:: Silent install to a custom directory
lixPresentr-Setup-1.0.5.exe /S /D=C:\Apps\lixPresentr

:: Silent install for all users (requires admin)
lixPresentr-Setup-1.0.5.exe /S /allusers
```

## Installer return codes

The installer returns one of the following exit codes:

| Code | Scenario | Description |
|---|---|---|
| `0` | Installation successful | The installer completed without errors. |
| `1` | Generic failure | An unexpected error occurred during installation. |
| `2` | Aborted by installer | The installer aborted before completion (internal error). |
| `1602` | Cancelled by user | The user clicked Cancel or closed the installer window. |
| `1618` | Already in progress | Another installation of lixPresentr is already running. |
| `1638` | Newer version already installed | A newer version of lixPresentr is already present on the system. |

Return codes follow Microsoft's standard MSI/Win32 conventions where applicable. The installer does **not** require a system reboot under any circumstances and never returns `3010`.

## Uninstall

The application registers a standard uninstaller in the Windows Apps & Features list under the display name **lixPresentr**.

- Uninstaller binary: `%LOCALAPPDATA%\Programs\lixPresentr\Uninstall lixPresentr.exe`
- Silent uninstall: `Uninstall lixPresentr.exe /S`
- User data is **preserved by default** on uninstall (settings, local Bible DB, slide templates remain in `%APPDATA%\lixPresentr\`).

## System requirements

- Windows 10 (1809+) or Windows 11
- x64 processor
- 4 GB RAM minimum
- 500 MB free disk space (plus space for downloaded Bible versions)
- No additional runtime dependencies required (Node.js, Chromium, and all libraries are bundled)

## Network requirements

The application works **fully offline** after installation. The installer itself does **not** require network access. Optional cloud features (sync, voice transcription, AI assistant) require an internet connection at runtime only.

## Supported languages

The installer UI is available in:
- English (en-US)
- French (fr-FR)

The language is selected at the start of the installation process.

## Support

- Website: https://www.lixpresentr.app
- Documentation: https://www.lixpresentr.app/docs
- Contact: contact@lixpresentr.app
- Issues: https://github.com/Creativlix-Technologies/lixpresentr-releases/issues
