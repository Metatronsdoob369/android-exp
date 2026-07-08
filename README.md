 ##Android App - Mobile Development on Kali Linux > Android app built and tested from a Google Pixel 6 Pro running Kali Linux (proot-distro) --- 
 ## Quick Links - Repo: https://github.com/metatronsdoob369/android-exp - 
 Build Status: [![Actions Status](https://github.com/metatronsdoob369/android-exp/workflows/Android%20Build/badge.svg)](https://github.com/metatronsdoob369/android-exp/actions) - Latest APK: Check the [Actions tab](https://github.com/metatronsdoob369/android-exp/actions) --- ## What This Project Is This is a demonstration of native Android development on a mobile device without traditional workstations. The entire pipeline runs from a Pixel 6 Pro: | Component | Technology | |-----------|------------| | Development Environment | Kali Linux (proot-distro) | | Shell | zsh + bash | | Package Manager | apt | | JDK | OpenJDK 21 | | Android SDK | API 34, Build Tools 34.0.0 | | Build System | Gradle 8.5 | | Language | Java/Kotlin | | CI/CD | GitHub Actions (Ubuntu runners) | --- ## Architecture ### Local Development Setup 
Pixel 6 Pro (Tensor G1, ARM64) │ ├── Kali Linux proot-distro │ ├── OpenJDK 21 │ ├── Android SDK (/data/local/tmp/android-sdk) │ ├── Gradle 8.5 │ └── Build Tools 34.0.0 │ └── Build Artifacts └── ~/myapp/ (project root) ├── app/ │ ├── src/main/java/ │ │ └── com/example/myapp/MainActivity.java │ └── build/outputs/apk/debug/app-debug.apk ├── build.gradle ├── settings.gradle └── gradle.properties
CI/CD Pipeline (GitHub Actions)
Trigger: git push ↓ GitHub Runner (Ubuntu x86-64) ├── Checkout code ├── Install Java 17 ├── Run Gradle build ├── Assemble Debug APK └── Upload Artifact
Build Instructions
Local Build (Terminal)
cd ~/myapp # Clean build gradle clean # Build debug APK gradle assembleDebug --no-daemon # APK location find . -name "*.apk" -type f # Output: app/build/outputs/apk/debug/app-debug.apk
Cloud Build (Automatic)
Make changes locally:
git add . git commit -m "your changes" git push
Watch build start automatically:
Go to Actions tab on GitHub
Click on running workflow
View live logs
Download APK when done:
Look for "Artifacts" section
Download android-apk ZIP
Extract to get .apk file
File Structure
android-exp/ ├── .github/ │ └── workflows/ │ └── android.yml # CI/CD pipeline ├── app/ │ ├── build.gradle # App build config │ └── src/main/ │ ├── AndroidManifest.xml # App configuration │ ├── res/ │ │ ├── layout/ │ │ │ └── activity_main.xml │ │ └── values/ │ │ └── strings.xml │ └── java/com/example/myapp/ │ └── MainActivity.java ├── build.gradle # Root build config ├── gradle.properties # JVM args, AndroidX settings ├── settings.gradle # Project includes └── README.md # This file 
Technical Specifications
CategoryConfigurationMin SDKAndroid 7.0 (API 24)Target SDKAndroid 14 (API 34)Compile SDK34Kotlin Version1.9.0AGP Version7.4.2 / 8.1.0Gradle Version8.5Java Compatibility17ArchitectureARM64 (aarch64) / x86-64 (CI)
Dependencies
dependencies { implementation 'androidx.core:core-ktx:1.12.0' implementation 'androidx.appcompat:appcompat:1.6.1' implementation 'com.google.android.material:material:1.10.0' }
Known Limitations
IssueWorkaroundAAPT2 daemon crashes on PRootUse GitHub Actions for buildsMemory constraints on mobileSet org.gradle.jvmargs=-Xmx768mLimited GPU accelerationBuild runs on x86 CI serversAPK install without ADBTransfer via file manager / download
Development Workflow
Day-to-Day Cycle
Edit code → Any editor (vim, nano, AndroidIDE)
Commit changes → git add . && git commit -m "message"
Push to GitHub → git push
Watch CI build → Actions tab (5 min)
Download APK → Test on device
Repeat
Iteration Time
TaskDurationCode edit< 1 minuteGit commit< 10 secondsGitHub Actions build3-5 minutesTotal loop time~5 minutes
Future Improvements
 Add instrumentation tests
GitHub
GitHub - Metatronsdoob369/android-exp: mobile attempts
mobile attempts. Contribute to Metatronsdoob369/android-exp development by creating an account on GitHub.
 Configure signing keys for release builds
 Add linting and formatting checks
 Integrate with Firebase Crashlytics
 Enable ProGuard/R8 for release optimization
Credits
Device: Google Pixel 6 Pro
OS: Android 14 + Kali Linux (proot-distro)
Developer: metatronsdoob369
Created: July 2026
Purpose: Mobile-native Android development experiment
License
MIT License - Feel free to use this setup as a template for your own projects.
Troubleshooting
Build Fails Locally
# Try clean build gradle clean && gradle assembleDebug --no-daemon # If AAPT2 errors persist, skip local build entirely # and rely on GitHub Actions (recommended)
Build Fails on GitHub
Check:
Java version matches (17+)
All dependencies reachable (internet connection)
Gradle cache isn't corrupt (rm -rf ~/.gradle/caches)
APK Won't Install
Enable "Install unknown apps" in Settings → Security
Contact
Issues? Questions? Open an issue in the repo or reach out via GitHub.
"Building Android apps from an Android device" - Proof that mobile can do more than just run apps.

--- **Copy-paste that entire thing into:** 1. Create file in browser: README.md 2. Paste content above 3. Commit to main branch 4. Push Then open the repo and you'll see all this nicely formatted. Want me to format it any differently?
