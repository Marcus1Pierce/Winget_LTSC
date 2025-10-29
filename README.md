# Installing and Using WinGet on Windows IoT Enterprise (LTSC)

This guide explains how to install and use **WinGet**, Microsoft's command-line package manager, on **Windows IoT Enterprise LTSC** systems that do not have access to the Microsoft Store.

---

## 1. Requirements
- OS: Windows 10 or Windows 11 IoT Enterprise LTSC  
  (Tested on Windows 10 IoT Enterprise LTSC 2021)  
  See the official documentation:  
  [Install WinGet Client - Windows IoT Enterprise](https://learn.microsoft.com/en-us/windows/iot/iot-enterprise/deployment/install-winget-windows-iot)

---

## 2. Download the Required Files

All required files are available from the [WinGet CLI GitHub releases page](https://github.com/microsoft/winget-cli/releases/latest) (download the **latest stable version**, not a pre-release).

You must download:
- The `.msixbundle` file  
- `License1.xml`  
- `DesktopAppInstaller_Dependencies.zip`  

---

## 3. Extract Dependencies

1. Open `DesktopAppInstaller_Dependencies.zip`.  
2. Navigate to the folder matching your device architecture (`x64`, `arm64`, etc.).  
3. You should see files similar to the following:
   - `Microsoft.VCLibs.**.appx`  
   - `Microsoft.WindowsAppRuntime.**.appx`  

These must be installed before WinGet itself.

---

## 4. Install the Packages

**Run the commands below in an elevated PowerShell window.**  
Important: before running any command, make sure PowerShell’s current directory is the folder where you extracted the files (use `cd "C:\path\to\folder"` or `Set-Location`). Verify with `pwd`. Adjust file names and paths in the commands as needed.

```powershell
Add-AppxPackage -Path .\Microsoft.VCLibs.140.00.UWPDesktop_14.0.33728.0_x64.appx
```
```powershell
Add-AppxPackage -Path .\Microsoft.VCLibs.140.00_14.0.33519.0_x64.appx
```
```powershell
Add-AppxPackage -Path .\Microsoft.WindowsAppRuntime.1.8_8000.616.304.0_x64.appx
```
If you want to install for current users on the system, use this command:
```powershell
Add-AppxPackage -Path .\Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle -LicensePath .\e53e159d00e04f729cc2180cffd1c02e_License1.xml
```
If you want to install for all users on the system, use this command instead for the last step:
```powershell
Add-AppxProvisionedPackage -Online -PackagePath .\Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle -LicensePath .\e53e159d00e04f729cc2180cffd1c02e_License1.xml
```

## 5. Verify the Installation
To confirm that WinGet is installed, run to check version installed:
```powershell
winget --version
```

## 6. Additional Notes & Tips
This method is for systems without Microsoft Store access (e.g., IoT Enterprise LTSC).

The file versions shown above are examples only — always use the versions from the latest release on GitHub.

For usage examples and more commands, check the official WinGet documentation.

### Usage Examples
```powershell
# Search for a package
winget search brave
```

```powershell
# Install a package
winget install Brave.Brave
```

### My Apps
```powershell
winget install Google.Chrome.EXE RARLab.WinRAR Adobe.Acrobat.Reader.64-bit RustDesk.RustDesk DucFabulous.UltraViewer
```
### Additional
```powershell
winget install joncampbell123.DOSBox-X
```