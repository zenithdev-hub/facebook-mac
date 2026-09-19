# Facebook for macOS (facebook-mac)

A lightweight, high-performance, and privacy-focused native macOS wrapper for Facebook and Facebook Messages, built entirely on top of Apple's modern **WebKit** framework and optimized for **macOS 11.0 (Big Sur) and later**.

Unlike heavy, resource-hogging Electron-based alternatives that bundle an entire Chromium browser instance, **facebook-mac** utilizes the system's native rendering capabilities. This architecture ensures an incredibly small disk footprint, minimal RAM consumption, and exceptional energy efficiency, allowing you to stay connected without draining your MacBook's battery.

---

## 🚀 Key Features

* **Native WebKit Core:** Powered by `WKWebView` (the same engine behind Safari), ensuring blazing-fast page loads, smooth scrolling, and perfect rendering of Facebook’s modern interface.
* **Resource Efficient:** Consumes only a fraction of the RAM and CPU cycles used by standard web browsers or Electron wrappers.
* **Persistent Sessions:** Securely retains cookies, login tokens, and cache within Apple's isolated data stores, so you never have to re-authenticate after closing the app.
* **Optimized Aspect Ratio & UI:** Pre-configured with a cinema-standard 16:9 responsive frame (`1354 × 789` startup size) that blends naturally into the macOS multitasking environment.
* **Privacy & Isolation:** Keeps your social media browsing completely separate from your primary web browser, minimizing cross-site tracking vectors.
* **Modern macOS Architecture:** Written natively using contemporary Apple frameworks, omitting legacy code for maximum forward compatibility.

---

## 💻 System Requirements

* **Operating System:** macOS 11.0 (Big Sur), macOS 12 (Monterey), macOS 13 (Ventura), macOS 14 (Sonoma), or newer.
* **Architecture:** Universal Binary (Native support for both **Apple Silicon M1/M2/M3/M4** chips and Intel Core processors).
* **Development IDE:** Xcode 12.0 or higher (if building from source).

---

## 🛠️ Technical Deep Dive

### Why WebKit over Electron?
Most modern desktop chat applications are built using Electron, which packs a massive Node.js runtime and a Google Chromium browser into every single app. This results in apps that easily take up 500MB+ of disk space and hundreds of megabytes of active RAM. 

`facebook-mac` bypasses this bloat entirely by tapping directly into macOS's native `WebKit` subsystem. By inheriting the system's shared web rendering engine, the executable size remains under a few megabytes, and the application lifecycle management is handled natively by the macOS kernel.

### The Redirect Architecture
Due to recent platform adjustments by Meta, standalone endpoints like `messenger.com` heavily restrict desktop multitasking or forcefully redirect to core infrastructure layouts. This repository bypasses the standard web browser loop by targeting the isolated full-screen communications node at `https://facebook.com`. This guarantees a dedicated, distraction-free environment that functions exclusively as an independent communication tool, shielding you from the primary Facebook News Feed.

---

## 🔨 How to Build from Source

If you want to compile and run this application yourself using Xcode, follow these simple sequential steps:

1. **Clone the Repository:**
   ```bash
   git clone https://github.com
   cd facebook-mac
   ```

2. **Open the Project:**
   Launch Xcode and open the `messenger.xcodeproj` (or your specific project directory file).

3. **Configure Network Capabilities:**
   Because macOS operates on a strict app-sandboxing security model, you must grant the application network access privileges:
   * Select the root project node in the left sidebar.
   * Navigate to the **Signing & Capabilities** tab.
   * Under the **App Sandbox** section, ensure that **Outgoing Connections (Client)** is checked.

4. **Verify Deployment Target:**
   * In the **General** tab, under **Deployment Info**, ensure the macOS target drop-down is set to `11.0` or higher.

5. **Compile and Run:**
   Press `Cmd + R` or click the **Play** button in the upper-left corner of Xcode to compile the native Swift code and boot the wrapper.

---

## 📦 Distribution & Packaging

To compile a production-ready, highly-optimized `.app` bundle for distribution:
1. Set the active scheme destination to **Any Mac** or **My Mac**.
2. Go to the top menu bar and select **Product** -> **Archive**.
3. Once the compilation completes and the Organizer window appears, click **Distribute App**.
4. Choose **Custom** -> **Copy App** to extract a clean, unsigned standalone application bundle directly to your Desktop.

---

## 🔒 Security & Privacy Notice

This application is **100% open-source**. It does not feature any backend servers, analytic collection trackers, middleman injection scripts, or proprietary credential logging utilities. All network traffic, cookie exchanges, and authentication procedures happen directly and securely between your machine's native `WKWebView` instance and the official, encrypted Facebook servers (`*.facebook.com`).

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details. Free to use, modify, and redistribute as you see fit.
