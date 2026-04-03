# Clean Install Plan for R36S (Boot Loop / Black Screen / Blinking Dash)

Given your symptom (logo -> long loading -> black screen with blinking dash), the fastest path is a **full clean reflash** with a known-good image.

## Recommended clean images (verified sources)

### Option A (recommended first): ArkOS R3XS multipanel image
- Releases page: https://github.com/AeolusUX/ArkOS-R3XS/releases
- Use the R33S/R35S/R36S **"Download Multipanel Image"** from release **ArkOS R3XS V2.0 (07312025-1)**.

Why first: it is specifically packaged for mixed panel revisions without manual DTB swapping.

### Option B (fallback): UnofficialOS RK3326-CLONE
- Releases page: https://github.com/RetroGFX/UnofficialOS/releases
- Use the image listed as **RK3326-CLONE** for R33S/R35S/R36S class devices.
- Follow clone install instructions linked from the same release notes/wiki.

## Clean install steps (do not skip)

1. **Use a known good SD card**
   - Prefer branded A1/A2 card, 64GB+.
   - Avoid the stock included card for testing.

2. **Fully erase then flash image**
   - Windows: Rufus / Win32 Disk Imager
   - macOS/Linux: balenaEtcher or `dd`
   - After flashing, safely eject and reinsert once to ensure partition table is readable.

3. **First boot with only TF1 inserted**
   - Remove TF2 (games card) for first boot.
   - Let first boot run for up to 10 minutes.

4. **If boot succeeds, then add TF2**
   - Insert games card after OS setup completes.

5. **If still failing at blinking dash**
   - Reflash the *other* firmware option above.
   - Confirm root partition UUID in `boot.ini` matches actual root partition UUID.
   - Capture UART serial logs for exact failure stage.

## Quick verification checklist

- [ ] New/fresh SD card used
- [ ] Correct image family selected (R36S multipanel or RK3326-CLONE)
- [ ] Flash completed without write errors
- [ ] First boot attempted with TF1 only
- [ ] Boot partition contains `Image`, `uInitrd`, and expected DTBs
