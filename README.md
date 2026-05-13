# 🚀 Flutter Animated Portfolio — IBaD ULLaH

<div align="center">

![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-3.x-0175C2?style=for-the-badge&logo=dart&logoColor=white)
![Provider](https://img.shields.io/badge/Provider-6.1.2-7C3AED?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Android%20%7C%20iOS-lightgrey?style=for-the-badge)

**A LinkedIn-ready animated Flutter portfolio app showcasing glassmorphism UI, custom animations, Provider state management, and multi-page navigation.**

</div>

---

## 📱 Screenshots

> _Run the app and take screenshots to add here_

| Home | Skills | Projects | Contact |
|------|--------|----------|---------|
| Animated name + opacity slider | Skill bars + tech chips | Expandable project cards | Copy-to-clipboard contacts |

---

## ✨ Features

### 🏠 Home Screen
- **Spinning gradient avatar ring** — SweepGradient rotating border with pulse animation
- **Animated ShaderMask name** — LinearGradient shader applied to text with scale + opacity breathing effect using `AnimationController`
- **Custom particle system** — 20 floating particles rendered via `CustomPainter` with random speed, color, and size
- **Animated grid background** — Moving circuit-board grid drawn with `CustomPainter`
- **Live opacity slider** — `Slider` widget connected to `Provider`, instantly updates 3 gradient cards
- **3 animated color cards** — `AnimatedContainer` with gradient + glow box shadow that responds to slider value
- **Bouncing animation demo** — 3 boxes with staggered `AnimationController` bounce using `Transform.translate`
- **Provider live status badge** — Pulsing green dot showing real-time `ChangeNotifier` state

### ⚡ Skills Screen
- **Animated skill progress bars** — `scaleX` grow-in animation using `CurvedAnimation` with `Interval` for staggered delays
- **Stats grid** — 4-cell grid with `ShaderMask` gradient numbers
- **Tech stack chips** — Scrollable `Wrap` of styled technology badges
- **ShaderMask gradient header** — Consistent branding across all screens

### 📂 Projects Screen
- **6 expandable project cards** — Tap to expand/collapse with animated `FadeTransition` + `SlideTransition`
- **Gradient left-accent border** — Each card has a unique color gradient stripe
- **Staggered entry animation** — Cards slide in with index-based delay
- **Action buttons** — "View Code" and "Demo" buttons inside each card
- **Project tags** — Technology chips displayed per project

### 📬 Contact Screen
- **5 contact links** — LinkedIn, GitHub, Email, WhatsApp, Instagram
- **Copy to clipboard** — Tap the copy icon on any contact to copy the value, with a `SnackBar` confirmation
- **Pulsing availability badge** — Animated green glow dot showing open-to-work status
- **Hire Me button** — Gradient CTA button
- **Availability badges** — Mobile Dev, UI/UX, AI Integration tags

### 🧭 Navigation
- **Bottom navigation bar** — Smooth `FadeTransition` + `SlideTransition` between all 4 pages
- **Glassmorphism cards** — Semi-transparent frosted glass containers used throughout
- **Dark gradient background** — Deep purple-to-navy gradient consistent across all screens

---

## 🗂️ Project Structure

```
lib/
├── main.dart                        # App entry point, MultiProvider setup
├── providers/
│   └── color_provider.dart          # ChangeNotifier for opacity slider state
└── screens/
    ├── home_screen.dart             # BottomNavigationBar + page switcher
    ├── color_capacity_screen.dart   # Home page — main animated screen
    ├── skills_screen.dart           # Skills, stats, tech stack
    ├── projects_screen.dart         # Expandable project showcase
    └── contact_screen.dart          # Contact links + availability
```

---

## 🛠️ Tech Stack

| Technology | Purpose |
|-----------|---------|
| **Flutter 3.x** | UI framework |
| **Dart 3.x** | Programming language |
| **Provider 6.1.2** | State management (`ChangeNotifier` pattern) |
| **AnimationController** | Name pulse, bounce, particle, bar animations |
| **CustomPainter** | Particle system, moving grid background |
| **ShaderMask** | Gradient text effect |
| **AnimatedContainer** | Smooth opacity/gradient card transitions |
| **AnimatedSwitcher** | Page transition animation |
| **TickerProviderStateMixin** | Multiple animation controllers per screen |

---

## 🚀 Getting Started

### Prerequisites

Make sure you have Flutter installed and set up:

```bash
flutter --version   # Should be 3.x or higher
dart --version      # Should be 3.x or higher
```

If not installed, follow the official guide: https://docs.flutter.dev/get-started/install

### Installation

**1. Clone or download this repository**

```bash
git clone https://github.com/your-username/flutter-portfolio.git
cd flutter-portfolio
```

Or download the ZIP and extract it.

**2. Install dependencies**

```bash
flutter pub get
```

**3. Run the app**

```bash
# For Android (with emulator or device connected)
flutter run

# For iOS (macOS only)
flutter run -d ios

# For a specific device
flutter devices          # list connected devices
flutter run -d <device-id>
```

**4. Build release APK**

```bash
flutter build apk --release
```

---

## 📦 Dependencies

```yaml
dependencies:
  flutter:
    sdk: flutter
  provider: ^6.1.2        # State management
  cupertino_icons: ^1.0.6 # iOS-style icons
```

Only **one external package** (`provider`) — everything else is pure Flutter.

---

## ⚙️ How It Works

### Provider State Management

`ColorProvider` holds a single `double _value` (0.0 → 1.0). The `Slider` on the home screen calls `provider.setValue()`, which calls `notifyListeners()`. All three gradient cards listen via `context.watch<ColorProvider>()` and rebuild instantly.

```dart
// color_provider.dart
class ColorProvider extends ChangeNotifier {
  double _value = 1.0;
  double get value => _value;

  void setValue(double newValue) {
    _value = newValue;
    notifyListeners();  // triggers rebuild in all listeners
  }
}
```

### Animation Architecture

Each screen uses `TickerProviderStateMixin` to support multiple `AnimationController` instances running simultaneously:

```dart
with TickerProviderStateMixin {
  late AnimationController _nameController;   // breathing name effect
  late AnimationController _pulseController;  // avatar ring + live badge
  late AnimationController _particleController; // particle system
}
```

### CustomPainter Particle System

Particles are pre-generated with random properties and painted each frame:

```dart
class _ParticlePainter extends CustomPainter {
  void paint(Canvas canvas, Size size) {
    for (final p in particles) {
      final t = (progress * p.speed * 10 + p.offset) % 1.0;
      final y = size.height * (1 - t);  // bottom to top
      canvas.drawCircle(Offset(p.x * size.width, y), p.size / 2, paint);
    }
  }
}
```

---

## 🎨 Design System

| Element | Value |
|---------|-------|
| Primary purple | `#7C3AED` |
| Light purple | `#A78BFA` |
| Blue | `#3B82F6` |
| Pink | `#EC4899` |
| Background | `#0A0A1A → #1A0533 → #0D1A3D` |
| Glass card opacity | `7%` white with `24%` white border |
| Border radius (cards) | `24px` |
| Border radius (chips) | `20px` |
| Border radius (buttons) | `14–16px` |

---

## 🔧 Customization

### Change the name and tagline
In `color_capacity_screen.dart`, find and update:


Text('IBaD ULLaH', ...)        // your name
Text('Flutter Developer  ·  UI Designer  ·  AI Enthusiast', ...)  // your tagline


And the avatar initials:
```dart
Text('IU', ...)   // change to your initials
```

### Update contact info
In `contact_screen.dart`, update the `_contacts` list:

```dart
_ContactItem(platform: 'LinkedIn', value: 'your-linkedin-handle', ...),
_ContactItem(platform: 'Email',    value: 'your@email.com', ...),
```

### Add / remove projects
In `projects_screen.dart`, add entries to the `_projects` list:

```dart
_ProjectData(
  title: 'Your App Name',
  subtitle: 'Tech · Stack',
  description: 'What this app does...',
  tags: ['Flutter', 'Firebase'],
  icon: Icons.your_icon,
  gradientColors: [Color(0xFF...), Color(0xFF...)],
),
```

### Change skill bars
In `skills_screen.dart`, update the `_skills` list:

```dart
_SkillData('Your Skill', 0.90, [Color(0xFF...), Color(0xFF...)]),
//                        ^ percentage 0.0 to 1.0
```

---

## 🐛 Troubleshooting

**Error: Could not find package "provider"**
```bash
flutter pub get
```

**Error: Import path not found**

Make sure `pubspec.yaml` has `name: flutter_portfolio` and your imports use relative paths:
```dart
import 'providers/color_provider.dart';
import 'screens/home_screen.dart';
```

**Black screen on startup**
- Check that `main.dart` wraps `MyApp` in `MultiProvider`
- Make sure all screen files exist in the `screens/` folder

**Animations not smooth**
- Run in release mode: `flutter run --release`
- Make sure you're not running on a very old emulator

---

## 📄 License

```
MIT License

Copyright (c) 2025 IBaD ULLaH

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

---

## 🤝 Connect With Me

| Platform | Link |
|----------|------|
| 💼 LinkedIn | [ibad-ullah-dev](https://linkedin.com/in/ibad-ullah-dev) |
| 🐙 GitHub | [github.com/ibadullah](https://github.com/ibadullah) |
| 📧 Email | ibadk304@gmail.com |
| 💬 WhatsApp | +92 300 000 0000 |

---

<div align="center">

**Made with ❤️ and Flutter by IBaD ULLaH**

_If you found this useful, please ⭐ star the repo and share it on LinkedIn!_

`#Flutter` `#Dart` `#MobileUI` `#FlutterDev` `#Provider` `#UIDesign` `#OpenSource`

</div>