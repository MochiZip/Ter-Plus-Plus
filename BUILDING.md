# Building Ter-Plus-Plus

Instructions for building Ter-Plus-Plus from source.

## Prerequisites

### All Platforms
- Git
- Node.js 16+ (or your preferred runtime)
- npm/yarn (or equivalent package manager)

### Windows
- Visual Studio Build Tools or Visual Studio 2019+
- Python 3.8+

### macOS
- Xcode Command Line Tools: `xcode-select --install`
- Python 3.8+

### Linux
- Build essentials: `sudo apt install build-essential` (Debian/Ubuntu)
- Python 3.8+

## Clone the Repository

```bash
git clone https://github.com/MochiZip/Ter-Plus-Plus.git
cd Ter-Plus-Plus
```

## Install Dependencies

```bash
npm install
# or
yarn install
```

## Build the Browser

### Development Build
```bash
npm run dev
```

### Production Build
```bash
npm run build
```

### Build for Specific Platform

```bash
# Windows
npm run build:windows

# macOS
npm run build:macos

# Linux
npm run build:linux

# All platforms
npm run build:all
```

## Run Tests

```bash
npm test
```

## Create Installers

```bash
npm run package
# or for specific platform:
npm run package:windows
npm run package:macos
npm run package:linux
```

## Troubleshooting

### Build fails on Windows
- Ensure Visual Studio Build Tools are installed
- Try: `npm install --global windows-build-tools`

### Build fails on macOS
- Update Xcode: `xcode-select --install`
- Clear cache: `rm -rf node_modules && npm install`

### Build fails on Linux
- Install development headers: `sudo apt-get install build-essential python3`

---

For more information, see the [main README](./README.md).
