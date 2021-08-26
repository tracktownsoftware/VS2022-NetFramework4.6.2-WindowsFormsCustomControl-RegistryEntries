# VS2022-NetFramework4.6.2-WinFormsControl-RegistryEntries
A possible bug in VS2022 is it does not apply the "Toolbox Controls Installer" registry entry to automatically populate the VS2022 toolbox with a .NET Framework 4.6.2 Windows Forms custom control. This works in VS2019 (and VS2017).

Microsoft documentation (see the sections about AssemblyFoldersEx registration):  [The Toolbox Controls Installer](https://www.microsoft.com/en-us/download/details.aspx?id=35536)

In this repo I use the following acronymns:
- DN462 for .Net Framework 4.6.2
- DN35 for .Net Framework 3.5

There are two folders in this repo.
1. NetFramework4.6.2_Example - A .Net Framework 4.6.2 Windows Forms custom control example that shows Microsoft's "Toolbox Controls Installer" registry entry working in VS2019, but not working in VS2022
2. NetFramework3.5_Example - A .Net Framework 3.5 Windows Forms custom control example that shows Microsoft's "Toolbox Controls Installer" registry entry working in **both** VS2019 and VS2022!
  
### Folder NetFramework4.6.2_Example contains a .Net Framework 4.6.2 example of a Windows Forms custom control. Registry entries should populate the VS toolbox (using Visual Toolbox Installer) and inform Visual Studio the location of an external .design.dll file used for designer extensibility.
Follow the steps below to see the NetFramework4.6.2_Example
1. Open the DN462_WinFormsControl.sln in Visual Studio 2019 (you can probably do this in VS2022 preview but I have not tested).
2. Build release configuration
3. From the solution folder run DN462_CopyBinToTempFolder.bat (or copy files by hand) to copy bin output to the paths below:
    - C:\temp\DN462_WinFormsControl\bin\DN462_WinFormsControl.dll
    - C:\temp\DN462_WinFormsControl\bin\design\DN462_WinFormsControl.Design.dll
4. Run DN462_RegistryEntriesForVS2019.reg to add 32-bit **WOW6432Node** registry entries that:
    - Automatically load MyButton control into the VS2019 Toolbox for Windows Forms projects
    - Inform VS2019 that DN462_WinFormsControl.Design.dll is in the Design subfolder (supports designer extensibility)
6. In VS2019 make a new .Net Framework Windows Forms project. 
- 1. Open the Form1 design surface.
- 2. Open the VS2019 Toolbox. Observe that the MyButton control is in the VS toolbox (thanks to the toolbox registry entry in step 4).
- 3. Click MyButton in the toolbox and then click+drag on Form1 design surface to draw MyButton control
- 4. Rt-click MyButton control on Form1 design surface to use functional design-time context menu items (image below)
