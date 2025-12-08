# ESPHome Configuration Repository

This repository contains ESPHome configuration files for various devices used in the project. ESPHome allows you to easily manage firmware for ESP8266/ESP32 based devices, integrating them with Home Assistant or other MQTT platforms.

## Repository Structure

```
config/
├── <device>.yaml   # ESPHome configuration for a device (one file per device)
├── secrets.yaml    # Secrets (Wi‑Fi credentials, API keys, etc.) – **never commit real secrets**
└── archive/        # Archived/old configuration files
```

## Getting Started

1. **Install ESPHome** (if you haven't already). It is recommended to use a Python virtual environment:
   ```bash
   python -m venv .venv            # create a virtual environment in the project root
   source .venv/bin/activate       # activate the venv (Linux/macOS)
   pip install --upgrade pip       # upgrade pip inside the venv
   pip install esphome
   ```

2. **Run the ESPHome Dashboard** (relative to the repository root):
   ```bash
   cd $(git rev-parse --show-toplevel)   # or simply stay in the project root
   esphome dashboard config/
   ```
   This will start a local web UI (default at `http://localhost:6052`) where you can edit, validate, and upload firmware.

3. **Validate a configuration** (using a relative path). Note that the ESPHome command expects the action *before* the file path:
   ```bash
   esphome validate config/esphome-picow.yaml
   ```

4. **Compile and upload firmware** (choose the appropriate device). Again, the command comes first:
   ```bash
   esphome run config/esphome-picow.yaml
   ```
   The command will compile the firmware and either flash it over USB or OTA, depending on the configuration.

## Secrets Management

The `secrets.yaml` file should contain key‑value pairs for any sensitive data (Wi‑Fi credentials, API keys, etc.). Reference them in your device YAML files using the `!secret` tag, e.g.:

```yaml
wifi:
   ssid: !secret wifi_ssid
   password: !secret wifi_password
```

**Important:** Never store real secrets in a public repository. Keep `secrets.yaml` private or add it to `.gitignore`.

## Adding a New Device

1. Copy an existing YAML file as a starting point.
2. Update the `esphome:` name, Wi‑Fi credentials, and any hardware pins.
3. Add the new file to the `config/` directory.
4. Validate and flash using the steps above.

## Contributing

- Keep the repository tidy: remove unused files, move old configurations to `archive/`.
- Update the README when adding new devices or changing the structure.
- Ensure that any new secrets are added to `secrets.yaml` and that the file is excluded from version control (`.gitignore`).

## License

This collection of configuration files is provided under the MIT License. Feel free to adapt them for your own projects.
