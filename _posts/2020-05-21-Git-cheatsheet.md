---
layout: post
title: Git cheatsheet
---
These are git commands not used everyday but I find them useful very often.

Abort merge (before it's committed)
```
git reset --hard HEAD
```
Get files changed in last commit
```
git diff HEAD~1 --name-only
```
Get branches merged to master
```
git branch --merged master
```
