# LuliPR-TC ACR

PromeRotation Taiwan-client ACR for Reaper (RPR) and Ninja (NIN). The source is synchronized with the national-client 1.5.7 release and built against the Taiwan-client SDK.

## Build

```powershell
dotnet build Luli.csproj --configuration Release
```

The project targets `net9.0-windows` and uses `PromeRotation.SDK.TC` for Dalamud API 13 and PromeRotation references.

UI images stay embedded in the DLL: transparent pet/loader frames use PNG, and opaque backgrounds use high-quality JPEG at their original resolution. Both use built-in Windows WIC codecs without a WebP extension. Verify the actual DLL's image names and decoding after changing assets:

```powershell
./tools/verify-ui-textures.ps1 -AssemblyPath bin/Release/LuliReaperPR.dll
```

## Ninja manual Suiton

The hotkey panel's `预备水遁` queues one Ten → Chi → Jin → Suiton group per click,
using the same priority, verification and five-second request debounce as manual
Raiton. It does not enable an automatic preparation toggle. It waits for a legal
GCD submission window and rejects requests during countdowns, fixed openers,
another mudra sequence, Kassatsu, an existing Suiton buff, or insufficient mudra
charges. Opener countdown actions remain independent.

```powershell
./tools/verify-ninja-suiton-hotkey.ps1
./tools/verify-ninja-debug.ps1
```

## Ninja delay burst

The `延后爆发` QT defaults to off and affects normal rotation decisions.
When enabled, it holds Suiton, Dokumori, Kunai's Bane,
Ten Chi Jin, Dream Within a Dream, Bunshin and Kassatsu. Raiton spends mudra only
at 1.8 charges or more, and its Fleeting Raiju proc remains usable without waiting
for a burst window. This mode enables those overflow Raiton/Raiju decisions even
if their individual QTs are off. Fixed opener/countdown sequences and manual
hotkeys keep their own behavior.

```powershell
./tools/verify-ninja-delay-burst.ps1
```

## Ninja post-ninjutsu weaving

Normal rotation decisions allow one ability after Suiton, Hyosho Ranryu or
Raiton, then wait for the next GCD. The shared confirmation deduplication stays
in place; Suiton and Hyosho no longer have a separate 2.5-second deduplication
window. The single-weave counter advances on confirmed action effects.

## Ninja automatic potion

The `爆发药` QT defaults to off. Normal oGCD decisions use Reaper's ordinary
`0612` rule with Kunai's Bane (`36958`, `介毒之术`) replacing Arcane Circle:
use a potion when its cooldown is strictly between 2.5 and 5 seconds, an item
is available and off cooldown, and at least 0.6 seconds remain on the GCD.
Automatic potions wait during mudra, Ten Chi Jin and `延后爆发`.
The rule follows the live skill/item cooldowns rather than fixed timestamps.
Fixed opener potions continue to use the separate `起手使用爆发药` setting.

```powershell
./tools/verify-ninja-delay-burst.ps1
```

## Package

The build output is `bin/Release/LuliReaperPR.dll`. The release workflow packages the DLL, dependency manifest, and opener settings. `repo.json` advertises both RPR and NIN.

The [PromeRotation development reference manual](PromeRotation%20%E5%BC%80%E5%8F%91%E5%8F%82%E8%80%83%E6%89%8B%E5%86%8C.md) was written for the national client/API 15. TC builds use API 13; the SDK package and compile results are authoritative for TC compatibility.

The current rotation version is `1.5.7`. Push a matching version tag or run the `Build and Release` workflow manually to publish.
