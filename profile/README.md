# WinCore 11

[![Version 1 Release (Latest)](https://img.shields.io/badge/Version-1.0.0%20Latest-0078D4?style=for-the-badge&logo=github&logoColor=white)](https://github.com/WinCore11)
[![Download autounattend.xml](https://img.shields.io/badge/⬇%20Download-autounattend.xml-107C10?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/WinCore11/.github/raw/main/profile/autounattend.xml)

## Introduction

Welcome to **WinCore 11**. This repository provides a highly optimized unattended Windows installation file (`autounattend.xml`) designed to automate setup, remove unnecessary bloatware, and apply advanced system and network tweaks for maximum performance.

</br>

> [!NOTE]
> This specific optimizer has been heavily engineered exclusively for the **WinCore 11** experience. We focused intensely on preserving essential daily functionalities (like touchscreens, Microsoft Store, and Xbox/Minecraft compatibility) while maximizing raw system responsiveness and gaming performance.

## Acknowledgements

The foundation of this project comes from the excellent work done by **[memstechtips](https://github.com/memstechtips)** in their **UnattendedWinstall** project. We have built upon their solid base file to provide additional bug fixes, network optimizations, and compatibility adjustments exclusively tailored for the **WinCore 11** brand.

## Key Changes & Fixes

While the core functionality inherits from `memstechtips`, we found and resolved several issues to ensure broader compatibility (e.g., keeping Minecraft and Xbox related apps functional) and better network/system performance.

Here is the comprehensive list of the 21 major improvements and changes made in this optimized version:

1. **Microsoft Edge is Retained**
   - Removed the `EdgeRemoval.ps1` script creation block (~570 lines) and its execution call. Edge is no longer removed.
2. **Xbox Packages Kept (Minecraft Compatibility)**
   - Removed `GamingApp`, `XboxApp`, `XboxIdentityProvider`, `XboxGameOverlay`, `Xbox.TCUI`, and `XboxGamingOverlay` from the bloatware package removal list. This ensures Minecraft and core Xbox gaming services function correctly right out of the box.
3. **SystemResponsiveness Bug Fix**
   - Corrected value from `10` -> `4294967295` (restoring the default Windows value which resolves the responsiveness bug).
4. **NetworkThrottlingIndex Disabled**
   - Changed from `10` -> `4294967295` to completely disable network throttling for unrestricted network throughput.
5. **Smart PowerThrottlingOff (Device Dependent)**
   - Now utilizes a `Win32_Battery` WMI query. `PowerThrottlingOff` is gracefully skipped on laptops to preserve battery life but explicitly applied on desktops and batteryless devices for maximum performance.
6. **Faster Shutdown Speeds**
   - Set `ClearPageFileAtShutdown = 0`. The page file is no longer deleted upon shutting down, leading to significantly faster shutdown times.
7. **Proper LUA (UAC) Sequencing**
   - Set `EnableLUA = 1`. This value is now correctly applied at the very end of the installation process, ensuring all other system configuration scripts complete successfully without User Account Control (UAC) interference. Re-enabling UAC (`1`) at the end specifically fixes a known bug where drag-and-drop functionality between applications breaks when LUA is left entirely disabled (`0`).
8. **TcpAckFrequency Optimization**
   - Changed from `2` -> `1`. An advanced network optimization that disables Nagle's algorithm for lower latency.
9. **TCPNoDelay Enabled**
   - Changed from `0` -> `1` to eliminate delay in TCP communication.
10. **TcpDelAckTicks Disabled**
    - Newly added setting configuring `TcpDelAckTicks = 0`, which turns off the delayed ACK timer for faster packet acknowledgment.
11. **File Explorer "This PC" Default for All Users**
    - Injected `LaunchTo = 1` into the `DefaultUser` registry hive block. This ensures that File Explorer opens to "This PC" instead of "Home" or "Quick Access" for all newly created users on the system.
12. **Start Menu Centered (Windows 11 Default)**
    - Changed `TaskbarAl = 0` (left-aligned) -> `1` (Windows 11 default, center alignment).
13. **Microsoft Store is Retained**
    - The Microsoft Store is explicitly kept during the optimized setup, ensuring full access to Store apps and updates without manual reinstallation.
14. **Windows Photos App is Retained**
    - The default modern Windows Photos app is no longer removed and the legacy Windows Photo Viewer registry hacks have been omitted, keeping the native experience intact.
15. **User Convenience Features Kept Active**
    - Options to "Sleep" and "Lock" the computer from the Start Menu are retained, and the `Win+L` locking shortcut remains enabled for daily user convenience.
16. **Background Apps Kept Active**
    - The `LetAppsRunInBackground` registry tweak was removed to ensure modern (UWP) apps like WhatsApp, Mail, and Spotify continue to act normally and receive notifications while minimized.
17. **Taskbar System Tray Overflow Kept Active**
    - The `EnableAutoTray` tweak was removed to prevent the taskbar from becoming cluttered. All background app icons (like Steam, Spotify, etc.) are properly neatly hidden inside the system tray overflow menu (up arrow).
18. **Taskbar Icons Kept Default Size**
    - Removed the `TaskbarSmallIcons` registry tweak. This setting is completely unsupported in Windows 11 and causes graphical corruption/overlapping issues on the taskbar if applied.
19. **Touch, Biometrics & Sensors Kept Active**
    - Removed `WbioSrvc` (Windows Hello / Fingerprint), `TabletInputService` (Touchscreen / Pen), and Sensor service disablers entirely from the script. This ensures touch monitors, drawing tablets, and biometric peripherals work seamlessly out of the box on all systems, without relying on flawed driver or battery checks.
20. **Restored Premium UI Animations**
    - Replaced the overly aggressive `UserPreferencesMask` visual effects tweaks with a balanced user-provided configuration. Menus, taskbar interactions, and window minimizing/maximizing transitions are kept smooth instead of feeling instantly teleported/broken, maintaining a premium fast experience.
21. **Essential First-Party Apps Retained**
    - `Mail and Calendar`, `Windows Alarms & Clock`, and `Windows Camera` were removed from the BloatRemoval script list. This ensures normal daily PC functionality remains available right out of the box without forcing the user to re-download basic tools (e.g. for testing their laptop camera).

## Core Features (Inherited from Original)

In addition to the WinCore 11 optimizations above, this configuration still provides the foundational benefits of a fully debloated Windows installation layout:

- **Bypasses Windows 11 system requirements** (TPM, Secure Boot, CPU, RAM).
- **Skips forced Microsoft account creation** during Windows setup.
- **Privacy & Security**: Disables all telemetry, tracking, and advertising.
- **Power Settings**: Injects the Winhance Power Plan for optimal performance.
- **Bloatware Removal**: Strips out Copilot, OneDrive, pre-installed sponsor apps, and unnecessary default services.
- **Windows Updates**: Disables forced auto-updates and configures Windows Update to only notify.
- **Customization & Dark Theme**: Enables Windows Dark Mode instantly on first login, and unpins all unwanted icons from the start menu.
- **Clean Explorer**: Restores the Classic Context Menu (Right Click), shows file extensions by default, and declutters the navigation pane inside File Explorer.

## Usage

> [!IMPORTANT]  
> Ensure the answer file downloaded remains named exactly `autounattend.xml`; otherwise, it won't be recognized by the Windows Installer and the process will not be automated.

1. Download or copy the included `autounattend.xml` file.
2. Place `autounattend.xml` at the root of your bootable Windows 10 or Windows 11 installation USB drive.
3. Boot from the USB and install Windows as usual. The setup will automatically read the file, bypass most of the installation prompts, and apply all WinCore 11 optimizations seamlessly.
