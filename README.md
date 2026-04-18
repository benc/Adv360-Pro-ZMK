# Kinesis Advantage 360 Pro ZMK Config — personal fork

Personal fork of [KinesisCorporation/Adv360-Pro-ZMK](https://github.com/KinesisCorporation/Adv360-Pro-ZMK).
For keyboard documentation, layer colors, upgrade notes, beta testing, and general ZMK usage,
see the **[upstream README](https://github.com/KinesisCorporation/Adv360-Pro-ZMK/blob/master/README.md)**
and **[ZMK docs](https://zmk.dev/docs)**.

## My modifications

- **Forgejo Actions CI** (`.forgejo/workflows/build.yml`) — self-hosted build, single matrix
  job over `adv360_left` / `adv360_right`. The first step bootstraps `node` inside the
  `zmkfirmware/zmk-build-arm:stable` container via [mise](https://mise.jdx.dev/) so the
  runner can exec JS-based actions (`checkout`, `cache`, `upload-artifact`).
- **Dropped the Clique / ZMK Studio build variant** — keymap lives in git, not in
  on-device settings, so Studio's live-edit flow isn't useful here.
- **Local build via `make`** — uses Podman or Docker against the stock ZMK image. See
  `Makefile` and `bin/build.sh`.
- Personal keymap tweaks in `config/adv360.keymap`, `config/adv360_left.keymap`,
  `config/adv360_right.keymap`, and `config/macros.dtsi`.

## Editing the keymap

I use **[nickcoutsos/keymap-editor](https://nickcoutsos.github.io/keymap-editor/)** —
a web GUI that reads and writes the `.keymap` files directly via GitHub OAuth, so every
change lands as a commit and CI rebuilds the firmware. Git stays the source of truth.

Kinesis's own editor at <https://kinesiscorporation.github.io/Adv360-Pro-GUI> also works
but stores state differently and can diverge from git.

Key positions for combos etc. are documented in [`assets/key-positions.md`](assets/key-positions.md).

## Building

- **CI:** push to trigger `.forgejo/workflows/build.yml`; download `firmware-left` /
  `firmware-right` artifacts.
- **Locally:** `make all` (both halves) or `make left` (left only). Requires Docker or
  Podman; `make` picks whichever is on `PATH`. `make clean` resets everything.

## Flashing

Standard Adv360 Pro procedure — see the
[upstream instructions](https://github.com/KinesisCorporation/Adv360-Pro-ZMK/blob/master/README.md#flashing-firmware),
the [Quick Start Guide](https://kinesis-ergo.com/wp-content/uploads/Advantage360-Professional-QSG-v8-25-22.pdf),
and the [User Manual](https://kinesis-ergo.com/wp-content/uploads/Advantage360-ZMK-KB360-PRO-Users-Manual-v3-10-23.pdf).
