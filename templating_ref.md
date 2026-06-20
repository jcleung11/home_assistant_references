# Home Assistant Templating Reference (v2026.6.4)

## Core Rules & Syntax Requirements

### The Quoting Rule
A single-line template **must** be wrapped in quotes (`"` or `'`). 
- **Why:** Without quotes, YAML treats `{{` as the start of a flow-style mapping and will fail to load.
- **Example:** `value_template: "{{ states('sensor.temp') | float > 20 }}"`

### Quotes inside Templates
If your template includes internal quotes, use the opposite quote for the outer wrapper.
- **Single inner quote:** `"{{ is_state('light.kitchen', 'on') }}"`
- **Double inner quote:** `'{{ states["sensor.temp"] }}'`

---

## Multi-line Template Structures
When a template becomes complex, multi-line blocks are preferred over single lines to improve readability and avoid quoting conflicts.

| Marker | Name | Behavior | Common Use Case |
| :--- | :--- | :--- | :--- |
| `>` | Folded | Joins newlines into spaces (unless they are empty). | Complex logic scripts / multi-condition checks. |
| `|` | Literal | Keeps newline characters as they are. | Multi-line notification text or logs. |
| `>-` | Folded + Strip | Joins newlines AND strips the final trailing newline. | **Recommended** for all `value_template` fields. |
| `|-` | Literal + Strip | Keeps newlines but removes/strips the last one. | Multi-line text where the very last "enter" key isn't needed. |

## Critical Pitfalls
1.  **Indentation:** Inside a `|` or `>` block, every line must align with the first line of content in that block. If you decrease indentation on any line, YAML will cut off the block at that point.
2.  **Malformed Newlines**: Incorrectly indented multi-line blocks cause Home Assistant to fail during startup (invalid configuration).

---
*Last updated: 2026-06-18 | Reference for Home Assistant version 2026.6.4*
