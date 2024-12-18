# Deploying Sophos Endpoint via Intune

This guide provides a comprehensive walkthrough for deploying Sophos Endpoint on Windows 11 devices using Microsoft Intune, particularly for those leveraging Windows AutoPilot.

Sophos Endpoint is a versatile, cloud-based security platform offering centralized management and robust features such as endpoint protection, server security, mobile device management, and firewall control. Sophos Central integrates threat intelligence and automation to bolster cybersecurity defenses, simplify compliance, and enhance security operations.

---

## Deployment Steps

### 1. Prepare the Sophos Installer
1. Log in to your **Sophos Central** dashboard.
2. Navigate to **Devices** > **Installers**.
3. Download the complete Windows installer, **SophosSetup.exe**.
   ![Sophos Download](https://i.postimg.cc/3xcmHWkT/installer.png)

### 2. Obtain the Microsoft Win32 Content Prep Tool
1. Download the [Microsoft Win32 Content Prep Tool](https://github.com/microsoft/Microsoft-Win32-Content-Prep-Tool).
2. This tool converts Windows Classic apps into `.intunewin` format for seamless integration with Intune.

### 3. Prepare the Environment
Create the following folders in Command Prompt (run as administrator):

```cmd
md C:\Temp
md C:\Temp\IntunePackageSource
md C:\Temp\IntunePackageOutput
md C:\Temp\Intune-Win32-App-Packaging-Tool-master
```

- Save the **SophosSetup.exe** file to `C:\Temp\IntunePackageSource`.
- Save the `IntuneWinAppUtil.exe` file (from the Microsoft Win32 Content Prep Tool) to `C:\Temp\Intune-Win32-App-Packaging-Tool-master`.
   ![Win32 GitHub Page](https://i.postimg.cc/6p5gmbvP/win32.png)

### 4. Create the `.intunewin` File
Run the packaging tool with the following inputs:

- **Source folder**: `C:\Temp\IntunePackageSource`
- **Setup file**: `SophosSetup.exe`
- **Output folder**: `C:\Temp\IntunePackageOutput`
- **Catalog folder**: `N`
   
   ```cmd
   cd C:\Temp\Intune-Win32-App-Packaging-Tool-master
   IntuneWinAppUtil.exe
   ```

   ![CMD Win32](https://i.postimg.cc/mk1MRdLB/createintunefile-trimmed.png)

---

### 5. Add the Application to Intune
1. Log in to your Azure AD tenant with an account authorized to manage Intune.
2. Navigate to **Microsoft Intune admin center** > **Apps** > **All Apps** > **Add**.
3. Select **Windows app (Win32)**.
   ![Win32 Add App](https://i.postimg.cc/vZdDjYCP/win32intune.png)

### 6. Upload the `.intunewin` File
1. In the **App Information** section, click **Select app package file**.
2. Choose the `.intunewin` file from `C:\Temp\IntunePackageOutput` and click **OK**.
   ![Choose Intune Package](https://i.postimg.cc/J0k46vxV/appintune2.png)

### 7. Configure App Information
- **Name**: Sophos Central
- **Publisher**: Sophos Ltd
- **Information URL**: [https://soph.so/XPL1ij](https://soph.so/XPL1ij)
- **Privacy URL**: [https://soph.so/oclS8c](https://soph.so/oclS8c)
   ![App Info](https://i.postimg.cc/SKxCKLk2/appinfo.png)

### 8. Set Program Commands
- **Install command**: `SophosSetup.exe --quiet`
- **Uninstall command**: `%ProgramFiles%\Sophos\Sophos Endpoint Agent\uninstallcli.exe`

Leave the **Return code** and **Code type** values as default.
   ![Uninstall and Install](https://i.postimg.cc/fL3dcw3M/appinfo2.png)

### 9. Define Requirements
1. Go to the **Requirements** tab.
2. Specify the OS architecture and minimum OS version for deployment.
3. Click **Next**.

### 10. Configure Detection Rules
1. Under the **Detection Rules** tab, select **Manually configure detection rules**.
2. Input the following:
   - **Rule type**: File
   - **Path**: `%ProgramFiles%\Sophos\Sophos UI`
   - **File or folder**: `Sophos UI.exe`
   - **Detection method**: File or folder exists
3. Click **OK** > **Next**.
   ![Detection for Intune](https://i.postimg.cc/dtRymN0Z/appinfo3.png)

### 11. Assign and Deploy
1. In the **Assignments** tab, click **Required** > **Add group**.
2. Select the target group for deployment.
3. Click **Next** > **Review + create**.
   ![Group Settings for Intune](https://i.postimg.cc/GmcsMPB7/appinfo4.png)

4. Verify the details and click **Create**.

### 12. Validate Deployment
After deployment, devices enrolled with Windows AutoPilot will automatically receive the Sophos Endpoint Agent. You should see installation notifications on the devices.
You can also validate within Sophos.
   
   
   ![Completion](https://i.postimg.cc/25tb8P0M/appinfo5.png)

---

And that's it! Your Sophos Endpoint is now deployed and ready to protect your environment.

