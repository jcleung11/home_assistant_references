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

---
*Last updated: 2026-06-18 | Reference for Home Assistant version 2026.6.4*
