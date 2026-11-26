# Awesome MPC Sample [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of firmware resources, custom Knob FX plugins, developer tools, community OS mods, and Linux setup guides for the **Akai Professional MPC Sample**.

## Contents

- [Official Resources](#official-resources)
- [What's New in Firmware v1.4](#whats-new-in-firmware-v14)
- [Custom Knob FX Plugins & SDK (v1.4+)](#custom-knob-fx-plugins--sdk-v14)
- [Custom OS Mods, Bootloaders & Emulators](#custom-os-mods-bootloaders--emulators)
- [Linux Installation, Updates & Dev Setup](#linux-installation-updates--dev-setup)
  - [Updating Firmware on Linux](#updating-firmware-on-linux)
  - [Fixing `mpc-sample.local` on Linux](#fixing-mpc-samplelocal-on-linux)
  - [SSH & Remote Screen (v1.4 Developer Mode)](#ssh--remote-screen-v14-developer-mode)
  - [Building Custom Plugins on Linux](#building-custom-plugins-on-linux)
- [Hardware & Storage Notes](#hardware--storage-notes)
- [Communities](#communities)
- [Contributing](#contributing)
- [License](#license)

---

## Official Resources

- [Akai Pro — MPC Sample Downloads](https://www.akaipro.com/downloads-and-support/downloads/?product=MPC%20Sample) — Official hub for firmware `.img` files, Windows/macOS updaters, drivers, and user manuals.
- [MPC Sample Firmware Downloads](https://www.akaipro.com/downloads-and-support/downloads/firmware/mpc/sample/) — Direct firmware download page.
- [MPC Sample 1.4.0 Release Notes (PDF)](https://cdn.inmusicbrands.com/akai/sample/MPC%20Sample%201.4.0%20Release%20Notes.pdf) — Full changelog, known issues, and developer notes for v1.4.0.
- [MPC Sample Firmware Update Guide](https://support.akaipro.com/en/support/solutions/articles/69000877649-mpc-sample-firmware-update) — Official desktop updater and manual web-upload instructions.
- [MPC Sample 1.4 Dev Enhancements (Beta) FAQ](https://support.inmusicstore.com/en/support/solutions/articles/69000885361-mpc-sample-1-4-dev-enhancements-beta-frequently-asked-questions) — Official documentation for custom plugins, Developer Mode, SSH, screenshots, and Remote Screen.

---

## What's New in Firmware v1.4

Firmware **v1.4.0** transforms the MPC Sample into an open-plugin platform while adding several workflow upgrades:

- **Dev Enhancements (Beta):** Enable via `SHIFT + PAD 8 (MIDI Config)` → `Dev Enhancements (Beta)`. Unlocks custom Knob FX plugins, USB SSH access, Remote Screen + audio sharing, PNG screenshots (saved to `/Screenshots` on your microSD card), and prompted `autorun` scripts at the card root.
- **Resample Pad:** Render a pad's active Knob FX directly into the sample so you can stack multiple effects sequentially.
- **Auto-Playback After Sequence-Length Recording:** Samples recorded to sequence length begin playing back immediately when recording finishes, enabling live looper workflows.
- **16-Level Tune (Scale Modes):** Play pitched samples across all 16 pads constrained to a chosen musical scale (chromatic mode remains available).
- **Sample Preview Volume & Step Edit Previews:** Hold `SHIFT` in the Sample Select browser for a Preview Volume slider, and toggle Preview inside Step Edit to audition events while scrolling.
- **Usage Monitor:** Inspect real-time CPU, RAM, internal disk, and microSD card usage from MIDI Config (essential when testing third-party plugins).

---

## Custom Knob FX Plugins & SDK (v1.4+)

> **Note:** Desktop VST2 plugins will **not** work on the MPC Sample. Plugins must be compiled specifically for 64-bit ARM Linux using the MPC Plugin SDK or Open MPC toolchain and placed in a `VST2 Plugins` folder at the root of your microSD card. Third-party plugins run in-process without crash isolation—save your project before testing new effects and check the Usage Monitor if you hear dropouts.

- [MPC Plugin Builder SDK](https://github.com/inmusic-software/mpc-plugin-builder-sdk) — Official MIT-licensed SDK from inMusic/Akai for building custom effects (and instruments for larger MPCs) in C++ or via an AI coding agent workflow.
- [Open MPC Plugin Catalog](https://open-mpc.github.io/) — Browsable community catalog of free, checksummed standalone VST2 plugins and add-ins with an MPC Sample compatibility filter.
- [open-mpc/mpc-vst-plugins](https://github.com/open-mpc/mpc-vst-plugins) — Community plugin toolchain, porting guides, Skin Studio, benchmarks, and add-ins (including screen drawing helpers for MPC Sample).
- [Sample Mods](https://samplemods.com/) — Community directory tracking MPC Sample mods, custom firmwares, plugins, and release changelogs.

---

## Custom OS Mods, Bootloaders & Emulators

> **Firmware Compatibility Warning (v1.3 vs. v1.4):** Firmware v1.4 requires OS mods hooked into the v1.3 binary to be rebuilt against v1.4, and changes how `autorun` scripts launch (Developer Mode must be enabled and you must confirm the boot prompt). Check each project's supported firmware version before updating past `1.3.0.12`.

- [Melodee](https://github.com/keremimo/melodee-sample) — Full alternative groovebox OS built on `sample-base` featuring 16 tracks, VST3/LV2/CLAP/VST2 plugin hosting, stem separation, SFZ/SF2/XPM/DecentSampler playback, chord progressions, and a web UI at `http://melodee.local`. *(Supports `1.3.0.12` and `1.4.0.7`/`1.4.0.8` with Developer Mode enabled; runs at 44.1 kHz without Screen Mirror on 1.4.)*
- [SampQOL OS](https://github.com/snarebes/SampQOL-OS) — Free SD-card quality-of-life mod adding 16 drum tracks, step sequencer, Track View, mixer with pad/track/submix inserts and sidechain, 128-slice chop, on-device stem separation, and 16 USB outputs. *(Requires firmware `1.3.0.12`.)*
- [SampleBoot](https://github.com/pxcm/SampleBoot) — Non-destructive multi-OS boot selector from a single microSD card; choose between stock firmware, Melodee, SampQOL OS, or MPC Simple at power-on with the encoder. *(Tested on firmware `1.3.0.12`.)*
- [MPC Simple](https://sourceforge.net/projects/mpcsimple/) — Ground-up JUCE-based alternative OS aiming for a classic MPC workflow with modern enhancements and MPC 2.0 project loading.
- [mpc-sample-emulator](https://github.com/Phenix2417/mpc-sample-emulator) — Run the MPC Sample firmware and test SD-card mods like SampleBoot and SampQOL inside a Linux environment (including Android's Debian Linux Terminal).

---

## Linux Installation, Updates & Dev Setup

Akai only ships desktop firmware updaters for Windows and macOS. On Linux, you can update firmware, access SSH, and build custom plugins natively without Wine or a VM.

### Updating Firmware on Linux

> **Tip:** Akai's v1.4.0 release notes note that the automatic `mpc-sample.local` web updater can miss the 1.4.0 update. Use **Manual Update** with the `.img` file instead.

1. Download the manual firmware `.img` file from the [Akai Pro MPC Sample Downloads](https://www.akaipro.com/downloads-and-support/downloads/?product=MPC%20Sample) page.
2. Connect the MPC Sample to your Linux machine using a data-capable USB-C cable and power it on.
3. Open `http://mpc-sample.local` (or `http://192.168.155.1` if mDNS is unavailable) in your browser.
4. Select **Manual Firmware Upload** / **Manual Update**, pick the downloaded `.img` file, and wait for the unit to reboot automatically. Do not unplug the cable during the update.

### Fixing `mpc-sample.local` on Linux

If your browser cannot reach `http://mpc-sample.local` over USB:

1. **Try the direct USB IP first:** Open `http://192.168.155.1` in a private/incognito browser window.
2. **Verify mDNS (`avahi-daemon`):** Ensure `avahi-daemon` is installed and active (`sudo systemctl enable --now avahi-daemon`) and that `/etc/nsswitch.conf` includes `mdns_minimal [NOTFOUND=return]` before `dns`.
3. **NetworkManager USB interface binding:** On distros using NetworkManager (such as Manjaro/KDE Plasma or Fedora), create a dedicated Wired connection profile restricted specifically to the MPC's USB network interface (commonly `usb0`), save it, reconnect, and reload `http://mpc-sample.local` in a private window.

### SSH & Remote Screen (v1.4 Developer Mode)

1. On the MPC Sample, press `SHIFT + PAD 8 (MIDI Config)` and scroll to **Dev Enhancements (Beta)**.
2. Enable **Developer Mode** (starts the USB SSH server) and/or **Remote Screen**.
3. Check the **Remote Screen** page on the hardware for the generated address and password.
4. Connect from a Linux terminal:

```bash
ssh root@<mpc-address>
```

> **Security Note:** Remote Screen video and shared audio are unencrypted—anyone on the same network with the displayed password can view your screen and hear audio.

### Building Custom Plugins on Linux

The official [MPC Plugin Builder SDK](https://github.com/inmusic-software/mpc-plugin-builder-sdk) runs natively on Linux with minimal setup:

- **Requirements:** `git` and **Python 3.9+**. The build script (`tools/build.py`) automatically fetches the Zig cross-compiler on first run (GNU cross-compilers and Docker are also supported—see `docs/building.md` in the SDK repo).
- **Deploying to MPC Sample:** Compile your effect plugin, mount the microSD card (directly or via the MPC Sample's **SD Card Access** mode), and copy the compiled plugin folder into `VST2 Plugins/` at the root of the card.
- **Loading on Hardware:** Enable **Custom Plug-In Support** inside `Dev Enhancements (Beta)`. Your effect will appear at the bottom of the **Knob FX** list.

---

## Hardware & Storage Notes

- **microSD Formatting:** Format cards as **exFAT** for cross-OS compatibility and SD-card mods.
- **Card Speed:** Use a reputable UHS-I (V30 / A2) microSD card—v1.4 lists a known `"Disk Too Slow"` warning when scrubbing through long streaming samples.
- **USB Audio on Linux:** The MPC Sample works as a class-compliant USB audio/MIDI device under PipeWire/ALSA.
- **Backup Rule:** Always back up your microSD card before installing custom firmware mods or testing beta plugins. To revert any SD-card `autorun` mod back to stock, power off the unit, remove the card, and rename the root `autorun` folder (e.g., to `autorun-off`).

---

## Communities

- [r/mpcsample](https://www.reddit.com/r/mpcsample/) — Dedicated subreddit for MPC Sample workflows, v1.4 news, and custom firmware releases.
- [r/mpcdev](https://www.reddit.com/r/mpcdev/) — Developer community for MPC Plugin SDK, Open MPC, and firmware modding.
- [r/mpcusers](https://www.reddit.com/r/mpcusers/) — General Akai MPC community for sampling tips, kits, and hardware troubleshooting.

---

## Contributing

Contributions are welcome! Please read the contribution guidelines before opening a pull request:

1. Ensure every added resource is actively maintained, clearly described, and notes its **supported firmware version** (`1.3.0.12`, `1.4+`, or both).
2. Keep descriptions concise, objective, and ending with a period.
3. Add one item per pull request when possible so changes are easy to review.

---

## License

[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the contributors have waived all copyright and related or neighboring rights to this work.
