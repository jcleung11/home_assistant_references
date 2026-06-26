# Home Assistant Dashboards Reference (v2026.6.4)

## Core Concepts
Dashboards are the primary interface for interacting with your smart home. They consist of **Views** and **Cards**.

### Dashboard Modes
- **Storage mode** (default): Config stored in `.storage/lovelace.*` JSON files, edited via the UI. Requires HA restart to pick up manual file edits.
- **YAML mode**: Config stored in `/config/*.yaml` files. Changes are picked up without restart — just use **Settings > System > Reload All Configs** or call `lovelace.reload_resources`.

**Prefer YAML mode** for dashboards managed via external scripts/rsync.

### View Types
- **Sections (Default):** Organizes cards into defined sections with headings. The modern standard.
- **Masonry:** Cards are arranged in a grid, automatically filling spaces. Best for many small cards.
- **Panel:** One single card takes up the entire width/height (useful for maps or iframes).
- **Sidebar:** Two-column layout with a wide left pane and narrow right pane.

### Card Types
- **Tile:** The primary card type — clean, shows entity state, supports toggle and fan speed control via popup.
- **Heading:** Section header within a grid section. Use `heading: "Room Name"` to label room groups.
- **Button, Entity, Gauge, Sensor, etc.** — standard HA cards for specific use cases.

## Adding a YAML Dashboard

1. Create `lights_fans.yaml` in `/config/` with view definitions.
2. Register it in `configuration.yaml`:
```yaml
lovelace:
  dashboards:
    lights-fans:       # ⚠️ Key MUST contain a hyphen (-)
      mode: yaml
      filename: lights_fans.yaml
      title: Lights & Fans
      icon: mdi:lightbulb-group
      show_in_sidebar: true
```
3. Push + restart HA (first time only). Future changes to the `.yaml` file need only a **Reload All Configs**.

## Sections View Structure
```yaml
views:
  - type: sections
    title: "My Dashboard"
    icon: mdi:home
    sections:
      - type: grid
        cards:
          - type: heading
            heading: "Room Name"
          - type: tile
            entity: light.example
            name: "My Light"
```
Each `section` is a responsive grid. Use multiple `type: grid` sections (one per room) with a `heading` card for the room name.

## Entity ID Reference (this setup)
| Entity | Type | Room |
|--------|------|------|
| `light.downstairs_lights` | Group | Downstairs |
| `light.lights_kitchen` | Light | Kitchen |
| `light.lights_dining_table` | Light | Dining |
| `light.lights_living` | Light | Living |
| `light.lights_entry_hallway` | Light | Hallway (down) |
| `light.lights_stairs` | Light | Stairs |
| `fan.master_ceiling_fan` | Fan | Master |
| `light.master_ceiling_fan` | Light | Master |
| `fan.loft_ceiling_fan_2` | Fan | Loft |
| `light.loft_ceiling_fan_2` | Light | Loft |
| `light.hue_downlight` | Light | Loft |
| `fan.chloe_ceiling_fan_2` | Fan | Chloe |
| `light.chloe_ceiling_fan_2` | Light | Chloe |
| `fan.office_ceiling_fan_2` | Fan | Office |
| `light.office_ceiling_fan_2` | Light | Office |
| `fan.leo_ceiling_fan` | Fan | Leo |
| `light.leo_ceiling_fan` | Light | Leo |
| `light.lights_upstairs_hallway` | Light | Hallway (up) |

---
*Last updated: 2026-06-22 | Reference for Home Assistant version 2026.6.4*
