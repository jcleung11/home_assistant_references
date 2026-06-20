# Home Assistant Dashboards Reference (v2026.6.4)

## Core Concepts
Dashboards are the primary interface for interacting with your smart home. They consist of **Views** and **Cards**.

### View Types
- **Masonry:** Cards are arranged in a grid, automatically filling spaces. Best for many small cards.
- **Panel:** One single card takes up the entire width/height (useful for weather or central controls).
- **Sections (Default):** Organizes cards into defined sections, which is currently the standard for modern UI.

### Dashboard Components
*   **Cards**: The basic unit of display. Examples include:
    *   **Tile:** The primary "new" card type designed to be clean and functional.
    *   **Entity/Button:** Simple controls for switches or sensing status.
    *   **Gauge:** Visual representation of a numeric range (e.g., temperature).
    *   **Logbook / Directory:** Displaying lists of recent history or system navigation.

## Configuration Syntax
- **Cards & Layouts**: Defined in the `lovelace.yaml` or via dashboard configuration.
- **Grid/Stack**: Used to group multiple cards into a single row (Horizontal Stack) or column (Vertical Stack).
- **Conditionals**: Logic within dashboards that shows cards only if certain conditions are met (e.g., "only show outside sensors when the sun is down").

---
*Last updated: 2026-06-18 | Reference for Home Assistant version 2026.6.4*
