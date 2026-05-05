# EarTrumpet via Verk

## Overview

This repository is a customized fork of **[EarTrumpet](https://github.com/File-New-Project/EarTrumpet)**, a native Windows desktop application designed to replace the default volume control mixer. It provides advanced, per-application volume routing and control by interfacing directly with low-level Windows Core Audio APIs.

The "via Verk" distribution introduces specific architectural modifications to the graphical user interface (GUI) and audio routing workflows. The primary objective of these modifications is to optimize the user experience by reducing interaction friction, automating the visibility of active audio endpoints, and consolidating routing controls.

## Modifications & Enhancements

The following structural and behavioral changes distinguish this build from the upstream repository:

*   **Unified Dynamic Device Flyout:** The manual "Expand" functionality for secondary playback devices has been deprecated. The application now employs a unified view where the designated Default Speaker is permanently anchored at the top of the interface. Secondary devices are evaluated dynamically and will only render in the flyout if they are actively hosting non-system application audio. When an application ceases playback, the host device is automatically removed from the active view.
*   **Universal Context Routing:** The application routing workflow has been consolidated into a native context menu. Users may right-click any application item—regardless of its current host device—to instantiate a routing menu. Selecting an alternative playback device from this menu instantly re-routes the application's audio stream and updates the dynamic flyout accordingly.
*   **System Audio Filtering:** The view models have been updated to explicitly filter the default Windows "System Sounds" session. Secondary devices broadcasting exclusively system sounds are classified as inactive and remain hidden from the primary interface, ensuring a streamlined user experience.
*   **Modern Compilation Compliance:** The project configuration files (`.csproj`) have been updated with dynamic path resolution for newer Windows 10 SDKs (e.g., 10.0.19041.0), ensuring immediate compilation compatibility with Visual Studio 2022.
*   **Diagnostic Stability:** Safe-casting and null-conditional operators were introduced into the internal `SnapshotData` diagnostic routines. This prevents recursive `NullReferenceException` faults if the application encounters an error prior to the full initialization of the UI Theme Manager.

## Installation Guide

As a customized fork, this version is not distributed via the Microsoft Store and must be installed manually.

### Option 1: Pre-built Release Deployment
If you currently utilize the official Microsoft Store version of EarTrumpet, it is installed in the restricted `C:\Program Files\WindowsApps` directory and cannot be directly overwritten. You must perform a clean replacement to utilize this fork.

1. **Uninstall Upstream Build:** Open the Windows Start Menu, locate the existing "EarTrumpet" application, right-click, and select **Uninstall**. This step is mandatory to prevent system tray conflicts.
2. **Download Binary:** Navigate to the [Releases](https://github.com/VerkCoding/EarTrumpetViaVerk/releases) tab of this repository and download the latest compiled `EarTrumpet.exe`.
3. **Configure Autostart:** Move the downloaded executable to a permanent directory on your local filesystem. Create a shortcut to the executable and place it within your Windows Startup directory (accessible via `Win + R` -> `shell:startup`). This ensures the application initializes upon system boot.

### Option 2: Source Compilation
For developers wishing to compile the application locally:

1. Clone this repository to your local development environment.
2. Open `EarTrumpet.vs15.sln` using Visual Studio 2022.
3. Configure the build parameters to **Release** and target the **x86** platform.
4. Right-click the **EarTrumpet** project within the Solution Explorer and execute a **Build**.
5. Upon successful compilation, the executable will be generated at `EarTrumpet\Build\Release\EarTrumpet.exe`.

## Upstream Attributions & Licensing

This project acknowledges and preserves the foundational work of the original EarTrumpet development team. The following links provide access to the upstream documentation, policies, and acknowledgments.

*   [Technical Information](./EarTrumpet/README.md)
*   [Upstream Compilation Guide](./COMPILING.md)
*   [Upstream Contribution Guidelines](./CONTRIBUTING.md)
*   [Privacy Policy](./PRIVACY.md)
*   [Project License](./LICENSE)
*   [Change Log](./CHANGELOG.md)

### Supported Operating Systems
* Windows 10 1803 (April 2018 Update) through Windows 10 22H2
* Windows 11

### Credits
* David Golden ([@GoldenTao](https://www.twitter.com/GoldenTao))
* Rafael Rivera ([@WithinRafael](https://www.twitter.com/WithinRafael))
* Dave Amenta ([@davux](https://www.twitter.com/davux))
* [Contributors](https://github.com/File-New-Project/EarTrumpet/graphs/contributors)

*Special thanks to Artjom Korman for the "Horn" icon via the Noun Project.*