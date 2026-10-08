# Cosyra for Herdr

Open your Cosyra cloud workspace inside Herdr. The plugin adds a `Cosyra` workspace with one tab per Cosyra terminal. Each tab is attached to its terminal over SSH, so your agents run in the cloud and the same terminals are open on your phone in the Cosyra app.

Guide: https://cosyra.com/guides/herdr-cosyra.html

## Requirements

- Herdr 0.8.0 or newer, macOS or Linux
- The Cosyra CLI 0.13.0-rc.5 or newer: `curl -fsSL https://cosyra.com/install.sh | bash`
- Signed in: `cosyra auth login`
- The Cosyra SSH host set up: `cosyra ssh-config`

## Install

```bash
herdr plugin install portablcorp/herdr-cosyra
```

## Use

```bash
herdr plugin action invoke cosyra.open
```

- **Open Cosyra workspace** (`cosyra.open`): creates the workspace and a tab for each terminal. If you have no terminals, it wakes your workspace and creates one.
- **Refresh Cosyra terminals** (`cosyra.refresh`): adds tabs for new terminals and reattaches tabs that lost their connection.
- When you focus the workspace or Herdr starts, tabs are renamed to match and tabs for closed terminals are removed. A tab you closed stays closed until you open or refresh.

To open it from a key, add this to `~/.config/herdr/config.toml` and run `herdr server reload-config`:

```toml
[[keys.command]]
key = "prefix+shift+c"
type = "plugin_action"
command = "cosyra.open"
description = "open Cosyra workspace"
```

## Behaviour

- Closing a tab detaches only. The Cosyra terminal keeps running.
- Opening the same terminal on your phone detaches the Herdr tab. Press Enter in the tab to reattach.
- A tab keeps the workspace awake while it is attached. Close the tabs to let the workspace sleep.
- A sleeping workspace wakes when a tab attaches.
- The plugin only types into a tab when Herdr reports a plain shell in it, and never closes a tab that is running another program.

## Configuration

Optional. Create `env` in the plugin config directory (`herdr plugin config-dir cosyra`):

```
COSYRA_BIN=/path/to/cosyra
```

## Troubleshooting

```bash
herdr plugin log list --plugin cosyra
```
