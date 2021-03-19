# Patching Docker Desktop using these assemblies
Simply navigate to "C:\Program Files\Docker\Docker" and drop the assemblies found in this repository.

# Patching Docker Desktop manually
Required tool: https://github.com/dnSpy/dnSpy/releases/download/v6.1.8/dnSpy-net-win64.zip

Navigate to "C:\Program Files\Docker\Docker". In this directory you will find a file called "Docker.ApiServices.dll". Open the file with dnSpy. On the left, Docker.ApiServices will appear. Navigate to Docker.ApiServices > Docker.ApiServices.Dll > Docker.ApiServices.Update > Updater > CheckForUpdates. This is the function that checks for Docker Desktop updates. Right click on the code that appears on the right and press "Edit Method". Remove all the code from the function and simply add "return;". Hit compile and save the module. Auto-updating is now disabled in Docker Desktop. If you can't write to the Docker directory directly due to permission issues: Save the file somewhere else and manually drag the file into the Docker directory.