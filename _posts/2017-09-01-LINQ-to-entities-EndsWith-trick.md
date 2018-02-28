---
layout: post
title: LINQ to entities string filtering trick
published: true
---
Optimize query that uses string filtering.

To speed up a query that uses 
```
.Where(p => p.Name.EndsWith("Smith")
```
add additional field to database that has reversed value from the Name field and create an index on it. 
Then use it like so:
```
.Where(p => p.Name.StartsWith("htimS").
```
