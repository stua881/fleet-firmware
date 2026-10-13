# fleet-firmware

Compiled firmware for every device in the FleetWatcher fleet. Sources are private;
each source repo's CI publishes here when a version tag is pushed.

## Releases

Each release is tagged `<project>-v<version>`, and its assets are named after the
device they are for, plus a `SHA256SUMS` file. Tags with a suffix (`-test`, `-rc1`)
are pre-releases and should not be used for OTA.

| Project | Tag | Source repo |
|---|---|---|
| LoRa gateway | `lora-truck-gateway-v1.2.0` | stua881/lora-truck-gateway |
| LoRa node | `lora-truck-node-v0.5.0` | stua881/lora-truck-node |
| BLE / cellular gateway | `bletracker-gateway-v2.2.0` | stua881/BLETracker (`firmware/`) |

## Devices

| Device | Hardware | Project / build env | Asset | How to update |
|---|---|---|---|---|
| LoRa Bridge (1995), 48CA435B9BEC | LilyGO T-Beam S3 Supreme | lora-truck-gateway / `tbeam-supreme` | `lora-truck-gateway-<ver>.bin` | Web `/update` upload, or USB (esptool) |
| Home T3, 10061C314BDC | LilyGO T3 V1.6.1 | lora-truck-gateway / `t3-v161` | `lora-truck-gateway-t3-v161-<ver>.bin` | Web `/update` upload, or USB |
| 2012 plant gateway, ESP32_2012 | Seeed XIAO ESP32-C3 | BLETracker / `xiao-esp32c3` | `bletracker-gateway-xiao-esp32c3-<ver>.bin` | FleetWatcher OTA push, or USB (`--no-stub`, 115200) |
| TruckGateway_1E64, 24587CE41E64 | Seeed XIAO ESP32-S3 | BLETracker / `xiao-esp32s3` | `bletracker-gateway-xiao-esp32s3-<ver>.bin` | FleetWatcher OTA push, or USB |
| Cellular gateway, 1020BA720910 | LilyGO T-SIM7670G-S3 | BLETracker / `t-sim7670g-s3` | `bletracker-gateway-t-sim7670g-s3-<ver>.bin` | USB (no OTA over cellular yet) |
| LoRa node 736C | Seeed XIAO nRF52840 + Wio-SX1262 | lora-truck-node / `xiao-nrf52840` | `lora-truck-node-<ver>.uf2` | Double-tap reset, copy the .uf2 to the drive |
| LoRa node D80A | RAK4631 | lora-truck-node / `rak4631` | `lora-truck-node-rak4631-<ver>.uf2` | Double-tap reset, copy the .uf2 to the drive |

The `.bin` files are app images, which keep a device's saved settings (Wi-Fi, server,
gateway name). They are built with no Wi-Fi passwords or other secrets compiled in.
A blank board also needs the bootloader and partition table published alongside the
app image (USB flash at the offsets in the source repo's README).
