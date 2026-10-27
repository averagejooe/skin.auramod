
# AuraMod for Matrix

Please read [wiki](https://github.com/SerpentDrago/skin.auramod/wiki) for Matrix Install and post install instructions

![image](https://user-images.githubusercontent.com/21133858/119548063-d2253d80-bd63-11eb-8db7-a1d6062788b2.png)

---

## This fork

A personal fork of [SerpentDrago/skin.auramod](https://github.com/SerpentDrago/skin.auramod).
Upstream credit belongs to skyfsza, inb4after, SerpentDrago, and jurialmunkey (original Aura).

## v2.1.0 — hide the SxxExx label on artwork

Adds a skin setting that hides the `S01:E04` style label printed on top of artwork in
library views. It is **hidden by default**; existing installs get the new default applied
once on first load.

**Where to find it:** Skin Settings → Library → *Disable episode label on artwork*

The setting is a checkbox. Ticked = label hidden, unticked = label visible.

### Files changed

| File | Change |
|---|---|
| `1080i/Includes_View_Posters.xml` | 7 `<visible>` conditions appended |
| `1080i/Includes_View.xml` | 1 `<visible>` condition appended |
| `1080i/SkinSettings.xml` | New radiobutton control `id="9513"` |
| `1080i/Startup.xml` | Seeds the setting on first load |
| `language/*/strings.po` | New string `#31935` (all 7 languages) |
| `addon.xml` | Version `2.0.4` → `2.1.0` |
| `changelog.txt` | Release note |

No images, textures, or dependencies were touched. `media/Textures.xbt` is unchanged,
so no texture-cache rebuild is required.

---

## Installation

Pick **one** of the two methods below. If you already have AuraMod installed and only want
this setting, method 2 is faster and safer.

### Method 1 — Install the zip

1. Download `skin.auramod-2.1.0.zip`.
2. In Kodi: **Settings → Add-ons → Install from zip file**.
3. Point it at the downloaded zip.

> ⚠️ **Warning — expect a black screen on Fire TV / low-power devices**
>
> Installing a skin from a zip **removes the existing skin folder first**, including Kodi's
> current skin. Kodi briefly runs with no skin at all, which appears as a black screen.
> It then falls back to Estuary and extracts the new copy.
>
> The long delay afterwards is **not** a crash. AuraMod depends on `script.skinshortcuts`,
> which rebuilds `1080i/script-skinshortcuts-includes.xml` from your saved menu data the
> first time the skin loads. That file is generated, not shipped, so every fresh install
> pays this cost. On a Fire TV Stick 4K expect it to take noticeably longer than a normal
> restart.
>
> Your menu, widgets, and settings are **not lost** — they live in
> `userdata/addon_data/script.skinshortcuts/skin.auramod/` and survive the reinstall.
> They are being recomputed, not rebuilt from scratch.
>
> **Do not force-close Kodi while the menu is rebuilding.** Let it finish. If it looks
> wedged, restart once and give it a full run before assuming something is broken.

### Method 2 — Replace files in place (recommended for updates)

No reinstall, no Estuary fallback, no menu rebuild. Copy the changed files over the
existing skin folder, then reload the skin.

**Files to copy** (only these five are required):

```
1080i/Includes_View_Posters.xml
1080i/Includes_View.xml
1080i/SkinSettings.xml
1080i/Startup.xml
language/resource.language.en_gb/strings.po
```

Optionally also copy `addon.xml` and `changelog.txt` so Kodi reports version `2.1.0`.
The other six `strings.po` files are optional — untranslated strings fall back to English.

**Steps**

1. Locate the skin folder (paths below) and **back it up** — copy `skin.auramod` somewhere safe.
2. Overwrite the five files above, keeping the same folder structure.
3. In Kodi, go to **Skin Settings → Reload skin**, or restart Kodi.
4. The setting appears under **Skin Settings → Library**.

> **Note:** `Startup.xml` only runs when the skin loads. If the label is still visible
> straight after a reload, restart Kodi once so the new default is seeded.

#### Skin folder locations

| Platform | Path |
|---|---|
| Windows | `%APPDATA%\Kodi\addons\skin.auramod\` |
| Android / Fire TV | `/storage/emulated/0/Android/data/org.xbmc.kodi/files/.kodi/addons/skin.auramod/` |
| LibreELEC / CoreELEC | `/storage/.kodi/addons/skin.auramod/` |
| macOS | `~/Library/Application Support/Kodi/addons/skin.auramod/` |
| Linux | `~/.kodi/addons/skin.auramod/` |

On Android and Fire TV, the `.kodi` folder is often hidden and difficult to reach with an
on-device file manager. Copying files in is easier from a PC over a network share or an
FTP server add-on running on the device. A plain USB stick works too if the device has a
spare port or an OTG adapter.

> **Avoid changing `addon.xml`** during a file-copy update unless you also intend to
> reinstall from zip. Kodi only re-reads add-on metadata at startup, and a version number
> that doesn't match an installed zip can cause it to prompt for an upgrade you didn't
> intend. Editing the XML views alone never requires a version bump.
