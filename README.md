# create-project

A Claude Cowork plugin that scaffolds new projects, sub-projects, and Change Requests inside your Obsidian vault — consistently structured, every time.

On first run it walks you through a one-time setup wizard to configure your vault path and folder preferences. After that, invoke it and it gets straight to work.

---

## What it does

Every project gets the same folder structure:

```
<project-slug>/
├── CLAUDE.md        ← populated with project context
├── learnings.md     ← pre-seeded: gotchas, patterns, open questions
├── notes/           ← manual notes
├── meetings/
├── decisions/
├── reference/
└── deliverables/
```

Three workflows are supported:

- **Top-level project** — new entry under any of your configured top-level folders (e.g. `work/` or `personal/`)
- **Sub-project** — new workstream under an existing project
- **Change Request** — numbered scope document tracked under any project

---

## Prerequisites

- [Claude Desktop](https://claude.ai/download) installed
- A paid Claude plan (Pro, Max, Team, or Enterprise)
- [Obsidian](https://obsidian.md) installed with an existing vault
- The Obsidian MCP connected in Cowork: **Settings → Connectors → Obsidian**

---

## Installation

1. Download `create-project.plugin` from the [Releases](../../releases) page
2. Open Claude Desktop and switch to the **Cowork** tab
3. Click **Customize** in the left sidebar
4. Click **Browse Plugins**
5. Upload the `.plugin` file
6. The skill will appear as `create-project`

---

## First-time setup

The first time you invoke the skill, a one-time setup wizard runs. It asks:

- **Vault root path** — absolute path to your Obsidian vault (e.g. `/Users/yourname/Documents/MyVault`)
- **Existing vault or fresh?** — if you have an existing vault, it will ask whether to use the advised folder structure or map to your own
- **Folder structure** — advised (`work/` + `personal/`) or custom (you define the top-level folders)
- **Contacts tracking** — whether you track stakeholders in a contacts/people folder, and where
- **Change Requests** — whether you use CRs and what naming format you prefer
- **Root routing table** — whether to maintain a root `CLAUDE.md` that maps projects to their deliverables folders

Your answers are saved to `.create-project-config.md` at your vault root. The wizard never runs again unless you delete that file.

---

## Usage

Invoke via the Cowork chat:

```
/createproject
create a new project
scaffold a project
add a sub-project to <project>
new CR for <project>
add a change request
```

---

## Resetting your configuration

To re-run the setup wizard, delete `.create-project-config.md` from your vault root and invoke the skill again.

To change a single preference without re-running the wizard, open `.create-project-config.md` directly in Obsidian and edit the relevant field.

---

## Config file reference

Located at `VAULT_ROOT/.create-project-config.md`. Fields:

| Field | Values | Effect |
|-------|--------|--------|
| Root | Absolute path | Used for all file operations |
| Mode | `advised` / `custom` | Determines top-level folder options |
| Top-level folders | List of folder names | Options presented when creating a project |
| Contacts Enabled | `yes` / `no` | Enables stakeholder contact file creation |
| Contacts Path | Relative path | Where contact files are written |
| CR Enabled | `yes` / `no` | Enables the Change Request workflow |
| CR Naming Format | `cr-XX-description` / `CR-001-description` / `custom` | Slug format for CR folders |
| Routing Table Mode | `yes_existing` / `yes_create` / `no` | Controls root CLAUDE.md routing table updates |

---

## How index file updates work

The skill only updates index files that already exist in your vault. It never creates vault infrastructure you haven't opted into:

- `<top-level-folder>/CLAUDE.md` — updated if present
- Contacts index — updated if contacts are enabled and the directory exists
- Root `CLAUDE.md` routing table — behaviour controlled by your config

---

## Author

Eugene Lai
