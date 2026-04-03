# R36S Boot Investigation + Fix

## What was found

1. `boot.ini` was hard-coded to a single DTB (`rk3326-r35s-linux.dtb`).
2. This card already contains multiple DTB variants (`rk3326-rg351mp-linux.dtb`, `.orig`, `.tony`), which is usually done to support different LCD panel revisions on R33S/R35S/R36S units.
3. Community DTB guidance for R36S family explicitly calls out that newer units may require trying different DTBs / screen-specific variants.

## Changes made

- Updated `boot.ini` to try DTBs in fallback order:
  1. `rk3326-r35s-linux.dtb`
  2. `rk3326-rg351mp-linux.dtb`
  3. `rk3326-rg351mp-linux.dtb.orig`
  4. `rk3326-rg351mp-linux.dtb.tony`
- Removed single quotes around the root UUID in kernel args to avoid passing quoted UUID text to the kernel command line parser.

## Why this should help

A common R36S failure mode is black screen / no complete boot when the selected DTB does not match the panel/hardware revision. The fallback logic allows one image to boot across multiple known variants without manual file renaming each attempt.

## If still not booting

- Re-check the root filesystem UUID in `boot.ini` against the actual root partition UUID on the SD card.
- Confirm the card image wrote correctly (checksum and full-capacity write).
- If available, capture serial output on UART to identify whether boot fails at DTB load, kernel init, or root mount.

## Reference

- AeolusUX R36S-DTB README: <https://github.com/AeolusUX/R36S-DTB>
