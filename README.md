# Deploying Sophos Endpoint in Intune 💻

This guide demonstrates how to deploy Sophos Endpoint to a Windows 11 AutoPilot device using Microsoft Intune.

Sophos Endpoint is a robust cloud-based platform designed for centralized security and management across diverse IT environments. It delivers advanced features such as endpoint protection, server security, firewall management, and mobile device management. By integrating threat intelligence and automation, Sophos Central empowers businesses to defend against cyber threats, streamline security operations, and simplify compliance efforts.

## Steps to Deploy Sophos Endpoint to Intune

1. Log in to your Sophos Central dashboard, navigate to the **Devices** section, and select **Installers**.
2. Click Download Complete Windows Installer to download the Endpoint Protection installer. It should download SophosSetup.exe
   ![Sophos Download](https://i.postimg.cc/3xcmHWkT/installer.png)

3. Download the Microsoft [Microsoft Win32 Content Prep Tool](https://github.com/microsoft/Microsoft-Win32-Content-Prep-Tool)
4. You can use the Microsoft Win32 Content Prep Tool to convert Windows Classic apps to the .intunewin format, making them ready for upload and assignment in Intune.

   ![Win32 Github Page](https://i.postimg.cc/6p5gmbvP/win32.png)

