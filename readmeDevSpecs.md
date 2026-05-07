# 📦 Developer Handover & Setup Guide

## 1. **Prerequisites**

- **Flutter SDK**: Install the latest stable version from [flutter.dev](https://flutter.dev/docs/get-started/install).
- **Dart SDK**: Comes bundled with Flutter.
- **Android Studio** (or VS Code with Flutter/Dart plugins): For Android development.
- **Xcode** (macOS only): For iOS development.
- **Java JDK 8+**: Required for Android builds.
- **Kotlin**: Comes with Android Studio.
- **Git**: For version control.

---

## 2. **Clone the Repository**

```sh
git clone <REPO_URL>
cd sms-proj
```

---

## 3. **Flutter Dependencies**

Install all Dart/Flutter dependencies:

```sh
flutter pub get
```

---

## 4. **Platform-Specific Setup**

### **Android**

1. **local.properties**  
   - Not checked into version control for security.
   - Create a file at `android/local.properties` with:
     ```
     flutter.sdk=<path-to-your-flutter-sdk>
     ```
     Example:
     ```
     flutter.sdk=C:\\src\\flutter
     ```
   - Optionally, add:
     ```
     flutter.versionCode=1
     flutter.versionName=1.0
     ```

2. **Android SDK**  
   - Open the project in Android Studio.
   - Let it install any missing SDK components.

3. **Build/Run**  
   - Use Android Studio or:
     ```sh
     flutter run
     ```

### **iOS (macOS only)**

1. **CocoaPods**  
   - Install if not present:
     ```sh
     sudo gem install cocoapods
     ```

2. **Install Pods**  
   ```sh
   cd ios
   pod install
   cd ..
   ```

3. **Build/Run**  
   - Use Xcode or:
     ```sh
     flutter run
     ```

---

## 5. **Common Issues & Fixes**

- **GradleException not found**:  
  If you see `unable to resolve class GradleException`, ensure you are using a compatible Gradle version and the Flutter SDK path is correct in `local.properties`.

- **Dependencies not found**:  
  Run `flutter pub get` and ensure you have a stable internet connection.

- **AndroidX issues**:  
  Make sure all plugins and dependencies are up to date.

---

## 6. **Project Structure Overview**

- `lib/` – Main Dart code (UI, logic, models, providers, services, widgets)
- `android/` – Android-specific code and configuration
- `ios/` – iOS-specific code and configuration
- `assets/` – Images, animations, etc.
- `pubspec.yaml` – Flutter dependencies and assets
- `README.md` – Project documentation

---

## 7. **Build & Run**

- **Android**:  
  `flutter run` or use Android Studio.

- **iOS**:  
  `flutter run` or use Xcode (on macOS).

- **Web**:  
  `flutter run -d chrome`

---

## 8. **Code Quality**

- **Linting**:  
  Run `flutter analyze` to check for code issues.

- **Testing**:  
  Run `flutter test` to execute unit/widget tests.

---

## 9. **Environment Variables & Secrets**

- Do **not** commit sensitive data.
- Use `.env` files or platform-specific secure storage for API keys, etc.

---

## 10. **Further Reading**

- [Flutter Documentation](https://flutter.dev/docs)
- [Dart Documentation](https://dart.dev/guides)
- [Android Studio Setup](https://developer.android.com/studio)
- [Xcode Setup](https://developer.apple.com/xcode/)

---

## 11. **Contact**

For any issues, reach out to the previous developer or project maintainer.

---

**This guide should be included in your `README.md` for future reference.** 