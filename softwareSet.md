#Windows


1. Windows 10 下我一直抱怨它对于内存占用不够积极，原来是 Windows File Cache 默认设定的问题，改为 Level 2 后，File Cache 就积极了很多，
cmd 管理员模式运行

```
fsutil behavior set memoryusage 2

```
