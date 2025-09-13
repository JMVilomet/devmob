# Changelog

All notable changes to DevMob will be documented in this file.

This project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-09-02

### Added
- **Core DevMob Script**: Complete bash script for React Native development environment management
- **Docker Environment**: Full containerized development stack with Android SDK
- **Project Management**: Support for both Expo and React Native CLI projects
- **Android SDK Management**: Dynamic SDK version installation and AVD creation
- **Device Support**: USB and wireless ADB connectivity for physical devices
- **Emulator Support**: Android emulator with GUI and hardware acceleration
- **Wireless Debugging**: Automatic pairing and connection recovery
- **Multi-Project Support**: Ability to work with multiple projects simultaneously

### Features
- `./devmob init` - Initialize development environment
- `./devmob build` - Build and start Docker containers
- `./devmob expo [project]` - Create and run Expo projects
- `./devmob create [project]` - Create and run React Native CLI projects
- `./devmob use <version>` - Install Android SDK versions
- `./devmob emulator start/stop` - Control Android emulator
- `./devmob connect <ip:port>` - Wireless device debugging
- `./devmob android/ios [project]` - Run apps on devices
- `./devmob start/stop [project]` - Development server management
- `./devmob devices` - List connected devices
- `./devmob shell [project]` - Direct container access
- `./devmob test [project]` - Run project tests

### Technical Specifications
- **Base Image**: Ubuntu 22.04
- **Node JS**: Dynamic version support
- **Android SDK**: Dynamic version support
- **Build Tools**: Dynamic version support for Android build tools and NDK 
- **Hardware Support**: X11 access, USB devices
- **Storage**: Android images, platforms and AVDs persisted using host-mounted shared volumes

### Documentation
- Comprehensive README 
- Installation and setup instructions
- Configuration documentation

---

## [1.0.1] - 2025-09-07

### Added
- **Shell Command Enhancement**: Added `--root` option to `shell` command for opening root shell in project directory
  - Usage: `./devmob shell --root [project]`
  - Opens bash shell as root user when --root flag is present

---

## [1.0.2] - 2025-09-13

### Added
- **Logcat Command**: New `logcat` command for React Native debugging with smart device detection
  - Usage: `./devmob logcat` (auto-detects device) or `./devmob logcat -s <device>` (specify device)
  - Filters logs to show only ReactNative and ReactNativeJS messages (`*:S ReactNative:V ReactNativeJS:V`)
  - **Smart Device Detection**: Automatically prioritizes real devices over emulators when multiple devices are connected
  - **Device Priority System**: Real devices (IP addresses) have highest priority, emulators have lowest priority

---

