---
layout: post
title: Add windows service
---
Add a windows service from windows service executable file.
```
sc create Redis2 binPath= "\"C:\Program Files\Redis2\redis-server.exe\" --service-run \"C:\Program Files\Redis2\redis.windows-service.conf\""
```
