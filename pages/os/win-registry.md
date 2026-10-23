### Prace s registrama

regedit.exe  
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options" /v GlobalFlag /s  

### WER dumpy

[Windows Error Reporing](https://docs.microsoft.com/en-us/windows/desktop/wer/collecting-user-mode-dumps) dump je otisk procesy v okamziku jeho zhrouceni (.NET aplikace)

##### WER - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps

DumpFolder (REG_EXPAND_SZ) = %LOCALAPPDATA%\CrashDumps ... cesta kam se ukladaji WER dumpy  
DumpCount (REG_DWORD) = 10 ... Pocet dumpu ukladanych v adresari  
DumpType (REG_DWORD) = 1 ... typ dumpu = 0 custom, 1 mini, 2 full  
CustomDumpFlags (REG_DWORD) = MiniDumpWithDataSegs | MiniDumpWithUnloadedModules | MiniDumpWithProcessThreadData. ... specificke volby pro dump  

##### IFEO - HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\calc.exe

"Debugger"="vsjitdebugger.exe" ... spusti tento debugger soucasne s programem  
GlobalFlag ... specificke debug parametry k programu
