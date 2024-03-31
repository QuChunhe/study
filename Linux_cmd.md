要查看Linux系统的磁盘空间

df：disk free
* -h : --human-readable
* -l : --local 限制列出的文件结构

du: Summarize disk usage of the set of FILEs
* -h或--human-readable 以K，M，G为单位，提高信息的可读性。
* -H或--si 与-h参数相同，但是K，M，G是以1000为换算单位。
* -s或--summarize 仅显示指定目录或文件的总大小，而不显示其子目录的大小。
* -S或--separate-dirs 显示个别目录的大小时，并不含其子目录的大小。
* --max-depth=<目录层数> 超过指定层数的目录后，予以忽略。


```shell
killall snap-store
sudo snap refresh snap-store
```