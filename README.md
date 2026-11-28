# Bluetooth-jammer-esp32 — ESP32/nRF24L01 RF experiment source

This repository collects Arduino sketches and prebuilt firmware binaries for experiments with **nRF24L01 2.4 GHz radio modules driven by ESP32 boards**. The source targets the same ISM band used by Bluetooth, BLE, and Wi-Fi devices. It is a documentation-and-source archive, **not** a build guide or an operating manual.

> **Legal warning:** intentionally interfering with radio communications (jamming) is illegal in many jurisdictions and can disrupt safety-critical and emergency communications. Only conduct RF experiments in a properly shielded enclosure or a licensed test facility, with the necessary permissions. Check local regulations before you buy or flash hardware.

## Provenance

This is a copy of the now-archived upstream project [smoochiee/Bluetooth-jammer-esp32](https://github.com/smoochiee/Bluetooth-jammer-esp32): the repository HEAD and commit history match upstream. The author points to [Noisy-boy-esp32-Bluetooth-jammer](https://github.com/smoochiee/Noisy-boy-esp32-Bluetooth-jammer) as the newer project with updated code. No changes to the original source or binaries are made here.

## What the repository contains

| Path | Contents |
|---|---|
| [INO/FOR VSPI PIN.ino](INO/FOR%20VSPI%20PIN.ino) | Sketch using the ESP32 VSPI bus with one nRF24L01 module |
| [INO/FOR HSPI PIN.ino](INO/FOR%20HSPI%20PIN.ino) | Sketch using the ESP32 HSPI bus with one nRF24L01 module |
| [INO/FOR DUAL PINS.ino](INO/FOR%20DUAL%20PINS.ino) | Variant using two nRF24L01 modules |
| [INO/User_control_channel.ino](INO/User_control_channel.ino) | Channel-selection example from upstream |
| [web/](web/) | Prebuilt ESP32 binary/bootloader/partition images, browser-flasher manifests, and `flash1.html` |
| [LICENSE](LICENSE) | GNU General Public License v3 |
| [GCash-MyQR-16032024181536.PNG.jpg](GCash-MyQR-16032024181536.PNG.jpg) | Donation QR image retained from upstream |

## What the code does, at a high level

The sketches initialize an nRF24L01 over SPI using the [RF24](https://github.com/nRF24/RF24) library and `ezButton`, put the radio into continuous-carrier mode, and sweep or step through channels in the 2.4 GHz band. They also shut down the ESP32's own Wi-Fi and Bluetooth controllers. The original README described nominal component choices (one or two nRF24 modules, an ESP32, a decoupling capacitor, and an optional toggle switch) and reported roughly 10 m of effect in its own informal tests; those claims are not independently verified here, and real-world results depend on hardware, protocol, distance, and environment.

This README intentionally omits wiring diagrams, pin assignments, channel tables, and flashing steps. Those details remain in the source files and upstream README for readers with a legitimate, lawful test setup.

## Responsible use

- Do not operate this hardware near public Bluetooth/Wi-Fi devices, medical or assistive technology, vehicles, aircraft, or emergency services.
- Use a shielded test enclosure or an authorized RF test range, keep transmission power and duration minimal, and stop if interference reaches unintended equipment.
- Respect spectrum regulations and the rights of other spectrum users; jamming is prohibited in many countries even on unlicensed bands.
- This material is provided for RF education and research only, with no warranty and no endorsement of disruptive use.

## Credits and license

Licensed under the **GNU General Public License v3** — see [LICENSE](LICENSE). Original work and media are credited to **smoochiee** (upstream author). The original README also thanks ATOMNFT (header/donations), ParrotStore, Sok Ponleu, and Philipp Simon, and asks that credit be preserved when the code is reused. The GPL v3 file contains only the standard license text, so no additional copyright holder is asserted here.

## Quick start — 1 or 2 commands

```bash
./setup.sh          # install dependencies
./setup.sh run      # start the project (when a run target exists)
```

`setup.sh` detects this repository's build system and installs the right toolchain
dependencies. Use `./setup.sh test` to run the available checks. If a project has no
standard run target, the script prints the correct command from the sections above.
