# Home Assistant Automations Reference (v2026.6.4)

## Core Concepts
Automations in Home Assistant are sequences of actions triggered by specific events or conditions. They can be defined via the UI (stored in `automations.yaml`) or directly in `configuration.yaml`.

### Structure of an Automation
*   **id**: Unique identifier for your automation. Required for any automation to be usable in the UI and to enable debug traces.
*   **alias**: A human-readable name for the automation.
*   **description**: A detailed explanation of what the automation does.
*   **init_state**: Determines if an automation starts as "on" or "off" when Home Assistant restarts.
*   **trace**: Configuration for debug traces (e.g., `stored_traces: 10`).

### Logic Flow
1.  **Triggers**: The *why*. Anything that causes the automation to run (State changes, Time, Events, etc.).
2.  **Conditions**: The *when*. Requirements that must be true for the actions to execute if a trigger occurs.
3.  **Actions**: The *what*. The result of the successful logic flow (calling services, switching lights, notifying users).

### Automation Modes (Execution Behavior)
| Mode | Description |
| :--- | :--- |
| **single** | Default mode. If already running, do not start a new run; issue a warning. |
| **restart** | Stop the current running instance and start a brand-new one from the beginning immediately. |
| **queued** | Queue runs if triggered while currently active. Each will run sequentially in order of arrival. |
| **parallel** | Run multiple instances simultaneously. Useful for "fire and forget" actions that don't interact with each other. |

## Variables
- `variables`: Scope across conditions and actions. Can include complex objects or templates.
- `trigger_variables`: Specifically used within template triggers to pass data from the trigger event into the action logic.

## Technical Organization
To maintain a clean configuration, it is recommended to use:
1.  **auto_blueprint**: For reuse of common patterns.
2.  **scripts**: For long sequences of actions that don't need complex "if" checks in every instance (reusable blocks).
3.  **automations.yaml**: Utilizing the `!include` format to separate automation logic from main system configuration.

---
*Last updated: 2026-06-18 | Reference for Home Assistant version 2026.6.4*
