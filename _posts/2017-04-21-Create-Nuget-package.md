---
layout: post
title: Create Nuget package script
published: true
---

Use script to pack all packages, and publish them to a local NuGet repository.

When packing using .csproj file all of the information from .nuspec file will be automatically applied, but in addition the version number and all of the packed project references (to .dll compiled from other projects, or to other NuGet packages) will be automatically gathered from project file and included in final package manifest. Also, this will guarantee that package is packed as correct profile (PCL or .NET standard) - the same that is used for development.

```
param (
[parameter (mandatory=$true,position=0)]
[string]$projectPath,
[parameter (mandatory=$true,position=1)]
[string]$nuspecPath
)

Push-Location (Split-Path $MyInvocation.MyCommand.Path)

# Configuration
$nugetPath = "nuget" #path to nuget.exe - currently it uses PATH
$localFeedPath = "C:\NuGet.Local\"


# Create local feed directory
if(!(Test-Path $localFeedPath) )
{
    New-Item -ItemType Directory -Force -Path $localFeedPath
}

# Pack project 
cd $projectPath

& $nugetPath pack $nuspecPath -IncludeReferencedProjects -Symbols

# Upload project to local feed
$package = Resolve-Path "*.nupkg" | Where-Object { !( $_ | Select-String "symbols" -quiet) } # select only .nupkg file
$symbols = Resolve-Path "*.nupkg" | Where-Object { ( $_ | Select-String "symbols" -quiet) } # select only symbols.nupkg

if($symbols) {
    $packageToPublish = $symbols
}
else {
    $packageToPublish = $package
}

& $nugetPath add (Resolve-Path $packageToPublish) -source $localFeedPath

Pop-Location
```
