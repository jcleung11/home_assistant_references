# Home Assistant Configuration & Organization Reference (v2026.6.4)

## Core configuration Principles
Home Assistant uses YAML for its core configuration. For larger systems, organization is key to preventing "entity soup."

### File Structure & YAML Management
- **Multi-file Configuration**: Use the `!include` directive in `configuration.yaml` to split content into separate files (e.g., `automations.yaml`, `scripts.yaml`). This keeps the main config clean and manageable.
- **Standard Syntax**: Ensure proper indentation and consistent usage of quotes, especially when embedding templates.

### Security & Safety
- **Secrets Management**: Use the `!secret` tag to reference variables from your `secrets.yaml` file. Never hardcode passwords or API keys directly in configuration files.
- **Validation**: Always run "Check Configuration" (via Developer Tools or CLI) before restarting Home Assistant after manual YAML edits.

## Organization & Scaling Logic
Properly grouping assets allows you to target groups of devices in automations and filters your view of the system's data.

### Core Organization Tools:
| Feature | Purpose | Capability |
| :--- | :--- | :--- |
| **Areas** | Physical location (e.g., "Kitchen") | Target all lights in a room; auto-generates UI cards for that area. |
| **Floors** | High-level grouping of Areas | Logical separation (e.g., "Main Floor", "Garage"). |
| **Labels** | Flexible tags (e.g., "high_power") | Can be assigned to sensors, automations, and scripts; excellent for filtering data in tables. |
| **Categories** | Table-specific groupings | Used in the UI to organize items like Scenes or Scripts into logical groups. |

### Group Integrations vs. Logical Groups
- **Group Integration**: Creates a single "virtual" entity from multiple entities (e.g., a group of three switches). 
- **Better for:** Logic that requires comparing several device states as one unit in an automation.
- *Contrast:* Unlike Area or Label, Group Integration does not provide UI filtering/organization logic; it is strictly a logical grouping tool.

## Switch as Light (Smart Switches → Light Entities)

Smart switches (relays, wall switches) create `switch.*` entities by default. To make them appear as lights in the UI, create template light entities that wrap them.

### Correct Syntax (HA 2026.6+)

Use the top-level `template:` key with the modern format (full docs: https://www.home-assistant.io/integrations/template/):

```yaml
template:
  - light:
      - name: "Lights Dining Table"
        unique_id: lights_dining_table
        state: "{{ is_state('switch.lights_dining_table', 'on') }}"
        turn_on:
          action: switch.turn_on
          target:
            entity_id: switch.lights_dining_table
        turn_off:
          action: switch.turn_off
          target:
            entity_id: switch.lights_dining_table
```

This creates `light.lights_dining_table` that mirrors the switch's on/off state.

### Deprecated Syntaxes (DO NOT USE)

These were removed and will cause config errors in HA 2026.6+:

| Deprecated Syntax | Removed In | Notes |
|---|---|---|
| `light:` → `platform: switch` | HA 2024.12 | Old switch-as-light YAML format |
| `light:` → `platform: template` → `lights:` | HA 2026.6 | Legacy template entity format |
| `switch_as_x:` YAML config | Never supported | `switch_as_x` is UI-only (Helpers → Switch as X) |

### UI-Only Alternative

For simple cases without YAML, create helpers directly in the UI:
**Settings → Devices & Services → Helpers → Create Helper → Switch as X**

Select the switch entity and choose "Light" as the target type. Repeat per switch.

---
*Last updated: 2026-06-20 | Reference for Home Assistant version 2026.6.4*
