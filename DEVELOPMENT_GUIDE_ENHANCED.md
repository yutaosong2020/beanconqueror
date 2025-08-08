# Beanconqueror Development Guide - Enhanced

This comprehensive guide covers everything you need to know to develop and test the Beanconqueror app, including hardware limitations, platform requirements, and practical development workflows.

## Quick Start Summary

### Technology Stack
- **Framework**: Ionic 8.5.0 + Angular 18.2.7
- **Mobile Platform**: Capacitor 6.1.2
- **Language**: TypeScript 5.4.5
- **Package Manager**: npm

### Prerequisites
- **Node.js**: Version 20.12.2 (see `.nvmrc`)
- **npm**: Compatible version
- **Git**: For version control

### Optional (for mobile testing)
- **Android Studio**: For Android development/testing
- **Xcode**: For iOS development/testing (macOS only)

## Development Workflows

### 1. Browser Development (Recommended Start) 🌐

**Best for**: 80% of development work, fastest iteration

```bash
npm install
npm start
# Opens http://localhost:4200
```

**What Works in Browser:**
✅ All UI components and layouts  
✅ Navigation and routing  
✅ Data entry and storage  
✅ Charts and graphs  
✅ Settings and preferences  
✅ Import/export functionality  
✅ Internationalization  
✅ Business logic testing  

**Browser Development Tips:**
- Use Chrome DevTools (F12)
- Enable device simulation (click mobile icon)
- Select phone preset (iPhone, Pixel, etc.)
- Test responsive layouts

**What Doesn't Work in Browser:**
❌ Bluetooth connectivity (smart scales)  
❌ Camera access  
❌ NFC scanning  
❌ QR code scanning  
❌ Device-specific features (haptics, etc.)  

### 2. Android Development 🤖

#### Android Emulator Testing

**What You Need:**
- Android Studio installed
- Android emulator configured

**Setup:**
```bash
npm run build
CAPACITOR_PLATFORM_OVERRIDE=android npm run cap sync android
npm run cap open android
# Use Android Studio to run on emulator
```

**Emulator Capabilities:**
✅ UI and layout testing  
✅ Touch interactions  
✅ App navigation  
✅ Performance testing  
⚠️ Camera (limited, uses webcam)  
❌ Bluetooth connectivity  
❌ Real hardware features  

#### Android Physical Device Testing

**What You Need:**
- Android device with Developer Options enabled
- USB debugging enabled
- USB cable

**Setup:**
```bash
# Enable Developer Options on your Android device:
# Settings > About Phone > Tap "Build Number" 7 times
# Settings > Developer Options > Enable "USB Debugging"

npm run build
CAPACITOR_PLATFORM_OVERRIDE=android npm run cap run android
```

**Physical Device Capabilities:**
✅ All app functionality  
✅ Real Bluetooth connectivity  
✅ Camera and photo features  
✅ All hardware features  

### 3. iOS Development 🍎

#### iOS Simulator Testing (macOS only)

**What You Need:**
- macOS with Xcode installed
- iOS Simulator (comes with Xcode)

**Setup:**
```bash
npm run build
CAPACITOR_PLATFORM_OVERRIDE=ios npm run cap sync ios
npm run cap open ios
# Use Xcode to run on iOS Simulator
```

**Simulator Capabilities:**
✅ UI and layout testing  
✅ Touch interactions  
✅ App navigation  
✅ Performance testing  
❌ Camera functionality  
❌ Bluetooth connectivity  
❌ Real hardware features  

#### iOS Physical Device Testing

**Apple Developer Account Requirements:**

**Option 1: Free Apple Developer Account**
- ✅ Test on your own device only
- ⚠️ Apps expire after 7 days (need to rebuild)
- ⚠️ Limited to 3 apps at a time
- ✅ Perfect for development and testing

**Option 2: Paid Apple Developer Program ($99/year)**
- ✅ Test on unlimited devices
- ✅ Apps don't expire
- ✅ TestFlight distribution
- ✅ App Store submission

**Setup for Physical Device:**
```bash
# 1. Create Apple Developer Account (free or paid)
# 2. Add Apple ID to Xcode (Preferences > Accounts)
# 3. Connect iPhone/iPad via USB
# 4. Enable Developer Mode on device
# 5. Trust developer certificate on device

npm run build
CAPACITOR_PLATFORM_OVERRIDE=ios npm run cap run ios
```

