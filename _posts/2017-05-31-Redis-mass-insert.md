---
layout: post
title: Redis mass insert
---
Add multiple entries to Redis DB from a file using redis-cli from powershell.

```
 Get-Content D:\redis-mass.txt | .\redis-cli.exe -h 172.18.178.86 --pipe
 ```
