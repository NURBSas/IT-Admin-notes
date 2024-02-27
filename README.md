## Trinti Windows 11/10/7 Profilius atsijungiant vartotojui nuo paskyros.

Pasileidžiam - gpedit.msc
Einam keliu: Computer Configuration / Administrative Templates / System / User Profiles /

Susirandam - Delete user profiles older than a specified number of days on system restart

Spaudžiam: Enable - ir nustatom "1" dieną.

Paleidžiam kompiuterį iš naujo

## MS Offiso klaida po Windows 10/11 atnaujinimo "Licenzijos klaida"

Programinis kodas C# kalbai:

using Microsoft.Win32;

### // Pridedame Network Service prie S-1-5-20 registro rakto teisių.
RegistryKey key = Registry.Users.OpenSubKey("S-1-5-20", true);
RegistrySecurity rs = new RegistrySecurity();

### // Sukuriame naują naudotojo teisių įrašą ir pridedame Network Service su visais leidimais
RegistryAccessRule rule = new RegistryAccessRule("Network Service",
    RegistryRights.FullControl,
    InheritanceFlags.ContainerInherit | InheritanceFlags.ObjectInherit,
    PropagationFlags.None,
    AccessControlType.Allow);

rs.AddAccessRule(rule);

### // Atnaujiname rakto teises su naujais leidimais
key.SetAccessControl(rs);

If WScript.Arguments.length = 0 Then
   Set objShell = CreateObject("Shell.Application")
   'Pass a bogus argument, say [ uac]
   objShell.ShellExecute "wscript.exe", Chr(34) & _
      WScript.ScriptFullName & Chr(34) & " uac", "", "runas", 1
Else

## Microsoft Internet Explorerio gražinimas į numatytasias naršykles vietoje Edge

Programinis kodas VBScript:

Dim wshShell
Dim myKey

Set WshShell = CreateObject("WScript.Shell")

myKey = "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Edge\IEToEdge\RedirectionMode"
WshShell.RegWrite myKey,0,"REG_DWORD"

myKey = "HKEY_CURRENT_USER\SOFTWARE\AppDataLow\Software\Microsoft\Edge\IEToEdge\DisableUpsellEdge"
WshShell.RegWrite myKey,1,"REG_DWORD"

myKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Edge\IEToEdge\RedirectionMode"
WshShell.RegWrite myKey,0,"REG_DWORD"

myKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Ext\CLSID\1FD49718-1D00-4B19-AF5F-070AF6D5D54C"
WshShell.RegWrite myKey,0,"REG_DWORD"

myKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects\{1FD49718-1D00-4B19-AF5F-070AF6D5D54C}\NoInternetExplorer"
WshShell.RegWrite myKey,1,"REG_DWORD"

myKey = "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects\{1FD49718-1D00-4B19-AF5F-070AF6D5D54C}\NoInternetExplorer"
WshShell.RegWrite myKey,1,"REG_DWORD"

Set WshShell = Nothing

CreateObject("InternetExplorer.Application").Visible=true

End If

## Microsoft Teams vartotoju atvaizdavimas su klaida // Error

Reikų ištrinti failą settings.json

Failo kelias: _%AppDAta%\Roaming\Microsoft\Teams\settings.json_

## Microsoft OneDrive pridėti pasirinktą aplanką iš bet kurios PC vietos

Naudojam CMD __mklink__ komandą norint susieti pasirinktą aplanką su OneDrive pasiekiamais aplankais. 

mklink /j "C:\Users\ZENKA\OneDrive - ZENKA\DOC_failai" "D:\DOC_failai"

## Microsoft New Teams iconos atvaizdavimas ant Desktop'o

Paleidžiam __RUN__ komanda _Win+R_ ir įvedam komandą __shell:AppsFolder__ atsidariusiame lange ieškome Teams ir surade pertempiam ant darbalaukio.

Galima tai realizuoti PowerShell pagalba:

    Get-AppxPackage MSTeams
    $AppLink = "MSTeams_8wekyb3d8bbwe!MSTeams"
    $ShortuctName = "Teams"
    $WScriptShell = New-Object -ComObject WScript.Shell
    $Shortcut = $WScriptShell.CreateShortcut("$([Environment]::GetFolderPath("Desktop"))\$ShortuctName.lnk")
    $Shortcut.Arguments="shell:AppsFolder\$AppLink"
    $Shortcut.TargetPath = "shell:AppsFolder\$AppLink"
    $Shortcut.Save()



