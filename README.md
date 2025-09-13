# DevMob

**A Docker-based React Native development environment that eliminates setup complexity and provides a consistent, reproducible mobile development stack.**

[![Docker](https://img.shields.io/badge/Docker-Required-blue.svg)](https://www.docker.com/)
[![React Native](https://img.shields.io/badge/React%20Native-Supported-green.svg)](https://reactnative.dev/)
[![Expo](https://img.shields.io/badge/Expo-Supported-purple.svg)](https://expo.dev/)
[![Android](https://img.shields.io/badge/Android-SDK%20Included-brightgreen.svg)](https://developer.android.com/)

## Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Usage](#usage)
  - [Environment Management](#environment-management)
  - [Project Creation](#project-creation)
  - [Development Server](#development-server)
  - [Device Management](#device-management)
  - [Debugging](#debugging)
  - [Android SDK Management](#android-sdk-management)
  - [Emulator Control](#emulator-control)
  - [Wireless Debugging](#wireless-debugging)
  - [Testing](#testing)
  - [Shell Access](#shell-access)
- [Examples](#examples)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgments](#acknowledgments)

## Features

DevMob solves the "works on my machine" problem for React Native development by containerizing the entire mobile development stack. Key features include:

### 🚀 **Project Management**
- **Dual Project Support**: Create both Expo and React Native CLI projects
- **Automatic Detection**: Intelligent project type detection and command routing
- **Quick Setup**: One-command project creation with dependency installation

### 📱 **Device & Emulator Support**
- **Android Emulator**: Full GUI support
- **Physical Devices**: USB and wireless ADB connectivity
- **Wireless Debugging**: Automatic pairing and connection recovery
- **Multi-Device**: Support for multiple connected devices

### 🛠 **Development Tools**
- **Metro/Expo Server**: Functional and supporting hot reloading
- **Testing Framework**: command to run project tests directly in the current project
- **Shell Access**: Direct container access for advanced operations

### 🔧 **Android SDK Management**
- **Dynamic Installation**: Install any Android SDK version on-demand
- **AVD Management**: Automatic Android Virtual Device creation
- **Build Tools**: Complete Android build toolchain
- **NDK Support**: Native Development Kit included

### 🌐 **Cross-Platform Development**
- **Android Support**: Full Android development stack
- **iOS Support**: iOS development commands (requires macOS host)
- **Expo Integration**: Seamless Expo workflow support
- **Universal Commands**: Consistent CLI across project types

## Prerequisites

### System Requirements

- **Operating System**: Linux with Docker support
- **Docker**: Docker Engine and Docker Compose
- **Storage**: At least 7GB free space for both image and container

## Installation

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd devmob
   ```

2. **Make the script executable**:
   ```bash
   chmod +x devmob
   ```

3. **Initialize the environment**:
   ```bash
   ./devmob init
   ```

4. **Build the containers**:
   ```bash
   ./devmob build
   ```

## Quick Start

Get up and running with a new React Native project in minutes:

```bash
# 1. Initialize environment
./devmob init

# 2. Build containers
./devmob build

# 3. Install an Android SDK version
./devmob use 30

# 4. Start the emulator
./devmob emulator start

# 5. Create a new Expo project
./devmob expo

```

For React Native CLI projects:

```bash
# Create React Native CLI project
./devmob create

# Run on Android device/emulator
./devmob android
```

## Usage

#### Initialize Environment
```bash
./devmob init
```
Creates `.env` file, sets up X11 forwarding, and prepares Android SDK directories.

#### Build Containers
```bash
./devmob build
```
Builds and starts Docker containers with all development tools.

#### Start/Stop Services
```bash
./devmob start [project_name]    # Start development server
./devmob stop                    # Stop all containers
```

#### View Logs
```bash
./devmob logs              # Show container logs
```

### Project Creation

#### Create Expo Project
```bash
./devmob expo [project_name]
```
- Creates new Expo project with latest template
- Installs dependencies automatically
- Starts development server

#### Create React Native CLI Project
```bash
./devmob create [project_name]
```
- Initializes React Native CLI project
- Sets up build configuration
- Installs dependencies
- Starts Metro bundler

### Development Server

#### Start Development Server
```bash
./devmob start [project_name]
```
- Automatically detects and stops existing Metro processes
- Starts fresh development server
- Supports hot reloading and live updates

### Device Management

#### List Connected Devices
```bash
./devmob devices
```
Shows all connected Android devices and emulators.

### Debugging

#### View React Native Logs
```bash
./devmob logcat [-s <device>]
```

**Auto-detect device** (recommended):
```bash
./devmob logcat
```
- Automatically detects connected devices
- Prioritizes real devices over emulators
- Shows only ReactNative and ReactNativeJS logs

**Specify device manually**:
```bash
./devmob logcat -s 192.168.1.100:5555
./devmob logcat -s emulator-5554
```

#### Run on Android
```bash
./devmob android [project_name]
```
- Auto-detects project type (Expo vs React Native CLI)
- Uses appropriate build command
- Installs and launches app on connected device/emulator

#### Run on iOS
```bash
./devmob ios [project_name]
```
- Supports iOS development (requires macOS host)
- Auto-detects project type
- Uses appropriate iOS build tools

### Android SDK Management

#### Install SDK Version
```bash
./devmob use <version>
```
Example:
```bash
./devmob use 34    # Install Android 14 (API 34)
```

This command:
- Downloads and installs SDK platform
- Installs compatible build tools
- Downloads system images
- Creates AVD (Android Virtual Device)

### Emulator Control

#### Start Emulator
```bash
./devmob emulator start
```
Launches the `default_avd` Android Virtual Device with GUI support.

#### Stop Emulator
```bash
./devmob emulator stop
```
Gracefully stops the running emulator instance.

### Wireless Debugging

#### Connect to Device
```bash
./devmob connect <ip:port> [pair_port]
```

Example:
```bash
./devmob connect 192.168.1.100:5555
```

**With pairing** (for first-time connection):
```bash
./devmob connect 192.168.1.100:5555 43210
```

The command provides:
- Automatic pairing for new devices
- Connection retry logic
- Troubleshooting guidance
- Port change detection

### Testing

#### Run Tests
```bash
./devmob test [project_name]
```
Executes the project's test suite using npm test.

### Shell Access

#### Open Project Shell
```bash
./devmob shell [project_name]
```
Opens bash shell in the specified project directory for advanced operations.

#### Execute Custom Commands
```bash
./devmob <any_command>
```
Passes any command directly to the container:
```bash
./devmob ls -la                    # List files
./devmob npm install lodash       # Install package
./devmob logcat                   # View React Native logs (filtered)
./devmob adb logcat               # View all Android logs (unfiltered)
```

## Examples

### Complete Development Workflow

```bash
# 1. Setup environment
./devmob init
./devmob build

# 2. Install Android SDK
./devmob use 34

# 3. Start emulator
./devmob emulator start

# 4. Create and run Expo project
./devmob expo MyExpoApp
# Development server starts automatically

# 5. In another terminal, run on Android
./devmob android MyExpoApp
```

### Physical Device Development

```bash
# 1. Enable wireless debugging on Android device
# Settings > Developer Options > Wireless Debugging

# 2. Connect to device
./devmob connect 192.168.1.100:5555

# 3. View logs while developing
./devmob logcat

# 4. Run your app
./devmob android MyProject
```

## Configuration

### Environment Variables

The `.env` file (created by `./devmob init`) contains:

```bash
# User and display settings
UID=1000
GID=1000
DISPLAY=:0

# Hardware access
RENDER_GID=105
KVM_GID=104

# Localization
LANG=en_US.UTF-8
LANGUAGE=en_US:en
LC_ALL=en_US.UTF-8
TZ=Europe/Paris

# Android SDK configuration
SDK_VERSION=commandlinetools-linux-11076708_latest.zip
ANDROID_BUILD_VERSION=36
ANDROID_TOOLS_VERSION=36.0.0
NDK_VERSION=27.1.12297006
ANDROID_HOME=/opt/android

# Node.js and tools
NODE_VERSION=22.14
WATCHMAN_VERSION=4.9.0
CMAKE_VERSION=3.30.5
```

### Container Configuration

Key [`docker-compose.yaml`](docker-compose.yaml) settings:

- **Memory Limit**: 8GB RAM, 2GB shared memory
- **Network**: Host network mode for device connectivity
- **Volumes**: Persistent Android SDK and project storage
- **Devices**: GPU, USB, and KVM access
- **Security**: Privileged mode for hardware access

### Default Project Settings

- **Default Project Name**: `devmobApp`
- **Default Device**: `pixel_6`
- **Container Name**: `devmob`

Modify these in the [`devmob`](devmob) script header:

```bash
PROJECT=devmobApp
DEVICE_DEF="pixel_6"
CONTAINER=devmob
```

## Troubleshooting

### Common Issues

#### Emulator GUI Not Showing
```bash
# Enable X11 forwarding on your host
xhost +local:docker

# Check DISPLAY variable
echo $DISPLAY

# Verify GPU access
ls -la /dev/dri
```

#### Device Connection Issues
```bash
# Restart ADB
./devmob adb kill-server
./devmob adb start-server

```

### Network Issues

#### Wireless Debugging Problems
1. Ensure both devices are on the same network
2. Check firewall settings
3. Restart wireless debugging on Android device
4. Try different connection ports

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**DevMob** - Making React Native development consistent, reproducible, and hassle-free across all environments.