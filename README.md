# Home Assistant Scripts & Automations

This repository contains custom scripts and automation configurations for my Home Assistant instance.

## Contents

### 1. Automation: Kitchen Light Switch (`ikea_e2001_e2002_switch_to_light_automation.yml`)
Configures the **IKEA E2001/E2002** Zigbee switch to control the kitchen counter LEDs.
*   **Blueprint:** Uses `EPMatt/ikea_e2001_e2002.yaml`.
*   **Features:**
    *   **Short Press (Up/Down):** Turns lights On/Off AND toggles the motion sensor automation (`automation.kitchen_worktop_switch_light_on_motion`).
    *   **Long Press (Up/Down):** Dimming (Brightness +/-).
    *   **Long Press (Left/Right):** Color Temperature (Warm/Cool).
    *   **Short Press (Left/Right):** Step Color Temperature.

### 2. Helper Scripts (`scripts.yml`)
Contains 4 helper scripts used by the automation above to handle smooth transitions for brightness and color temperature:
*   `light_increase_brightness` / `light_decrease_brightness`
*   `light_increase_color_temp` / `light_decrease_color_temp`

## Deployment

The repository files correspond to entries in your Home Assistant configuration files.

### Deploying Changes

You can deploy changes by copying the content to your Home Assistant server via SSH.

**Prerequisites:**
*   SSH access to Home Assistant (e.g., via "Terminal & SSH" add-on).
*   User: `hassio` (or configured user).

**Steps:**

1.  **Backup current config** (optional but recommended):
    ```bash
    cp /config/automations.yaml /config/automations.yaml.bak
    cp /config/scripts.yaml /config/scripts.yaml.bak
    ```

2.  **Update Automations:**
    *   Open `/config/automations.yaml` on the server.
    *   Find the automation block with ID `1713265076593`.
    *   Replace it with the content of `ikea_e2001_e2002_switch_to_light_automation.yml`.

3.  **Update Scripts:**
    *   Open `/config/scripts.yaml` on the server.
    *   Update the definitions for `light_increase_brightness`, etc., with the content from `scripts.yml`.

4.  **Reload Configuration:**
    *   In Home Assistant UI: **Developer Tools** -> **YAML** -> **Reload Automations** (and **Reload Scripts**).

### Syncing from Server (Restore)

To update this repository with the live configuration from the server:

```bash
# Example SSH command to view remote file content
ssh -p 22 hassio@homeassistant.local "cat /config/automations.yaml"
```
