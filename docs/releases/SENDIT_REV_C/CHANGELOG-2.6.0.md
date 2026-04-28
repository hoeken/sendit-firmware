# Version 2.6.0

## SendIt

### 🛠️ Improvements & Enhancements

- **PSRAM Support**
  - Enabled 8MB OPI PSRAM on ESP32-S3-WROOM-1-N16R8 (N16R8 variant)
  - Moved mbedTLS dynamic allocations to PSRAM, freeing internal heap for concurrent TLS connections
  - Configured asymmetric TLS record buffers (16KB in / 4KB out) to minimize per-session PSRAM usage
  - Added `sdkconfig.defaults` to properly configure PSRAM via IDF Kconfig

- **ADC Channel Config Validation**
  - Introduced `sanitizeConfig()` to validate config inputs before applying them
  - `type` field validated against whitelist: `raw`, `digital_switch`, `thermistor`, `4-20ma`, `high_volt_divider`, `low_volt_divider`, `ten_k_pullup`
  - `digitalInputMode` validated against: `direct`, `inverted`, `toggle_rising`, `toggle_falling`
  - `displayDecimals` clamped to 0–4; `averageWindowMs` clamped to 0–10000 (min 20 if non-zero)
  - `calibrationTable` validated as a proper array of `[v, y]` pairs when `useCalibrationTable` is true

## Infrastructure

- Updated to YarrboardFramework v3.0.0
- Updated firmware URL base to `firmware.sendit.yarrboard.com`

---