## Recommended Development Phases

### Phase 1: Core Development (Browser Only)
**Time**: 80% of development work  
**Focus**: UI, business logic, data flow  
**Tools**: Browser + DevTools  

```bash
npm start
# Develop core features in browser
```

### Phase 2: Mobile UI Testing (Emulator/Simulator)
**Time**: 15% of development work  
**Focus**: Mobile-specific UI, performance  
**Tools**: Android Emulator or iOS Simulator  

### Phase 3: Hardware Feature Testing (Physical Devices)
**Time**: 5% of development work  
**Focus**: Bluetooth, camera, final UX  
**Tools**: Real Android/iOS devices  

**Required for Testing:**
- Bluetooth coffee scales (Acaia, Decent Scale, etc.)
- Camera functionality
- Final user experience validation

## Live Reload Development

### Browser Live Reload
```bash
npm start
# Automatically reloads on file changes
```

### Mobile Live Reload
⚠️ **Warning**: Opens development server on external network interface

```bash
# Android
CAPACITOR_PLATFORM_OVERRIDE=android npm run ionic capacitor run android --livereload --external

# iOS  
CAPACITOR_PLATFORM_OVERRIDE=ios npm run ionic capacitor run ios --livereload --external
```

## Platform-Specific Requirements

### Android Requirements
- **Min SDK**: 26 (Android 8.0)
- **Target SDK**: 34 (Android 14)
- **Compile SDK**: 35
- **Gradle**: 8.4.0

### iOS Requirements
- **Min iOS**: 13.0
- **CocoaPods**: For dependency management
- **macOS**: Required for iOS development

## Hardware Feature Testing Matrix

| Feature | Browser | Android Emulator | iOS Simulator | Physical Device |
|---------|---------|------------------|---------------|-----------------|
| UI/Layout | ✅ | ✅ | ✅ | ✅ |
| Navigation | ✅ | ✅ | ✅ | ✅ |
| Data Storage | ✅ | ✅ | ✅ | ✅ |
| Charts/Graphs | ✅ | ✅ | ✅ | ✅ |
| Bluetooth Scales | ❌ | ❌ | ❌ | ✅ |
| Camera | ❌ | ⚠️ | ❌ | ✅ |
| QR/NFC Scanning | ❌ | ❌ | ❌ | ✅ |
| File System | ⚠️ | ✅ | ✅ | ✅ |
| Performance | ⚠️ | ✅ | ✅ | ✅ |

## Capacitor Platform Override

**Important**: Due to legacy compatibility, you must set the platform environment variable:

```bash
# Set this environment variable for all cap commands
export CAPACITOR_PLATFORM_OVERRIDE=android  # or ios

# Or prefix each command:
CAPACITOR_PLATFORM_OVERRIDE=android npm run cap sync android
```

## Production Builds

```bash
# Create optimized production build
npm run build --configuration production

# Sync to both platforms
npm run capsync

# Or sync individually
CAPACITOR_PLATFORM_OVERRIDE=android npm run cap sync android
CAPACITOR_PLATFORM_OVERRIDE=ios npm run cap sync ios
```

## Code Quality Tools

The project includes automated code quality tools:

```bash
# Linting
npm run lint

# Testing
npm test

# Code formatting (automatic via git hooks)
# Uses Prettier + ESLint + Husky
```

## Troubleshooting

### Common Issues

**Capacitor commands fail:**
- Ensure `CAPACITOR_PLATFORM_OVERRIDE` is set
- Check that you're using the correct platform (android/ios)

**Build fails:**
- Run `npm install` to ensure dependencies are up to date
- Clear node_modules and reinstall if needed

**Camera doesn't work in emulator:**
- Expected behavior - use physical device for camera testing

**Bluetooth doesn't connect:**
- Emulators cannot connect to real Bluetooth devices
- Use physical device with actual coffee scales

## Getting Help

- **Documentation**: Check existing issues and discussions
- **Code Quality**: SonarCloud dashboard available
- **Community**: See README.md for community links

## Summary for New Developers

1. **Start with browser development** - fastest and covers most functionality
2. **Use emulators/simulators** for mobile UI testing when needed  
3. **Use physical devices** only for hardware features (Bluetooth, camera)
4. **Free Apple Developer Account** is sufficient for iOS testing
5. **Focus on core features first**, hardware features later

This approach allows you to be productive immediately without needing expensive hardware or complex mobile development setup!
