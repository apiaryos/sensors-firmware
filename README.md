# sensors-firmware

Signed firmware binaries for an ESP32-S3 BLE scanner project.

Each release is an ESP-IDF app image (xtensa, esp32s3) paired with
an Ed25519 detached signature that devices verify against a
compiled-in public key before activation.

## Layout

- `scanner-esp32s3-<version>.bin` — firmware image for the LilyGo
  T-SIM7080G (ESP32-S3).
- `scanner-esp32s3-<version>.sig` — raw 64-byte Ed25519 signature over
  the corresponding `.bin` bytes.

Source: https://github.com/apiaryos/sensors-ble-scan

## Signature verification

Every device is flashed with a specific Ed25519 public key at
build time. Binaries published here can be read by anyone but
cannot be modified — devices refuse to activate any image whose
signature doesn't verify against their compiled-in key.

Current production public key fingerprint (SHA-256 of the 64-char
lowercase hex encoding of the 32-byte key):

    751b1844e98a903bdb9461bbb732b70570b10a830c0c55bde5ecf5d19af57c76

## Using a binary

Devices fetch binaries automatically once per upload cycle via an
OTA metadata endpoint. Manual download has no practical use — the
binary is target-specific (xtensa-esp32s3) and pairs with
per-device credentials provisioned into flash NVS.

---

Commits on this repo are produced automatically by CI on tag
pushes to [apiaryos/sensors-ble-scan](https://github.com/apiaryos/sensors-ble-scan).
