# Emoji-Recolour
dont share or sell it without my permission
# ✨ Universal Discord Emoji Recolorer & Auto-Uploader
**Created by T4N1SHQ** | **Support Server:** [https://discord.gg/n45bDCzgN3](https://discord.gg/n45bDCzgN3)

A standalone, zero-dependency-conflict tool (`emoji_recolorer.py`) that recolors custom Discord emojis (both **static PNG/WEBP** and **animated GIFs** frame-by-frame) from any source color to **any target color (`#HEX` or preset name)** while keeping transparency, shadows, white/grey/black details, and non-matching colors untouched.

It works with **any Discord bot** (Python `discord.py`, Node.js `discord.js`, or local image folders) and automatically uploads the recolored emojis to your bot's **Discord Application Emojis** and updates the emoji IDs in your code files.

---

## 🎨 Supported Colors (`--from-color` & `--to-color`)

### 1. Source Colors (`--from-color` / `FROM_COLOR`)
Choose which color in your existing emojis you want to replace (all other colors are left untouched):
- `red` *(default — replaces red, crimson, and scarlet pixels only)*
- `blue` *(replaces blue pixels only)*
- `green` *(replaces green pixels only)*
- `yellow` *(replaces yellow/gold pixels only)*
- `orange` *(replaces orange pixels only)*
- `purple` *(replaces purple/violet pixels only)*
- `pink` *(replaces pink/magenta pixels only)*
- `cyan` *(replaces cyan/aqua pixels only)*
- `all` *(recolors **every** colored pixel in the emoji to your target color while keeping white, grey, black, and transparency intact)*
- Or pass any custom `#RRGGBB` hex code (e.g. `--from-color "#FF0000"`)

### 2. Target Colors (`--to-color` / `TO_COLOR`)
You can pass **any Hex color code** (e.g. `#9B59B6`, `#00FFAA`, `#38BDF8`) **OR** any of these built-in preset names:

| Preset Name | Hex Code | Visual Style |
| :--- | :--- | :--- |
| `purple` | `#9B59B6` | After Hours Royal Purple |
| `neon_purple` | `#A855F7` | Bright Neon Purple |
| `violet` | `#8B5CF6` | Electric Violet |
| `indigo` | `#6366F1` | Deep Indigo |
| `blue` | `#3B82F6` | Modern Discord Blue |
| `sky` | `#0EA5E9` | Sky Blue |
| `cyan` | `#06B6D4` | Cyber Cyan |
| `teal` | `#14B8A6` | Ocean Teal |
| `green` | `#22C55E` | Neon Emerald Green |
| `emerald` | `#10B981` | Mint Emerald |
| `lime` | `#84CC16` | Acid Lime |
| `yellow` | `#EAB308` | Sunshine Yellow |
| `gold` | `#F59E0B` | Royal Gold |
| `orange` | `#F97316` | Sunset Orange |
| `red` | `#EF4444` | Crimson Red |
| `crimson` | `#DC2626` | Deep Blood Red |
| `rose` | `#F43F5E` | Sakura Rose |
| `pink` | `#EC4899` | Hot Neon Pink |
| `magenta` | `#D946EF` | Cyber Magenta |
| `white` | `#FFFFFF` | Clean Monochrome White |

---

## 🚀 Way 1: Use in ANY Bot via Command Line (Python, Node.js, etc.)

Drop `emoji_recolorer.py` into any bot's root folder and run it from your terminal or hosting panel:

### Example A — Recolor all Red emojis to Neon Purple in a Python Bot:
```bash
python emoji_recolorer.py --token "YOUR_BOT_TOKEN" --from-color red --to-color "#A855F7" --files utils/emoji.py
```

### Example B — Recolor all Red emojis to Cyan in a Node.js (`discord.js`) Bot:
```bash
python emoji_recolorer.py --token "YOUR_BOT_TOKEN" --from-color red --to-color cyan --files src/emojis.json src/config.js
```

### Example C — Recolor ALL colored emojis to Gold using `.env`:
1. Copy `.env.example` to `.env` and fill in `BOT_TOKEN`, `FROM_COLOR="all"`, `TO_COLOR="gold"`, and `TARGET_FILES="utils/emoji.py"`.
2. Run:
```bash
python emoji_recolorer.py
```
*(If you don't create a `.env` or pass flags, running `python emoji_recolorer.py` opens an interactive prompt asking for your token, source color, and target color!)*

---

## 🐍 Way 2: Import Directly Inside Any `discord.py` Bot (`on_ready`)

If you want your `discord.py` bot to automatically recolor and sync its emojis on startup:

1. Place `emoji_recolorer.py` in your bot's root folder (or `utils/emoji_recolorer.py`).
2. Add these 2 lines inside your `on_ready()` event in `main.py` / `afterhours.py`:

```python
from emoji_recolorer import sync_and_recolor_emojis

@bot.event
async def on_ready():
    print(f"Logged in as {bot.user}")
    # Recolors all 'red' emojis to '#9B59B6' (or 'cyan', 'blue', 'gold', etc.)
    # and updates utils/emoji.py automatically!
    bot.loop.create_task(
        sync_and_recolor_emojis(
            bot,
            from_color="red",       # 'red', 'blue', 'green', 'all', etc.
            to_color="#9B59B6",     # Any #HEX code or preset name
            target_files=["utils/emoji.py"]
        )
    )
```

---

## 📁 Way 3: Recolor a Local Folder of `.png` / `.gif` Emoji Images Offline

If you have a folder of `.png`, `.webp`, or animated `.gif` emoji files on your computer and want to recolor all of them without uploading to Discord yet:

```bash
python emoji_recolorer.py --input-dir ./my_emojis --output-dir ./purple_emojis --from-color red --to-color neon_purple
```

All recolored `.png` and animated `.gif` files will be saved in `./purple_emojis/` ready to upload anywhere.
