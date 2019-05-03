# windows tips

<!-- TOC -->

- [windows tips](#windows-tips)
    - [Windows Environments Variables](#windows-environments-variables)
    - [directory](#directory)
    - [system](#system)
    - [task](#task)
    - [file operation](#file-operation)
    - [executable](#executable)
    - [link](#link)
    - [remote desktop](#remote-desktop)
    - [vscode](#vscode)

<!-- /TOC -->

## Windows Environments Variables

环境变量的意义在于可以在cmd中不用输入路径就打开一个外部的exe(比如`firefox`)

## directory


- `mkdir`: make directory
- `rmdir`: rmove directory
- `cd`: change directory
- `dir`: list directory
- `tree`: same as linux `tree`
- `mkline`: create soft or hard link;

## system

- `ver`: windows version, or `winver`
- `systeminfo`: detailed system information
- `help`: show all commands; `help dir`, show command help
- `shutdown`
    - `shutdown -s -t 600`: shutdown in 600s
    - `shutdown -r -t 600`: reboot in 600s
    - `shutdown -a`: abort shutdown
- `set`: Displays, sets, or removes Windows environment variables.
- `cls`: clear screen

## task

- `start`: `start "" "H:\chengCPP"`, `start /min "" notepad.exe`
- `tasklist`: list all tasks
- `taskkill`: kill task; `taskkill /im notepad.exe`
- `cmd`: start a new cmd

## file operation

- `type`: same as linux `cat`
- `rename`: rename a file or files
- `move`: same as linux `mv`
- `copy`: same as linux `cp`
- `del`: same as linux `rm`
- `findstr`: same as linux `grep`, `conda list|findstr numpy`

## executable

- `calc`: calculator
- `write`: ms writer
- `notepad`: notepad
- `mspaint`: window paint
- `charmap`: character map
- `dxdiag`: DirectX info
- `gpedit.msc`: group strategy
- `regedit`: reg edit
- `mstsc`: remote desktop
- `taskmgr`: taskmgr
- `services`: services

## link

将下面内容两个分别`.bat`文件中

```bash
# 移除快捷键小箭头
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Icons" /v 29 /d "%systemroot%\system32\imageres.dll,197" /t reg_sz /f
taskkill /f /im explorer.exe
attrib -s -r -h "%userprofile%\AppData\Local\iconcache.db"
del "%userprofile%\AppData\Local\iconcache.db" /f /q
start explorer
pause
```

```bash
# 找回快捷键小箭头
reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Icons" /v 29 /f
taskkill /f /im explorer.exe
attrib -s -r -h "%userprofile%\AppData\Local\iconcache.db"
del "%userprofile%\AppData\Local\iconcache.db" /f /q
start explorer
pause
```

## remote desktop

出现CredSSP的时候:https://blog.csdn.net/myweaven/article/details/79324668

```bash
# or reg
Windows Registry Editor Version 5.00
 
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\CredSSP\Parameters]
"AllowEncryptionOracle"=dword:00000002
```

## vscode

将portable的vscode添加到window的context menu

```bash
Windows Registry Editor Version 5.00
; Open files
[HKEY_CLASSES_ROOT\*\shell\Open with VS Code]
@="Edit with VS Code"
"Icon"="D:\\ProgrammingTools\\VSCode\\Code.exe,0"
[HKEY_CLASSES_ROOT\*\shell\Open with VS Code\command]
@="\"D:\\ProgrammingTools\\VSCode\\Code.exe\" \"%1\""
; This will make it appear when you right click ON a folder
; The "Icon" line can be removed if you don't want the icon to appear
[HKEY_CLASSES_ROOT\Directory\shell\vscode]
@="Open Folder"
"Icon"="D:\\ProgrammingTools\\VSCode\\Code.exe,0"
[HKEY_CLASSES_ROOT\Directory\shell\vscode\command]
@="\"D:\\ProgrammingTools\\VSCode\\Code.exe\" \"%1\""
; This will make it appear when you right click INSIDE a folder
; The "Icon" line can be removed if you don't want the icon to appear
[HKEY_CLASSES_ROOT\Directory\Background\shell\vscode]
@="Open Folder"
"Icon"="D:\\ProgrammingTools\\VSCode\\Code.exe,0"
[HKEY_CLASSES_ROOT\Directory\Background\shell\vscode\command]
@="\"D:\\ProgrammingTools\\VSCode\\Code.exe\" \"%V\""
```

notepad++ add to context menu

```bash
Windows Registry Editor Version 5.00

; created by Walter Glenn
; for How-To Geek
; article: http://www.howtogeek.com/281490/how-to-add-open-with-notepad-to-the-windows-context-menu-for-all-files/

; add key
[HKEY_CLASSES_ROOT\*\shell\Notepad\Command]
@="D:\\File Tools\\npp\\notepad++.exe %1"

; remove key
;[-HKEY_CLASSES_ROOT\*\shell\Notepad\Command]
```