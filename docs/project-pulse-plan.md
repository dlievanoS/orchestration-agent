# Project Pulse dashboard implementation plan

## Objective

Build a polished, static Project Pulse dashboard that gives Mona an immediately
readable view of projects, their statuses, priorities, owners, and progress.
The dashboard must be accessible, responsive, data-driven from a local JSON
file, and easy to preview from the Codespace.

## Implementation phases and assignments

### Phase 1: Define the dashboard experience

**Owner: Designer**

- Define the information hierarchy for the dashboard: summary area, project
  cards, status badges, priority treatment, progress indicators, and project
  metadata.
- Specify the responsive behavior for narrow and wide viewports and the
  accessible visual treatment for color, contrast, focus, and readable text.
- Provide the visual direction that Coder will implement in the following
  files:

| File | Assigned work |
| --- | --- |
| `app/index.html` | Define the semantic dashboard structure and stable hooks, including `.dashboard` and `.project-card`. |
| `app/styles.css` | Define the visual system, layout, responsive breakpoints, component states, and accessible focus styling. |

**Output:** A concise implementation-ready design specification covering
content hierarchy, card anatomy, color-independent status and priority cues,
spacing, typography, and responsive rules.

### Phase 2: Establish the dashboard data contract

**Owner: Coder**

| File | Assigned work |
| --- | --- |
| `app/project-data.json` | Create deterministic sample project data with the fields needed by the dashboard, such as project name, owner, status, priority, progress, due date, and summary. |

The JSON schema should contain enough varied states to demonstrate the UI
(for example, multiple statuses and priorities) without requiring a backend.
Use valid, consistently shaped JSON and values that can be rendered without
special-case behavior.

### Phase 3: Implement the dashboard and preview configuration

**Owner: Coder**

| File | Assigned work |
| --- | --- |
| `app/index.html` | Implement the semantic page shell; load `styles.css`; load and render `project-data.json`; present a clear loading or error state if local data cannot be loaded. |
| `app/styles.css` | Implement the approved visual direction with responsive grid behavior, project-card styling, status and priority cues, visible keyboard focus, and readable contrast. |
| `.vscode/launch.json` | Add a strict JSON, comment-free launch configuration that serves the app with `cwd` set to `${workspaceFolder}/app` and opens `index.html`, rather than a directory listing. |

Coder must keep the dashboard deterministic and ensure that the implementation
uses the agreed data contract rather than duplicating project data in markup.

## Dependencies and sequencing

1. **Phase 1 precedes implementation of `app/index.html` and
   `app/styles.css`.** Coder needs the Designer's content hierarchy,
   component states, and responsive specifications before implementing the
   visual layer.
2. **Phase 2 precedes data rendering in `app/index.html`.** The page's
   rendering logic must target the agreed JSON fields and handle every
   included status and priority value.
3. **Phase 3 follows both Phases 1 and 2.** It combines the approved design
   direction with the finalized data contract.
4. **`.vscode/launch.json` depends only on the final app location and can be
   prepared during Phase 3.** Verify it after `app/index.html` exists so its
   startup URL opens the dashboard successfully.

## Parallel work decisions

- **May run in parallel:** Designer's Phase 1 specification and Coder's
  Phase 2 data-contract work, provided Coder does not implement visual
  dashboard files until the design direction is available.
- **Must run sequentially:** Coder's work on `app/index.html` and
  `app/styles.css` starts after the Phase 1 design output and Phase 2 data
  contract are accepted. Rendering and styling should be integrated in one
  implementation phase because their markup hooks and responsive behavior are
  tightly coupled.
- **May run alongside final styling:** Coder may draft `.vscode/launch.json`
  once the `app/` location is confirmed, but must validate it only after the
  dashboard entry point is present.

## Validation expectations

Coder validates the completed dashboard against the following expectations:

1. `app/project-data.json` parses as valid JSON and every project follows the
   agreed field contract.
2. `app/index.html` loads the stylesheet and renders each project from
   `project-data.json`; no sample project data is duplicated in HTML.
3. The dashboard includes recognizably distinct project cards, status badges,
   priority treatment, owner and progress information, and a clear Project
   Pulse heading in the first view.
4. At narrow and wide viewport sizes, content remains usable without clipped
   controls or horizontal overflow; project cards reflow appropriately.
5. Keyboard focus is visible, headings follow a logical hierarchy, controls
   have accessible names, and status or priority is understandable without
   color alone.
6. The CSS includes the deterministic `.dashboard` and `.project-card` hooks,
   maintains readable color contrast, and does not depend on unavailable
   external assets.
7. `.vscode/launch.json` is strict valid JSON, has no comments, sets
   `cwd` to `${workspaceFolder}/app`, starts the dashboard server
   deterministically, and opens `index.html`.
8. Preview the app from the configured launch path and confirm that data loads
   successfully; also confirm that any load failure produces an explicit,
   understandable error state.

## Risks and edge cases

- Browsers commonly restrict `fetch()` from `file://` URLs, so the launch
  configuration must serve `app/` over HTTP rather than opening the file
  directly.
- Data fields may be missing or malformed; rendering must report malformed or
  unavailable data clearly rather than silently showing an empty dashboard.
- Status and priority labels must remain understandable for users who cannot
  distinguish color and at small viewport widths.
