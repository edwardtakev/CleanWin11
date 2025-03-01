# Windows 11 Debloat & Customization PowerShell Script

This PowerShell script removes preinstalled Windows 11 apps, disables telemetry, tracking, and unwanted features, and customizes the taskbar and Start Menu.

## Features

- **Remove Preinstalled Apps:** Remove individual or all unwanted preinstalled apps.
- **Disable Telemetry & Tracking:** Turn off data collection, advertising ID, and suggested content.
- **Disable Bing Web Search, Cortana, Copilot, Recall Snapshots:** Remove and disable these features for better privacy.
- **Turn Off Mouse Acceleration:** Disable Enhance Pointer Precision.
- **Customize Taskbar & Start Menu:** Hide search box, Task View, Widgets, Chat icons, and recommended section.
- **Remove Pinned Apps from Start:** Clear all pinned apps from the Start Menu.

## How to Use

1. **Save the Script:**
   Save the PowerShell script as `RemoveWin11Apps.ps1`.

2. **Run PowerShell as Administrator:**
   Right-click Start and select **Windows Terminal (Admin)** or **PowerShell (Admin)**.

3. **Enable Script Execution (if required):**
   ```powershell
   Set-ExecutionPolicy RemoteSigned
   ```

4. **Navigate to Script Directory:**
   ```powershell
   cd C:\Path\To\Script
   ```

5. **Run the Script:**
   ```powershell
   .\RemoveWin11Apps.ps1
   ```

6. **Follow the On-Screen Menu:**
   Select the option for the task you want to perform.

## Options Menu

1. **Remove specific apps**
2. **Remove all unwanted preinstalled apps**
3. **Disable Telemetry, Tracking & Suggested Content**
4. **Disable & Remove Bing Web Search, Cortana, Copilot, Recall Snapshots**
5. **Turn off Enhance Pointer Precision (Mouse Acceleration)**
6. **Customize Taskbar & Start Menu**
7. **Exit**

## Disclaimer

Use this script at your own risk. Be sure to back up important data before making changes to your system.

## License

MIT License

