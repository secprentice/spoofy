# spoofy

[![npm version](https://img.shields.io/npm/v/spoofy)](https://www.npmjs.com/package/spoofy)
[![license](https://img.shields.io/npm/l/spoofy)](LICENSE)

> **⚠️ Work in Progress**: This is a modernized fork of the original `spoof` project, updated for compatibility with modern macOS (Sequoia 15.4+, Tahoe 26+). **Currently only macOS is fully supported.** Modern Windows and Linux support is planned but not yet implemented.

### Easily spoof your MAC address on macOS!

A Node.js utility for changing MAC addresses. Currently focused on reliable macOS support with Windows and Linux support coming soon.

## About This Fork

This repository is a fork of the original `spoof` project, updated to work with modern macOS versions where Apple has removed the `airport` CLI tool and introduced new WiFi driver restrictions.

### What's Changed

- **Modern macOS Support**: Fixed MAC spoofing for macOS Sequoia 15.4+ and Tahoe 26+
- **Removed `airport` dependency**: The deprecated `airport -z` command has been replaced with modern `networksetup` commands
- **Timing-sensitive MAC changes**: WiFi MAC addresses are now changed in the brief window after power-on but before network connection
- **Better error handling**: Ensures WiFi interface is always restored, even if MAC change fails
- **Cleaner codebase**: Removed deprecated code paths and unnecessary constants

## Installation

### From npm

```bash
npm install -g spoofy
```

### From source

```bash
git clone https://github.com/basedbytes/spoofy.git
cd spoofy
npm install
npm install -g .
```

## Quick Start

List network interfaces:
```bash
spoofy list
```

Randomize MAC address (WiFi is typically `en0` on macOS):
```bash
sudo spoofy randomize en0
```

**Note:** WiFi will disconnect briefly and may need to reconnect to networks.

## Usage

You can always see up-to-date usage instructions by running `spoofy --help`.

### List available devices

```bash
spoofy list
```

Output:

```
- "Ethernet" on device "en4" with MAC address 70:56:51:BE:B3:00
- "Wi-Fi" on device "en0" with MAC address 70:56:51:BE:B3:01 currently set to 70:56:51:BE:B3:02
- "Bluetooth PAN" on device "en1"
```

### List only Wi-Fi devices

```bash
spoofy list --wifi
```

### Randomize MAC address _(requires root)_

Using hardware port name:

```bash
sudo spoofy randomize wi-fi
```

Or using device name:

```bash
sudo spoofy randomize en0
```

### Set specific MAC address _(requires root)_

```bash
sudo spoofy set 00:11:22:33:44:55 en0
```

### Reset to original MAC address _(requires root)_

```bash
sudo spoofy reset wi-fi
```

**Note**: On macOS, restarting your computer will also reset your MAC address to the original hardware address.

## Platform Support

### macOS ✅

- ✅ **Fully supported** and tested on macOS Tahoe 26.2
- ✅ Works on macOS Sequoia 15.4+
- ⚠️ Older versions may work but are untested

### Linux 🚧

**Coming soon!** Linux support is planned but not yet implemented in this fork.

Running MAC change commands on Linux will display a "coming soon" message. You can still use `spoofy list` to view network interfaces.

The upcoming Linux implementation will use modern `ip link` commands instead of the deprecated `ifconfig` tool.

### Windows 🚧

**Coming soon!** Windows support is planned but not yet implemented in this fork.

Running MAC change commands on Windows will display a "coming soon" message. You can still use `spoofy list` to view network interfaces.

The upcoming Windows implementation will use PowerShell for more reliable adapter management.

## Known Issues

- WiFi will briefly disconnect when changing MAC address
- Some network restrictions or hardware may prevent MAC spoofing
- Requires sudo/root privileges for all MAC address changes

## Troubleshooting

If you encounter errors:

1. Make sure you're running with `sudo` (required for network changes)
2. Ensure WiFi is turned on before attempting to change MAC
3. On modern macOS, you may need to reconnect to WiFi after the change
4. Try running `networksetup -detectnewhardware` if changes don't take effect

## Contributing

This is an active fork. Contributions, bug reports, and feature requests are welcome!

## License

MIT License (inherited from original project)

## Credits

Originally based on the `spoof` project. This fork maintains compatibility with modern operating systems.
