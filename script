### PowerShell Script to Remove Preinstalled Windows 11 Apps with Options ###

# Menu for user to choose options
Write-Output "Select an option:"
Write-Output "1. Remove specific apps"
Write-Output "2. Remove all unwanted preinstalled apps"
Write-Output "3. Disable Telemetry, Tracking & Suggested Content"
Write-Output "4. Disable & Remove Bing Web Search, Cortana, Copilot, Recall Snapshots"
Write-Output "5. Turn off Enhance Pointer Precision (Mouse Acceleration)"
Write-Output "6. Customize Taskbar & Start Menu (Hide Search, Task View, Widgets, Chat, Recommended Section)"
Write-Output "7. Remove all pinned apps from Start Menu"
Write-Output "8. Exit"
$choice = Read-Host "Enter your choice (1/2/3/4/5/6/7/8)"

# List of unwanted preinstalled apps
$UnwantedApps = @(
    "Microsoft.BingNews",
    "Microsoft.GetHelp",
    "Microsoft.Getstarted",
    "Microsoft.Microsoft3DViewer",
    "Microsoft.MicrosoftOfficeHub",
    "Microsoft.MicrosoftSolitaireCollection",
    "Microsoft.MixedReality.Portal",
    "Microsoft.MSPaint",
    "Microsoft.People",
    "Microsoft.SkypeApp",
    "Microsoft.Todos",
    "Microsoft.WindowsAlarms",
    "Microsoft.WindowsCamera",
    "Microsoft.WindowsMaps",
    "Microsoft.Xbox.TCUI",
    "Microsoft.XboxGameOverlay",
    "Microsoft.XboxGamingOverlay",
    "Microsoft.XboxIdentityProvider",
    "Microsoft.XboxSpeechToTextOverlay",
    "Microsoft.YourPhone",
    "Microsoft.ZuneMusic",
    "Microsoft.ZuneVideo"
)

switch ($choice) {
    1 {
        $appName = Read-Host "Enter the exact app name (e.g., Microsoft.MSPaint)"
        $Package = Get-AppxPackage -Name $appName -AllUsers
        if ($Package) {
            Write-Output "Removing $($Package.Name)"
            Remove-AppxPackage -Package $Package.PackageFullName -AllUsers
        } else {
            Write-Output "$appName not found. Skipping."
        }

        $ProvisionedPackage = Get-AppxProvisionedPackage -Online | Where-Object {$_.DisplayName -eq $appName}
        if ($ProvisionedPackage) {
            Write-Output "Removing provisioned package $($ProvisionedPackage.DisplayName)"
            Remove-AppxProvisionedPackage -Online -PackageName $ProvisionedPackage.PackageName
        } else {
            Write-Output "$appName not provisioned. Skipping."
        }
    }
    2 {
        foreach ($App in $UnwantedApps) {
            $Package = Get-AppxPackage -Name $App -AllUsers
            if ($Package) {
                Write-Output "Removing $($Package.Name)"
                Remove-AppxPackage -Package $Package.PackageFullName -AllUsers
            } else {
                Write-Output "$App not found. Skipping."
            }
        }

        foreach ($App in $UnwantedApps) {
            $ProvisionedPackage = Get-AppxProvisionedPackage -Online | Where-Object {$_.DisplayName -eq $App}
            if ($ProvisionedPackage) {
                Write-Output "Removing provisioned package $($ProvisionedPackage.DisplayName)"
                Remove-AppxProvisionedPackage -Online -PackageName $ProvisionedPackage.PackageName
            } else {
                Write-Output "$App not provisioned. Skipping."
            }
        }
    }
    3 {
        Write-Output "Disabling Telemetry, Tracking & Suggested Content..."

        # Disable telemetry
        Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection" -Name "AllowTelemetry" -Type DWord -Value 0

        # Disable advertising ID
        Set-ItemProperty -Path "HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\AdvertisingInfo" -Name "Enabled" -Type DWord -Value 0

        # Disable suggestions in Settings
        Set-ItemProperty -Path "HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\ContentDeliveryManager" -Name "SubscribedContent-338393Enabled" -Type DWord -Value 0

        # Disable tips, tricks, and suggestions
        Set-ItemProperty -Path "HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\ContentDeliveryManager" -Name "SoftLandingEnabled" -Type DWord -Value 0

        # Disable suggested apps in Start Menu
        Set-ItemProperty -Path "HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\ContentDeliveryManager" -Name "SystemPaneSuggestionsEnabled" -Type DWord -Value 0

        Write-Output "Telemetry, tracking, and suggested content disabled."
    }
    4 {
        Write-Output "Disabling & Removing Bing Web Search, Cortana, Copilot, Recall Snapshots..."

        # Disable Bing Web Search
        Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\Windows Search" -Name "DisableWebSearch" -Type DWord -Value 1

        # Disable Cortana
        Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\Windows Search" -Name "AllowCortana" -Type DWord -Value 0
        Get-AppxPackage -Name "Microsoft.549981C3F5F10" -AllUsers | Remove-AppxPackage -AllUsers

        # Disable Windows Copilot
        Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsCopilot" -Name "TurnOffWindowsCopilot" -Type DWord -Value 1

        # Disable Recall Snapshots (if applicable)
        Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\Experience" -Name "DisableSnapshot" -Type DWord -Value 1

        Write-Output "Bing Web Search, Cortana, Copilot, and Recall Snapshots disabled and removed."
    }
    5 {
        Write-Output "Turning off Enhance Pointer Precision (Mouse Acceleration)..."

        # Turn off Enhance Pointer Precision
        Set-ItemProperty -Path "HKCU:\Control Panel\Mouse" -Name "MouseSpeed" -Value 0
        Set-ItemProperty -Path "HKCU:\Control Panel\Mouse" -Name "MouseThreshold1" -Value 0
        Set-ItemProperty -Path "HKCU:\Control Panel\Mouse" -Name "MouseThreshold2" -Value 0

        Write-Output "Enhance Pointer Precision (Mouse Acceleration) turned off."
    }
    6 {
        Write-Output "Customizing Taskbar & Start Menu..."

        # Hide Search icon/box from taskbar
        Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Search" -Name "SearchboxTaskbarMode" -Value 0

        # Hide Task View button
        Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" -Name "ShowTaskViewButton" -Value 0

        # Disable and hide Widgets
        Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" -Name "TaskbarDa" -Value 0

        # Hide Chat (Meet Now) icon
        Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" -Name "TaskbarMn" -Value 0

        # Disable & hide Recommended section in Start Menu
        Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" -Name "Start_ShowRecommendations" -Value 0

        Write-Output "Taskbar & Start Menu customized."
    }
    7 {
        Write-Output "Removing all pinned apps from Start Menu..."
        $startLayoutPath = "$env:APPDATA\Microsoft\Windows\Start Menu\Programs"
        Remove-Item -Path "$startLayoutPath\*" -Force -Recurse -ErrorAction SilentlyContinue
        Write-Output "All pinned apps removed from Start Menu."
    }
    8 {
        Write-Output "Exiting script. No changes made."
    }
}

Write-Output "Finished."
