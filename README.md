
# scoop-anaconda3  🚀🐍

> **Always‑fresh Scoop bucket for the latest Anaconda Distribution**
> Maintained by [@jahanbani](https://github.com/jahanbani) – auto‑updated every six hours by GitHub Actions.Anaconda publishes new Windows installers several times a year, but the manifest in Scoop’s official **Extras** bucket often lags behind.This bucket tracks **every** new build (e.g. `Anaconda3‑2025.06‑1`) within hours, so you can install or upgrade with a single command—even if you also keep Extras for other apps.
---
#
# Quick start — get the newest Anaconda without touching Extras

```
powershell
# 1  Add this bucket (alias = anaconda)scoop bucket add anaconda https://github.com/jahanbani/scoop-anaconda3

# 2  Install or upgrade, explicitly referencing this bucketscoop install anaconda/anaconda3

# first‑time installscoop update  anaconda/anaconda3

# later upgrades

```
#
#
# Why the **`anaconda/`** prefix?Scoop stops searching as soon as it finds a manifest called `anaconda3.json`.If you added the Extras bucket first, its older manifest “wins” unless you either* use the bucket‑qualified name (`anaconda/anaconda3`), **or*** move this bucket higher in your bucket list (next section).

---
#
# (Optional) Make this bucket the default for Anaconda

```
powershell
# Re‑add the bucket so it sits above Extras in Scoop’s listscoop bucket rm anacondascoop bucket add anaconda https://github.com/jahanbani/scoop-anaconda3

# Now the usual commands pick the newer manifest automaticallyscoop update

# pulls all bucketsscoop update anaconda3

# upgrades Anaconda to the latest build

```
> **Tip:** If you never use Extras you can simply remove it:
>
> ```
powershell
> scoop bucket rm extras
> ```
---
#
# ⚠️  Path‑length warning (260‑char limit)The Anaconda 2025+ installers still rely on a legacy extractor that fails when any file path exceeds the classic **MAX\_PATH = 260** characters.If your Windows user name is long (e.g. `C:\Users\Firstname.Lastname\…`) **the silent install can abort with “Failed to extract packages”.**Two easy fixes:
| Fix
| One‑liner        |
|
---

---

---

---

---

---

---

---

---

---

---
| ---

---

---

---

---
- |
| **Install Scoop in a short root**
| \`\`\`powershell
| # fresh install\$env\:SCOOP='C:\scoop'

# (optional) persist for future sessions[Environment]: :SetEnvironmentVariable\('SCOOP','C\scoop','User'\)irm get.scoop.sh
| iex

```
|
| **Relocate an existing Scoop**
|
```
powershellscoop
 uninstall anaconda3 -p
# optional clean‑upscoop config SCOOP 'C:\scoop'scoop reset *

```
 |
| **Enable long paths in Windows**
| *Run as Admin*, then reboot:

```
powershellreg
 add HKLM\System\CurrentControlSet\Control\FileSystem /v LongPathsEnabled /t REG_DWORD /d 1 /f
```
 |Once Scoop’s root is short (`C:\scoop\apps\…`) the installer finishes silently on any PC.
---
#
# How the bucket stays current* Each manifest contains `checkver` + `autoupdate` rules that scrape <https://repo.anaconda.com/archive/

> .* A GitHub Action called **Excavator** runs every six hours:  1. Finds the newest installer filename.  2. Grabs the SHA‑256 from the same table row.  3. Updates `version`, `url`, and `hash` in the manifest and commits the change.* A second workflow installs the new build on a Windows runner to verify the hash before merging.You just run `scoop update`; the bucket takes care of itself.
---
#
# FAQ
| Question
| Answer |
|
---

---

---
-
| ---

---
--|
| **Will this overwrite my existing conda envs?**
| No. The manifest marks `App\envs` as `persist`, so your environments survive upgrades. |
| **Can I install an older build?**
| Yes: `scoop install anaconda3@2024.10-1` installs any version still hosted in the archive. |
| **32‑bit Windows?**
| Anaconda dropped 32‑bit support after 2022‑05. Use `anaconda3‑2022.05` from the **Versions** bucket. |
| **How do I verify the hash?**
| Every hash comes directly from the “SHA256” column on the archive page. Feel free to cross‑check at <https://repo.anaconda.com/archive/
> .
| ---
#
# License & trademarksManifest files are released under the [Unlicense](LICENSE).“Anaconda”® is a trademark of Anaconda Inc.; this project is **not** affiliated with or endorsed by Anaconda Inc.

```
