---
layout: post
title: Create Nuget package script
---

Use script to pack all packages, and publish them to a local NuGet repository.

When packing using .csproj file all of the information from .nuspec file will be automatically applied, but in addition the version number and all of the packed project references (to .dll compiled from other projects, or to other NuGet packages) will be automatically gathered from project file and included in final package manifest. Also, this will guarantee that package is packed as correct profile (PCL or .NET standard) - the same that is used for development.

