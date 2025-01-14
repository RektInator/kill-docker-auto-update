# Kill Docker Auto Updates
This repository contains patched binaries that disable the auto-updating process of Docker Desktop. If you rather patch the binaries yourself, the instructions can be found under ``Patching Docker Manually``.

## Patching Docker
Simply navigate to `C:\Program Files\Docker\Docker` and drop the assemblies found in this repository. Use the binaries for the correct version of Docker.

## Patching Docker Manually
Required tool: https://github.com/dnSpy/dnSpy/releases/download/v6.1.8/dnSpy-net-win64.zip

### Version 4.x.x
1. Navigate to `C:\Program Files\Docker\Docker`. In this directory you will find a file called `Docker.Core.dll`.
2. Open the file with dnSpy.
3. On the left, `Docker.Core` will appear. Navigate to `Docker.Core` > `Docker.Core.Dll` > `Docker.Core.UpdateDownloader` > `BuildComparer` > `IsVersionSuperior`. This is the function that checks if another version of Docker Desktop is newer than the currently installed version.
4. Right click on the code that appears on the right and press `Edit Method (C#)`.
5. Remove all the code from the function body and simply add `return false;`.
6. Hit compile and save the module (File -> Save All). Docker Desktop no longer finds new versions automatically.
7. Navigate to `%AppData%\Docker Desktop`. In this directory you will find a file called `versions.json`.
8. Remove the `versions.json` file. This file may contain data about newer versions that have been found already.

:bulb: If you can't write to the Docker directory directly due to permission issues: Save the file somewhere else and manually drag the file into the Docker directory.

### Version 3.x.x
1. Navigate to `C:\Program Files\Docker\Docker`. In this directory you will find a file called `Docker.ApiServices.dll`.
2. Open the file with dnSpy.
3. On the left, `Docker.ApiServices` will appear. Navigate to `Docker.ApiServices` > `Docker.ApiServices.Dll` > `Docker.ApiServices.Update` > `Updater` > `CheckForUpdates`. This is the function that checks for Docker Desktop updates.
4. Right click on the code that appears on the right and press `Edit Method (C#)`.
5. Remove all the code from the function body and simply add `return;`.
6. Hit compile and save the module. Auto-updating is now disabled in Docker Desktop.

:bulb: If you can't write to the Docker directory directly due to permission issues: Save the file somewhere else and manually drag the file into the Docker directory.
