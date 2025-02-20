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

## Microsoft Outlook 2013-16 klaida 'Cannot start Microsoft Outlook. Cannot open the Outlook window. Invalid XML, the view cannot be loaded.'

Paleidžiam __RUN__ komanda: _outlook.exe /resetnavpane_

## MS Windows 11 instaliacijos pradžia be interneto (localiam vartotojui sukurti)

Pasiekus regiono pasirinkimą spaudžiam __Shift + F10__

Atsidarius _CMD_ įvedam: __OOBE\BYPASSNRO__ ir paleižiam kompiuterį iš naujo.

Vėl pasileidus instaliacijai spaudžiam __Shift + F10__

Atsidarius _CMD_ įvedam: __ipconfig /release__ spaudžiam _Enter_ ir uždarom _CMD_ langą.

Pasirenkam instaliaciją be interneto.

## MS Windows 10/11 Nuotolinės pagalbos užtemimo išjungimas (arba įjungimas)

secpol.msc -> Local Policies -> Security Options -> User Account Control: Switch to the secure desktop with promting for elevation (Disable)

     HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System

     PromptOnSecureDesktop DWORD

     0 = Disable
     1 = Enable

## MS PowerShell politikos keitimas arba anuliavimas konkrečiai situacijai

Patikrinti kokios bendrai yra politikos:

     Set-ExecutionPolicy -List

Pakeisti konkrečiam skriptui:

     Start-Process powershell -ArgumentList "-ExecutionPolicy Bypass -File 'C:\path\to\your\script.ps1'" -NoNewWindow

Pakeisti konkrečiai sesijai:

     Set-ExecutionPolicy Bypass -Scope Process

## MS Windows profilių migravimas iš vieno PC į kitą PC naudojant USMT servisą

Instaliuojam: adksetup.exe (servisą Windows 10/11)

Tada pasileidžiam CMD administratoriaus teisėm ir nurodom kelią iki serviso.

CMD komanda keliui iki serviso:

     cd /d C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\User State Migration Tool\amd64

CMD komanda sukurti profilio atvaizdui (kelias į C:\tmp\ kur bus suformuotas atvaizdas):

     scanstate c:\tmp\ /o /c /i:miguser.xml /localonly /uel:180 /ue:%computername%\*

CMD komanda atstatanti profilio atvaizdą kitam kompiuteryje:

     loadstate c:\tmp /all /i:miguser.xml /c

## Clonezilla atvaizdų iš USB automatizavimo algoritmas

a) USB pirštelio gaminimo procesas su "RUFUS".
b) DISK GENIUS padarome dvi particijas (Clonezilla ir Images).
c) Kuriame Clonezillos paleidimo mechanizmą.

__Meniu kodas:__ /boot/grub/grub.cfg

     menuentry "Automatinis HP 645 atvaizdo atkūrimas"{
       set root=(hd0,msdos1)
       linux /live/vmlinuz boot=live live-config noswap nolocales ocs_prerun="mount /dev/sda2 /home/partimag/" ocs_live_run="ocs-sr -q -c -j2 -k0 -scr -p reboot restoredisk 2024-10-09-11-img-HP-Elitebook nvme0n1" ocs_live_batch="yes" keyboard-layouts="us" vga=791
       initrd /live/initrd.img
     }

__Reikšmės ir rekomendacijos:__

Šaltinio particija (__sda2__):

Jei USB rakto antroji particija sistemoje matoma kaip __sdb2__ (o ne __sda2__), pakeisk ocs_prerun į: __text__

ocs_prerun="__mount /dev/sdb2 /home/partimag/__"
    
Patikrink tai paleidęs „__Clonezilla__“ ir naudodamas __lsblk__.

Tikslinis diskas (__nvme0n1__):

Jei HDD yra __sda__, o ne __nvme0n1__, pakeisk __nvme0n1__ į __sda__ komandoje __ocs_live_run__.

Atvaizdo pavadinimas:

Pakeisk __2024-10-09-11-img-HP-Elitebook__ į tikrąjį atvaizdo aplanko pavadinimą, esantį antrojoje particijoje.
