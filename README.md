# SWAP CAN VOODOO — Firmware Binaries

Pre-built firmware binaries for the SWAP CAN VOODOO system.

This repository hosts the **latest stable binaries** for end users. No build tools required — just flash and go.

---

## What's in here

The system runs on two boards, each with its own firmware:

| It is for | Version | Latest binary | Board |
|-----------|---------|---------------|-------|
| **Screen (front display)** | V 0.9.1 | [Download](https://github.com/Biohazard86/SWAP-CAN-VOODOO-BIN/raw/refs/heads/main/releases/SCREEN_BIN/SCREEN_Swap-Can-VOODOO-V0.9.1.bin) | Display unit on the front (use left USB-C) |
| **Back (white PCB)** | V 0.9.1 | [Download](https://github.com/Biohazard86/SWAP-CAN-VOODOO-BIN/raw/refs/heads/main/releases/BACK_PCB_BIN/BACK_PCB_Swap-Can-VOODOO-V0.9.1.bin) | ECU communication board on the back of the gauge |
> Both boards must run **matching firmware versions** from the same release. Mismatched versions may use incompatible data framing.

---

## Changes
- V0.9.1
  - Add alarms control
  - Add buzzer
  - Add SSR control
  - Remember the position of the brightness slider
  - Add units to 'speed' tag on the logs
  - Add missfire for each cyl for Miss200 and Miss1000 on the logs
  - Bug fix
 
- V0.9
  - Base release 


---

## How to flash

You can flash directly from your browser — no software to install.

1. Connect the board to your computer via USB.
2. Open the web flasher: **https://esptool.spacehuhn.com** (Use Firefox or Chrome)
3. Click **Connect** and select the board's serial port. (For the back PCB, you need to hold BOOT button while you connect the USB-C)
4. Set the flash address to **`0x0`** (unless noted otherwise for a specific binary below).
5. Select the correct `.bin` file for the board you're flashing.
6. Click **Program** and wait for it to finish  (this process is slow for the screen bin, takes about 20-30 minutes. Only a few seconds for the white PCB).
7. Reset the board.

Repeat for the second board with its corresponding binary.

> **Tip:** If the board isn't detected, hold the **BOOT** button while plugging in (or while clicking Connect), then release. Some boards need to be put into download mode manually.


---

## Notes & safety

- **Match versions.** Always flash the Screen and Back PCB with binaries from the same release.
- **DO NOT upload the bin while still connected to the car** Take the display out of the car and use a good data cable. Random states of the pins (SSRs, CAN communication, etc) can be activated during the upload.
- **First boot.** After flashing fresh firmware, the device may take a few seconds to start. Configuration (alarm thresholds, screen brightness, SSR conditions) is stored on-device and persists across reboots.
- **SSR outputs.** If the link between the two boards is lost, the Back PCB drives all SSR outputs to a safe state. Keep both boards connected and powered for normal operation.
- **Wrong binary on wrong board** won't damage anything, but the device won't work correctly — just reflash with the right one.


---

## Troubleshooting

| Symptom | Try this |
|---------|----------|
| Board not detected by web flasher | Hold **BOOT** while connecting, try a different USB cable/port (must be a data cable, not charge-only) |
| Flash fails partway | Lower the baud rate, use a shorter/better USB cable |
| Screen boots but shows no data | Check the wiring between the two boards; make sure the Back PCB is powered and flashed with a matching version |
| Settings reset after reboot | Reflash; if it persists, the NVS partition may need erasing (full erase before flashing) |

---

*This repo contains binaries only. Flash at your own risk on your own hardware.*
