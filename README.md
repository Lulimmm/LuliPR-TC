# LuliPR-TC ACR

PromeRotation Taiwan-client ACR for Reaper (RPR) and Ninja (NIN). The source is synchronized with the national-client 1.4.3 release and built against the Taiwan-client SDK.

## Build

```powershell
dotnet build Luli.csproj --configuration Release
```

The project targets `net9.0-windows` and uses `PromeRotation.SDK.TC` for Dalamud API 13 and PromeRotation references.

## Package

The build output is `bin/Release/LuliReaperPR.dll`. The release workflow packages the DLL, dependency manifest, and opener settings. `repo.json` advertises both RPR and NIN.

The [PromeRotation development reference manual](PromeRotation%20%E5%BC%80%E5%8F%91%E5%8F%82%E8%80%83%E6%89%8B%E5%86%8C.md) was written for the national client/API 15. TC builds use API 13; the SDK package and compile results are authoritative for TC compatibility.

The current rotation version is `1.4.3`. Push a matching version tag or run the `Build and Release` workflow manually to publish.
