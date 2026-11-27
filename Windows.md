
```shell
  powercfg -a
 powercfg /hibernate on
```

```shell
$env:JAVA_HOME = "C:\Users\QuChunhe\.jdks\corretto-1.8.0_504"
$env:PATH = "$env:JAVA_HOME\bin;$env:PATH"
mvn clean package '-Dfile.encoding=UTF-8'

wsl --install -d Ubuntu-24.04
wsl.exe -d Ubuntu-24.04

wsl -l -v
wsl --manage Ubuntu-24.04 --move "D:\Program Files\WSL\Ubuntu-24.04"


Start-Process powershell -Verb RunAs -ArgumentList "-Command", "icacls 'D:\Program Files\WSL\Ubuntu-24.04\ext4.vhdx' /grant 'QuChunhe:(F)'; icacls 'D:\Program Files\WSL\Ubuntu-24.04' /grant 'QuChunhe:(OI)(CI)(F)'; pause"

```