# scoop-anaconda3  🚀🐍

> **Always-fresh Scoop bucket for the latest Anaconda Distribution**
> Maintained by [@jahanbani](https://github.com/jahanbani) – auto-updated every six hours by GitHub Actions.

Anaconda releases new Windows installers several times a year, but the manifest in Scoop’s official **Extras** bucket often lags behind.
This bucket tracks **every** new build (e.g. `Anaconda3-2025.06-1`) within hours, so you can install or upgrade with a single command—even if you also keep Extras for other apps.

---

## Quick start — get the newest Anaconda without touching Extras

```powershell
# 1  Add this bucket (alias = anaconda)
scoop bucket add anaconda https://github.com/jahanbani/scoop-anaconda3

# 2  Install or upgrade, explicitly referencing this bucket
scoop install  anaconda/anaconda3      # first-time install
scoop update   anaconda/anaconda3      # later upgrades
```

### Why the **`anaconda/`** prefix?

Scoop stops searching as soon as it finds a manifest called `anaconda3.json`.
If you added the Extras bucket first, its older manifest “wins” unless you either

* use the bucket-qualified name (`anaconda/anaconda3`), **or**
* move this bucket higher in your bucket list (next section).

---

## (Optional) Make this bucket the default for Anaconda

```powershell
# Re-add the bucket so it sits above Extras in Scoop’s list
scoop bucket rm anaconda
scoop bucket add anaconda https://github.com/jahanbani/scoop-anaconda3

# Now the usual commands pick the newer manifest automatically
scoop update               # pulls all buckets
scoop update anaconda3     # upgrades Anaconda to the latest build
```

> **Tip:** If you never use Extras you can simply remove it:
> `scoop bucket rm extras`

---

## How the bucket stays current

* Each manifest contains `checkver` + `autoupdate` rules that scrape [https://repo.anaconda.com/archive/](https://repo.anaconda.com/archive/).
* A GitHub Action called **Excavator** runs every six hours:

  1. Finds the newest installer filename
  2. Grabs the SHA-256 from the same table row
  3. Updates `version`, `url`, and `hash` in the manifest and commits the change.
* A second workflow installs the new build on a Windows runner to verify the hash before the commit is merged.

You just run `scoop update`; the bucket takes care of itself.

---

## FAQ

| Question                                        | Answer                                                                                                                                                                        |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Will this overwrite my existing conda envs?** | No. The manifest marks `App\envs` as `persist`, so your environments survive upgrades.                                                                                        |
| **Can I install an older build?**               | Yes: `scoop install anaconda3@2024.10-1` installs any version still hosted in the archive.                                                                                    |
| **32-bit Windows?**                             | Anaconda dropped 32-bit support after 2022-05. Use `anaconda3-2022.05` from the **Versions** bucket.                                                                          |
| **How do I verify the hash?**                   | Every hash comes directly from the “SHA256” column on the archive page. Feel free to cross-check at [https://repo.anaconda.com/archive/](https://repo.anaconda.com/archive/). |

---

## License & trademarks

Manifest files are released under the [Unlicense](LICENSE).
“Anaconda”® is a trademark of Anaconda Inc.; this project is **not** affiliated with or endorsed by Anaconda Inc.
