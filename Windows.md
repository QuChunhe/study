
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
```