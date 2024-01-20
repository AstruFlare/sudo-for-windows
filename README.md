# Sudo for Windows

This software is licensed under [MIT Lincense](LICENSE).

- **⚠ Warning: This software may have security vulnerabilities and should be used with caution.**

[Latest release](https://github.com/sharedwonder/sudo-for-windows/releases/latest)

- In the future, I will provide a way to install and uninstall automatically.

## 1.Introducing

As we all know, in Linux we can use sudo and su to elevate privileges (get root privileges).

But in Windows, we shuold elevate privileges through UAC (User Account Control). This makes us have to open a new terminal with administrator privileges when we want to run commands as administrator.

So I made this software. It can help us run commands as administrator without having to open a new terminal.

## 2.Install

First, download the compressed package of this software ([download the latest version](https://github.com/sharedwonder/sudo-for-windows/releases/latest)) and extract to a secure directory (***PLEASE SET PERMISSIONS TO PREVENT STANDARD USERS FROM MODIFYING THESE FILES. OTHERWISE, STANDARD USERS WILL BE ABLE TO RUN ELEVATED PROCESSES***).

Use this command to create the service for this software:

```powershell
sc create SudoService type= own start= auto binPath= "<path-service-exe>" DisplayName= "Sudo for Windows Service"
```

- Replace `<path-service-exe>` with the path to "SudoService.exe".

Then, start the service:

```powershell
sc start SudoService
```

- The service will start automatically the next time.

At last, add the directory where the software is stored to the PATH environment variable.

**Now, you can use sudo and su commands in Windows!**

## 3.Uninstall

Use this command to stop the service:

```powershell
sc stop SudoService
```

Then, remove the service:

```powershell
sc delete SudoService
```

At last, remove the directory where the software is stored.

## 4.Build

Required environment:

- [Microsoft Visual Studio 2022](https://aka.ms/vs) or later *with Microsoft Visual C++ Build Tools v143 or later*
- Microsoft Windows SDK 10.0 or later

Commands:

```powershell
git clone https://github.com/sharedwonder/sudo-for-windows.git
cd sudo-for-windows
msbuild "Sudo for Windows.sln" -p:Configuration=Release -p:Platform=<arch>
```

- Replace `<arch>` with the architecture (x64, x86, ARM, ARM64) you want to build.

Then you can see the target files in the directory `release\<arch>`.

There should be the following target files:

- su.exe
- sudo.exe
- SudoConfiguration.dll
- SudoHelper.exe
- SudoRpcClient.dll
- SudoService.exe
