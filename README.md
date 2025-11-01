# Hellbot Magna 2 300 / Wanhao D12 300 (single/dual extruder) — Klipper Configuration

### For MKS Robin Nano v1.3 board

This repository contains Klipper configuration files and notes for the Hellbot Magna 2 300 / Wanhao D12 300 3D printer, specifically tailored for the MKS Robin Nano v1.3 control board.

Contents
- `printer.cfg` — main Klipper config for this printer
- `klipper-config/` — makefile settings to compile the firmware

## Prerequisites

- A host running Klipper (Raspberry Pi or similar).
- Klipper installed and configured on the host. See the Klipper docs: https://www.klipper3d.org/
- Optional: Moonraker + Mainsail or Fluidd for web control and monitoring.
- Basic familiarity with SSH and copying files to your Klipper host.

## Quick install

1. Copy `klipper-config/` to your Klipper firmware directory (commonly `~/klipper`) and compile the firmware:

```cd ~/klipper
cp -r /path/to/this/repo/klipper-config ./
make -j$(nproc)
```
2. Flash the compiled firmware to the MKS Robin Nano v1.3 board:
- Copy the generated `klipper.bin` file from `~/klipper/out/` to a FAT32 formatted microSD card.
- Rename it to `Robin_nano35.bin`.
- Insert the microSD card into the printer and power it on. The board should flash the firmware automatically (LED will blink during flashing).
- After flashing, the printer will get stuck displaying `Updating 100%`. Power off the printer, remove the microSD card, and power it back on.
- **The printer will now be stuck showing `Booting...`, this is normal behavior and it's expecting Klipper to connect.**
3. Copy `printer.cfg` to your Klipper config directory (commonly `~/klipper_config/printer.cfg` or `/home/pi/klipper_config/printer.cfg`).
	- If you use a web UI (Mainsail/Fluidd) you can upload `printer.cfg` there.
4. Restart the Klipper service to load the new config.
5. If you changed stepper or heater settings, test movement and heaters carefully before loading filament.

## Troubleshooting

- Klipper won't connect to MCU: check USB cable, correct port in `printer.cfg`, and dmesg for serial device. If you're following a full guide, make sure that **you're NOT** running the signing script (`scripts/sign_mks_robin_nano.sh`), as this board does not require it.

## Contributing

If you have improvements, bug fixes, or alternate configs for different printer variants, please open a PR. When submitting changes, include:

- A short description of the change
- Hardware differences (board, thermistor type, probe model)
- Any testing performed

## License

This repository is available under the terms of the included [LICENSE](LICENSE) file.