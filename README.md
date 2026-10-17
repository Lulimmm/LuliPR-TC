# Luli Reaper PR (繁中服)

PromeRotation Reaper ACR, adapted for the Taiwan/Traditional Chinese client using `PromeRotation.SDK.TC`.

## Build

Requires the .NET 9 SDK. Restore and build with:

```powershell
dotnet build Luli.csproj --configuration Release
```

The SDK package supplies compile-time references for Dalamud API 13 and PromeRotation. Runtime dependencies are provided by the installed game/plugin environment.

## ACR package

The build output is `bin/Release/LuliReaperPR.dll`. The release workflow packages it with its dependency manifest and opener configuration for PromeRotation.

## Release

Push a version tag such as `v1.0.10` or run the `Build and Release` workflow manually.
