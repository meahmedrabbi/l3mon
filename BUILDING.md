# Building the L3MON APK

This guide explains how to build the L3MON Android client APK file.

## Prerequisites

Before building the APK, ensure you have the following installed:

1. **Java Development Kit (JDK) 11 or higher**
   - **Debian/Ubuntu:**
     ```bash
     sudo apt-get install openjdk-11-jdk
     ```
   - **Fedora/RHEL:**
     ```bash
     sudo yum install java-11-openjdk-devel
     ```
   - **macOS (using Homebrew):**
     ```bash
     brew install openjdk@11
     ```
   - **Windows:** Download from [Adoptium](https://adoptium.net/)

2. **Android SDK** (or Android Studio)
   - Download [Android Studio](https://developer.android.com/studio) which includes the SDK
   - Or install the [Android command-line tools](https://developer.android.com/studio#command-line-tools-only)

3. **Android SDK Platform 34** (Android 14)
   - Via Android Studio SDK Manager, or:
     ```bash
     sdkmanager "platforms;android-34"
     ```

## Building the APK

### Option 1: Using the Built-In APK Builder (Server)

L3MON includes a built-in APK builder accessible from the web dashboard:

1. Start the L3MON server:
   ```bash
   cd server
   npm install
   npm start
   ```

2. Navigate to `http://<SERVER_IP>:22533` in your browser

3. Log in and go to the **APK Builder** page

4. Enter your server's IP address and port (default: `22222`)

5. Click **Build** — the server will:
   - Patch the APK with your server address
   - Compile the APK using apktool
   - Sign the APK automatically

6. Download the built APK from the dashboard

### Option 2: Building from Source with Gradle

1. **Clone the repository:**
   ```bash
   git clone https://github.com/user/l3mon.git
   cd l3mon/client
   ```

2. **Configure the server address:**

   Edit `app/src/main/java/com/etechd/l3mon/IOSocket.java` and update the server URL:
   ```java
   ioSocket = IO.socket("http://YOUR_SERVER_IP:22222?model=...");
   ```
   Replace `YOUR_SERVER_IP` with your actual server IP address.

3. **Set up `local.properties`:**

   Create or update `local.properties` in the `client/` directory:
   ```properties
   sdk.dir=/path/to/your/Android/sdk
   ```

4. **Build the debug APK:**
   ```bash
   chmod +x gradlew
   ./gradlew assembleDebug
   ```
   The APK will be generated at:
   ```
   app/build/outputs/apk/debug/app-debug.apk
   ```

5. **Build the release APK:**
   ```bash
   ./gradlew assembleRelease
   ```
   The unsigned APK will be generated at:
   ```
   app/build/outputs/apk/release/app-release-unsigned.apk
   ```

### Option 3: Building with Android Studio

1. Open Android Studio
2. Select **File > Open** and navigate to the `client/` directory
3. Wait for Gradle sync to complete
4. Edit `IOSocket.java` to set your server IP address
5. Select **Build > Build Bundle(s) / APK(s) > Build APK(s)**
6. The APK will be in `app/build/outputs/apk/`

## Signing the APK

For release builds, you need to sign the APK:

### Generate a Keystore

```bash
keytool -genkey -v -keystore my-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias my-alias
```

### Sign Using apksigner

```bash
apksigner sign --ks my-release-key.jks --out app-release-signed.apk app-release-unsigned.apk
```

### Sign Using jarsigner (Alternative)

```bash
jarsigner -verbose -sigalg SHA256withRSA -digestalg SHA-256 -keystore my-release-key.jks app-release-unsigned.apk my-alias
zipalign -v 4 app-release-unsigned.apk app-release-signed.apk
```

## Installing the APK

1. **Transfer** the APK to the target Android device

2. **Enable** "Install from Unknown Sources" on the device:
   - Go to **Settings > Security** (or **Settings > Apps > Special Access > Install Unknown Apps**)
   - Enable the option for your file manager or browser

3. **Install** the APK by tapping on it

## Troubleshooting

- **Gradle sync fails:** Make sure your `local.properties` points to a valid Android SDK location
- **Build tools not found:** Install the required build tools via SDK Manager:
  ```bash
  sdkmanager "build-tools;34.0.0"
  ```
- **Java version error:** Ensure JDK 11+ is installed and `JAVA_HOME` is set correctly
- **APK not installing:** Ensure "Unknown Sources" is enabled and the device runs Android 5.0 (API 21) or higher
- **Connection issues:** Verify the server IP and port in `IOSocket.java` match your L3MON server configuration

## Minimum Device Requirements

- Android 5.0 (Lollipop, API 21) or higher
- Target: Android 14 (API 34)
- Internet connectivity to communicate with the L3MON server
