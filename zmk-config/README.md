# Nova42 ZMK Configuration

Custom ZMK firmware configuration for the Nova42 split keyboard.

## Keyboard Specifications

- **Controller:** nice!nano v2 (nRF52840)
- **Matrix:** 6 columns × 4 rows per half (COL2ROW)
- **Layout:** 21 keys per side (3 rows × 6 keys + 3 thumb keys), 42 total
- **Communication:** Bluetooth (split)

## Pin Configuration

- **Row pins:** P0.31, P0.29, P0.02, P1.15 (Pro Micro 21, 20, 19, 18)
- **Column pins:** P0.08, P0.06, P0.17, P0.20, P0.22, P0.24 (Pro Micro 0, 1, 2, 3, 4, 5)

## Features

- ZMK Studio support (left half only)
- Bluetooth split keyboard communication

## Building

### Prerequisites

- [Zephyr SDK](https://docs.zephyrproject.org/latest/getting_started/index.html) installed
- West tool installed (`pip3 install west`)

### Build Commands

```bash
# Set up environment
export ZEPHYR_SDK_INSTALL_DIR=$HOME/zephyr-sdk-0.17.0
export ZEPHYR_TOOLCHAIN_VARIANT=zephyr

# Build left half (with ZMK Studio)
west build -d build/nova42_left -b nice_nano//zmk -S studio-rpc-usb-uart -- -DSHIELD=nova42_left -DCONFIG_ZMK_STUDIO=y

# Build right half
west build -d build/nova42_right -b nice_nano//zmk -- -DSHIELD=nova42_right
```

The compiled `.uf2` files will be in:
- `build/nova42_left/zephyr/zmk.uf2`
- `build/nova42_right/zephyr/zmk.uf2`

## Flashing

1. Put the nice!nano into bootloader mode (double-tap reset)
2. Mount the UF2 drive
3. Copy the `.uf2` file to the drive

## License

MIT
